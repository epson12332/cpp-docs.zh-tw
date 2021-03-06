---
title: 自訂 C 命令列處理
ms.date: 11/04/2016
helpviewer_keywords:
- _spawn functions
- command line, processing
- command-line processing
- startup code, customizing command-line processing
- environment, environment-processing routine
- _setargv function
- command line, processing arguments
- suppressing environment processing
- _exec function
ms.assetid: c20fa11d-b35b-4f3e-93b6-2cd5a1c3c993
ms.openlocfilehash: 1abdb0c104755efc86543ac4773359078e855999
ms.sourcegitcommit: f4be868c0d1d78e550fba105d4d3c993743a1f4b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/12/2019
ms.locfileid: "56147031"
---
# <a name="customizing-c-command-line-processing"></a>自訂 C 命令列處理

如果您的程式不接受命令列引數，您可以隱藏執行命令列處理的程式庫常式用法，藉此稍微節省空間。 這個常式稱為 **_setargv** (在寬字元環境中則稱為 **_wsetargv**)，如[展開萬用字元引數](../c-language/expanding-wildcard-arguments.md)中所述。 若要隱藏其用途，請在包含 **main** 函式的檔案中定義不執行任何動作的常式，並將此常式命名為 **_setargv** (在寬字元環境中則命名為 **_wsetargv**)。 然後，您的 **_setargv** 或 **_wsetargv** 定義將會達成對 **_setargv** 或 **_wsetargv** 的呼叫，且不會載入程式庫版本。

同樣地，如果您從未透過 `envp` 引數存取過環境資料表，則可以自行提供空的常式以取代環境處理常式 **_setenvp** (或 **_wsetenvp**)。

如果您的程式會在 C 執行階段程式庫中呼叫 **_spawn** 或 **_exec** 常式系列，則您不應該隱藏環境處理常式，因為此常式的作用是將環境從繁衍處理序傳遞到新的處理序。

## <a name="see-also"></a>另請參閱

[main 函式和程式執行](../c-language/main-function-and-program-execution.md)
