---
title: 編譯器錯誤 C2671
ms.date: 11/04/2016
f1_keywords:
- C2671
helpviewer_keywords:
- C2671
ms.assetid: fc0ee40f-c8f3-408f-b89d-745d149c4169
ms.openlocfilehash: 92ed646b0e4c5d2bbc6556c2a7b1ef66d8192ec1
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62165069"
---
# <a name="compiler-error-c2671"></a>編譯器錯誤 C2671

'function': 靜態成員函式沒有 'this' 指標

A`static`成員函式嘗試存取`this`。

下列範例會產生 C2671:

```
// C2671.cpp
struct S {
   static S* const func() { return this; }  // C2671
};
```