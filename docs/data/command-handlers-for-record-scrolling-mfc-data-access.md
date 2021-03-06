---
title: 記錄捲動的命令處理常式 (MFC 資料存取)
ms.date: 11/04/2016
helpviewer_keywords:
- record views [C++], scrolling
- record scrolling [C++]
- scrolling records
ms.assetid: f8b13477-2a37-459e-a30c-806fb78165ac
ms.openlocfilehash: 66944221910dbd23d78a78fc951030efbee86bd0
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62398030"
---
# <a name="command-handlers-for-record-scrolling--mfc-data-access"></a>記錄捲動的命令處理常式 (MFC 資料存取)

[CRecordView](../mfc/reference/crecordview-class.md)類別會提供預設命令處理下列標準命令：

- ID_RECORD_MOVE_FIRST

- ID_RECORD_MOVE_LAST

- ID_RECORD_MOVE_NEXT

- ID_RECORD_MOVE_PREV

`OnMove`成員函式提供預設命令處理所有的四個命令，將記錄間移動。 發出這些命令時，RFX (或 DFX) 會將新的記錄載入記錄集的欄位，DDX 則將值移到記錄表單的控制項中。 如需 RFX 的詳細資訊，請參閱[資料錄欄位交換 (RFX)](../data/odbc/record-field-exchange-rfx.md)。

> [!NOTE]
>  請務必為與標準記錄巡覽命令相關聯的任何使用者介面物件，使用這些標準命令 ID。

## <a name="see-also"></a>另請參閱

[支援資料錄檢視的瀏覽](../data/supporting-navigation-in-a-record-view-mfc-data-access.md)