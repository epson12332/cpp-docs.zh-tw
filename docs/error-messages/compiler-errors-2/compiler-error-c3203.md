---
title: 編譯器錯誤 C3203
ms.date: 11/04/2016
f1_keywords:
- C3203
helpviewer_keywords:
- C3203
ms.assetid: 6356770e-22c1-434c-91fe-f60b0aa23b91
ms.openlocfilehash: c55160c855a6188a616f957acee43e409b751b62
ms.sourcegitcommit: 7d64c5f226f925642a25e07498567df8bebb00d4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/08/2019
ms.locfileid: "65447806"
---
# <a name="compiler-error-c3203"></a>編譯器錯誤 C3203

'type'：特製化的類別樣板或泛型，無法做為樣板或泛型參數 'param' 的樣板或泛型引數，必須是實數類型

傳遞至類別樣板或泛型的引數無效。 類別樣板或泛型預期將類型做為參數。

針對 Visual Studio 2005 所進行的編譯器一致性工作可能會導致此錯誤： 非特製化的類別樣板不能做為基底類別清單中的樣板引數。 若要解決 C3203，必須在將它做為基底類別清單中的樣板參數時，將樣板類型參數明確加入至樣板類別名稱。

```
// C3203.cpp
template< typename T >
struct X {
   void f(X) {}
};

template< typename T >
struct Y : public X<Y> {   // C3203
// try the following line instead
// struct Y : public X<Y<T> > {
   void f(Y) {}
};

int main() {
   Y<int> y;
}
```

下列範例會產生 C3203，並示範如何修正此問題：

```
// C3203_b.cpp
// compile with: /c
template <class T>
struct S1 {};

template <class T>
class C1 {};

typedef C1<S1> MyC1;   // C3203

// OK
template <template <class> class T>
class C2 {};

typedef C2<S1> MyC1;

template <class T>
class C3 {};

typedef C3<S1<int> > MyC12;
```

使用泛型時，也會發生 C3203：

```
// C3203_c.cpp
// compile with: /clr /c
generic <class T>
value struct GS1 {};

generic <class T>
value struct GC1 {};

typedef GC1<GS1> MyGC1;   // C3203
typedef GC1<GS1<int> > MyGC2;   // OK
```