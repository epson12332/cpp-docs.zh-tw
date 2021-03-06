---
title: 作法：固定指標和陣列
ms.date: 10/12/2018
ms.topic: reference
helpviewer_keywords:
- pointers, pinning
- arrays [C++], pinning
ms.assetid: ee783260-e676-46b8-a38e-11a06f1d57b0
ms.openlocfilehash: ae8c1da79f41cf9209f2765ce5aa2f7ca3d34aea
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "65515683"
---
# <a name="how-to-pin-pointers-and-arrays"></a>作法：固定指標和陣列

對 Managed 物件中定義的子物件執行 Pin 動作，與對整個物件執行 Pin 動作具有相同的效果。  例如，如果對陣列中的任何元素執行 Pin 動作，則整體陣列都會受到 Pin 動作影響。 語言並未提供任何擴充功能可用來宣告 Pin 陣列。 若要對陣列執行 Pin，請對其元素類型宣告 Pin 指標，然後對其中一個元素執行 Pin 動作。

## <a name="example"></a>範例

### <a name="code"></a>程式碼

```cpp
// pin_ptr_array.cpp
// compile with: /clr
#include <stdio.h>
using namespace System;

int main() {
   array<Byte>^ arr = gcnew array<Byte>(4);
   arr[0] = 'C';
   arr[1] = '+';
   arr[2] = '+';
   arr[3] = '\0';
   pin_ptr<Byte> p = &arr[1];   // entire array is now pinned
   unsigned char * cp = p;

   printf_s("%s\n", cp); // bytes pointed at by cp
                         // will not move during call
}
```

```Output
++
```

## <a name="see-also"></a>另請參閱

[pin_ptr (C++/CLI)](pin-ptr-cpp-cli.md)