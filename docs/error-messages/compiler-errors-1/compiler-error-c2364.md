---
title: 編譯器錯誤 C2364
ms.date: 11/04/2016
f1_keywords:
- C2364
helpviewer_keywords:
- C2364
ms.assetid: 4f550571-94b5-42ca-84cb-663fecbead44
ms.openlocfilehash: 051468ea861190dd3f6a28dc272f1bab155145af
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62230395"
---
# <a name="compiler-error-c2364"></a>編譯器錯誤 C2364

'type': 對自訂屬性的類型不合法

為自訂屬性的具名引數會限制為編譯時間常數。 例如，整數類資料類型 （int、 char 等），system:: type ^，以及 system:: object ^。

## <a name="example"></a>範例

下列範例會產生 C2364。

```
// c2364.cpp
// compile with: /clr /c
using namespace System;

[attribute(AttributeTargets::All)]
public ref struct ABC {
public:
   // Delete the following line to resolve.
   ABC( Enum^ ) {}   // C2364
   ABC( int ) {}   // OK
};
```