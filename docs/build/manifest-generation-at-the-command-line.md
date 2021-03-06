---
title: 命令列的資訊清單產生過程
ms.date: 11/04/2016
helpviewer_keywords:
- manifests [C++]
- manifest tool (mt.exe)
ms.assetid: fc2ff255-82b1-4c44-af76-8405c5850292
ms.openlocfilehash: 37036ceedc59e20374fd1106a051ab2a66edd143
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62273772"
---
# <a name="manifest-generation-at-the-command-line"></a>命令列的資訊清單產生過程

當建置 C /C++連結器已處理所有目的檔，並建置最終二進位檔之後，會產生從命令列使用 nmake 或類似的工具、 資訊清單的應用程式。 連結器會收集儲存在目的檔中的組件資訊，並結合成最終的資訊清單檔案的這項資訊。 根據預設，連結器會產生名為的檔案*binary_name*。*延伸模組*以描述最終二進位檔。 連結器不會內嵌於二進位檔的資訊清單檔，並只會產生資訊清單中的，外部檔案。 有數種方式可內嵌於最終的二進位檔，例如使用資訊清單[資訊清單工具 (mt.exe)](https://msdn.microsoft.com/library/aa375649)或編譯成資源檔的資訊清單。 請務必記住，特定的規則有內嵌於最終的二進位檔，以啟用累加連結，這類功能的資訊清單時所需遵循簽章，以及編輯後繼續。 中會討論這些和其他選項[How to:內嵌資訊清單內的 C /C++應用程式](how-to-embed-a-manifest-inside-a-c-cpp-application.md)建置命令列上時。

## <a name="see-also"></a>另請參閱

[資訊清單](/windows/desktop/sbscs/manifests)<br/>
[/INCREMENTAL (以累加方式連結)](reference/incremental-link-incrementally.md)<br/>
[強式名稱組件 (組件簽署) (C++/CLI)](../dotnet/strong-name-assemblies-assembly-signing-cpp-cli.md)<br/>
[編輯後繼續](/visualstudio/debugger/edit-and-continue)<br/>
[了解 C/C++ 程式的資訊清單產生過程](understanding-manifest-generation-for-c-cpp-programs.md)<br/>
