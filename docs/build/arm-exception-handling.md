---
title: ARM 例外狀況處理
ms.date: 07/11/2018
ms.assetid: fe0e615f-c033-4ad5-97f4-ff96af45b201
ms.openlocfilehash: f4e56284ce8db18ec76b0143253ee1e25f3fd82c
ms.sourcegitcommit: 28eae422049ac3381c6b1206664455dbb56cbfb6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/31/2019
ms.locfileid: "66450489"
---
# <a name="arm-exception-handling"></a>ARM 例外狀況處理

Windows on ARM 對非同步硬體產生的例外狀況和同步軟體產生的例外狀況，使用相同的結構化例外狀況處理機制。 語言專屬例外狀況處理常式使用語言協助程式函式，以 Windows 結構化例外狀況處理為基礎，進行建置。 本文件說明在 Windows ARM，和 Microsoft ARM 組譯工具和 MSVC 編譯器所產生的程式碼所使用的語言協助程式中處理的例外狀況。

## <a name="arm-exception-handling"></a>ARM 例外狀況處理

在 ARM 上的 Windows 會使用*回溯程式碼*來控制堆疊回溯期間[結構化例外狀況處理](/windows/desktop/debug/structured-exception-handling)(SEH)。 回溯程式碼是儲存在可執行映像檔 .xdata 區段的位元組序列。 它們以抽象方法描述函式序言和結尾程式碼的作業，因此函式序言的影響可以在準備回溯至呼叫者堆疊框架時復原。

ARM EABI (內嵌應用程式二進位介面) 會指定使用回溯程式碼的例外狀況回溯模型，但這對於 Windows 中的 SEH 回溯而言是不夠的，SEH 回溯必須處理處理器在函式序言或結尾中間的非同步情況。 Windows 亦會將回溯控制分為函式級別回溯和語言專屬範圍回溯，其在 ARM EABI 中統一。 基於上述原因，Windows on ARM 會指定回溯資料和程序的更多詳細資料。

### <a name="assumptions"></a>假設

