---
title: 編譯器錯誤 C2094
ms.date: 11/04/2016
f1_keywords:
- C2094
helpviewer_keywords:
- C2094
ms.assetid: 9e4f8f88-f189-46e7-91c9-481bacc7af87
ms.openlocfilehash: 072c51ca4ae25c6f51b1841ea129a7b4fb495bdf
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62377094"
---
# <a name="compiler-error-c2094"></a>編譯器錯誤 C2094

標籤 'identifier' 未定義

函式中沒有 [goto](../../cpp/goto-statement-cpp.md) 陳述式所使用的標籤。

## <a name="example"></a>範例

下列範例會產生 C2094：

```cpp
// C2094.c
int main() {
   goto test;
}   // C2094
```

可能的解決方式：

```cpp
// C2094b.c
int main() {
   goto test;
   test:
   {
   }
}
```