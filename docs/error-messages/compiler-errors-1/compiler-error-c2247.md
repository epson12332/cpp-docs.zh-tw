---
title: 編譯器錯誤 C2247
ms.date: 11/04/2016
f1_keywords:
- C2247
helpviewer_keywords:
- C2247
ms.assetid: 72efa03e-615e-4ef9-aede-0a98654b20fd
ms.openlocfilehash: ab1f83e2075128441cbffd2d939e3b99b45be4c3
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62301366"
---
# <a name="compiler-error-c2247"></a>編譯器錯誤 C2247

' identifier' 無法存取，因為 'class' 會使用繼承自 'class' 的 'specifier'

`identifier` 繼承自類別，宣告具有私用或受保護的存取權。

下列範例會產生 C2247:

```
// C2247.cpp
class A {
public:
   int i;
};
class B : private A {};    // B inherits a private A
class C : public B {} c;   // so even though C's B is public
int j = c.i;               // C2247, i not accessible
```

也可因為針對 Visual Studio.NET 2003年所進行的編譯器一致性處理而產生這個錯誤： 存取控制與受保護的成員。 透過繼承自其 (n) 為成員的類別 (A) 的類別 (B) 的成員函式時，可以只存取受保護的成員 (n)。

在 Visual Studio.NET 2003年和 Visual Studio.NET 版本，視覺效果中有效的程式碼的C++，宣告為 friend 的型別成員。 也可以使用公用繼承。

```
// C2247b.cpp
// compile with: /c
// C2247 expected
class A {
public:
   void f();
   int n;
};

class B: protected A {
   // Uncomment the following line to resolve.
   // friend void A::f();
};

void A::f() {
   B b;
   b.n;
}
```

C2247 也可能會導致針對 Visual Studio.NET 2003年所進行的編譯器一致性工作： 私用基底類別現在無法存取。 型別是私用基底類別的類別 (A) （B） 不應存取的型別 （C），做為基底類別使用 B。

在 Visual Studio.NET 2003年和 Visual Studio.NET 版本，視覺效果中有效的程式碼的C++，使用範圍運算子。

```
// C2247c.cpp
// compile with: /c
struct A {};

struct B: private A {};

struct C : B {
   void f() {
      A *p1 = (A*) this;   // C2247
      // try the following line instead
      // ::A *p2 = (::A*) this;
   }
};
```