---
title: 編譯器錯誤 C2847
ms.date: 11/04/2016
f1_keywords:
- C2847
helpviewer_keywords:
- C2847
ms.assetid: 9ad9a0e0-8b16-49d9-a5be-f8eda2372aa9
ms.openlocfilehash: 99c49be746cea6fb80c5e24667bcd97556a0ad04
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62161039"
---
# <a name="compiler-error-c2847"></a>編譯器錯誤 C2847

無法將 sizeof 套用於 Managed 或 WinRT 型別 'class'

[Sizeof](../../cpp/sizeof-operator.md)運算子在編譯時期取得物件值。 Managed 或 WinRT 型別、介面或實值型別的大小是動態的，因此無法在編譯時間得知。

例如，下列範例會產生 C2847：

```
// C2847.cpp
// compile with: /clr
ref class A {};

int main() {
   A ^ xA = gcnew A;
   sizeof(*xA);   // C2847 cannot use sizeof on managed object
}
```
