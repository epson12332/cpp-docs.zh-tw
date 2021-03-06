---
title: 編譯器警告 (層級 4) C4239
ms.date: 11/04/2016
f1_keywords:
- C4239
helpviewer_keywords:
- C4239
ms.assetid: a23dc16a-649e-4870-9a24-275de1584fcd
ms.openlocfilehash: 067d1aef41280f4d14fe799e4f4ee26a9f1b9f5a
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62401016"
---
# <a name="compiler-warning-level-4-c4239"></a>編譯器警告 (層級 4) C4239

使用非標準擴充: 'token': 從 'type' 到 'type' 的轉換

此類型轉換不允許C++標準，但它允許為延伸模組。 這項警告被後面一律至少一個線條的說明描述違反的語言規則。

## <a name="example"></a>範例

下列範例會產生 C4239。

```
// C4239.cpp
// compile with: /W4 /c
struct C {
   C() {}
};

void func(void) {
   C & rC = C();   // C4239
   const C & rC2 = C();   // OK
   rC2;
}
```

## <a name="example"></a>範例

完全不允許從整數類資料類型轉換為列舉類型。

下列範例會產生 C4239。

```
// C4239b.cpp
// compile with: /W4 /c
enum E { value };
struct S {
   E e : 2;
} s = { 5 };   // C4239
// try the following line instead
// } s = { (E)5 };
```