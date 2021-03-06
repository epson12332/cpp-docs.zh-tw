---
title: /C (前置處理時保留註解)
ms.date: 11/04/2016
f1_keywords:
- VC.Project.VCCLCompilerTool.KeepComments
- /c
- VC.Project.VCCLWCECompilerTool.KeepComments
helpviewer_keywords:
- comments, not stripping during preprocessing
- preserve comments during preprocessing
- -c compiler option [C++]
- c compiler option [C++]
- /c compiler option [C++]
ms.assetid: 944567ca-16bc-4728-befe-d414a7787f26
ms.openlocfilehash: c5854fd1255ab509d8778828de25638dd821d74b
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62272828"
---
# <a name="c-preserve-comments-during-preprocessing"></a>/C (前置處理時保留註解)

在前置處理過程中保留註解。

## <a name="syntax"></a>語法

```
/C
```

## <a name="remarks"></a>備註

這個編譯器選項需要 **/E**， **/P**，或 **/EP**選項。

下列程式碼範例會顯示來源的程式碼註解。

```
// C_compiler_option.cpp
// compile with: /E /C /c
int i;   // a variable
```

此範例會產生下列輸出。

```
#line 1 "C_compiler_option.cpp"
int i;   // a variable
```

### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>在 Visual Studio 開發環境中設定這個編譯器選項

1. 開啟專案的 [屬性頁]  對話方塊。 如需詳細資訊，請參閱 <<c0> [ 設定C++Visual Studio 中的編譯器和組建屬性](../working-with-project-properties.md)。</c0>

1. 按一下 [C/C++]  資料夾。

1. 按一下 **前置處理器**屬性頁。

1. 修改**保留註解**屬性。

### <a name="to-set-this-compiler-option-programmatically"></a>若要以程式方式設定這個編譯器選項

- 請參閱 <xref:Microsoft.VisualStudio.VCProjectEngine.VCCLCompilerTool.KeepComments%2A>。

## <a name="see-also"></a>另請參閱

[MSVC 編譯器選項](compiler-options.md)<br/>
[MSVC 編譯器命令列語法](compiler-command-line-syntax.md)<br/>
[/E (前置處理至 stdout)](e-preprocess-to-stdout.md)<br/>
[/P (前置處理至檔案)](p-preprocess-to-a-file.md)<br/>
[/EP (前置處理至 stdout 不加 #line 指示詞)](ep-preprocess-to-stdout-without-hash-line-directives.md)
