---
title: CStreamRowset 類別
ms.date: 11/04/2016
f1_keywords:
- ATL::CStreamRowset<TAccessor>
- ATL::CStreamRowset
- CStreamRowset
- ATL.CStreamRowset<TAccessor>
- ATL.CStreamRowset
- CStreamRowset::CStreamRowset
- CStreamRowset.CStreamRowset
- ATL.CStreamRowset.CStreamRowset
- ATL::CStreamRowset::CStreamRowset
- CStreamRowset
- CStreamRowset<TAccessor>::CStreamRowset
- ATL::CStreamRowset<TAccessor>::CStreamRowset
- CStreamRowset<TAccessor>.Close
- ATL.CStreamRowset<TAccessor>.Close
- CStreamRowset::Close
- CStreamRowset<TAccessor>::Close
- ATL::CStreamRowset::Close
- ATL.CStreamRowset.Close
- ATL::CStreamRowset<TAccessor>::Close
- CStreamRowset.Close
helpviewer_keywords:
- CStreamRowset class
- CStreamRowset class, constructor
- Close method
ms.assetid: a106e953-a38a-464e-8ea5-28963d9e4811
ms.openlocfilehash: b566ddab89d2198e3f6b24eb9a20c60747749d1a
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62368665"
---
# <a name="cstreamrowset-class"></a>CStreamRowset 類別

用於`CCommand`或`CTable`宣告。

## <a name="syntax"></a>語法

```cpp
template <class TAccessor = CAccessorBase>
class CStreamRowset
```

### <a name="parameters"></a>參數

*TAccessor*<br/>
存取子類別。

## <a name="requirements"></a>需求

**標題:** atldbcli.h

## <a name="members"></a>成員

### <a name="methods"></a>方法

|||
|-|-|
|[CStreamRowset](#cstreamrowset)|建構函式。 具現化並初始化`CStreamRowset`物件。|
|[關閉](#close)|版本[ISequentialStream](/previous-versions/windows/desktop/ms718035(v=vs.85))類別中的介面指標。|

## <a name="remarks"></a>備註

使用`CStreamRowset`在您`CCommand`或`CTable`宣告，例如：

[!code-cpp[NVC_OLEDB_Consumer#11](../../data/oledb/codesnippet/cpp/cstreamrowset-class_1.cpp)]

或

[!code-cpp[NVC_OLEDB_Consumer#12](../../data/oledb/codesnippet/cpp/cstreamrowset-class_2.cpp)]

`ICommand::Execute` 會傳回`ISequentialStream`指標，它會儲存在`m_spStream`。 然後，您使用`Read`方法來擷取 XML 格式 （Unicode 字串） 資料。 例如: 

[!code-cpp[NVC_OLEDB_Consumer#13](../../data/oledb/codesnippet/cpp/cstreamrowset-class_3.cpp)]

SQL Server 2000 執行 XML 格式化中，並會傳回所有的資料行和資料列集，以單一的 XML 字串的所有資料列。

> [!NOTE]
>  這項功能只能搭配 SQL Server 2000。

## <a name="cstreamrowset"></a> CStreamRowset::CStreamRowset

具現化並初始化`CStreamRowset`物件。

### <a name="syntax"></a>語法

```cpp
CStreamRowset();
```

## <a name="close"></a> CStreamRowset::Close

版本[ISequentialStream](/previous-versions/windows/desktop/ms718035(v=vs.85))類別中的介面指標。

### <a name="syntax"></a>語法

```cpp
void Close();
```

## <a name="see-also"></a>另請參閱

[OLE DB 消費者樣板](../../data/oledb/ole-db-consumer-templates-cpp.md)<br/>
[OLE DB 消費者範本參考](../../data/oledb/ole-db-consumer-templates-reference.md)