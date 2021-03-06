---
title: max_is (C++ COM 屬性)
ms.date: 10/02/2018
f1_keywords:
- vc-attr.max_is
helpviewer_keywords:
- max_is attribute
ms.assetid: 7c851f5c-6649-4d77-a792-247c37d8f560
ms.openlocfilehash: dca2a3dc18aa3c3e75bbb682ed0b1b90adcd9236
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62409274"
---
# <a name="maxis"></a>max_is

指定有效的陣列索引的最大值。

## <a name="syntax"></a>語法

```cpp
[ max_is("expression") ]
```

### <a name="parameters"></a>參數

*expression*<br/>
一或多個 C 語言的運算式。 允許空白的引數位置。

## <a name="remarks"></a>備註

**Max_is** C++屬性具有相同的功能[max_is](/windows/desktop/Midl/max-is) MIDL 屬性。

## <a name="requirements"></a>需求

### <a name="attribute-context"></a>屬性內容

|||
|-|-|
|**適用於**|欄位**結構**或是**聯集**，參數的介面，介面方法|
|**可重複**|否|
|**必要屬性**|None|
|**無效屬性**|**size_is**|

如需詳細資訊，請參閱 [屬性內容](cpp-attributes-com-net.md#contexts)。

## <a name="example"></a>範例

請參閱[first_is](first-is.md)如需如何指定的陣列區段的範例。

## <a name="see-also"></a>另請參閱

[IDL 屬性](idl-attributes.md)<br/>
[Typedef、Enum、Union 和 Struct 屬性](typedef-enum-union-and-struct-attributes.md)<br/>
[參數屬性](parameter-attributes.md)<br/>
[first_is](first-is.md)<br/>
[last_is](last-is.md)<br/>
[length_is](length-is.md)<br/>
[size_is](size-is.md)