Windows on ARM 的可執行映像檔使用可攜式執行檔 (PE) 格式。 如需詳細資訊，請參閱 < [Microsoft PE 和 COFF 規格](https://go.microsoft.com/fwlink/p/?linkid=84140)。 例外狀況處理資訊會儲存在映像檔的 .pdata 和 .xdata 區段。

例外狀況處理機制會對遵循適用於 Windows on ARM 的 ABI 之程式碼，進行下列假設：

- 當函式主體中發生例外狀況時，序言作業是否復原，以及結尾作業是否以正向方式執行都無關緊要。 這兩個作業會產生相同的結果。

- 序言和結尾通常會彼此鏡像。 這可用於減少描述回溯所需的中繼資料的大小。

- 函式通常相對來說會較小。 數個最佳化依賴這一特質，進行高效的資料封裝。

- 如果在結尾上放置條件，則它會同等地套用至結尾中的每一個指令。

- 如果堆疊指標 (SP) 儲存在序言的其他暫存器中，則該暫存器必須在函式中自始至終保持不變，如此原始 SP 才可能隨時復原。

- 除非 SP 儲存在其他暫存器，否則對它的所有操作都必須嚴格發生在序言和結尾中。

- 若要回溯任何堆疊框架，需要下列作業：

  - 以 4 個位元組的增量，調整 r13 (SP)。

  - 彈出一個或多個整數暫存器。

  - 彈出一個或多個 VFP (虛擬浮點數) 暫存器。

  - 將任意暫存器值複製到 r13 (SP)。

  - 使用較小的後置遞減作業，從堆疊載入 SP。

  - 剖析數個定義良好框架類型中的一個。

### <a name="pdata-records"></a>.pdata 記錄。

PE 格式映像檔中的 .pdata 記錄是固定長度項目的已排序陣列，這些項目會描述每一個堆疊操作函式。 不呼叫其他函式的分葉函式在不操作堆疊時，不需要 .pdata 記錄。 (即它們不需要任何區域儲存區，也無需儲存或還原靜態暫存器)。 這些函式的記錄可以從 .pdata 區段省略，以節省空間。 上述其中一個函式的回溯作業可以將連結暫存器 (LR) 的傳回位址，複製到程式計數器 (PC)，以向上移至呼叫者。

ARM 的每一個 .pdata 記錄長度都是 8 個位元組。 記錄的一般格式會將函式開頭的相對虛擬位址 (RVA) 置於第一個 32 位元字組，後接包含可變長度 .xdata 區塊指標，或者描述標準函式回溯序列之封裝字組的第二個字組，如下表所示：

|字組位移|Bits|用途|
|-----------------|----------|-------------|
|0|0-31|*函式開始 RVA*是函式開頭的 32 位元 RVA。 如果函式包含捲動方塊程式碼，則必須設定此位址的低位元。|
|1|0-1|*旗標*是 2 位元欄位，指出如何解譯其餘 30 個位元的第二個.pdata 字組。 如果*旗標*為 0，則其餘位元會構成*例外狀況資訊 RVA* (具有較低的兩個位元隱含為 0)。 如果*旗標*是不是零，則其餘位元會構成*封裝回溯資料*結構。|
|1|2-31|*例外狀況資訊 RVA*或是*封裝回溯資料*。<br /><br /> *例外狀況資訊 RVA*是.xdata 區段中所儲存的可變長度例外狀況資訊結構的位址。 此資料必須是對齊的 4 位元組。<br /><br /> *封裝回溯資料*是從函式，假設為標準格式回溯所需的作業的精簡的描述。 在此情況下，不需要 .xdata 記錄。|

### <a name="packed-unwind-data"></a>封裝的回溯資料

對於如下所述之序言和結尾遵循標準格式的函式而言，可以使用封裝的回溯資料。 這樣做即可不需要 .xdata 記錄，並可大幅減少提供回溯資料所需的空間。 標準序言和結尾設計用來滿足不需要例外狀況處理常式之簡單函式的一般需求，並以標準順序執行其設定和拆除作業。

下表顯示封裝回溯資料的 .pdata 記錄格式：

|字組位移|Bits|用途|
|-----------------|----------|-------------|
|0|0-31|*函式開始 RVA*是函式開頭的 32 位元 RVA。 如果函式包含捲動方塊程式碼，則必須設定此位址的低位元。|
|1|0-1|*旗標*是 2 位元欄位，具有下列意義：<br /><br />-00 = 封裝回溯資料未使用;其餘的位元指向.xdata 記錄。<br />-01 = 封裝回溯資料。<br />10 = 封裝回溯的資料函式會假設沒有序言。 這在描述與函式開頭不連續的函式片段時非常有用。<br />-11 = 保留。|
|1|2-12|*函式長度*是 11 位元欄位，提供整個函式，以位元組為單位除以 2 的長度。 如果函式大於 4K 位元組，則必須改為使用完整 .xdata 記錄。|
|1|13-14|*Ret*是 2 位元欄位，指出如何函式會傳回：<br /><br />-00 = 透過彈出 {pc} 傳回 ( *L*旗標位元必須設為 1 在此情況下)。<br />-01 = 使用 16 位元分支傳回。<br />10 = 使用 32 位元分支傳回。<br />-11 完全 = 無結尾。 這在描述可能僅包含序言而結尾在別處的不連續函式片段非常有用。|
|1|15|*H*是 1 位元旗標，指出是否函式 」 參數寫入堆疊 」 的整數參數註冊所推送的函式開頭的 (r0-r3)，並傳回前先取消配置 16 個位元組的堆疊。 (0 = 不將寄存器參數寫入堆疊，1 = 將寄存器參數寫入堆疊)。|
|1|16-18|*Reg* 3 位元欄位，指出索引之最後一個儲存靜態暫存器。 如果*R*位元為 0，則只有整數暫存器儲存，且會假設範圍為 r4-rN，其中 N 等於 4 + *Reg*。如果*R*位元為 1，則只有浮點暫存器儲存，且會假設範圍為 d8-dN，其中 N 等於 8 + *Reg*。特殊組合*R* = 1 並*Reg* = 7，表示會儲存任何暫存器。|
|1|19|*R*是 1 位元旗標，指出是否已儲存的非暫時性暫存器是整數暫存器 (0) 還是浮點數暫存器 (1)。 如果*R*設為 1 時， *Reg*欄位設定為 7、 不推送任何靜態暫存器。|
|1|20|*L*是 1 位元旗標，指出是否函式儲存/還原 LR，以及指出的其他暫存*Reg*欄位。 (0 = 不儲存/還原，1 = 儲存/還原)。|
|1|21|*C*是 1 位元旗標，指出函數是否包含額外的指示，來設定快速堆疊查核行程 (1) 與否 (0) 的框架鏈結。 如果設定此位元，則會隱含地將 r11 加入所儲存整數靜態暫存器的清單。 (請參閱下面的如果限制*C*旗標用。)|
|1|22-31|*堆疊調整*是 10 位元欄位，指出堆疊的這個函式，除以 4 而配置的位元組數目。 不過，僅可以對 0x000-0x3F3 之間的值直接進行編碼。 配置大於 4044 個位元組堆疊的函式必須使用完整 .xdata 記錄。 如果*堆疊調整*欄位為 0x3F4 或更大，則較低的 4 個位元具有特殊意義：<br /><br />位元 0-1 指出堆疊調整 (1-4) 減 1 的字組的數目。<br />位元 2 會設定為 1，如果序言此調整結合至其推入作業。<br />位如果結尾此調整結合至其彈出作業，是設定為 1 元 3。|

由於上述編碼中可能存在冗餘，所以適用下列限制：

- 如果*C*旗標設為 1 時：

   - *L*旗標也必須設定為 1，因為框架鏈結需要 r11 和 LR。

   - r11 必須不會包含在所描述的暫存器集合*Reg*。也就是說，如果推入 r4-r11， *Reg*應該在因為僅描述 r4-r10 *C*旗標隱含 r11。

- 如果*Ret*欄位設定為 0， *L*旗標必須設定為 1。

違反這些限制會導致不支援的序列。

下面討論的目的而言，兩個虛擬旗標衍生自*堆疊調整*:

- *PF*或 「 序言摺疊 」 指出*堆疊調整*為 0x3F4 或更大、 位元 2 會設定。

- *EF*或 「 結尾摺疊 」 指出*堆疊調整*為 0x3F4 或更大、 位元 3 設定。

標準函式的序言可能具有多達 5 個指令 (請注意，3a 和 3b 互斥)：

|指令|下列情況中會假設 Opcode 存在：|大小|Opcode|回溯程式碼|
|-----------------|-----------------------------------|----------|------------|------------------|
|1|*H*==1|16|`push {r0-r3}`|04|
|2|*C*= = 1 或*L*= = 1 或*R*= = 0 或 PF==1 = = 1|16/32|`push {registers}`|80-BF/D0-DF/EC-ED|
|3a|*C*= = 1 和 (*L*= = 0 並*R*= = 1 且 PF==0 = = 0)|16|`mov r11,sp`|C0-CF/FB|
|3b|*C*= = 1 和 (*L*= = 1 或*R*= = 0 或 PF==1 = = 1)|32|`add r11,sp,#xx`|FC|
|4|*R*= = 1， *Reg* ！ = 7|32|`vpush {d8-dE}`|E0-E7|
|5|*堆疊調整*！ = 0 且 PF = = 0|16/32|`sub sp,sp,#xx`|00-7F/E8-EB|

指示 1，則一律存在如果*H*位元會設為 1。

若要設定框架鏈結，指令 3a 或 3b 存在於如果*C*設定位元。 如果除了 r11 和 LR 之外未推入任何暫存器，則它為 16 位元 `mov`；否則，其為 32 位元 `add`。

如果未指定非摺疊調整，則指令 5 為明確堆疊調整。

指令 2 和 4 基於是否需要推入而設定。 下表摘要說明根據儲存的暫存器*C*， *L*， *R*，以及*PF*欄位。 在所有情況下， *N*等於*Reg* + 4， *E*等於*Reg* + 8，以及*S*等於 (~*堆疊調整*) 和 3。

|C|L|R|PF|推入的整數暫存器|推入的 VFP 暫存器|
|-------|-------|-------|--------|------------------------------|--------------------------|
|0|0|0|0|r4-r*N*|none|
|0|0|0|1|r*S*-r*N*|none|
|0|0|1|0|none|d8-d*E*|
|0|0|1|1|r*S*-r3|d8-d*E*|
|0|1|0|0|r4-r*N*，LR|none|
|0|1|0|1|r*S*-r*N*，LR|none|
|0|1|1|0|LR|d8-d*E*|
|0|1|1|1|r*S*-r3，LR|d8-d*E*|
|1|0|0|0|r4-r*N*、 r11|none|
|1|0|0|1|r*S*-r*N*、 r11|none|
|1|0|1|0|r11|d8-d*E*|
|1|0|1|1|r*S*-r3，r11|d8-d*E*|
|1|1|0|0|r4-r*N*，r11，LR|none|
|1|1|0|1|r*S*-r*N*，r11，LR|none|
|1|1|1|0|r11、LR|d8-d*E*|
|1|1|1|1|r*S*-r3，r11，LR|d8-d*E*|

標準函式的結尾遵循類似格式，但方向相反且具有其他選項。 結尾可能長達 5 個指令，且其格式由序言的格式嚴格指定。

|指令|下列情況中會假設 Opcode 存在：|大小|Opcode|
|-----------------|-----------------------------------|----------|------------|
|6|*堆疊調整*！ = 0 和*EF*= = 0|16/32|`add   sp,sp,#xx`|
|7|*R*= = 1， *Reg*！ = 7|32|`vpop  {d8-dE}`|
|8|*C*= = 1 或 (*L*= = 1 並*H*= = 0) 或*R*= = 0 或*EF*= = 1|16/32|`pop   {registers}`|
|9a|*H*= = 1， *L*= = 0|16|`add   sp,sp,#0x10`|
|9b|*H*= = 1， *L*= = 1|32|`ldr   pc,[sp],#0x14`|
|10a|*Ret*==1|16|`bx    reg`|
|10b|*Ret*==2|32|`b     address`|

如果指定非摺疊調整，則指令 6 為明確堆疊調整。 因為*PF*無關*EF*，就可以將指令 5 而不存在指令 6 或反之亦然。

指令 7 和 8 使用與序言相同的邏輯，以判斷從堆疊還原暫存器，但這些兩個變更： 首先， *EF*用來取代*PF*; 其次，如果*Ret* = 0，則在註冊清單中 LR 取代為 PC 和結尾會立即結束。

如果*H*設定，則指令 9a 或 9b 是存在。 使用指令 9a 時*L*為 0，以指出 LR 未在堆疊上。 在此情況下，會手動調整堆疊並*Ret*必須為 1 或 2，以指定明確傳回。 使用指令 9b 時*L*為 1，以指出過早結束結尾，並傳回並調整堆疊，在相同的時間。

如果結尾尚未結束，則指令 10a 或 10b 已存在的情況，就表示 16 位元或 32 位元的分支，根據的值*Ret*。

### <a name="xdata-records"></a>.xdata 記錄

當封裝回溯格式不足以描述函式的回溯時，必須建立可變長度的 .xdata 記錄。 此記錄的位址儲存在 .pdata 記錄的第二個字組。 .xdata 的格式為具有四個區段的可變長度封裝字組集：

1. 1 或 2 字組標頭描述 .xdata 結構的整體大小，並提供關鍵函式資料。 第二個字組時才存在*結尾計數*並*程式碼字組*欄位都設定為 0。 下表詳細說明這些欄位：

   |字組|Bits|用途|
   |----------|----------|-------------|
   |0|0-17|*函式長度*是 18 位元欄位，指出以位元組為單位，除以 2 的函式的總長度。 如果函式大於 512 KB，則必須使用多個 .pdata 和 .xdata 記錄，來描述函式。 如需詳細資料，請參閱本文件中的＜大型函式＞一節。|
   |0|18-19|*Vers*是 2 位元欄位，描述其餘 xdata 的版本。 目前僅定義版本 0，保留值 1-3。|
   |0|20|*X*是 1 位元欄位，指出存在 (1) 與否 (0) 的例外狀況資料。|
   |0|21|*E*是 1 位元欄位，指出描述單一結尾的資訊會封裝到標頭 (1) 而不需要其他範圍字組的更新版本 (0)。|
   |0|22|*F*是 1 位元欄位，指出此記錄是描述函式片段 (1) 或完整的函式 (0)。 片段隱含無序言，且應忽略所有序言處理。|
   |0|23-27|*結尾計數*是 5 位元欄位，有兩種意義，視狀態而定*E*元：<br /><br /> -如果*E*是 0，則這個欄位是第 3 節中所述的例外狀況範圍總數的計數。 如果超過 31 個範圍存在於函式，則此欄位中，*程式碼字組*欄位必須同時設為 0 指出需要擴充字組。<br />-如果*E*為 1，此欄位會指定僅描述結尾之第一個回溯程式碼索引。|
   |0|28-31|*程式碼字組*是 4 位元欄位，指定包含所有在第 4 節中的回溯程式碼所需的 32 位元字組的數目。 如果超過 15 個字組所需的超過 63 個回溯程式碼位元組，這個欄位並*結尾計數*欄位必須同時設為 0 指出需要擴充字組。|
   |1|0-15|*擴充的結尾計數*是 16 位元欄位，編碼為異常大數目的結尾時，提供更多空間。 包含此欄位的擴充字組時才存在*結尾計數*並*程式碼字組*的第一個標頭文字中的欄位都設定為 0。|
   |1|16-23|*擴充程式碼字組*是 8 位元欄位，編碼為異常大數目的回溯程式碼字組時，提供更多空間。 包含此欄位的擴充字組時才存在*結尾計數*並*程式碼字組*的第一個標頭文字中的欄位都設定為 0。|
   |1|24-31|保留|

1. 例外狀況資料之後 (如果*E*標頭中的位元已設為 0) 是一份結尾範圍，這會壓縮至一個字組的其中一個，並以遞增的開始位移順序儲存的相關資訊。 每一個範圍包含下列欄位：

   |Bits|用途|
   |----------|-------------|
   |0-17|*結尾開始位移*是 18 位元欄位，描述在結尾，以位元組為單位除以 2，相對於函式的開頭的位移。|
   |18-19|*Res*是 2 位元欄位，保留供未來擴充。 其值必須為 0。|
   |20-23|*條件*是 4 位元欄位，可提供執行結尾時的條件。 對於無條件的結尾，它應該設定為 0xE，指出「永遠」。 (結尾必須完全是有條件的或完全是無條件的，而在 Thumb-2 模式下，結尾以 IT opcode 後的第一個指令開始)。|
   |24-31|*結尾開始索引*是 8 位元欄位，指出描述此結尾之第一個回溯程式碼的位元組索引。|

1. 在結尾範圍清單之後是包含回溯程式碼的位元組陣列，在本文章的＜回溯程式碼＞一節有詳細描述。 此陣列在最近完整字組界面的結尾處填補。 位元組以 Little-Endian 順序儲存，因此可在 Little-Endian 模式下直接擷取。

1. 如果*X*標頭中的欄位為 1，回溯程式碼位元組後面接著例外狀況處理常式資訊。 這包括一個*例外狀況處理常式 RVA*包含例外狀況處理常式，後面緊接跟著 （可變長度） 的資料量的例外狀況處理常式所需的位址。

設計 .xdata 記錄是為了可以提取前 8 個位元組，並計算記錄的完整大小，不包括後續可變大小例外狀況資料的長度。 此程式碼片段會計算記錄大小：

```cpp
ULONG ComputeXdataSize(PULONG *Xdata)
{
    ULONG EpilogueScopes;
    ULONG Size;
    ULONG UnwindWords;

    if ((Xdata[0] >> 23) != 0) {
        Size = 4;
        EpilogueScopes = (Xdata[0] >> 23) & 0x1f;
        UnwindWords = (Xdata[0] >> 28) & 0x0f;
    } else {
        Size = 8;
        EpilogueScopes = Xdata[1] & 0xffff;
        UnwindWords = (Xdata[1] >> 16) & 0xff;
    }

    if (!(Xdata[0] & (1 << 21))) {
        Size += 4 * EpilogueScopes;
    }
    Size += 4 * UnwindWords;
    if (Xdata[0] & (1 << 20)) {
        Size += 4;
    }
    return Size;
}
```

雖然序言和每一個結尾回溯程式碼中的索引，兩者之間會共用表格。 它們全部都可以共用相同的回溯程式碼，這很正常。 建議編譯器撰寫者針對此情況進行最佳化，因為可以指定的最大索引為 255，這會限制特定函式可能具有的回溯程式碼總數。

### <a name="unwind-codes"></a>回溯程式碼

回溯程式碼陣列是一組指令序列，用於確切描述如何以作業必須復原的順序，來復原序言的影響。 回溯程式碼是迷你指令集，編碼為位元組的字串。 當執行完成時，向呼叫函式傳回的位址位於 LR 暫存器中，而所有靜態暫存器會還原為呼叫該函式時的值。

如果已保證例外狀況僅在函式主體中發生，而不會在序言或結尾中發生，則只需要一個回溯序列即可。 不過，Windows 回溯模型需要能夠從部分執行的序言或結尾回溯。 為了符合此需求，已仔細對回溯程式碼進行設計，讓其與序言和結尾中的每一個相關 opcode，具有明確的一對一對應。 這有下列幾個含意：

- 可以透過計算回溯程式碼的數目，來計算序言和結尾的長度。 即使使用可變長度 Thumb-2 指令，也可以這樣做，因為 16 位元和 32 位元作業碼具有不同的對應。

- 透過計算經過結尾範圍開頭的指令數目，可以跳過相同數目的回溯程式碼，並執行系列的其餘部分，以完成結尾所執行之部分執行的回溯。

- 透過計算序言結尾之前的指令數目，可以跳過相同數目的回溯程式碼，並執行序列的其餘部分，以僅復原序言中已完成執行的那些部分。

下表顯示從回溯程式碼到作業碼的對應。 最常見的程式碼只有一個位元組，需要兩個、三個甚至四個位元組的程式碼較不常見。 每一個程式碼都從最重要的位元組到最不重要的位元組進行儲存。 回溯程式碼結構與 ARM EABI 中所述的編碼不同，因為這些回溯程式碼設計用來與序言和結尾中的 opcode 進行一對一對應，以容許回溯部分執行的序言和結尾。

|位元組 1|位元組 2|位元組 3|位元組 4|Opsize|說明|
|------------|------------|------------|------------|------------|-----------------|
|00-7F||||16|`add   sp,sp,#X`<br /><br /> 其中 X 為 (Code & 0x7F) \* 4|
|80-BF|00-FF|||32|`pop   {r0-r12, lr}`<br /><br /> 如果 Code & 0x2000，r0-r12 會彈出如果在 Code & 0x1FFF 中設定對應的位元會彈出 LR 其中|
|C0-CF||||16|`mov   sp,rX`<br /><br /> 其中 X 為 Code & 0x0F|
|D0-D7||||16|`pop   {r4-rX,lr}`<br /><br /> 其中，X 為 (Code & 0x03) + 4 和 LR，則會彈出如果 Code & 0x04|
|D8-DF||||32|`pop   {r4-rX,lr}`<br /><br /> 其中，X 為 (Code & 0x03) + 8 和 LR，則會彈出如果 Code & 0x04|
|E0-E7||||32|`vpop  {d8-dX}`<br /><br /> 其中，X 為 (Code & 0x07) + 8|
|E8-EB|00-FF|||32|`addw  sp,sp,#X`<br /><br /> 其中 X 為 (Code & 0x03FF) \* 4|
|EC-ED|00-FF|||16|`pop   {r0-r7,lr}`<br /><br /> 如果程式碼 & 0x0100 和 r0-r7 會彈出如果在 Code & 0x00FF 中設定對應的位元會彈出 LR 其中|
|EE|00-0F|||16|Microsoft 專有|
|EE|10-FF|||16|可用|
|EF|00-0F|||32|`ldr   lr,[sp],#X`<br /><br /> 其中 X 為 (Code & 0x000F) \* 4|
|EF|10-FF|||32|可用|
|F0-F4||||-|可用|
|F5|00-FF|||32|`vpop  {dS-dE}`<br /><br /> 其中，S 為 (Code & 0x00F0) >> 4 而 E 為 Code & 0x000F|
|F6|00-FF|||32|`vpop  {dS-dE}`<br /><br /> 其中 S 是 ((Code & 0x00F0) >> 4) + 16 而 E 為 (Code & 0x000F) + 16|
|F7|00-FF|00-FF||16|`add   sp,sp,#X`<br /><br /> 其中 X 為 (Code & 0x00FFFF) \* 4|
|F8|00-FF|00-FF|00-FF|16|`add   sp,sp,#X`<br /><br /> 其中 X 為 (Code & 0x00FFFFFF) \* 4|
|F9|00-FF|00-FF||32|`add   sp,sp,#X`<br /><br /> 其中 X 為 (Code & 0x00FFFF) \* 4|
|FA|00-FF|00-FF|00-FF|32|`add   sp,sp,#X`<br /><br /> 其中 X 為 (Code & 0x00FFFFFF) \* 4|
|FB||||16|nop (16 位元)|
|FC||||32|nop (32 位元)|
|FD||||16|end + 16 位元 nop (結尾中)|
|FE||||32|end + 32 位元 nop (結尾中)|
|FF||||-|end|

這會顯示每個位元組的十六進位值的範圍中的回溯程式碼*程式碼*，以及作業碼大小*Opsize*和對應的原始指令解釋。 空儲存格表示較短的回溯程式碼。 如果指令具有涵蓋多位元組的大型值，則會最先儲存最重要的位元。 *Opsize*欄位會顯示與每一個 thumb-2 作業相關聯的隱含 opcode 大小。 表格中具有不同編碼的明顯重複項目用於區分不同的作業碼大小。

設計回溯程式碼，以便程式碼的第一個位元組告知程式碼的總大小 (以位元組為單位)，以及指令資料流中對應的 opcode 大小。 若要計算序言或結尾的大小，從序列的開頭到結尾查核回溯程式碼，並使用查閱資料表或類似方法，來判定對應 opcode 的長度。

回溯程式碼 0xFD 和 0xFE 等同於一般結束程式碼 0xFF，但在結尾中，會負責處理額外的一個 nop作業碼，16 位元或 32 位元。 對於序言，程式碼 0xFD、0xFE 及 0xFF 完全相等。 這會負責處理一般結尾結束符號 `bx lr` 或 `b <tailcall-target>`，其沒有等同的序言指令。 這會增加回溯序列可以在序言和結尾之間共用的機會。

在許多情況下，應該可以對序言和所有結尾使用相同的回溯程式碼集。 不過，若要處理部分執行序言和結尾的回溯，您可能需要具有順序或行為不同的多個回溯程式碼序列。 這就是為什麼每一個結尾對回溯陣列都有自己的索引，以顯示開始執行的位置。

### <a name="unwinding-partial-prologues-and-epilogues"></a>回溯部分序言和結尾

最常見的回溯情況是在遠離序言和所有結尾的函式主體中發生例外狀況。 在此情況下，回溯器會執行回溯陣列中從索引 0 開始的程式碼，然後繼續直到偵測到結尾 opcode。

當序言或結尾執行時，如果發生例外狀況，則僅會部分地建構堆疊框架，且回溯器必須確切判定發生了什麼，以便正確進行復原。

例如，假設如下序言和結尾序列：

```asm
0000:   push  {r0-r3}         ; 0x04
0002:   push  {r4-r9, lr}     ; 0xdd
0006:   mov   r7, sp          ; 0xc7
...
0140:   mov   sp, r7          ; 0xc7
0142:   pop   {r4-r9, lr}     ; 0xdd
0146:   add   sp, sp, #16     ; 0x04
0148:   bx    lr
```

在每一個作業碼旁邊，是用於描述此作業的適當回溯程式碼。 序言的回溯程式碼序列是結尾之回溯程式碼的鏡像，不包括最終的指令。 這屬於常見情況，也是為什麼序言的回溯程式碼一律假定為以序言執行的反向順序來儲存。 以下為我們提供常見的回溯程式碼集：

```asm
0xc7, 0xdd, 0x04, 0xfd
```

0xFD 程式碼是序列結束的特殊程式碼，表示結尾比序言長一個 16 位元的指令。 這可更好地共用回溯程式碼。

在本範例中，如果序言和結尾之間的函式主體執行時發生例外狀況，則回溯會從結尾開始，即在結尾程式碼的位移 0 處開始。 這對應於範例中的位移 0x140。 回溯器會執行完整回溯序列，因為沒有發生任何清除。 如果是在結尾程式碼開頭之後的一個指令發生例外狀況，則回溯器可以跳過第一個回溯程式碼而成功回溯。 指定作業碼之間的一對一對應與回溯程式碼，如果從指令開始回溯*n*在結尾，則回溯器應該略過第一個*n*回溯程式碼。

對於序言，會以相反的方式執行相似的邏輯。 如果從序言中的位移 0 開始回溯，則無需執行任何動作。 如果從序言中的一個指令開始回溯，則回溯序列應該從距離結尾一個回溯程式碼處開始，因為序言回溯程式碼以相反的順序儲存。 在一般情況下，如果從指令開始回溯*n*在序言回溯應該開始執行*n*回溯程式碼從代碼清單的結尾。

序言和結尾回溯程式碼不總是完全相符的。 在該情況下，回溯程式碼陣列可能需要包含數個程式碼序列。 若要判定開始處理程式碼的位移，請使用下列邏輯：

1. 如果從函式主體內開始回溯，則從索引 0 開始執行回溯程式碼，然後繼續直到到達結束作業碼。

2. 如果從結尾內開始回溯，請使用結尾範圍提供的結尾專屬開始索引。 計算 PC 距離結尾開頭多少個位元組。 向前跳過整個回溯程式碼，直到處理所有已執行的指令為止。 執行在該位置開始的回溯序列。

3. 如果從序言內開始回溯，請從回溯程式碼的索引 0 開始。 計算序列中序言程式碼的長度，然後計算 PC 距離序言結尾多少個位元組。 向前跳過整個回溯程式碼，直到處理所有未執行的指令為止。 執行在該位置開始的回溯序列。

序言的回溯程式碼必須一律為陣列中的第一個程式碼。 在從主體內回溯的一般情況下，也使用這些程式碼來進行回溯。 任何結尾專屬程式碼序列應該緊接在序言程式碼序列之後。

### <a name="function-fragments"></a>函式片段

對於程式碼最佳化，將函式分割成不連續的部分可能更有用。 當完成此作業時，每一個函式片段都需要其自己的個別 .pdata (也可能需要 .xdata) 記錄。

假設函式序言在函式的開頭且無法分割，此時函式片段會有四種情況：

- 只有序言；所有結尾都在其他片段中。

- 序言和一個或多個結尾；其他結尾在其他片段中。

- 無序言或結尾；序言及一個或多個結尾在其他片段中。

- 只有結尾；序言和可能的其他結尾在其他片段中。

在第一種情況中，只有序言是必須描述的。 做法是在精簡.pdata 中正常描述序言，並指定*Ret*值為 3，指出無結尾。 在完整 .xdata 格式中，透過像平常那樣在索引 0 處提供序言回溯程式碼，並指定結尾計數為 0，來完成此作業。

第二種情況就像正常的函式。 如果片段中僅有一個結尾，且其在片段結束的位置，則可以使用精簡的 .pdata 記錄。 否則，必須使用 .xdata 記錄。 請記住，針對結尾開頭指定的位移相對於片段的開頭，而不是函式的原始開頭位置。

第三種和第四種情況分別是第一種和第二種情況的變異，只是它們不包含序言。 在這些條件下，會假設在結尾的開頭之前存在程式碼，且其被視為函式主體的一部分，通常透過復原序言的影響，對其進行回溯。 因此，上述情況必須以虛擬序言編碼，其會描述如何從主體內部進行回溯，但當判定是否在片段開頭執行部分回溯時，它會被視為 0 長度。 或者，透過使用與結尾相同的回溯程式碼，也可能描述此虛擬序言，因為這些程式碼假定執行相等的作業。

在第三個和第四個案例中，虛擬序言的存在會指定可能藉由設定*旗標*欄位設為 2，或藉由設定將精簡.pdata 記錄*F* 1.xdata 標頭中的旗標。 任何一種情況，都會忽略對部分序言回溯的檢查，且所有非結尾回溯都會被視為完整的。

#### <a name="large-functions"></a>大型函式

片段可用於描述大於 512 KB 限制的函式，該限制由 .xdata 標頭中的位元欄位施加。 若要描述非常大的函式，只要將其分成小於 512 KB 的片段即可。 每一個片段都應該進行調整，以便其不會將結尾分割成多個片段。

只有函式的第一個片段包含序言；所有其他片段都標記為無序言。 視結尾的數目而定，每一個片段可能包含零個或多個結尾。 請記住，片段中的每一個結尾範圍都會指定其相對於片段開頭，而不是函式開頭的開始位移。

如果片段沒有序言和結尾，則它仍需要自己的 .pdata (也可能需要 .xdata) 記錄，以描述如何從函式的主體內進行回溯。

#### <a name="shrink-wrapping"></a>壓縮包裝

函式片段的較複雜特殊情況是*包裝*，延後註冊技術可以節省從一開始要稍後函式，以簡單的情況下，不需要暫存器儲存最佳化的函式。 這可描述為外部區域配置堆疊空間，但儲存最少的一組暫存器，而內部區域則儲存並還原其他暫存器。

```asm
ShrinkWrappedFunction
    push   {r4, lr}          ; A: save minimal non-volatiles
    sub    sp, sp, #0x100    ; A: allocate all stack space up front
    ...                      ; A:
    add    r0, sp, #0xE4     ; A: prepare to do the inner save
    stm    r0, {r5-r11}      ; A: save remaining non-volatiles
    ...                      ; B:
    add    r0, sp, #0xE4     ; B: prepare to do the inner restore
    ldm    r0, {r5-r11}      ; B: restore remaining non-volatiles
    ...                      ; C:
    pop    {r4, pc}          ; C:
```

通常，會預期壓縮包裝函式為一般序言中的額外暫存器儲存預先配置空間，然後使用 `str` 或 `stm` 而不是 `push`，來執行暫存器儲存。 這可將所有堆疊指標操作保持在函式的原始序言中。

範例壓縮包裝函式必須分成三個區域，在註解中分別標記為 A、B 及 C。 第一個 A 區域涵蓋函式的開頭到其他靜態儲存的結尾。 必須建構 .pdata 或 .xdata 記錄，以將此片段描述為具有序言而沒有結尾。

中間的 B 區域會取得自己的 .pdata 或 .xdata 記錄，以描述沒有序言和結尾的片段。 不過，此區域的回溯程式碼必須仍存在，因為其會被視為函式主體。 程式碼必須描述複合序言，該序言代表儲存在區域 A 序言中的原始暫存器，以及進入區域 B 之前儲存的其他暫存器，就像它們由一序列作業產生的一樣。

區域 B 的暫存器儲存無法被視為「內部序言」，因為針對區域 B 描述的複合序言必須描述區域 A 序言和儲存的其他暫存器。 如果片段 B 描述為具有序言，則回溯程式碼還會隱含該序言的大小，且無法使用僅儲存其他暫存器的作業碼，以一對一對應的方式，描述複合序言。

其他暫存器儲存必須被視為區域 A 的部分，因為在它們完成之前，複合序言不會準確地描述堆疊的狀態。

最後的 C 區域會取得自己的 .pdata 或 .xdata 記錄，以描述沒有序言但有結尾的片段。

如果進入區域 B 之前完成的堆疊操作可以減少為一個指令，則替代方法也可以運作：

```asm
ShrinkWrappedFunction
    push   {r4, lr}          ; A: save minimal non-volatile registers
    sub    sp, sp, #0xE0     ; A: allocate minimal stack space up front
    ...                      ; A:
    push   {r4-r9}           ; A: save remaining non-volatiles
    ...                      ; B:
    pop    {r4-r9}           ; B: restore remaining non-volatiles
    ...                      ; C:
    pop    {r4, pc}          ; C: restore non-volatile registers
```

這裡的關鍵是在每一個指令界限上，堆疊完全與區域的回溯程式碼一致。 在此範例中，如果內部推入之前發生回溯，則它會被視為區域 A 的一部分，且僅會回溯區域 A 序言。 如果內部推入之後發生回溯，則會視為區域 B，也沒有序言，但具有描述內部推入和來自區域 a 類似邏輯的原始序言的回溯程式碼的一部分保存對於內部彈出。

### <a name="encoding-optimizations"></a>編碼最佳化

由於回溯程式碼很豐富，且能夠利用資料的精簡和擴充形式，所以有很多機會可以最佳化編碼，以進一步減少空間。 如果主動使用這些技術，可以將使用回溯程式碼之描述函式和片段的凈額外負荷變得非常小。

最重要的最佳化是要仔細，不要將用於回溯的序言/結尾界限，與編譯器視角的邏輯序言/結尾介面相混淆。 回溯界限可以壓縮，變得更緊密，以提高效率。 例如，在堆疊設定執行其他驗證檢查之後，序言可能包含程式碼。 但在所有堆疊操作完成之後，不需要對進一步作業進行編碼，超過該作業的任何項目都可以從回溯序言移除。

這一相同規則同樣適用於函式長度。 如果存在遵循函式中結尾的資料 (例如，常值集區)，則不應該包含該資料，以做為函式長度的一部分。 透過將函式壓縮為僅為函式一部分的程式碼，則結尾正好位於結束位置的機會會大很多，且可以使用精簡的 可以使用 .pdata 記錄。

在序言中，如果堆疊指標已儲存至其他暫存器，則通常不需要記錄任何進一步的作業碼。 若要回溯函式，要做的第一件事是從已儲存的暫存器復原 SP，以便進一步作業不會對回溯產生任何影響。

單指令結尾無需編碼為範圍或回溯程式碼。 如果在該指令執行之前發生回溯，則可以假定回溯來自函式的主體內，只要執行序言回溯程式碼即已足夠。 如果在執行單一指令之後發生回溯，則根據定義，它會發生在其他區域。

多指令結尾無需對結尾的第一個指令進行編碼，鑒於與上一點相同的原因：如果在該指令執行之前發生回溯，則完整序言回溯即已足夠。 如果在該指令之後發生回溯，則僅需要考慮後續作業即可。

應該主動重複使用回溯程式碼。 每一個結尾範圍指定的索引會指向回溯程式碼陣列中的任意開始點。 它無需指向前一個序列的開頭；它可以指向中間。 這裡所述的最佳方法是產生所需的程式碼序列，然後在序列的已編碼集區中，掃描是否存在確切的位元組相符項，並使用任何完美相符項，做為重複使用的起點。

如果在忽略單一指令結尾之後，沒有其餘的結尾，請考量使用精簡 .pdata 形式；這會更有可能缺少結尾。

## <a name="examples"></a>範例

在下列範例中，映像檔基礎位於 0x00400000。

### <a name="example-1-leaf-function-no-locals"></a>範例 1：分葉函式，無區域變數

```asm
Prologue:
  004535F8: B430      push        {r4-r5}
Epilogue:
  00453656: BC30      pop         {r4-r5}
  00453658: 4770      bx          lr
```

.pdata (固定，2 個字組)：

- 字組 0

   - *函式開始 RVA* = 的 0x000535F8 （= 0x004535F8 0x00400000）

- 字組 1

   - *旗標*= 1，指出標準序言和結尾格式

   - *函式長度*= 0x31 （= 0x62/2）

   - *Ret* = 1，指出 16 位元分支傳回

   - *H* = 0，指出參數不主目錄

   - *R*= 0 和*Reg* = 1，指出推入/彈出 r4-r5

   - *L* = 0，指出無 LR 儲存/還原

   - *C* = 0，指出無框架鏈結

   - *堆疊調整*= 0，指出無堆疊調整

### <a name="example-2-nested-function-with-local-allocation"></a>範例 2：具有區域配置的巢狀函式

```asm
Prologue:
  004533AC: B5F0      push        {r4-r7, lr}
  004533AE: B083      sub         sp, sp, #0xC
Epilogue:
  00453412: B003      add         sp, sp, #0xC
  00453414: BDF0      pop         {r4-r7, pc}
```

.pdata (固定，2 個字組)：

- 字組 0

   - *函式開始 RVA* = 0x000533AC (= 0x004533AC-0x00400000)

- 字組 1

   - *旗標*= 1，指出標準序言和結尾格式

   - *函式長度*= 0x35 （= 0x6A/2）

   - *Ret* = 0，指出彈出 {pc} 傳回

   - *H* = 0，指出參數不主目錄

   - *R*= 0 和*Reg* = 3，指出推入/彈出 r4-r7

   - *L* = 1，指出 LR 儲存/還原

   - *C* = 0，指出無框架鏈結

   - *堆疊調整*= 的 3 （= 0x0C/4）

### <a name="example-3-nested-variadic-function"></a>範例 3：巢狀的 Variadic 函式

```asm
Prologue:
  00453988: B40F      push        {r0-r3}
  0045398A: B570      push        {r4-r6, lr}
Epilogue:
  004539D4: E8BD 4070 pop         {r4-r6}
  004539D8: F85D FB14 ldr         pc, [sp], #0x14
```

.pdata (固定，2 個字組)：

- 字組 0

   - *函式開始 RVA* = 的 0x00053988 （= 0x00453988 0x00400000）

- 字組 1

   - *旗標*= 1，指出標準序言和結尾格式

   - *函式長度*= 0x2A （= 0x54/2）

   - *Ret* = 0，指出彈出 {pc}-樣式傳回 （在此情況下 release，ldr pc 上，[sp]，pc,[sp],#0x14 傳回值）

   - *H* = 1，指出參數主目錄

   - *R*= 0 和*Reg* = 2，指出推入/彈出 r4-r6

   - *L* = 1，指出 LR 儲存/還原

   - *C* = 0，指出無框架鏈結

   - *堆疊調整*= 0，指出無堆疊調整

### <a name="example-4-function-with-multiple-epilogues"></a>範例 4：具有多個結尾的函式

```asm
Prologue:
  004592F4: E92D 47F0 stmdb       sp!, {r4-r10, lr}
  004592F8: B086      sub         sp, sp, #0x18
Epilogues:
  00459316: B006      add         sp, sp, #0x18
  00459318: E8BD 87F0 ldm         sp!, {r4-r10, pc}
  ...
  0045943E: B006      add         sp, sp, #0x18
  00459440: E8BD 87F0 ldm         sp!, {r4-r10, pc}
  ...
  004595D4: B006      add         sp, sp, #0x18
  004595D6: E8BD 87F0 ldm         sp!, {r4-r10, pc}
  ...
  00459606: B006      add         sp, sp, #0x18
  00459608: E8BD 87F0 ldm         sp!, {r4-r10, pc}
  ...
  00459636: F028 FF0F bl          KeBugCheckEx     ; end of function
```

.pdata (固定，2 個字組)：

- 字組 0

   - *函式開始 RVA* = 的 0x000592F4 （= 0x004592F4 0x00400000）

- 字組 1

   - *旗標*= 0，指出存在.xdata 記錄 （必要項，因為多個結尾）

   - *.xdata address* - 0x00400000

.xdata (變數，6 個字組)：

- 字組 0

   - *函式長度*= 的 0x0001A3 （= 0x000346/2）

   - *Vers* = 0，指出 xdata 的第一個版本

   - *X* = 0，指出無例外狀況資料

   - *E* = 0，指出結尾範圍清單

   - *F* = 0，指出完整函式描述，包括序言

   - *結尾計數*= 0x04，指出 4 個結尾範圍

   - *程式碼字組*= 0x01，指出回溯程式碼的一個 32 位元字組

- 字組 1-4，描述 4 個位置的 4 個結尾範圍。 每一個範圍都具有一組常用的回溯程式碼，與序言共用，位於位移 0x00 處，且無條件，指定條件 0x0E (一律)。

- 回溯程式碼，在字組 5 處開始：(在序言/結尾之間共用)

   - 回溯程式碼 0 = 0x06:sp： 預存程序 + = (6 << 2)

   - 回溯程式碼 1 = 0xDE：pop {r4-r10, lr}

   - 回溯程式碼 2 = 0xFF：end

### <a name="example-5-function-with-dynamic-stack-and-inner-epilogue"></a>範例 5:具有動態堆疊和內部結尾的函式

```asm
Prologue:
  00485A20: B40F      push        {r0-r3}
  00485A22: E92D 41F0 stmdb       sp!, {r4-r8, lr}
  00485A26: 466E      mov         r6, sp
  00485A28: 0934      lsrs        r4, r6, #4
  00485A2A: 0124      lsls        r4, r4, #4
  00485A2C: 46A5      mov         sp, r4
  00485A2E: F2AD 2D90 subw        sp, sp, #0x290
Epilogue:
  00485BAC: 46B5      mov         sp, r6
  00485BAE: E8BD 41F0 ldm         sp!, {r4-r8, lr}
  00485BB2: B004      add         sp, sp, #0x10
  00485BB4: 4770      bx          lr
  ...
  00485E2A: F7FF BE7D b           #0x485B28    ; end of function
```

.pdata (固定，2 個字組)：

- 字組 0

   - *函式開始 RVA* = 的 0x00085A20 （= 0x00485A20 0x00400000）

- 字組 1

   - *旗標*= 0，指出存在.xdata 記錄 （由於多個結尾時需要）

   - *.xdata address* - 0x00400000

.xdata (變數，3 個字組)：

- 字組 0

   - *函式長度*= 的 0x0001A3 （= 0x000346/2）

   - *Vers* = 0，指出 xdata 的第一個版本

   - *X* = 0，指出無例外狀況資料

   - *E* = 0，指出結尾範圍清單

   - *F* = 0，指出完整函式描述，包括序言

   - *結尾計數*= 0x001，指出 1 個結尾範圍

   - *程式碼字組*= 0x01，指出回溯程式碼的一個 32 位元字組

- 字組 1:結尾範圍位移 0xC6 （= 0x18c/2），在 0x00 處，並具有條件 0x0E （一律） 開始回溯程式碼索引

- 回溯程式碼，在字組 2 處開始：(在序言/結尾之間共用)

   - 回溯程式碼 0 = 0xC6：sp = r6

   - 回溯程式碼 1 = 0xDC：pop {r4-r8, lr}

   - 回溯程式碼 2 = 0x04:sp： 預存程序 + = (4 << 2)

   - 回溯程式碼 3 = 0xFD：end，對於結尾，計數為 16 位元指令

### <a name="example-6-function-with-exception-handler"></a>範例 6:與例外狀況處理常式的函式

```asm
Prologue:
  00488C1C: 0059 A7ED dc.w  0x0059A7ED
  00488C20: 005A 8ED0 dc.w  0x005A8ED0
FunctionStart:
  00488C24: B590      push        {r4, r7, lr}
  00488C26: B085      sub         sp, sp, #0x14
  00488C28: 466F      mov         r7, sp
Epilogue:
  00488C6C: 46BD      mov         sp, r7
  00488C6E: B005      add         sp, sp, #0x14
  00488C70: BD90      pop         {r4, r7, pc}
```

.pdata (固定，2 個字組)：

- 字組 0

   - *函式開始 RVA* = 的 0x00088C24 （= 0x00488C24 0x00400000）

- 字組 1

   - *旗標*= 0，指出存在.xdata 記錄 （由於多個結尾時需要）

   - *.xdata address* - 0x00400000

.xdata (變數，5 個字組)：

- 字組 0

   - *函式長度*= 的 0x000027 （= 0x00004E/2）

   - *Vers* = 0，指出 xdata 的第一個版本

   - *X* = 1，指出存在例外狀況資料

   - *E* = 1，指出單一結尾

   - *F* = 0，指出完整函式描述，包括序言

   - *結尾計數*= 0x00，指出結尾回溯程式碼啟動位於位移 0x00 處

   - *程式碼字組*= 0x02，指出回溯程式碼的兩個 32 位元字組

- 回溯程式碼，在字組 1 處開始：

   - 回溯程式碼 0 = 0xC7：sp = r7

   - 回溯程式碼 1 = 0x05:sp： 預存程序 + = (5 << 2）。

   - 回溯程式碼 2 = 0xED/0x90：pop {r4, r7, lr}

   - 回溯程式碼 4 = 0xFF：end

- 字組 3 指定的例外狀況處理常式 = 0x0019A7ED (= 0x0059A7ED-0x00400000)

- 字組 4 及以上為內嵌例外狀況資料

### <a name="example-7-funclet"></a>範例 7:Funclet

```asm
Function:
  00488C72: B500      push        {lr}
  00488C74: B081      sub         sp, sp, #4
  00488C76: 3F20      subs        r7, #0x20
  00488C78: F117 0308 adds        r3, r7, #8
  00488C7C: 1D3A      adds        r2, r7, #4
  00488C7E: 1C39      adds        r1, r7, #0
  00488C80: F7FF FFAC bl          target
  00488C84: B001      add         sp, sp, #4
  00488C86: BD00      pop         {pc}
```

.pdata (固定，2 個字組)：

- 字組 0

   - *函式開始 RVA* = 的 0x00088C72 （= 0x00488C72 0x00400000）

- 字組 1

   - *旗標*= 1，指出標準序言和結尾格式

   - *函式長度*= 0x0B （= 0x16/2）

   - *Ret* = 0，指出彈出 {pc} 傳回

   - *H* = 0，指出參數不主目錄

   - *R*= 0 和*Reg* = 7，表示沒有暫存器未儲存/還原

   - *L* = 1，指出 LR 儲存/還原

   - *C* = 0，指出無框架鏈結

   - *堆疊調整*= 1，指出 1 × 4 位元組堆疊調整

## <a name="see-also"></a>另請參閱

[ARM ABI 慣例概觀](overview-of-arm-abi-conventions.md)<br/>
[Visual C++ ARM 移轉時常見的問題](common-visual-cpp-arm-migration-issues.md)
