---
title: ARM64 ABI 慣例概觀
ms.date: 03/27/2019
ms.openlocfilehash: bfb1b5b6be6a7a368c2ed7cab255da90ae7a22df
ms.sourcegitcommit: da32511dd5baebe27451c0458a95f345144bd439
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/07/2019
ms.locfileid: "65220983"
---
# <a name="overview-of-arm64-abi-conventions"></a>ARM64 ABI 慣例概觀

基本應用程式二進位介面 (ABI)，針對 Windows 編譯時，在大多數情況下，（ARMv8 或更新版本的架構） 的 64 位元模式中的 ARM 處理器上的執行會遵循 ARM 的標準 AArch64 EABI。 這篇文章強調一些主要的假設和 EABI 中記錄的變更。 32 位元 ABI 的相關資訊，請參閱[概觀的 ARM ABI 慣例](overview-of-arm-abi-conventions.md)。 如需有關標準 ARM EABI 的詳細資訊，請參閱 <<c0> [ 應用程式二進位介面 (ABI)，適用於 ARM 架構](http://infocenter.arm.com/help/index.jsp?topic=/com.arm.doc.subset.swdev.abi/index.html)（外部連結）。

## <a name="definitions"></a>定義

使用 64 位元支援的引進，ARM 已定義數個詞彙：

- **AArch32** – 舊版的 32 位元指令集架構 (ISA) 定義 ARM，包括 Thumb 模式下執行。
- **AArch64** – 新的 64 位元指令集架構 (ISA) ARM 所定義。
- **ARMv7** – 「 第 7 層代 」 的規格只包含 AArch32 支援的 ARM 硬體。 這個版本的 ARM 硬體是第一版的支援的 ARM Windows。
- **ARMv8** – 「 第 8 個層代 」 的規格包含支援 AArch32 和 AArch64 的 ARM 硬體。

Windows 也會使用下列詞彙：

- **ARM** – 指的是 32 位元 ARM 架構 (AArch32)，有時稱為 WoA (在 ARM 上的 Windows)。
- **ARM32** – 相同 ARM，上述; 為了清楚起見，本文件使用。
- **ARM64** – 指的是 64 位元 ARM 架構 (AArch64)。 沒有任何這類 WoA64 一樣。

最後，當參考資料型別，會參考來自 ARM 的下列定義：

- **短向量**– SIMD，向量的 8 個位元組或 16 個位元組的價值的項目直接代表的資料類型。 它會對齊其大小，8 個位元組或 16 個位元組，其中每個項目可以是 1、 2、 4 或 8 個位元組。
- **HFA （同質浮點彙總）** – 2 到 4 相同浮點成員的資料類型是浮點數或加倍。
- **（同質短向量彙總） 的 HVA** – 2 到 4 短向量成員相同的資料類型。

## <a name="base-requirements"></a>基底的需求

ARMv8 上執行，或更新版本的架構在任何時候，前提是 Windows 的 ARM64 版本。 兩者的浮點數和 NEON 支援都假設為會出現在 硬體。

ARMv8 規格允許 AArch32 應用程式的完整支援。 不過，不計劃 ARM64 版本的 Windows 上的現有 ARM32 應用程式的支援。 （也就是有 WOW64 並未規劃推出）。 這項支援受到重新評估在未來，但目前的工作假設。

ARMv8 規格會說明新的選擇性密碼編譯和 CRC helper opcode AArch32 和 AArch64。 目前選用項目，但建議使用支援它們。 若要利用這些作業碼，應用程式應該先將執行階段檢查其存在。

## <a name="endianness"></a>位元組序

為使用 ARM32 版本的 ARM64 Windows 上的 Windows，由小到大在模式中執行。 切換位元組序就會很難達成而 AArch64，在核心模式的支援，因此很容易就能強制執行。

## <a name="alignment"></a>對齊

ARM64 上執行的 Windows 可讓 CPU 硬體無障礙地處理未對齊的存取。 從 AArch32 有所改進，在這項支援現在也適用於所有 （包括多字存取） 的整數存取以及浮點數的存取。

不過，存取未快取 （裝置） 的記憶體仍必須一律對齊。 如果程式碼可能無法讀取或寫入未對齊的資料從取消快取的記憶體，它必須確定符合所有的存取。

[區域變數] 的預設版面配置對齊：

| 大小 （位元組） | 以位元組為單位的對齊方式 |
| - | - |
| 1 | 1 |
| 2 | 2 |
| 3, 4 | 4 |
| > 4 | 8 |

全域和靜態變數的預設版面配置對齊：

| 大小 （位元組） | 以位元組為單位的對齊方式 |
| - | - |
| 1 | 1 |
| 2 - 7 | 4 |
| 8 - 63 | 8 |
| >= 64 | 16 |

## <a name="integer-registers"></a>整數暫存器

AArch64 架構支援 32 整數暫存器：

| 登錄 | 動態？ | 角色 |
| - | - | - |
| x0 | 動態 | 參數/從頭開始註冊 1，結果註冊 |
| x1-x7 | 動態 | 參數/從頭開始註冊 2-8 |
| x8-x15 | 動態 | 臨時暫存器 |
| x16-x17 | 動態 | 內部程序呼叫臨時暫存器 |
| x18 | 靜態 | 平台註冊： 在核心模式中，指向 KPCR 目前的處理器。在使用者模式中，指向 TEB |
| x19-x28 | 靜態 | 臨時暫存器 |
| x29/fp | 靜態 | 框架指標 |
| x30/lr | 靜態 | 連結暫存器 |

為完整的 64 位元值 （透過 x0 x30) 或 32 位元值 （透過 w0 w30)，就能存取每個註冊。 32 位元 operations 零擴充其結果最多 64 位元。

