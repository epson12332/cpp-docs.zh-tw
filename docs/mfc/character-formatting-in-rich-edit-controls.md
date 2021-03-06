---
title: Rich Edit 控制項中的字元格式化
ms.date: 11/04/2016
helpviewer_keywords:
- formatting [MFC], characters
- rich edit controls [MFC], character formatting in
- CRichEditCtrl class [MFC], character formatting in
ms.assetid: c80f4305-75ad-45f9-8d17-d83d0fe79be5
ms.openlocfilehash: a7467f9cd6a14dc6dfc2c03b6eb35f71802454fb
ms.sourcegitcommit: c6f8e6c2daec40ff4effd8ca99a7014a3b41ef33
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/24/2019
ms.locfileid: "64344289"
---
# <a name="character-formatting-in-rich-edit-controls"></a>Rich Edit 控制項中的字元格式化

您可以使用 rich edit 控制項的成員函式 ([CRichEditCtrl](../mfc/reference/cricheditctrl-class.md)) 來格式化字元，並擷取格式化資訊。 字元，您可以指定字體、 大小、 色彩和效果，例如粗體、 斜體和受保護。

您可以將字元格式藉由套用[SetSelectionCharFormat](../mfc/reference/cricheditctrl-class.md#setselectioncharformat)並[SetWordCharFormat](../mfc/reference/cricheditctrl-class.md#setwordcharformat)成員函式。 若要判斷目前選取的文字格式的字元，請使用[GetSelectionCharFormat](../mfc/reference/cricheditctrl-class.md#getselectioncharformat)成員函式。 [CHARFORMAT](/windows/desktop/api/richedit/ns-richedit-_charformat)結構與這些成員函式用來指定字元的屬性。 其中一個重要成員**CHARFORMAT**是**dwMask**。 在 `SetSelectionCharFormat`並`SetWordCharFormat`， **dwMask**指定哪些字元屬性會設定由這個函式呼叫。 `GetSelectionCharFormat` 報告選取範圍; 中的第一個字元的屬性**dwMask**指定之屬性的選取範圍中一致。

您可以也取得和設定的 「 預設字元格式，「 這是套用至任何後續插入字元的格式。 例如，如果應用程式設定的預設字元格式為粗體，而且使用者再輸入字元，該字元是粗體。 若要取得和設定預設字元格式，使用[GetDefaultCharFormat](../mfc/reference/cricheditctrl-class.md#getdefaultcharformat)並[SetDefaultCharFormat](../mfc/reference/cricheditctrl-class.md#setdefaultcharformat)成員函式。

「 受保護 」 字元屬性不會變更文字的外觀。 如果使用者嘗試修改受保護的文字，rich edit 控制項，將會傳送其父視窗**EN_PROTECTED**通知訊息，讓父視窗，以允許或防止變更。 若要收到此通知訊息，您必須啟用使用它[SetEventMask](../mfc/reference/cricheditctrl-class.md#seteventmask)成員函式。 如需有關事件遮罩的詳細資訊，請參閱[來自 Rich Edit 控制項的通知](../mfc/notifications-from-a-rich-edit-control.md)稍後在本主題中。

前景色彩是字元的屬性，但是背景色彩是 rich edit 控制項的屬性。 若要設定背景色彩，請使用[SetBackgroundColor](../mfc/reference/cricheditctrl-class.md#setbackgroundcolor)成員函式。

## <a name="see-also"></a>另請參閱

[使用 CRichEditCtrl](../mfc/using-cricheditctrl.md)<br/>
[控制項](../mfc/controls-mfc.md)
