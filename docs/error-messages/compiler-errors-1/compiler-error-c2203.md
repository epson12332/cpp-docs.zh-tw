---
title: 編譯器錯誤 C2203
ms.date: 11/04/2016
f1_keywords:
- C2203
helpviewer_keywords:
- C2203
ms.assetid: 5497df43-86f6-43d5-b6cb-723c4c589b10
ms.openlocfilehash: 848fdad460402238f4957344dd49bd9128352b4c
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62383258"
---
# <a name="compiler-error-c2203"></a>編譯器錯誤 C2203

刪除操作員無法指定陣列的界限

具有 **/Za** (ANSI) 選項`delete`運算子可以刪除整個陣列，但沒有組件或特定成員的陣列。

下列範例會產生 C2203:

```
// C2203.cpp
// compile with: /Za
int main() {
   int *ar = new int[10];
   delete [4] ar;   // C2203
   // try the following line instead
   // delete [] ar;
}
```