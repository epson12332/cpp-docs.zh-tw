---
title: CWinApp:Application 類別
ms.date: 11/04/2016
f1_keywords:
- CWinApp
helpviewer_keywords:
- application class [MFC]
- CWinApp class [MFC], CWinThread
- MFC, WinMain and
- CWinApp class [MFC], multithreading
- CWinThread class [MFC], and CWinApp
- InitApplication method [MFC]
- WinMain method [MFC]
- WinMain method [MFC], in MFC
- CWinApp class [MFC], WinMain
ms.assetid: 935822bb-d463-481b-a5f6-9719d68ed1d5
ms.openlocfilehash: d9f0d4f5ba6b6b070b23ce98ecda8c7accf44934
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62241558"
---
# <a name="cwinapp-the-application-class"></a>CWinApp:Application 類別

在 MFC 中的主要應用程式類別，會封裝 Windows 作業系統應用程式的初始化、執行和終止。 在架構上建置的應用程式必須有一個並只有一個物件的類別衍生自[CWinApp](../mfc/reference/cwinapp-class.md)。 在建立視窗之前，會先建構這個物件。

`CWinApp` 是衍生自 `CWinThread`，表示執行應用程式的主執行緒，可能有一個或多個執行緒。 在最新版本的 MFC `InitInstance`，**執行**， `ExitInstance`，並`OnIdle`成員函式實際上是在類別中`CWinThread`。 這裡討論的這些函式就如同 `CWinApp` 成員一樣，因為這個討論將物件的角色視為應用程式物件而不是主要執行緒。

> [!NOTE]
>  執行應用程式的主要執行緒是由您的應用程式類別所組成。 您也可以使用 Win32 API 函式建立執行的次要執行緒。 這些執行緒可以使用 MFC 程式庫。 如需詳細資訊，請參閱 <<c0> [ 進行多執行緒處理](../parallel/multithreading-support-for-older-code-visual-cpp.md)。

就像 Windows 作業系統的任何程式一樣，您的架構應用程式具有 `WinMain` 函式。 在架構應用程式中，不過，您不會寫入 `WinMain`。 當應用程式啟動時，會由類別庫提供和呼叫。 `WinMain` 會執行註冊視窗類別等標準服務。 然後，呼叫應用程式物件的成員函式，來初始化和執行應用程式  (您可以覆寫 `WinMain` 呼叫的 `CWinApp` 成員函式來自訂 `WinMain`)。

為了初始化應用程式，`WinMain` 會呼叫應用程式物件的 `InitApplication` 和 `InitInstance` 成員函式。 若要執行的應用程式訊息迴圈中，`WinMain`呼叫**執行**成員函式。 在終止時，`WinMain` 會呼叫應用程式物件的 `ExitInstance` 成員函式。

> [!NOTE]
>  名稱中所示**粗體**本文件中指出提供的 Microsoft Foundation 類別庫和視覺項目C++。 以 `monospaced` 類型顯示的名稱，表示您建立或覆寫的項目。

## <a name="see-also"></a>另請參閱

[一般 MFC 主題](../mfc/general-mfc-topics.md)<br/>
[CWinApp 和 MFC 應用程式精靈](../mfc/cwinapp-and-the-mfc-application-wizard.md)<br/>
[可覆寫的 CWinApp 成員函式](../mfc/overridable-cwinapp-member-functions.md)<br/>
[特殊 CWinApp 服務](../mfc/special-cwinapp-services.md)
