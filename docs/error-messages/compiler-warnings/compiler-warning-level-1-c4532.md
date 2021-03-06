---
title: 編譯器警告 (層級 1) C4532
ms.date: 11/04/2016
f1_keywords:
- C4532
helpviewer_keywords:
- C4532
ms.assetid: 4e2a286a-d233-4106-9f65-29be1a94ca02
ms.openlocfilehash: bcadf31eda079ebb8ea7a496efe4c945e16b1ab7
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62160753"
---
# <a name="compiler-warning-level-1-c4532"></a>編譯器警告 (層級 1) C4532

'continue': 跳出 __finally/finally 區塊未定義在終止處理期間的行為

編譯器在遇到其中一個下列關鍵字：

- [continue](../../cpp/continue-statement-cpp.md)

- [break](../../cpp/break-statement-cpp.md)

- [goto](../../cpp/goto-statement-cpp.md)

造成共跳[__finally](../../cpp/try-finally-statement.md)或是[最後](../../dotnet/finally.md)異常終止期間的區塊。

如果發生例外狀況，而在堆疊回溯終止處理常式執行期間 (`__finally`或 finally 區塊)，和您的程式碼跳出`__finally`前封鎖`__finally`區塊結束，行為是未定義。 控制項不會傳回回溯程式碼，因此可能不正確處理例外狀況。

如果您必須跳出 **__finally**封鎖，請先檢查異常終止。

下列範例會產生 C4532;只是標記為註解跳躍陳述式，若要解決這些警告。

```
// C4532.cpp
// compile with: /W1
// C4532 expected
int main() {
   int i;
   for (i = 0; i < 10; i++) {
      __try {
      } __finally {
         // Delete the following line to resolve.
         continue;
      }

      __try {
      } __finally {
         // Delete the following line to resolve.
         break;
      }
   }
}
```