參數傳遞參數暫存器使用的區段，如需詳細資訊，請參閱。

不同於 AArch32，程式計數器 (PC) 和堆疊指標 (SP) 不是索引暫存器。 這些限制中如何存取它們。 也請注意，有沒有 x31 註冊。 該編碼方式，用於特殊用途。

框架指標 (x29) 是為了與快速堆疊查核行程 ETW 和其他服務所使用的相容性。 它必須指向上一個 {x29，x 30} 組堆疊上的。

## <a name="floating-pointsimd-registers"></a>浮點點對點/SIMD 暫存器

AArch64 架構也支援 32 浮點點對點/SIMD 暫存器，摘要如下：

| 登錄 | 動態？ | 角色 |
| - | - | - |
| v0 | 動態 | 參數/從頭開始註冊 1，結果註冊 |
| v1-v7 | 動態 | 參數/從頭開始註冊 2-8 |
| v8-v15 | 靜態 | 臨時暫存器 （僅限較低 64 個位元都是靜態） |
| v16-v31 | 動態 | 臨時暫存器 |

每個註冊為完整的 128 位元值 （透過 v0 v31 或 q0 q31） 存取。 便能存取 （透過 d0-d31) 的 64 位元值為 32 位元值 （透過 s0-s31) 為 16 位元值 （透過 h0-h31)，或為 8 位元值 （透過 b0 b31)。 小於 128 位元的存取只能存取完整的 128 位元暫存器的較低的位元。 它們不會影響其餘的位元除非另有指定。 （AArch64 是不同於 AArch32，其中較小的暫存器已封裝上的較大的暫存器）。

浮點控制暫存器 (FPCR) 中各種不同的位元欄位上有特定需求：

| Bits | 意義 | 動態？ | 角色 |
| - | - | - | - |
| 26 | AHP | 非 Volatile | 替代半精確度控制。 |
| 25 | DN | 非 Volatile | 預設 NaN 模式控制。 |
| 24 | FZ | 靜態 | 清除為零模式控制。 |
| 23-22 | RMode | 靜態 | 捨入模式控制。 |
| 15,12-8 | IDE/IXE/etc | 非 Volatile | 例外狀況截取啟用位元，必須一律為 0。 |

