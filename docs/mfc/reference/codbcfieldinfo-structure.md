---
title: CODBCFieldInfo 結構
ms.date: 11/04/2016
f1_keywords:
- CODBCFieldInfo
helpviewer_keywords:
- ODBC [MFC], data source information
- CODBCFieldInfo structure [MFC]
ms.assetid: 92598b4f-facc-4108-b282-63a179ff79ab
ms.openlocfilehash: bc2ad0c8319a60b773211dbd6b52b57bb2dbcafb
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62388187"
---
# <a name="codbcfieldinfo-structure"></a>CODBCFieldInfo 結構

`CODBCFieldInfo`結構包含 ODBC 資料來源中的欄位的相關資訊。

## <a name="syntax"></a>語法

```
struct CODBCFieldInfo
{
    CString m_strName;
    SWORD m_nSQLType;
    UDWORD m_nPrecision;
    SWORD m_nScale;
    SWORD m_nNullability;
};
```

#### <a name="parameters"></a>參數

*m_strName*<br/>
欄位的名稱。

*m_nSQLType*<br/>
SQL 資料類型的欄位。 這可以是 ODBC SQL 資料類型或驅動程式專屬的 SQL 資料型別。 如需有效的 ODBC SQL 資料類型的清單，請參閱 Windows SDK 中的 < SQL 資料類型 >。 如需驅動程式專用的 SQL 資料類型資訊，請參閱驅動程式的文件。

*m_nPrecision*<br/>
欄位的最大有效位數。 如需詳細資訊，請參閱 Windows SDK 中的 「 有效位數、 小數位數、 長度和顯示大小 」。

*m_nScale*<br/>
欄位的小數位數。 如需詳細資訊，請參閱 Windows SDK 中的 「 有效位數、 小數位數、 長度和顯示大小 」。

*m_nNullability*<br/>
是否欄位可接受 Null 值。 這可以是兩個值之一：SQL_NULLABLE 欄位可接受 Null 值，則 SQL_NO_NULLS 如果欄位不接受 Null 值。

## <a name="remarks"></a>備註

若要擷取此資訊，請呼叫[CRecordset::GetODBCFieldInfo](../../mfc/reference/crecordset-class.md#getodbcfieldinfo)。

## <a name="requirements"></a>需求

**標頭：** afxdb.h

## <a name="see-also"></a>另請參閱

[結構、樣式、回呼和訊息對應](../../mfc/reference/structures-styles-callbacks-and-message-maps.md)<br/>
[CRecordset::GetODBCFieldInfo](../../mfc/reference/crecordset-class.md#getodbcfieldinfo)<br/>
[CRecordset::GetFieldValue](../../mfc/reference/crecordset-class.md#getfieldvalue)
