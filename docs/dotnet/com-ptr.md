---
title: com::ptr
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- ptr
helpviewer_keywords:
- com::ptr
ms.assetid: ee302e3c-8fed-4875-a372-2e55003718d3
ms.openlocfilehash: 74e168fe916b930e499a82ca3fcf5c7d0d669719
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62209200"
---
# <a name="comptr"></a>com::ptr

可當做 CLR 類別成員使用之 COM 物件的包裝函式。 包裝函式也會自動執行 COM 物件，呼叫其解構函式時，釋出已擁有的參考，在物件上的存留期管理。 類似於[CComPtr 類別](../atl/reference/ccomptr-class.md)。

## <a name="syntax"></a>語法

```
#include <msclr\com\ptr.h>
```

## <a name="remarks"></a>備註

[com:: ptr 類別](../dotnet/com-ptr-class.md)定義於\<msclr\com\ptr.h > 檔案。

## <a name="see-also"></a>另請參閱

[C++ 支援程式庫](../dotnet/cpp-support-library.md)
