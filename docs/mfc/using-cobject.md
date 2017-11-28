---
title: "使用 CObject |Microsoft 文件"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: cpp-windows
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: CObject
dev_langs: C++
helpviewer_keywords:
- examples [MFC], CObject
- root base class for MFC
- derived classes [MFC], from CObject
- MFC, base class
- CObject class [MFC]
ms.assetid: d0cd19bb-2856-4b41-abbc-620fd64cb223
caps.latest.revision: "9"
author: mikeblome
ms.author: mblome
manager: ghogen
ms.openlocfilehash: a892d2831d21c17ceaa21a6403cf325a2b241c9b
ms.sourcegitcommit: ebec1d449f2bd98aa851667c2bfeb7e27ce657b2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/24/2017
---
# <a name="using-cobject"></a>使用 CObject
[CObject](../mfc/reference/cobject-class.md)適用於大部分 Microsoft Foundation 類別庫 (MFC) 是根基底類別。 `CObject`類別包含許多有用的功能，您可能想要併入您自己的程式物件，包括序列化支援、 執行階段類別資訊，以及物件的診斷輸出。 如果您衍生您的類別從`CObject`，您的類別可以利用這些弱點`CObject`功能。  
  
## <a name="what-do-you-want-to-do"></a>您想要做什麼  
  
-   [從 CObject 衍生類別](../mfc/deriving-a-class-from-cobject.md)  
  
-   [我在衍生類別中加入執行階段類別資訊、 動態建立和序列化支援](../mfc/specifying-levels-of-functionality.md)  
  
-   [存取執行階段類別資訊](../mfc/accessing-run-time-class-information.md)  
  
-   [動態建立物件](../mfc/dynamic-object-creation.md)  
  
-   [為方便診斷傾印物件的資料](http://msdn.microsoft.com/en-us/727855b1-5a83-44bd-9fe3-f1d535584b59)  
  
-   驗證物件的內部狀態 (請參閱[MFC ASSERT_VALID 和 CObject::AssertValid](http://msdn.microsoft.com/en-us/7654fb75-9e9a-499a-8165-0a96faf2d5e6))  
  
-   [具有永續性儲存體序列化它本身的類別](../mfc/serialization-in-mfc.md)  
  
-   看到一份[CObject 常見問題集](../mfc/cobject-class-frequently-asked-questions.md)  
  
## <a name="see-also"></a>另請參閱  
 [概念](../mfc/mfc-concepts.md)   
 [一般 MFC 主題](../mfc/general-mfc-topics.md)   
 [CRuntimeClass 結構](../mfc/reference/cruntimeclass-structure.md)   
 [檔案](../mfc/files-in-mfc.md)   
 [序列化](../mfc/serialization-in-mfc.md)
