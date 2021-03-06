---
title: 編譯器警告 (層級 4) C4625
ms.date: 11/04/2016
f1_keywords:
- C4625
helpviewer_keywords:
- C4625
ms.assetid: 4cc99e50-846c-4784-97da-48b977067851
ms.openlocfilehash: edcb43bf11c073e6ce721ba999fd99d28a8df15d
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62220490"
---
# <a name="compiler-warning-level-4-c4625"></a>編譯器警告 (層級 4) C4625

'derived class'：複製建構函式已隱含定義為刪除，因為基底類別複製建構函式無法存取或已被刪除

複製建構函式已遭刪除或無法在基底類別中存取，因此無法對衍生類別產生。 嘗試製作此類型的物件將會造成編譯器錯誤。

此警告預設為關閉。 如需詳細資訊，請參閱 [預設為關閉的編譯器警告](../../preprocessor/compiler-warnings-that-are-off-by-default.md) 。

## <a name="example"></a>範例

下列範例會產生 C4625，並示範如何修正此問題。

```
// C4625.cpp
// compile with: /W4 /c
#pragma warning(default : 4625)

struct A {
   A() {}

private:
   A(const A&) {}
};

struct C : private virtual A {};
struct B :  C {};   // C4625 no copy constructor

struct D : A {};
struct E :  D {};   // OK
```