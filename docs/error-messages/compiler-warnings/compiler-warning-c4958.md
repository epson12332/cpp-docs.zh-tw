---
title: 編譯器警告 C4958
ms.date: 11/04/2016
f1_keywords:
- C4958
helpviewer_keywords:
- C4958
ms.assetid: e79b9e9c-d572-4a3a-a3b6-60962b70864a
ms.openlocfilehash: 96b73975f391493340dd01d85ad30a8c888b44c0
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62208066"
---
# <a name="compiler-warning-c4958"></a>編譯器警告 C4958

> '*作業*': 指標算術不是可驗證

## <a name="remarks"></a>備註

使用指標算術會產生未經驗證的影像。

如需詳細資訊，請參閱 <<c0> [ 純粹的和可驗證程式碼 (C++/CLI)](../../dotnet/pure-and-verifiable-code-cpp-cli.md)。</c0>

**/Clr: safe**編譯器選項是在 Visual Studio 2015 中已被取代，不支援的 Visual Studio 2017 中。

發出這個警告即表示發生錯誤，而且可以使用 [warning](../../preprocessor/warning.md) pragma 或 [/wd](../../build/reference/compiler-option-warning-level.md) 編譯器選項予以停用。

## <a name="example"></a>範例

下列範例會產生 C4958：

```cpp
// C4958.cpp
// compile with: /clr:safe
// #pragma warning( disable : 4958 )
using namespace System;

int main( ) {
   Int32 arr[] = new Int32[10];
   Int32* p = &arr[0];
   p++;   // C4958
}
```

編譯器使用指標算術來實作陣列運算。 因此，無法驗證原生陣列。請改用 CLR 陣列。 如需詳細資訊，請參閱 [陣列](../../extensions/arrays-cpp-component-extensions.md)。

下列範例會產生 C4958：

```cpp
// C4958b.cpp
// compile with: /clr:safe
// #pragma warning( disable : 4958 )

int main() {
   int array[5];
   array[4] = 0;   // C4958
}
```