---
title: 編譯器錯誤 C2823
ms.date: 11/04/2016
f1_keywords:
- C2823
helpviewer_keywords:
- C2823
ms.assetid: 982b1b35-1a7c-456e-b711-f80cfe2d571e
ms.openlocfilehash: 5f9b60499fd3c3bd5f06834e3c4f6482031066d3
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62406960"
---
# <a name="compiler-error-c2823"></a>編譯器錯誤 C2823

> typedef 範本是不合法

範本中不允許`typedef`定義。

## <a name="example"></a>範例

下列範例會產生 C2823，，並示範修正此問題的一種方法：

```cpp
// C2823.cpp
template<class T>
typedef struct x {
   T i;   // C2823 can't use T, specify data type and delete template
   int i;   // OK
} x1;
```