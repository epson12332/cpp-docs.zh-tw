---
title: 編譯器警告 (層級 4) C4918
ms.date: 11/04/2016
f1_keywords:
- C4918
helpviewer_keywords:
- C4918
ms.assetid: 1bcf6d35-3467-4aa8-b2ef-cb33f4e70238
ms.openlocfilehash: 9662b561f6ce6c9f41327b267d17082b1eaa21a6
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62280343"
---
# <a name="compiler-warning-level-4-c4918"></a>編譯器警告 (層級 4) C4918

'character' : 在 pragma 最佳化清單中的無效字元

在 [最佳化](../../preprocessor/optimize.md) pragma 陳述式的最佳化清單中找到未知的字元。

例如，下列陳述式會產生 C4918：

```
// C4918.cpp
// compile with: /W4
#pragma optimize("X", on) // C4918 expected
int main()
{
}
```