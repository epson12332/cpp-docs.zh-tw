---
title: 編譯器錯誤 C2548
ms.date: 11/04/2016
f1_keywords:
- C2548
helpviewer_keywords:
- C2548
ms.assetid: 01e9c835-9bf3-4020-9295-5ee448c519f3
ms.openlocfilehash: 2c680d86a0ea69d67f9e53a481f2f096f4cc7878
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62353465"
---
# <a name="compiler-error-c2548"></a>編譯器錯誤 C2548

'class::member': 遺漏參數的預設參數

預設的參數清單遺漏參數。 如果您提供預設參數的參數清單中的任何位置，您必須定義所有後續的參數的預設參數。

## <a name="example"></a>範例

下列範例會產生 C2548:

```
// C2548.cpp
// compile with: /c
void func( int = 1, int, int = 3);  // C2548

// OK
void func2( int, int, int = 3);
void func3( int, int = 2, int = 3);
```