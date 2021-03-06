---
title: 工具列基本概念
ms.date: 11/04/2016
f1_keywords:
- RT_TOOLBAR
helpviewer_keywords:
- embedding toolbar in frame window class [MFC]
- application wizards [MFC], installing default application toolbars
- toolbars [MFC], creating
- resources [MFC], toolbar
- toolbar controls [MFC], toolbars created using Application Wizard
- toolbar controls [MFC], command ID
- RT_TOOLBAR resource [MFC]
- toolbars [MFC], adding default using Application Wizard
- LoadBitmap method [MFC], toolbars
- Toolbar editor [MFC], Application Wizard
- command IDs [MFC], toolbar buttons
- SetButtons method [MFC]
- CToolBar class [MFC], default toolbars in Application Wizard
- frame window classes [MFC], toolbar embedded in
- LoadToolBar method [MFC]
ms.assetid: cc00aaff-8a56-433b-b0c0-b857d76b4ffd
ms.openlocfilehash: 9c784db2e1a482b313147e6837d6bbbd16d0ecb4
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62168215"
---
# <a name="toolbar-fundamentals"></a>工具列基本概念

本文會說明基本的 MFC 實作，可讓您將預設工具列新增至您的應用程式中，應用程式精靈中選取一個選項。 涵蓋的主題包括：

- [應用程式精靈的 [工具列] 選項](#_core_the_appwizard_toolbar_option)

- [在程式碼中的工具列](#_core_the_toolbar_in_code)

- [編輯工具列資源](#_core_editing_the_toolbar_resource)

- [多個工具列](#_core_multiple_toolbars)

##  <a name="_core_the_appwizard_toolbar_option"></a> 應用程式精靈 工具列選項

若要取得單一工具列的預設按鈕，選取 標準停駐工具列選項，在標示為 使用者介面功能 頁面。 這會將程式碼加入您的應用程式的：

- 建立工具列物件。

- 管理工具列，包括停駐或浮動其能力。

##  <a name="_core_the_toolbar_in_code"></a> 在程式碼中的工具列

工具列[CToolBar](../mfc/reference/ctoolbar-class.md)物件宣告為您的應用程式的資料成員`CMainFrame`類別。 換句話說，工具列物件會內嵌在主框架視窗物件。 這表示，MFC 會建立工具列時它會建立框架視窗，並終結時終結框架視窗的工具列。 下列的部分類別宣告中的多個文件介面 (MDI) 應用程式中，顯示內嵌的工具列和內嵌的狀態列上的資料成員。 它也會顯示的覆寫`OnCreate`成員函式。

[!code-cpp[NVC_MFCListView#6](../atl/reference/codesnippet/cpp/toolbar-fundamentals_1.h)]

工具列作業發生`CMainFrame::OnCreate`。 MFC 呼叫[OnCreate](../mfc/reference/cwnd-class.md#oncreate)之後建立的視窗框架，但之前變成可見。 預設值`OnCreate`應用程式精靈 會產生沒有下列工具列工作：

1. 呼叫`CToolBar`物件的[建立](../mfc/reference/ctoolbar-class.md#create)成員函式來建立基礎[CToolBarCtrl](../mfc/reference/ctoolbarctrl-class.md)物件。

1. 呼叫[LoadToolBar](../mfc/reference/ctoolbar-class.md#loadtoolbar)載入工具列資源資訊。

1. 呼叫函數，讓停駐、 浮動和工具提示。 如需這些呼叫的詳細資訊，請參閱文章[停駐和浮動工具列](../mfc/docking-and-floating-toolbars.md)。

> [!NOTE]
>  MFC 一般範例[DOCKTOOL](../overview/visual-cpp-samples.md)包含舊和新的 MFC 工具列的圖例。 使用工具列`COldToolbar`需要在步驟 2 中的呼叫`LoadBitmap`(而非`LoadToolBar`) 和`SetButtons`。 新的工具列要求呼叫`LoadToolBar`。

停駐、 浮動和工具提示的呼叫是選擇性的。 您可以移除從這些行`OnCreate`如果您偏好。 結果是一個工具列，則會維持固定、 浮動、 變換位置無法且無法顯示工具提示。

##  <a name="_core_editing_the_toolbar_resource"></a> 編輯工具列資源

得到的應用程式精靈 的預設工具列根據**RT_TOOLBAR** MFC 4.0 版中導入的自訂資源。 您可以編輯此資源[工具列編輯器](../windows/toolbar-editor.md)。 編輯器可讓您輕鬆地新增、 刪除和重新排列按鈕。 它包含的圖形化編輯器非常類似於一般圖形編輯器，在視覺效果的按鈕C++。 如果您編輯工具列在視覺效果的舊版C++，您會發現工作更容易現在。

若要連接的工具列按鈕命令，您為按鈕提供的命令識別碼，例如`ID_MYCOMMAND`。 工具列編輯器中的按鈕的屬性頁中指定的命令 ID。 然後建立命令處理常式函式 (請參閱[將訊息對應至函式](../mfc/reference/mapping-messages-to-functions.md)如需詳細資訊)。

新[CToolBar](../mfc/reference/ctoolbar-class.md)成員函式適用於**RT_TOOLBAR**資源。 [LoadToolBar](../mfc/reference/ctoolbar-class.md#loadtoolbar)現在會取代[LoadBitmap](../mfc/reference/ctoolbar-class.md#loadbitmap)載入 工具列按鈕影像的點陣圖並[SetButtons](../mfc/reference/ctoolbar-class.md#setbuttons)設定按鈕樣式，並連接與點陣圖影像的按鈕。

如需有關使用工具列編輯器的詳細資訊，請參閱 <<c0> [ 工具列編輯器](../windows/toolbar-editor.md)。

##  <a name="_core_multiple_toolbars"></a> 多個工具列

應用程式精靈為您提供一個預設工具列。 如果您需要一個以上的工具列中您的應用程式時，您可以建立模型程式碼的預設工具列精靈產生的程式碼為基礎的其他工具列。

如果您想要顯示的工具列命令的結果，您必須：

- 使用工具列編輯器建立新的工具列資源，並將其在載入`OnCreate`具有[LoadToolbar](../mfc/reference/ctoolbar-class.md#loadtoolbar)成員函式。

- 內嵌的新[CToolBar](../mfc/reference/ctoolbar-class.md)主框架視窗類別中的物件。

- 請適當的函式呼叫中`OnCreate`停駐或浮動工具列、 設定其樣式中，然後依此類推。

### <a name="what-do-you-want-to-know-more-about"></a>您想要深入了解什麼

- [MFC 工具列實作 （在工具列上的概觀資訊）](../mfc/mfc-toolbar-implementation.md)

- [停駐和浮動工具列](../mfc/docking-and-floating-toolbars.md)

- [工具列工具提示](../mfc/toolbar-tool-tips.md)

- [CToolBar](../mfc/reference/ctoolbar-class.md)並[CToolBarCtrl](../mfc/reference/ctoolbarctrl-class.md)類別

- [使用工具列控制項](../mfc/working-with-the-toolbar-control.md)

- [使用舊的工具列](../mfc/using-your-old-toolbars.md)

## <a name="see-also"></a>另請參閱

[MFC 工具列實作](../mfc/mfc-toolbar-implementation.md)