## <a name="system-registers"></a>系統暫存器

AArch32，例如 AArch64 規格會提供三個系統控制 「 執行緒 ID 」 暫存器：

| 登錄 | 角色 |
| - | - |
| TPIDR_EL0 | 保留的。 |
| TPIDRRO_EL0 | 包含目前處理器的 CPU 數目。 |
| TPIDR_EL1 | 目前處理器的 KPCR 結構的點。 |

## <a name="floating-point-exceptions"></a>浮點例外狀況

選擇性 AArch64 系統上支援 IEEE 浮點例外狀況。 處理器變異都具有具有硬體浮點例外狀況，如 Windows 核心會以無訊息模式攔截例外狀況，並隱含 FPCR 暫存器中停用它們。 這個設陷確保處理器變異都具有標準化的行為。 否則，不含例外狀況支援的平台上開發的程式碼可能會發現本身有支援的平台上執行時，採用非預期的例外狀況。

## <a name="parameter-passing"></a>參數傳遞

對於非 variadic 函式，Windows ABI 會遵循 ARM 所傳遞的參數所指定的規則。 這些規則會直接從程序呼叫標準摘錄，AArch64 架構：

### <a name="stage-a--initialization"></a>階段 A-初始化

這個階段是一次，才能開始處理引數。

1. 下一個一般用途註冊號碼 」 (NGRN) 是設定為零。

1. 下一步 SIMD 和浮點註冊號碼 (NSRN) 是設定為零。

1. 下一個堆疊引數位址 (NSAA) 設定為目前的堆疊指標值 (SP)。

### <a name="stage-b--pre-padding-and-extension-of-arguments"></a>階段 B-預先填補和擴充功能的引數

每個引數清單中，會套用下列清單中第一個相符的規則。 如果沒有規則的相符項目引數會使用未經修改。

1. 如果引數型別是一種複合類型，其大小無法以靜態方式判斷呼叫端和被呼叫端，引數會複製到記憶體，而引數會取代所複製的指標。 (在 C 中沒有這類的型別 /C++ ，但它們存在於其他語言或語言擴充功能)。

1. 如果引數型別是 HFA 或 HVA，則使用引數未修改。

1. 如果引數型別是複合類型超過 16 個位元組，那麼引數會複製到呼叫端配置的記憶體和引數被複製的指標。

1. 如果引數型別是一種複合類型，則引數的大小會無條件進位到最接近的 8 個位元組的倍數。

### <a name="stage-c--assignment-of-arguments-to-registers-and-stack"></a>階段 C-引數指派給暫存器和堆疊

每個引數清單中，，直到已配置的引數，會依次套用下列規則。 當引數指派給暫存器中時，任何未使用的位元登錄中未指定值。 如果引數指派給堆疊位置時，任何未使用的填補位元組有未指定值。

1. 如果引數是半-、 單一、 雙精度浮點數-或四組數字單精確度浮點數或短向量類型和 NSRN 小於 8，則引數會配置到最小顯著性的位元暫存器 v\[NSRN]。 NSRN 都會加一。 現在已配置的引數。

1. 如果引數是 HFA 或 hva 使用即可，而且有足夠的未配置的 SIMD 和浮點數暫存器 （NSRN + 成員 ≤ 8 數目），則引數是 SIMD 和浮點數暫存器，每個成員的 HFA 或 HVA 一個暫存器配置。 NSRN 會依使用的暫存器號碼遞增。 現在已配置的引數。

1. 如果 HFA 或 HVA 引數，則 NSRN 會設定為 8，和引數的大小會四捨五入至最接近的 8 個位元組的倍數。

1. 如果引數是 HFA HVA、 四組數字單精確度浮點數或短向量類型，則 NSAA 會無條件進位至較大的一個 8 或引數的型別自然對齊。

1. 如果引數的一半或單精確度浮點數型別，則引數的大小會設定為 8 個位元組。 效果會如同引數必須已複製到最小顯著性的位元的 64 位元暫存器，而且其餘的位元填入未指定的值。

