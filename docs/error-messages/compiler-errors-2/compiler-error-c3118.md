---
title: 編譯器錯誤 C3118
ms.date: 11/04/2016
f1_keywords:
- C3118
helpviewer_keywords:
- C3118
ms.assetid: 40fbe681-8868-4cb2-a2b2-4db4449319a7
ms.openlocfilehash: 072bb821a9dc2547c9a2758fb1ca542bdbc66f86
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62281686"
---
# <a name="compiler-error-c3118"></a>編譯器錯誤 C3118

'interface': 介面不支援虛擬繼承

您嘗試以虛擬方式從介面繼承。 例如，套用至物件的

```
// C3118.cpp
__interface I1 {
};

__interface I2 : virtual I1 {   // C3118
};
```

會產生這個錯誤。