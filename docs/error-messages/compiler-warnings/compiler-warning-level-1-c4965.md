---
title: 編譯器警告 (層級 1) C4965
ms.date: 11/04/2016
f1_keywords:
- C4965
helpviewer_keywords:
- C4965
ms.assetid: 47f3f6dc-459b-4a25-9947-f394c8966cb5
ms.openlocfilehash: 2e93fdeba7f9b5b10340ccd1920807a3fcb345a0
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62383830"
---
# <a name="compiler-warning-level-1-c4965"></a>編譯器警告 (層級 1) C4965

整數 0; 的隱含 box請使用 nullptr 或明確轉換

視覺化C++功能實值型別的隱含 boxing。 造成 null 作業，使用 Managed Extensions for 指示C++現在已成為指派為 boxed 的 int。

如需詳細資訊，請參閱 [Boxing](../../extensions/boxing-cpp-component-extensions.md)中定義的介面的私用 C++ 專屬實作。

## <a name="example"></a>範例

下列範例會產生 C4965。

```
// C4965.cpp
// compile with: /clr /W1
int main() {
   System::Object ^o = 0;   // C4965

   // the previous line is the same as the following line
   // using Managed Extensions for C++
   // System::Object *o = __box(0);

   // OK
   System::Object ^o2 = nullptr;
   System::Object ^o3 = safe_cast<System::Object^>(0);
}
```