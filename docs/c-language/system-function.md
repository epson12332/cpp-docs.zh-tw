---
title: system 函式
ms.date: 11/04/2016
helpviewer_keywords:
- system function
ms.assetid: 0786ccdc-20cd-4d96-b3d8-3230507c3066
ms.openlocfilehash: e37de4e084de6727cf2858117945fd162f6b0d63
ms.sourcegitcommit: f4be868c0d1d78e550fba105d4d3c993743a1f4b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/12/2019
ms.locfileid: "56151217"
---
# <a name="system-function"></a>system 函式

**ANSI 4.10.4.5** 字串是由 **system** 函式執行的內容與執行模式

**system** 函式會執行內部作業系統命令，或從 C 程式 (而不是從命令列) 執行 .EXE、.COM (Windows NT 中的 .CMD) 或 .BAT 檔案。

系統函式會尋找命令解譯器，通常是 Windows NT 作業系統中的 CMD.EXE，或者 Windows 中的 COMMAND.COM。 系統函式接著會將引數字串傳遞給命令解譯器。

如需詳細資訊，請參閱 [system，_wsystem](../c-runtime-library/reference/system-wsystem.md)。

## <a name="see-also"></a>另請參閱

[程式庫函式](../c-language/library-functions.md)
