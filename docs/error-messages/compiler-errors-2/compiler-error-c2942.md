---
title: 編譯器錯誤 C2942
ms.date: 11/04/2016
f1_keywords:
- C2942
helpviewer_keywords:
- C2942
ms.assetid: 13abf744-8fa1-450d-886d-e5717c04956e
ms.openlocfilehash: 8a594b9d1d8374caa972f6bfdafe5d691e634a9a
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62366637"
---
# <a name="compiler-error-c2942"></a>編譯器錯誤 C2942

'class' : type-class-id 重複定義為函式的正式引數

您無法使用泛型或樣板類別作為正式引數。 您無法將引數直接傳遞給泛型或樣板類別的建構函式。

下列範例會產生 C2942：

```

// C2942.cpp
// compile with: /c
template<class T>
struct TC {};
void f(int TC<int>) {}   // C2942

// OK
struct TC2 {};
void f(TC2 i) {}
```

使用泛型時，也會發生 C2942：

```
// C2942b.cpp
// compile with: /clr /c
generic<class T>
ref struct GC {};
void f(int GC<int>) {}   // C2942
ref struct GC2 { };
void f(int GC2) {}
```