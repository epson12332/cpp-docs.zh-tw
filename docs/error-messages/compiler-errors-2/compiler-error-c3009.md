---
title: 編譯器錯誤 C3009
ms.date: 11/04/2016
f1_keywords:
- C3009
helpviewer_keywords:
- C3009
ms.assetid: aded5985-f5fd-4c3e-a157-16be55ec1313
ms.openlocfilehash: a1f4a20396e97c6b868a5678958970813b638499
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62350318"
---
# <a name="compiler-error-c3009"></a>編譯器錯誤 C3009

'label': 不允許跳入 OpenMP 結構化區塊

程式碼不能跳入或跳出 OpenMP 區塊。

下列範例會產生 C3009：

```
// C3009.c
// compile with: /openmp
int main() {
   #pragma omp parallel
   {
   lbl2:;
   }
   goto lbl2;   // C3009
}
```