---
title: 編譯器錯誤 C3353
ms.date: 11/04/2016
f1_keywords:
- C3353
helpviewer_keywords:
- C3353
ms.assetid: 5699c04b-d504-46ce-bf71-c200318fed71
ms.openlocfilehash: c38642d7abd4f2fd50792c548c9a5521b2da10ad
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62402641"
---
# <a name="compiler-error-c3353"></a>編譯器錯誤 C3353

'delegate'：只能從全域函式或 Managed 或 WinRT 類型的成員函式建立委派

使用宣告的委派[委派](../../extensions/delegate-cpp-component-extensions.md)關鍵字，只能在全域範圍內宣告。

下列範例會產生 C3353：

```
// C3353.cpp
// compile with: /clr
delegate int f;   // C3353
```