---
title: 嚴重錯誤 C1021
ms.date: 11/04/2016
f1_keywords:
- C1021
helpviewer_keywords:
- C1021
ms.assetid: e23171f4-ca6b-40c0-a913-a2edc6fa3766
ms.openlocfilehash: 35b94e6cea177121c38d06706b42437ec610c38a
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62383109"
---
# <a name="fatal-error-c1021"></a>嚴重錯誤 C1021

無效的前置處理器命令 'string'

`string` 不是有效的 [前置處理器指示詞](../../preprocessor/preprocessor-directives.md)。 若要解決這個錯誤，請使用 `string`的有效前置處理器名稱。

下列範例會產生 C1021：

```
// C1021.cpp
#BadPreProcName    // C1021 delete line
```