1. 如果引數是 HFA，HVA、 半-、 單一、 雙精度浮點數-或四組數字單精確度浮點數或短向量類型，則引數會複製到已調整的 nsaa 記憶體中。 NSAA 會增加引數的大小。 現在已配置的引數。

1. 如果引數是整數或指標類型，引數的大小小於或等於 8 個位元組，而且 NGRN 為少於 8，引數會複製到中 x 的最小顯著性位元\[NGRN]。 NGRN 都會加一。 現在已配置的引數。

1. 如果引數具有 16 的對齊方式，然後 NGRN 會無條件進位到下一個偶數。

1. 如果引數是整數型別、 引數的大小等於 16 和 NGRN 為少於 7，引數會複製到 x\[NGRN] 和 x\[NGRN + 1]。 x\[NGRN] 應該包含較低定址的雙字組引數的記憶體表示法。 NGRN 會增加兩個。 現在已配置的引數。

1. 如果引數是一種複合類型，而且引數的雙精度浮點數字的大小是不超過 8 減去 NGRN，則引數會複製到連續一般用途的暫存器，開始 x\[NGRN]。 引數會如同它已載入的暫存器，從雙精度浮點數字對齊位址，以及從記憶體載入連續的暫存器的 release，LDR 指示的適當順序。 暫存器的任何未使用組件的內容都不會指定此標準。 NGRN 會依使用的暫存器號碼遞增。 現在已配置的引數。

1. NGRN 設為 8。

1. NSAA 會無條件進位至較大的一個 8 或引數的型別自然對齊。

1. 如果引數是一種複合類型，然後將引數會複製到已調整的 nsaa 的記憶體。 NSAA 會增加引數的大小。 現在已配置的引數。

1. 如果引數的大小小於 8 個位元組，則引數的大小會設定為 8 個位元組。 效果就如同引數已複製到 64 位元暫存器的最小顯著性位元和其餘的位元已填入未指定的值。

1. 引數會複製到已調整的 nsaa 的記憶體。 NSAA 會增加引數的大小。 現在已配置的引數。

### <a name="addendum-variadic-functions"></a>附錄：Variadic 函式

接受可變數目的引數的函式的處理方式不同於上述，如下所示：

1. 所有的複合應用程式的處理很類似;HFAs 或 Hva 特別的處置。

1. 不使用 SIMD 和浮點數暫存器。

實際上，它相當於下列規則 C.12–C.15 配置虛數的堆疊，其中前 64 個位元組堆疊的載入 x0 x7，而通常放置任何其餘的堆疊引數的引數。

## <a name="return-values"></a>傳回值

X0 會傳回整數值。

S0、 d0，或 v0，視需要，會傳回浮點數的值。

S0 s3、 d0-d3 或 v0 v3，適當地傳回 HFA 和 HVA 值。

傳值方式傳回的類型取決於它們是否具有特定屬性的處理方式不同。 有所有這些屬性的類型

- 它們*彙總*根據 C + + 14 標準定義，也就是它們有沒有使用者提供的建構函式、 沒有私用或受保護的非靜態資料成員、 基底類別，並沒有虛擬函式，以及
- 它們具有 trivial 複製指派運算子，以及
- 它們有 trivial 解構函式

使用下列傳回樣式：

- 小於或等於 8 個位元組 x0 中傳回的類型。
- 小於或等於 16 個位元組 x0 x1，以包含較低順序的 8 個位元組的 x0 中傳回的類型。
- 對於大於 16 個位元組的型別，呼叫端都應該保留足夠的大小和對齊方式，用於儲存結果的記憶體區塊。 記憶體區塊的位址應該做為額外的引數傳遞給 x8 中的函式。 被呼叫端可能副常式執行期間修改結果的記憶體區塊，在任何時間點。 被呼叫者不一定要保留 x8 中儲存的值。

所有其他型別會使用此慣例：

