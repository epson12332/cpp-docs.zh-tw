---
title: 編譯器錯誤 C2186
ms.date: 11/04/2016
f1_keywords:
- C2186
helpviewer_keywords:
- C2186
ms.assetid: 284bfb7e-ab85-4fcb-9864-1ddf7f6c94ae
ms.openlocfilehash: 191b7109640fd253b24d00d86021d909891a4f95
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62378992"
---
# <a name="compiler-error-c2186"></a>編譯器錯誤 C2186

'operator': 類型 'void' 的運算元不合法

運算子具有 `void` 運算元。

下列範例會產生 C2186：

```
// C2186.cpp
// compile with: /c
void func1( void );
int  func2( void );
int i = 2 + func1();   // C2186 func1() is type void
int j = 2 + func2();   // OK both operands are type int
```