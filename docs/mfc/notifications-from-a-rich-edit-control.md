---
title: 來自 Rich Edit 控制項的告知
ms.date: 11/04/2016
helpviewer_keywords:
- messages [MFC], notification [MFC]
- CRichEditCtrl class [MFC], notifications
- rich edit controls [MFC], notifications
- notifications [MFC], from CRichEditCtrl
ms.assetid: eb5304fe-f4f3-4557-9ebf-3095dea383c4
ms.openlocfilehash: fcb1dda1d915dc13e01effed9ba99070b825a15e
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62238206"
---
# <a name="notifications-from-a-rich-edit-control"></a>來自 Rich Edit 控制項的告知

通知訊息報告事件影響 rich edit 控制項 ([CRichEditCtrl](../mfc/reference/cricheditctrl-class.md))。 它們可處理由父視窗，或使用訊息反映的豐富編輯控制項本身。 Rich edit 控制項支援的所有編輯控制項，以及數個其他工具搭配使用的通知訊息。 您可以判斷哪一個通知訊息的 rich edit 控制項就會將其父視窗傳送藉由設定它的 「 事件遮罩 」。

若要設定事件遮罩的 rich edit 控制項，使用[SetEventMask](../mfc/reference/cricheditctrl-class.md#seteventmask)成員函式。 Rich edit 控制項使用的您可以擷取目前的事件遮罩[GetEventMask](../mfc/reference/cricheditctrl-class.md#geteventmask)成員函式。

下面列出幾個特定的通知，以及它們的用法：

- EN_MSGFILTER 處理 EN_MSGFILTER 通知可讓類別，可能是 rich edit 控制項或其父視窗，篩選所有鍵盤和滑鼠輸入到控制項。 處理常式可以防止鍵盤或滑鼠訊息處理，或可以藉由修改指定變更的訊息[MSGFILTER](/windows/desktop/api/richedit/ns-richedit-_msgfilter)結構。

- EN_PROTECTED 處理 EN_PROTECTED 通知訊息來偵測當使用者嘗試修改受保護的文字。 若要標示某個範圍的文字，為受保護，您可以設定受保護的字元效果。 如需詳細資訊，請參閱 < [Rich Edit 控制項中的字元格式](../mfc/character-formatting-in-rich-edit-controls.md)。

- EN_DROPFILES 您可以讓使用者藉由處理 EN_DROPFILES 通知訊息放置在 rich edit 控制項中的檔案。 指定[ENDROPFILES](/windows/desktop/api/richedit/ns-richedit-_endropfiles)結構包含要卸除之檔案的相關資訊。

- 目前的選取範圍變更處理 EN_SELCHANGE 通知訊息時，可以偵測到 EN_SELCHANGE 應用程式。 指定通知訊息[SELCHANGE](/windows/desktop/api/richedit/ns-richedit-_selchange)結構，其中包含新的選取範圍的相關資訊。

## <a name="see-also"></a>另請參閱

[使用 CRichEditCtrl](../mfc/using-cricheditctrl.md)<br/>
[控制項](../mfc/controls-mfc.md)
