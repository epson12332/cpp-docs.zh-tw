---
title: 編譯器錯誤 C2507
ms.date: 11/04/2016
f1_keywords:
- C2507
helpviewer_keywords:
- C2507
ms.assetid: f102aff5-de7d-4c3f-9cac-2ddf9ce02b14
ms.openlocfilehash: 63f9594eb9ee8a251faafe7323418b343c03063c
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62165225"
---
# <a name="compiler-error-c2507"></a>編譯器錯誤 C2507

'identifier': 基底類別上的太多虛擬修飾詞

類別或結構宣告為`virtual`一次以上。 只有一個`virtual`修飾符可以出現在清單中每個類別的基底類別。

下列範例會產生 C2507:

```
// C2507.cpp
// compile with: /c
class A {};
class B : virtual virtual public A {};   // C2507
class C : virtual public A {};   // OK
```