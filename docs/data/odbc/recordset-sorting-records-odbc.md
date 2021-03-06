---
title: 資料錄集：排序資料錄 (ODBC)
ms.date: 11/04/2016
helpviewer_keywords:
- sorting data, recordset data
- ODBC recordsets, sorting
- recordsets, sorting
ms.assetid: b40b152e-0a91-452e-be7b-e5bc27f744c7
ms.openlocfilehash: 831f21901186ed0ae010b0f332327eefcba94b51
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62368626"
---
# <a name="recordset-sorting-records-odbc"></a>資料錄集：排序資料錄 (ODBC)

本主題適用於 MFC ODBC 類別。

本主題說明如何排序資料錄集。 您可以指定要根據排序的一或多個資料行，而且您可以指定遞增或遞減順序 (**ASC**或是**DESC**;**ASC**是預設值) 針對每個指定的資料行。 例如，如果您指定兩個資料行時，記錄來排序第一次命名的第一個資料行，然後按一下名為第二個資料行。 SQL **ORDER BY**子句會定義排序。 此架構會將附加**ORDER BY**子句資料錄集的 SQL 查詢，請選取範圍的排序子句控制項。

建構物件之後但在您呼叫之前，您必須建立資料錄集的排序次序及其`Open`成員函式 (或在呼叫之前`Requery`成員函式，以現有的資料錄集物件，其`Open`成員函式已先前呼叫）。

#### <a name="to-specify-a-sort-order-for-a-recordset-object"></a>若要指定的資料錄集物件的排序次序

1. 建構新的資料錄集物件 (或準備呼叫`Requery`一個現有的)。

1. 設定物件的值[m_strSort](../../mfc/reference/crecordset-class.md#m_strsort)資料成員。

   排序是以 null 結束的字串。 它包含的內容**ORDER BY**子句，但不是關鍵字**ORDER BY**。 例如，使用：

    ```
    recordset.m_strSort = "LastName DESC, FirstName DESC";
    ```

   not

    ```
    recordset.m_strSort = "ORDER BY LastName DESC, FirstName DESC";
    ```

1. 設定您需要例如篩選、 鎖定的模式或參數的其他任何選項。

1. 呼叫`Open`新的物件 (或`Requery`現有的物件)。

將選取的記錄排序所指定。 例如，若要排序的一組依姓氏，然後再依據名字的遞減次序的學生記錄，執行下列作業：

```cpp
// Construct the recordset
CStudentSet rsStudent( NULL );
// Set the sort
rsStudent.m_strSort = "LastName DESC, FirstName DESC";
// Run the query with the sort in place
rsStudent.Open( );
```

資料錄集包含的所有學生記錄，以遞減順序 (從 Z 到 A) 依據姓氏排序，再依據名字。

> [!NOTE]
>  如果您選擇覆寫資料錄集的預設 SQL 字串，傳遞您自己的 SQL 字串`Open`，如果您的自訂字串已，請勿設定排序**ORDER BY**子句。

## <a name="see-also"></a>另請參閱

[資料錄集 (ODBC)](../../data/odbc/recordset-odbc.md)<br/>
[資料錄集：參數化資料錄集 (ODBC)](../../data/odbc/recordset-parameterizing-a-recordset-odbc.md)<br/>
[資料錄集：篩選資料錄 (ODBC)](../../data/odbc/recordset-filtering-records-odbc.md)