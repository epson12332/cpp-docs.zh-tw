---
title: 編譯器錯誤 C3385
ms.date: 11/04/2016
f1_keywords:
- C3385
helpviewer_keywords:
- C3385
ms.assetid: 5f1838c1-986e-47db-8dbc-e06976b83cf3
ms.openlocfilehash: 0cf8f75588339420c688db6e808a62a9fb0ac15c
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62328759"
---
# <a name="compiler-error-c3385"></a>編譯器錯誤 C3385

'class::function' : 具有 DllImport 自訂屬性的函式不能傳回類別的執行個體

定義於使用 `DllImport` 屬性指定之 .dll 檔中的函式不能傳回類別的執行個體。

下列範例會產生 C3385：

```
// C3385.cpp
// compile with: /clr /c
using namespace System;
using namespace System::Runtime::InteropServices;

struct SomeStruct1 {};

public ref struct Wrap {
   [ DllImport("somedll.dll", CharSet=CharSet::Unicode) ]
   static SomeStruct1 f1([In, Out] SomeStruct1 *pS);   // C3385
};
```
