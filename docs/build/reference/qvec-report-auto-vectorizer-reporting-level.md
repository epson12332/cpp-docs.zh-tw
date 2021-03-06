---
title: /Qvec-report (自動向量化工具報告層級)
ms.date: 11/04/2016
ms.assetid: 4778c9a3-0692-4085-9b05-1bfeadf4c74a
ms.openlocfilehash: 655be3581eee4b23a8d0f2bcfaea7d07c8b1b07c
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62319248"
---
# <a name="qvec-report-auto-vectorizer-reporting-level"></a>/Qvec-report (自動向量化工具報告層級)

可讓編譯器的報告功能[Auto-vectorizer](../../parallel/auto-parallelization-and-auto-vectorization.md) ，並在編譯期間指定的輸出參考用訊息層級。

## <a name="syntax"></a>語法

```
/Qvec-report:{1}{2}
```

## <a name="remarks"></a>備註

**/Qvec-report:1**<br/>
輸出會向量化的迴圈的告知性訊息。

**/Qvec-report:2**<br/>
輸出會向量化的迴圈和迴圈未向量化，連同原因碼的參考用訊息。

如需原因代碼和訊息的詳細資訊，請參閱[向量化工具和平行化工具訊息](../../error-messages/tool-errors/vectorizer-and-parallelizer-messages.md)。

### <a name="to-set-the-qvec-report-compiler-option-in-visual-studio"></a>若要在 Visual Studio 中設定 /Qvec-report 編譯器選項

1. 在 [ **方案總管**] 中，開啟專案的捷徑功能表，然後選擇 [ **屬性**]。

1. 在 **屬性頁**對話方塊的  **C /C++**，選取**命令列**。

1. 在 **其他選項**方塊中，輸入`/Qvec-report:1`或`/Qvec-report:2`。

### <a name="to-set-the-qvec-report-compiler-option-programmatically"></a>以程式設計方式設定 /Qvec-report 編譯器選項

- 請使用 <xref:Microsoft.VisualStudio.VCProjectEngine.VCCLCompilerTool.AdditionalOptions%2A> 中的範例程式碼。

## <a name="see-also"></a>另請參閱

[/Q 選項 (低階運算)](q-options-low-level-operations.md)<br/>
[MSVC 編譯器選項](compiler-options.md)<br/>
[MSVC 編譯器命令列語法](compiler-command-line-syntax.md)<br/>
[以原生程式碼進行平行程式設計](https://blogs.msdn.microsoft.com/nativeconcurrency/2012/04/12/auto-vectorizer-in-visual-studio-2012-overview/)
