---
title: 運算式評估工具錯誤 CXX0064
ms.date: 11/04/2016
f1_keywords:
- CXX0064
helpviewer_keywords:
- CAN0064
- CXX0064
ms.assetid: aa509e71-0616-41ca-a94e-6c376b041e57
ms.openlocfilehash: 71e4e3e87b33849e6b487b79268ebc9574c2e5a6
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62299474"
---
# <a name="expression-evaluator-error-cxx0064"></a>運算式評估工具錯誤 CXX0064

無法在繫結的虛擬成員函式上設定中斷點

設定中斷點上的虛擬成員函式透過指標至物件，例如：

```
pClass->vfunc( int );
```

可以輸入類別，例如，在虛擬函式上設定中斷點：

```
Class::vfunc( int );
```

此錯誤是與 can0064 相同。