---
title: OLE DB 物件模型
ms.date: 10/22/2018
helpviewer_keywords:
- rowsets, OLE DB object model
- OLE DB, object model
ms.assetid: 1a274a25-c310-4430-a1ec-bd2bd8120eff
ms.openlocfilehash: 303ad4166f0f1126182956fae9c19f513be7cfb3
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62283802"
---
# <a name="ole-db-object-model"></a>OLE DB 物件模型

OLE DB 物件模型是由下列物件或元件所組成。 第四個物件或 （資料來源、 工作階段、 命令和資料列集） 所列出的元件，可讓您連接到資料來源，並檢視它。 其餘部分，從存取子，與相關出現時，使用的資料。

## <a name="data-sources"></a>Data Sources

資料來源物件可讓您連接到資料來源，例如檔案或 DBMS。 資料來源物件會建立和管理連線，並包含權限和驗證資訊 （例如登入名稱和密碼）。 資料來源物件可以建立一或多個工作階段。

## <a name="sessions"></a>工作階段

工作階段會管理與查詢和擷取資料的資料來源的特定互動。 每個工作階段是在單一交易。 交易是不可分割的工作單位 ACID 測試所定義。 如需 ACID 的定義，請參閱 <<c0> [ 交易](#vcconoledbcomponents_transactions)。

工作階段執行重要的工作，例如開啟資料列集，並傳回資料來源物件建立它。 工作階段時，也可以傳回中繼資料或資料來源 （例如資料表資訊） 的相關資訊。

一或多個命令時，可以建立工作階段。

## <a name="commands"></a>命令

文字命令，例如 SQL 陳述式執行命令。 如果文字命令中指定資料列集，例如 SQL**選取**陳述式，此命令會建立資料列集。

命令是只是文字命令，也就是 （例如 SQL 陳述式） 所傳遞的字串從取用者資料來源物件的執行提供者的基礎資料存放區的容器。 文字命令通常是 SQL**選取 **陳述式 (在此情況下，因為 SQL**選取**指定資料列集，此命令會自動建立一個資料列集)。

## <a name="rowsets"></a>資料列集

資料列集表格格式顯示資料。 索引是特殊案例的資料列集。 您可以從工作階段或命令來建立資料列集。

### <a name="schema-rowsets"></a>結構描述資料列集

結構描述有資料庫相關的中繼資料 （結構化資訊）。 結構描述資料列集是有結構描述資訊的資料列集。 用於 DBMS 部分 OLE DB 提供者支援結構描述資料列集物件。 如需有關結構描述資料列集的詳細資訊，請參閱 <<c0> [ 結構描述資料列集取得中繼資料](../../data/oledb/obtaining-metadata-with-schema-rowsets.md)並[結構描述資料列集類別和 Typedef 類別](../../data/oledb/schema-rowset-classes-and-typedef-classes.md)。

### <a name="view-objects"></a>檢視物件

檢視物件定義的資料列和資料行的資料列的子集。 它有自己的任何資料。 檢視物件無法結合來自多個資料列集的資料。

## <a name="accessors"></a>存取子

只有 OLE DB 會使用存取子的概念。 存取子會描述資料如何儲存在取用者。 它具有資料列集的欄位 （欄） 和您在消費者中宣告的資料成員之間的一組繫結 （稱為資料行對應）。

##  <a name="vcconoledbcomponents_transactions"></a> 交易

認可或中止在最低層級以外的巢狀的交易時，會使用交易物件。 交易是不可分割的工作單位 ACID 測試所定義。 ACID (line-of-business):

- 不可部分完成性，無法被分割成較小的工作單位

- 並行存取，一個以上的交易發生一次

- 隔離一筆交易具有有限的另一個變更的相關知識

- 持久性，交易進行永續性的變更

## <a name="enumerators"></a>列舉程式

列舉程式會搜尋可用的資料來源和其他列舉程式。 針對特定資料來源不自訂的取用者會使用列舉值，搜尋要使用的資料來源。

根的列舉值，隨附於 Microsoft Data Access SDK 中，會周遊尋找資料來源和其他列舉值的登錄。 其他列舉程式會周遊登錄或搜尋提供者特定的方式。

## <a name="errors"></a>錯誤

任何介面上的任何 OLE DB 物件可能會產生錯誤。 錯誤會有錯誤，包括選擇性的自訂錯誤物件的其他資訊。 這項資訊會儲存在 HRESULT。

## <a name="notifications"></a>通知

通知會使用的共用資料列集的合作取用者群組 （其中共用表示取用者會假設在相同交易中運作）。 通知可讓共用資料列集合作取用者以瞭解其對等電腦所執行的資料列集上的動作。

## <a name="see-also"></a>另請參閱

[OLE DB 程式設計](../../data/oledb/ole-db-programming.md)<br/>
[OLE DB 程式設計概觀](../../data/oledb/ole-db-programming-overview.md)