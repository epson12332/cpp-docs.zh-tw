---
title: 編譯器錯誤 C2381
ms.date: 11/04/2016
f1_keywords:
- C2381
helpviewer_keywords:
- C2381
ms.assetid: cc765f67-64ac-406f-93ef-ae7d548d58d7
ms.openlocfilehash: b29f7dac6c6d71e12eb0f003cdfc151dd2c349a7
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62347895"
---
# <a name="compiler-error-c2381"></a>編譯器錯誤 C2381

'function' : redefinition; __declspec(noreturn) differs

函式已宣告，並接著定義但所使用的定義[noreturn](../../cpp/noreturn.md) `__declspec`修飾詞。 善用`noreturn`構成函式的重複定義; 的宣告和定義要使用同意`noreturn`。

下列範例會產生 C2381:

```
// C2381.cpp
// compile with: /c
void f1();
void __declspec(noreturn) f1() {}   // C2381
void __declspec(noreturn) f2() {}   // OK
```