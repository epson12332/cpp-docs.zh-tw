---
title: HOW TO：在 Unmanaged 記憶體中存放物件參考
ms.custom: get-started-article
ms.date: 11/04/2016
helpviewer_keywords:
- object references, in native functions
- objects [C++], reference in native functions
- references, to objects in native functions
- gcroot keyword [C++], object reference in native function
ms.assetid: a61eb8ce-3982-477d-8d3d-2173fd57166d
ms.openlocfilehash: 0d8dc341d1fe2c61eba098abec9258a2c6dade79
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62387288"
---
# <a name="how-to-hold-object-reference-in-unmanaged-memory"></a>HOW TO：在 Unmanaged 記憶體中存放物件參考

您可以使用 gcroot.h，包裝<xref:System.Runtime.InteropServices.GCHandle>，以在 unmanaged 記憶體中保留 CLR 物件參考。 或者，您可以使用`GCHandle`直接。

## <a name="example"></a>範例

```
// hold_object_reference.cpp
// compile with: /clr
#include "gcroot.h"
using namespace System;

#pragma managed
class StringWrapper {

private:
   gcroot<String ^ > x;

public:
   StringWrapper() {
      String ^ str = gcnew String("ManagedString");
      x = str;
   }

   void PrintString() {
      String ^ targetStr = x;
      Console::WriteLine("StringWrapper::x == {0}", targetStr);
   }
};
#pragma unmanaged
int main() {
   StringWrapper s;
   s.PrintString();
}
```

```Output
StringWrapper::x == ManagedString
```

## <a name="example"></a>範例

`GCHandle` 可讓您保留在 unmanaged 記憶體中的受管理的物件參考的方法。  您使用<xref:System.Runtime.InteropServices.GCHandle.Alloc%2A>方法用來建立 managed 物件的不透明控制代碼和<xref:System.Runtime.InteropServices.GCHandle.Free%2A>釋放它。 此外，<xref:System.Runtime.InteropServices.GCHandle.Target%2A>方法可讓您取得上一步是從 managed 程式碼中的控制代碼的物件參考。

```
// hold_object_reference_2.cpp
// compile with: /clr
using namespace System;
using namespace System::Runtime::InteropServices;

#pragma managed
class StringWrapper {
   IntPtr m_handle;
public:
   StringWrapper() {
      String ^ str = gcnew String("ManagedString");
      m_handle = static_cast<IntPtr>(GCHandle::Alloc(str));
   }
   ~StringWrapper() {
      static_cast<GCHandle>(m_handle).Free();
   }

   void PrintString() {
      String ^ targetStr = safe_cast< String ^ >(static_cast<GCHandle>(m_handle).Target);
      Console::WriteLine("StringWrapper::m_handle == {0}", targetStr);
   }
};

#pragma unmanaged
int main() {
   StringWrapper s;
   s.PrintString();
}
```

```Output
StringWrapper::m_handle == ManagedString
```

## <a name="see-also"></a>另請參閱

[使用 C++ Interop (隱含 PInvoke)](../dotnet/using-cpp-interop-implicit-pinvoke.md)
