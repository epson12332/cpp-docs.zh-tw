---
title: Rich Edit 控制項的概觀
ms.date: 11/04/2016
helpviewer_keywords:
- rich edit controls [MFC]
ms.assetid: ad589b9f-a3fd-4820-bf1f-6b1965997e68
ms.openlocfilehash: c45cb638ec860bb803c7de32065606dc3cc176b2
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62160168"
---
# <a name="overview-of-the-rich-edit-control"></a>Rich Edit 控制項的概觀

> [!IMPORTANT]
>  如果您使用 rich edit 控制項在對話方塊中 (無論您的應用程式是 SDI、 MDI 或對話方塊架構)，您必須呼叫[AfxInitRichEdit](../mfc/reference/application-information-and-management.md#afxinitrichedit)一旦方塊會顯示對話方塊之前。 呼叫這個函式的一般位置是在程式的 `InitInstance` 成員函式中。 只需在第一次顯示對話方塊時呼叫它一次。 如果您使用 `AfxInitRichEdit`，不需要呼叫 `CRichEditView`。

Rich edit 控制項 ([CRichEditCtrl](../mfc/reference/cricheditctrl-class.md)) 提供程式設計介面，用於格式化文字。 然而，應用程式必須實作所有必要的使用者介面元件，讓使用者能夠執行格式化作業。 也就是說，Rich Edit 控制項支援變更所選取文字中的字元或段落屬性。 字元屬性的範例為粗體、斜體、字型系列和字型的點數大小。 段落屬性的範例包括對齊、邊界和定位停駐點。 不過，使用者介面全由您決定提供，不論是工具列按鈕、功能表項目或格式字元對話方塊。 也有函式可查詢 Rich Edit 控制項，以顯示目前選取範圍的屬性。 請使用這些函式顯示屬性的目前設定，例如，如果選取範圍有粗體字元格式屬性，則在命令 UI 中設定核取記號。

如需有關字元和段落格式的詳細資訊，請參閱 <<c0> [ 字元格式](../mfc/character-formatting-in-rich-edit-controls.md)並[段落格式](../mfc/paragraph-formatting-in-rich-edit-controls.md)本主題稍後的。

Rich Edit 控制項支援用於多行編輯控制項的大部分作業和通知訊息。 因此，已使用編輯控制項的應用程式可以輕鬆地變更成使用 Rich Edit 控制項。 其他訊息和通知讓應用程式能夠存取 Rich Edit 控制項的獨特功能。 編輯控制項的相關資訊，請參閱[CEdit](../mfc/reference/cedit-class.md)。

如需有關通知的詳細資訊，請參閱[來自 Rich Edit 控制項的通知](../mfc/notifications-from-a-rich-edit-control.md)本主題稍後的。

## <a name="see-also"></a>另請參閱

[使用 CRichEditCtrl](../mfc/using-cricheditctrl.md)<br/>
[控制項](../mfc/controls-mfc.md)
