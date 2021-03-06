---
title: /vd (停用建構替代)
ms.date: 11/04/2016
f1_keywords:
- /vd
helpviewer_keywords:
- -vd0 compiler option [C++]
- vd1 compiler option [C++]
- /vdn (Disable Construction Displacement) compiler option
- constructor displacements
- vtordisp fields
- /vd0 compiler option [C++]
- -vd1 compiler option [C++]
- /vd1 compiler option [C++]
- displacements compiler option
- vd0 compiler option [C++]
- Disable Construction Displacements compiler option
ms.assetid: 93258964-14d7-4b1c-9cbc-d6f4d74eab69
ms.openlocfilehash: db198dbdc7bd43ffd4de9bde39ee81a8b95a25ab
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62316882"
---
# <a name="vd-disable-construction-displacements"></a>/vd (停用建構替代)

## <a name="syntax"></a>語法

```
/vdn
```

## <a name="arguments"></a>引數

**0**<br/>
隱藏 vtordisp 建構函式/解構函式替代成員。 選擇此選項只有在特定的所有類別建構函式和解構函式都呼叫虛擬函式幾乎。

**1**<br/>
可讓隱藏的 vtordisp 建構函式/解構函式替代成員的建立。 預設值為這項選擇。

**2**<br/>
可讓您使用[dynamic_cast 運算子](../../cpp/dynamic-cast-operator.md)上所建構的物件。 例如，從虛擬基底類別的 dynamic_cast 在衍生類別。

**/ vd2**將 vtordisp 欄位，當您有具有虛擬函式的虛擬基底。 **/ vd1**應該就已足夠。 最常見情況 **/vd2**必須是唯一的虛擬函式，在您虛擬基底解構函式時。

## <a name="remarks"></a>備註

這些選項只適用於C++使用虛擬基底的程式碼。

視覺化C++會實作C++建構位移支援在已使用虛擬繼承的情況。 建構替代解決造成虛擬函式，宣告虛擬基底和衍生類別中覆寫時的問題，進一步衍生類別的建構期間會呼叫建構函式。

虛擬函式可能會收到不正確的問題是`this`指標結果的不一致的移動為虛擬基底類別和其衍生類別的替代。 此解決方案會提供稱為 [vtordisp] 欄位中，針對每個虛擬的基底類別的單一建構替代調整。

根據預設，每當程式碼定義使用者定義的建構函式和解構函式，並也會覆寫虛擬函式的虛擬基底時，會採用 vtordisp 欄位。

這些選項會影響整個原始程式檔。 使用[vtordisp](../../preprocessor/vtordisp.md)隱藏並再重新啟用 vtordisp 欄位的類別為基礎。

### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>在 Visual Studio 開發環境中設定這個編譯器選項

1. 開啟專案的 [屬性頁]  對話方塊。 如需詳細資訊，請參閱 <<c0> [ 設定C++Visual Studio 中的編譯器和組建屬性](../working-with-project-properties.md)。</c0>

1. 按一下 [C/C++]  資料夾。

1. 按一下 [命令列]  屬性頁。

1. 在 [其他選項]  方塊中，輸入編譯器選項。

### <a name="to-set-this-compiler-option-programmatically"></a>若要以程式方式設定這個編譯器選項

- 請參閱 <xref:Microsoft.VisualStudio.VCProjectEngine.VCCLCompilerTool.AdditionalOptions%2A>。

## <a name="see-also"></a>另請參閱

[MSVC 編譯器選項](compiler-options.md)<br/>
[MSVC 編譯器命令列語法](compiler-command-line-syntax.md)
