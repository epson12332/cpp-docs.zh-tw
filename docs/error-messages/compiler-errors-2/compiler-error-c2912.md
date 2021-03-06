---
title: 編譯器錯誤 C2912
ms.date: 11/04/2016
f1_keywords:
- C2912
helpviewer_keywords:
- C2912
ms.assetid: bd55cecd-ab1a-4636-ab8a-a00393fe7b3d
ms.openlocfilehash: b7f87ae2df5350fcfb2b7a662f517d8d7bd51ef8
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62408390"
---
# <a name="compiler-error-c2912"></a>編譯器錯誤 C2912

明確特製化 'declaration' 不是函式樣板的特製化

您不能特製化非樣板函式。

下列範例會產生 C2912：

```
// C2912.cpp
// compile with: /c
void f(char);
template<> void f(char);   // C2912
template<class T> void f(T);   // OK
```

因為編譯器一致性處理是在 Visual Studio.NET 2003 中完成，也會產生這個錯誤：針對每個明確特製化，您必須選擇明確特製化的參數，以致於它們會符合主要範本的參數。

```
// C2912b.cpp
class CF {
public:
   template <class A> CF(const A& a) {}   // primary template

   // attempted explicit specialization
   template <> CF(const char* p) {}   // C2912

   // try the following line instead
   // template <> CF(const char& p) {}
};
```