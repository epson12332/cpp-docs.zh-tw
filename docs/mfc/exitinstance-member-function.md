---
title: ExitInstance 成員函式
ms.date: 11/04/2016
f1_keywords: []
helpviewer_keywords:
- programs [MFC], terminating
- CWinApp class [MFC], ExitInstance
- ExitInstance method [MFC]
ms.assetid: 5bb597bd-8dab-4d49-8bcf-9c45aa8be4a2
ms.openlocfilehash: c76f588b22ad8ffd1d3dae954c5113feffb62a3f
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62405816"
---
# <a name="exitinstance-member-function"></a>ExitInstance 成員函式

[ExitInstance](../mfc/reference/cwinapp-class.md#exitinstance)類別成員函式[CWinApp](../mfc/reference/cwinapp-class.md)一份您的應用程式終止時，通常是因為使用者結束應用程式每次呼叫。

如果您需要特別清除處理，例如釋放繪圖裝置介面 (Graphics Device，GDI) 資源或解除配置程式執行期間使用的記憶體，則可以覆寫 `ExitInstance`。 不過，如文件和檢視這類標準項目的清除則是由 Framework，以及其他針對這些特定物件執行特殊清除的可覆寫函式所提供。

## <a name="see-also"></a>另請參閱

[CWinApp：應用程式類別](../mfc/cwinapp-the-application-class.md)
