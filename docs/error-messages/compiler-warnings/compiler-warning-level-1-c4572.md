---
title: 編譯器警告 (層級 1) C4572
ms.date: 11/04/2016
f1_keywords:
- C4572
helpviewer_keywords:
- C4572
ms.assetid: 482dee5a-29bd-4fc3-b769-9dfd4cd2a964
ms.openlocfilehash: e32509e4d32eef4f53b8d43a7db769844f1182c7
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62397233"
---
# <a name="compiler-warning-level-1-c4572"></a>編譯器警告 (層級 1) C4572

[ParamArray] 屬性之下已被取代 /clr，使用 '...'改為

使用指定的變數引數清單的過時樣式。 當編譯為 clr 時，使用省略語法，而不是<xref:System.ParamArrayAttribute>。 如需詳細資訊，請參閱[變數引數清單 （...）(C++/CLI)](../../extensions/variable-argument-lists-dot-dot-dot-cpp-cli.md).

## <a name="example"></a>範例

下列範例會產生 C4572。

```
// C4572.cpp
// compile with: /clr /W1
void Func([System::ParamArray] array<int> ^);   // C4572
void Func2(... array<int> ^){}   // OK

int main() {
   Func2(1, 2, 3);
}
```