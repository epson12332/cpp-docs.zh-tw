---
title: 編譯器錯誤 C3469
ms.date: 11/04/2016
f1_keywords:
- C3469
helpviewer_keywords:
- C3469
ms.assetid: e23b0e5c-c704-4e67-a868-bf02c2055d85
ms.openlocfilehash: 1e935fb90c93d6f301226f3e9029c04929f179ac
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62397428"
---
# <a name="compiler-error-c3469"></a>編譯器錯誤 C3469

'type': 泛型類別無法轉送

您無法對泛型類別使用類型轉送。

如需詳細資訊，請參閱 <<c0> [ 型別轉送 (C++/CLI)](../../extensions/type-forwarding-cpp-cli.md)。</c0>

## <a name="example"></a>範例

下列範例會建立元件。

```
// C3469.cpp
// compile with: /clr /LD
generic<typename T>
public ref class GR {};

public ref class GR2 {};
```

## <a name="example"></a>範例

下列範例會產生 C3466。

```
// C3469_b.cpp
// compile with: /clr /c
#using "C3469.dll"
[assembly:TypeForwardedTo(GR::typeid)];   // C3469
[assembly:TypeForwardedTo(GR2::typeid)];   // OK
```