---
title: 編譯器錯誤 C3286
ms.date: 11/04/2016
f1_keywords:
- C3286
helpviewer_keywords:
- C3286
ms.assetid: 554328c8-cf44-4f7d-a8d2-def74d28ecdd
ms.openlocfilehash: 8c09ea34c7dabf2cadecad7c76d766c9496f5a5a
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62381343"
---
# <a name="compiler-error-c3286"></a>編譯器錯誤 C3286

> '*規範*': 反覆運算變數不能有任何儲存類別規範

儲存類別不能指定反覆項目變數。 如需詳細資訊，請參閱 <<c0> [ 儲存類別 (C++)](../../cpp/storage-classes-cpp.md)並[針對每個，在](../../dotnet/for-each-in.md)。</c0>

## <a name="example"></a>範例

下列範例會產生 c3286:，，和也會示範正確使用方式。

```cpp
// C3286.cpp
// compile with: /clr
int main() {
   array<int> ^p = { 1, 2, 3 };
   for each (static int i in p) {}   // C3286
   for each (int j in p) {}   // OK
}
```