---
title: /Za、/Ze (停用語言擴充功能)
ms.date: 02/19/2019
f1_keywords:
- VC.Project.VCCLWCECompilerTool.DisableLanguageExtensions
- /za
- /ze
- VC.Project.VCCLCompilerTool.DisableLanguageExtensions
helpviewer_keywords:
- -Za compiler option [C++]
- Za compiler option [C++]
- language extensions, disabling in compiler
- -Ze compiler option [C++]
- language extensions
- enable language extensions
- /Za compiler option [C++]
- /Ze compiler option [C++]
- Disable Language Extensions compiler option
- Ze compiler option [C++]
ms.assetid: 65e49258-7161-4289-a176-7c5c0656b1a2
ms.openlocfilehash: 1db1dbdba4829ccf939cdc4f07ccfefe2474a35d
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62315881"
---
# <a name="za-ze-disable-language-extensions"></a>/Za、/Ze (停用語言擴充功能)

**/Za**編譯器選項會停用，並會發出錯誤與 ANSI C89/ISO C90 不相容的 Microsoft 延伸到 C。 已被取代 **/Ze**編譯器選項會啟用 Microsoft 擴充功能。 Microsoft 擴充功能預設為啟用。

## <a name="syntax"></a>語法

> **/Za**<br/>
> **/Ze**

## <a name="remarks"></a>備註

> [!NOTE]
> 善用 **/Za**程式碼會編譯為C++不建議使用。 **/Ze**選項已被取代，因為它的行為預設為開啟。 如需已被取代的編譯器選項的清單，請參閱 <<c0> [ 已取代及已移除的編譯器選項](compiler-options-listed-by-category.md#deprecated-and-removed-compiler-options)。

Microsoft C /C++編譯器支援編譯 C 程式碼有兩種：

- 編譯器預設會使用 C 編譯模式時的原始程式檔已 *.c*延伸模組，或當[/Tc](tc-tp-tc-tp-specify-source-file-type.md)或是[/TC](tc-tp-tc-tp-specify-source-file-type.md)指定選項。 C 編譯器是 C89/C90 編譯器，預設會啟用 Microsoft 對 C 語言擴充功能。 如需特定的擴充功能的詳細資訊，請參閱[C 的 Microsoft 擴充功能和C++ ](microsoft-extensions-to-c-and-cpp.md)。 當這兩個 C 編譯並 **/Za**指定選項，C 編譯器完全符合 C89/C90 標準。 編譯器會將 Microsoft 擴充關鍵字做為簡單識別項、 停用其他的 Microsoft 擴充功能，並會自動定義[ \_ \_STDC\_ \_ ](../../preprocessor/predefined-macros.md)預先定義C 程式巨集。

- 編譯器才能編譯 C 程式碼，在C++編譯模式。 此行為是不需要的原始程式檔的預設值 *.c*延伸模組，及何時[/Tp](tc-tp-tc-tp-specify-source-file-type.md)或是[/TP](tc-tp-tc-tp-specify-source-file-type.md)指定選項。 在C++編譯模式中，編譯器支援的已納入 ISO C99 和 C11 標準的這些組件C++標準。 幾乎所有的 C 程式碼也是有效C++程式碼。 少數的 C 關鍵字和程式碼建構不是有效C++程式碼，或會解譯為以不同的方式在C++。 編譯器行為根據C++在這些情況下的標準。 在C++編譯模式 **/Za**選項可能會導致非預期的行為，不建議。

其他編譯器選項可能會影響編譯器確保符合標準的方式。 針對用來指定特定 standard C< 方法和C++行為設定，請參閱 < [/Zc](zc-conformance.md)編譯器選項。 針對其他C++標準的合規性設定，請參閱[/permissive--](permissive-standards-conformance.md)並[/std](std-specify-language-standard-version.md)編譯器選項。

如需有關具有視覺效果的一致性問題C++，請參閱[非標準行為](../../cpp/nonstandard-behavior.md)。

### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>在 Visual Studio 開發環境中設定這個編譯器選項

1. 開啟專案的 [屬性頁]  對話方塊。 如需詳細資訊，請參閱 <<c0> [ 設定C++Visual Studio 中的編譯器和組建屬性](../working-with-project-properties.md)。</c0>

1. 在 [導覽] 窗格中，選擇**組態屬性** > **C /C++** > **語言**。

1. 修改**停用語言擴充功能**屬性。

### <a name="to-set-this-compiler-option-programmatically"></a>若要以程式方式設定這個編譯器選項

請參閱 <xref:Microsoft.VisualStudio.VCProjectEngine.VCCLCompilerTool.DisableLanguageExtensions%2A>。

## <a name="see-also"></a>另請參閱

[編譯器選項](compiler-options.md)<br/>
[/Zc (一致性)](zc-conformance.md)<br/>
[/permissive- (標準一致性)](permissive-standards-conformance.md)<br/>
[/std (指定語言標準版本)](std-specify-language-standard-version.md)<br/>
