---
title: 建立非強制回應屬性工作表
ms.date: 11/04/2016
helpviewer_keywords:
- modeless property sheets
- property sheets, modeless
- Create method [MFC], property sheets
ms.assetid: eafd8a92-cc67-4a69-a5fb-742c920d1ae8
ms.openlocfilehash: 39285927b67091f5b8762dab56009712d806d259
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62407987"
---
# <a name="creating-a-modeless-property-sheet"></a>建立非強制回應屬性工作表

一般來說，您建立屬性工作表會強制回應。 在使用非強制回應屬性工作表時，使用者必須先關閉屬性工作表之前使用的應用程式的任何其他部分。 這篇文章說明您可用來建立可讓使用者使用應用程式的其他部分時，將屬性工作表保持開啟的非強制回應屬性工作表的方法。

若要為非強制回應對話方塊而不是作為強制回應對話方塊的 顯示屬性工作表，請呼叫[CPropertySheet::Create](../mfc/reference/cpropertysheet-class.md#create)而不是[DoModal](../mfc/reference/cpropertysheet-class.md#domodal)。 您也必須實作一些額外的工作，以支援非強制回應屬性工作表。

其中一項額外的工作交換屬性工作表和屬性工作表開啟時，它正在修改的外部物件之間的資料。 這通常是相同的工作，與標準的非強制回應對話方塊。 此工作的一部分實作非強制回應屬性工作表和屬性設定要套用至外部物件之間的通訊通道。 這項實作是很不容易，如果您衍生的類別[CPropertySheet](../mfc/reference/cpropertysheet-class.md)您非強制回應屬性工作表。 本文假設您這麼做。

非強制回應屬性工作表和外部之間通訊的其中一個方法是要定義外部物件的指標從屬性工作表物件 （在檢視中，例如目前選取範圍）。 定義函式 (之類`SetMyExternalObject`) 中`CPropertySheet`-衍生類別，以將指標變更時將焦點從一個外部物件變更為另一個。 `SetMyExternalObject`函式必須重設每個屬性頁設定，以反映新選取的外部物件。 若要這麼做，`SetMyExternalObject`函式必須要能夠存取[CPropertyPage](../mfc/reference/cpropertypage-class.md)屬於物件`CPropertySheet`類別。

提供的屬性工作表內的屬性頁面的存取權最方便的方式是將內嵌`CPropertyPage`中的物件`CPropertySheet`-衍生物件。 內嵌`CPropertyPage`中的物件`CPropertySheet`-衍生的物件不同於典型的設計為強制回應對話方塊，其中會建立屬性工作表的擁有者`CPropertyPage`物件，並將它們傳遞至屬性工作表，以透過[Cpropertysheet:: Addpage](../mfc/reference/cpropertysheet-class.md#addpage)。

有許多使用者介面的替代方案，來判斷當強制回應屬性工作表的設定應該套用至外部物件。 有一個替代方法是套用目前的屬性頁的設定，每當使用者變更任何值。 另一個替代方式是提供 [套用] 按鈕，可讓使用者累積之前認可至外部物件的屬性頁中的變更。 處理 [套用] 按鈕之方法的資訊，請參閱文章[處理套用按鈕](../mfc/handling-the-apply-button.md)。

## <a name="see-also"></a>另請參閱

[屬性工作表](../mfc/property-sheets-mfc.md)<br/>
[交換資料](../mfc/exchanging-data.md)<br/>
[對話方塊的生命週期](../mfc/life-cycle-of-a-dialog-box.md)
