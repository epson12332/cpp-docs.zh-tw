---
title: 編譯器錯誤 C3224
ms.date: 11/04/2016
f1_keywords:
- C3224
helpviewer_keywords:
- C3224
ms.assetid: 129be22f-8f3e-4fc6-9ccd-d27d8ef91251
ms.openlocfilehash: dc64ca1aeef66eeb554be1316bf9433145b50cc3
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62174051"
---
# <a name="compiler-error-c3224"></a>編譯器錯誤 C3224

'type': 沒有任何多載泛型類別接受 'number' 個泛型類型引數

編譯器找不到適當的多載。

下列範例會產生 C3224：

```
// C3224.cs
// compile with: /target:library
public class C<T> {}
public class C<T,U> {}
```

然後，

```
// C3224b.cpp
// compile with: /clr
#using "C3224.dll"
int main() {
   C<int,int,int>^ c = gcnew C<int,int,int>();   // C3224
   C<int,int>^ c2 = gcnew C<int,int>();   // OK
}
```