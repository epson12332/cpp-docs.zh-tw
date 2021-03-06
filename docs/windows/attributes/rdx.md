---
title: rdx (C++ COM 屬性)
ms.date: 10/02/2018
f1_keywords:
- vc-attr.rdx
helpviewer_keywords:
- rdx attribute
ms.assetid: ff8e4312-c1ad-4934-bdaa-86f54409651e
ms.openlocfilehash: 2790c3de01d21242daee73fc442ad22d88739355
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62407493"
---
# <a name="rdx"></a>rdx

建立登錄機碼或修改現有的登錄機碼。

## <a name="syntax"></a>語法

```cpp
[ rdx(key, valuename=NULL, regtype) ]
```

### <a name="parameters"></a>參數

*key*<br/>
若要建立或開啟金鑰的名稱。

*valuename*<br/>
（選擇性）指定要設定的 [值] 欄位。 如果在索引鍵已經存在具有此名稱的值欄位，會將它加入。

*regtype*<br/>
要加入的登錄機碼的類型。 可以是下列其中之一： `text`， `dword`， `binary`，或`CString`。

## <a name="remarks"></a>備註

**Rdx** C++屬性建立或修改現有的登錄機碼的 COM 元件。 屬性會將 BEGIN_RDX_MAP 巨集將實作的目標成員的物件。 `RegistryDataExchange`插入 BEGIN_RDX_MAP 巨集，因為函式可以用來登錄和資料成員之間傳輸資料

這個屬性可以用於搭配[coclass](coclass.md)， [progid](progid.md)，或[vi_progid](vi-progid.md)屬性或其他屬性，表示其中一種。

## <a name="requirements"></a>需求

### <a name="attribute-context"></a>屬性內容

|||
|-|-|
|**適用於**|**類別**或是**struct**成員|
|**可重複**|否|
|**必要屬性**|None|
|**無效屬性**|None|

如需有關屬性內容的詳細資訊，請參閱 [屬性內容](cpp-attributes-com-net.md#contexts)。

## <a name="example"></a>範例

下列程式碼會加入稱為 MyValue 系統描述 CMyClass COM 元件的登錄機碼。

```cpp
// cpp_attr_ref_rdx.cpp
// compile with: /LD /link /OPT:NOREF
#define _ATL_ATTRIBUTES
#include "atlbase.h"

[module (name="MyLib")];

class CMyClass {
public:
   CMyClass() {
      strcpy_s(m_sz, "SomeValue");
   }

   [ rdx(key = "HKCR\\MyApp.MyApp.1", valuename = "MyValue", regtype = "text")]
   char m_sz[256];
};
```

## <a name="see-also"></a>另請參閱

[COM 屬性](com-attributes.md)<br/>
[registration_script](registration-script.md)