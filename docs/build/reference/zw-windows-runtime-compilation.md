---
title: /ZW (Windows 執行階段編譯)
ms.date: 04/08/2019
f1_keywords:
- VC.Project.VCCLCompilerTool.CompileAsWinRT
- /zw
helpviewer_keywords:
- /ZW
- -ZW compiler option
- /ZW compiler option
- -ZW
- Windows Runtime compiler option
ms.assetid: 0fe362b0-9526-498b-96e0-00d7a965a248
ms.openlocfilehash: 0808f66c4d4c4e99b3038ea18a1f71f4ebaca89a
ms.sourcegitcommit: 7d64c5f226f925642a25e07498567df8bebb00d4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/08/2019
ms.locfileid: "65446173"
---
# <a name="zw-windows-runtime-compilation"></a>/ZW (Windows 執行階段編譯)

編譯原始程式碼，以支援 MicrosoftC++元件擴充功能C++的通用 Windows 平台 (UWP) app 建立 /CX。

當您使用 **/ZW**編譯時，一律指定 **/EHsc**以及。

## <a name="syntax"></a>語法

```cpp
/ZW /EHsc
/ZW:nostdlib /EHsc
```

## <a name="arguments"></a>引數

**nostdlib**<br/>
表示 Platform.winmd、Windows.Foundation.winmd 和其他預設 Windows 中繼資料 (.winmd) 檔案未自動包含在編譯中。 相反地，您必須使用[/FU (命名強制 #using 檔案)](fu-name-forced-hash-using-file.md)編譯器選項，來明確指定 Windows 中繼資料檔案。

## <a name="remarks"></a>備註

當您指定 **/ZW**選項，則編譯器支援下列功能：

- 必要的中繼資料檔案、 命名空間、 資料類型，以及應用程式需要 Windows 執行階段中執行的函式。

- Windows 執行階段物件的參考計數 」 和 「 自動捨棄物件參考計數歸零時自動。

由於 incremental linker 不支援使用包含在.obj 檔案中的 Windows 中繼資料 **/ZW**選項，已被取代[/Gm （啟用最少重建）](gm-enable-minimal-rebuild.md)選項與不相容 **/ZW**。

如需詳細資訊，請參閱 < [VisualC++語言參考](../../cppcx/visual-c-language-reference-c-cx.md)。

## <a name="requirements"></a>需求

## <a name="see-also"></a>另請參閱

[MSVC 編譯器選項](compiler-options.md)<br/>
[MSVC 編譯器命令列語法](compiler-command-line-syntax.md)
