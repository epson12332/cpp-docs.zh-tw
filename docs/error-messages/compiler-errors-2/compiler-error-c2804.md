---
title: 編譯器錯誤 C2804
ms.date: 11/04/2016
f1_keywords:
- C2804
helpviewer_keywords:
- C2804
ms.assetid: b066e563-cca4-450c-8ba7-3b0d7a89f3ea
ms.openlocfilehash: 1ebcfdc2f2555fa694ab8dfeabe77e5140ddace2
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62408416"
---
# <a name="compiler-error-c2804"></a>編譯器錯誤 C2804

二元運算子 'operator operator' 的參數太多

多載的二元運算子成員函式會使用多個參數宣告。 二元運算子成員函式的第一個運算元參數 (其類型是運算子的封閉式類型) 為隱含。

## <a name="example"></a>範例

下列範例會產生 C2804，並示範如何修正此問題。

```
// C2804.cpp
// compile by using: cl /c /W4 C2804.cpp
class X {
public:
   X& operator+= (const X &left, const X &right);   // C2804
   X& operator+= (const X &right);   // OK - left operand implicitly *this
};

int main() {
   X x, y;
   x += y;   // equivalent to x.operator+=(y)
}
```

## <a name="example"></a>範例

下列範例會產生 C2804，並示範如何修正此問題。

```
// C2804_2.cpp
// compile with: /clr /c
ref struct Y {
   Y^ operator +(Y^ hY, int i);   // C2804
   static Y^ operator +(Y^ hY, int i);   // OK
   Y^ operator +(int i);   // OK
};
```