- 呼叫端都應該保留足夠的大小和對齊方式，用於儲存結果的記憶體區塊。 X0，或 x1 函式都應該記憶體區塊的位址傳遞做為額外的引數，如果這被傳遞 $ x0 中。 被呼叫端可能副常式執行期間修改結果的記憶體區塊，在任何時間點。 被呼叫端會傳回 x0 中的記憶體區塊的位址。

## <a name="stack"></a>堆疊

詳述加 ARM ABI，下列堆疊必須保持 16 位元組對齊在所有的時間。 AArch64 包含預存程序不是 16 位元組對齊，且預存程序相對載入或儲存時完成時，會產生堆疊對齊錯誤數目的硬體功能。 Windows 會執行隨時啟用這項功能。

4k 或多個值得堆疊配置的函式必須確定之前的最後一頁的每個頁面都會被接觸到的順序。 此動作可確保沒有任何程式碼可以 「 跳過 」 Windows 用於擴充堆疊的防護頁面。 通常觸碰由`__chkstk`協助程式，有自訂的呼叫慣例傳遞堆疊配置總量除以 16 x15。

## <a name="red-zone"></a>紅色區域

保留供分析和動態修補案例正下方的目前的堆疊指標的 16 位元組區域。 這個區域允許小心產生程式碼來插入儲存在兩個暫存器 [sp，# 16] 並臨時用它們進行任意目的。 Windows 核心可保證，如果例外狀況或中斷採取，在使用者和核心模式中，不覆寫這些 16 個位元組。

## <a name="kernel-stack"></a>核心堆疊

在 Windows 中的預設核心模式堆疊是六頁 (24 k)。 在核心模式中，請特別注意具有大型堆疊緩衝區的函式。 要中斷可能帶來少許的空餘空間，並建立堆疊異常錯誤檢查。

## <a name="stack-walking"></a>堆疊查核行程

在 Windows 內的程式碼會編譯啟用框架指標 ([/Oy-](reference/oy-frame-pointer-omission.md)) 若要啟用快速堆疊查核行程。 一般而言，x29 (fp) 指向下一個連結，在鏈結中，也就是 {fp，lr} 配對，表示前一個框架在堆疊上，傳回的位址指標。 第三方程式碼建議啟用框架指標，以提供改良的程式碼剖析和追蹤。

## <a name="exception-unwinding"></a>例外狀況回溯

透過使用回溯程式碼，協助使用回溯例外狀況處理期間。 回溯程式碼是.xdata 區段的可執行檔中儲存的位元組序列。 使得函式序言的影響可以復原在備份至呼叫者堆疊框架的準備，它們可以描述抽象的方式的序言和結尾的作業。 如需有關回溯程式碼的詳細資訊，請參閱 < [ARM64 例外狀況處理](arm64-exception-handling.md)。

ARM EABI 也會指定的例外狀況回溯模型會使用回溯程式碼。 不過，如上所示的規格並不足以回溯，因為在 Windows，必須處理電腦所在的函式序言或結尾中間的情況。

動態產生的程式碼應該與透過動態函式表格描述`RtlAddFunctionTable`和相關函式，以便產生的程式碼可以參與例外狀況處理。

## <a name="cycle-counter"></a>週期計數器

支援週期計數器所需的所有 ARMv8 Cpu 暫存器，Windows 會設定為可讀取任何層級的例外狀況，包括使用者模式的 64 位元暫存器。 它可以存取透過特殊 PMCCNTR_EL0 註冊，請在 組件的程式碼中使用 MSR opcode 或`_ReadStatusReg`內建函式在 C /C++程式碼。

週期計數器是真正的週期的計數器，而不是牆上的時鐘。 計數的頻率會隨著處理器頻率而定。 如果您認為您必須知道週期計數器的頻率，您不應使用循環計數器。 相反地，在您想要測量時鐘時間，您應該用於`QueryPerformanceCounter`。

## <a name="see-also"></a>另請參閱

[Visual C++ ARM 移轉時常見的問題](common-visual-cpp-arm-migration-issues.md)<br/>
[ARM64 例外狀況處理](arm64-exception-handling.md)
