---
title: 編譯器錯誤 C2637
ms.date: 11/04/2016
f1_keywords:
- C2637
helpviewer_keywords:
- C2637
ms.assetid: 58d94447-eb96-4d8f-a690-dd78d322462e
ms.openlocfilehash: 4231a811911fdf600b47962e929f6f3cff1f1bca
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62395452"
---
# <a name="compiler-error-c2637"></a>編譯器錯誤 C2637

'identifier': 無法修飾指向資料成員的指標

資料成員的指標不能有呼叫慣例。 若要解決，移除的呼叫慣例，或宣告成員函式的指標。

下列範例會產生 C2637:

```
// C2637.cpp
// compile with: /c
struct S {};
int __stdcall S::*pms1;   // C2637

// OK
int S::*pms2;
int (__stdcall S::*pms3)(...);
```