---
title: 連結器工具警告 LNK4237
ms.date: 11/04/2016
f1_keywords:
- LNK4237
helpviewer_keywords:
- LNK4237
ms.assetid: 87bfec39-5241-464f-9feb-517b49f352ea
ms.openlocfilehash: 62ce0a0edc7f15bc5a19e4630133976f413da35a
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62352654"
---
# <a name="linker-tools-warning-lnk4237"></a>連結器工具警告 LNK4237

指定時從 'dll'; 匯入了請使用 /subsystem: console 或 /subsystem: windows。

[了](../../build/reference/subsystem-specify-subsystem.md)時建置的 windows (Win32) 應用程式直接使用一或多個項目指定：

- kernel32.dll

- gdi32.dll

- user32.dll

- 其中一個 msvcrt\* dll。

解決這個警告不指定**了**。