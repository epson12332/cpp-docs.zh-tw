---
title: uuid （c + + 屬性） |Microsoft Docs
ms.custom: ''
ms.date: 10/02/2018
ms.technology:
- cpp-windows
ms.topic: reference
f1_keywords:
- vc-attr.uuid
dev_langs:
- C++
helpviewer_keywords:
- uuid attribute
ms.assetid: 90562a94-5e28-451b-a4b0-cadda7f66efe
author: mikeblome
ms.author: mblome
ms.workload:
- cplusplus
- uwp
ms.openlocfilehash: 2bd15720c30c3a3f298e0094304205fd7fe5caeb
ms.sourcegitcommit: 955ef0f9d966e7c9c65e040f1e28fa83abe102a5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/04/2018
ms.locfileid: "48790691"
---
# <a name="uuid-c-attributes"></a>uuid (C++ 屬性)

指定類別或介面的唯一識別碼。

## <a name="syntax"></a>語法

```cpp
[ uuid(
   "uuid"
) ]
```

### <a name="parameters"></a>參數

*uuid*<br/>
128 位元的唯一識別碼。

## <a name="remarks"></a>備註

如果未指定的介面或類別定義**uuid** c + + 屬性，則 Visual c + + 編譯器會提供一個。 當您指定**uuid**，您必須包含引號。

如果您未指定**uuid**，則編譯器會產生不同的屬性在電腦上的專案中的介面或類別具有相同名稱的相同 GUID。

您可以使用 Uuidgen.exe 或 Guidgen.exe 來產生您自己的唯一識別碼。 (若要執行這些工具，請按一下**開始**然後按一下**執行**功能表上。 然後輸入必要的工具的名稱）。

使用時，也不會使用 ATL 專案中，指定**uuid**屬性是如同指定[uuid](../../cpp/uuid-cpp.md) **__declspec**修飾詞。 若要擷取**uuid**的類別中，您可以使用[__uuidof](../../cpp/uuidof-operator.md)

## <a name="example"></a>範例

請參閱[可繫結](bindable.md)的範例使用的範例**uuid**。

## <a name="requirements"></a>需求

### <a name="attribute-context"></a>屬性內容

|||
|-|-|
|**適用於**|**類別**， **struct**，**介面**，**聯集**，**列舉**|
|**可重複**|否|
|**必要屬性**|無|
|**無效屬性**|無|

如需有關屬性內容的詳細資訊，請參閱 <<c0> [ 屬性內容](cpp-attributes-com-net.md#contexts)。

## <a name="see-also"></a>另請參閱

[IDL 屬性](idl-attributes.md)<br/>
[介面屬性](interface-attributes.md)<br/>
[類別屬性](class-attributes.md)<br/>
[Typedef、Enum、Union 和 Struct 屬性](typedef-enum-union-and-struct-attributes.md)<br/>
[uuid](/windows/desktop/Midl/uuid)  