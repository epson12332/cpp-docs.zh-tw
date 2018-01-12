---
title: "從 Typelib 精靈加入類別 |Microsoft 文件"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: cpp-windows
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: vc.codewiz.class.typelib
dev_langs: C++
helpviewer_keywords:
- Add Class from TypeLib Wizard [MFC]
- COM interfaces, adding classes
ms.assetid: 96152afd-9374-4649-a6ab-b0fa2a5592a3
caps.latest.revision: "10"
author: mikeblome
ms.author: mblome
manager: ghogen
ms.workload: cplusplus
ms.openlocfilehash: a4aad89b6f3227cac59b6429cc67975db3dad424
ms.sourcegitcommit: 8fa8fdf0fbb4f57950f1e8f4f9b81b4d39ec7d7a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="add-class-from-typelib-wizard"></a>從 Typelib 加入類別精靈
您可以使用此精靈，從可用的型別程式庫加入 MFC 類別。 精靈會建立從選取的類型程式庫加入每個介面的類別。  
  
 **新增從類別**  
 指定的型別程式庫，建立類別之後的位置。  
  
|選項|描述|  
|------------|-----------------|  
|**Registry**|類型程式庫會在系統中註冊。 已註冊型別程式庫中所列**可用的型別程式庫**。|  
|**檔案**|類型程式庫不一定登錄在系統中，但是包含在檔案中。 您必須提供中的檔案位置**位置**。|  
  
 **可用的型別程式庫**  
 列出目前已登錄在系統中的類型程式庫。 類型程式庫從這個清單選取以顯示在其介面**介面**清單。  
  
 請參閱 < 內分散式 COM:: 類型程式庫和語言整合 > MSDN library，如需有關註冊類型程式庫中。  
  
 **位置**  
 指定的型別程式庫的位置。 如果您按一下**檔案**下**加入類別來源**，您可以提供包含型別程式庫之檔案的位置。 若要瀏覽至檔案的位置，按一下省略符號按鈕。  
  
 **介面**  
 列出中目前選取的類型程式庫中的介面**可用的型別程式庫**清單。  
  
|傳送按鈕|描述|  
|---------------------|-----------------|  
|**>**|新增中目前選取的介面**介面**清單。 如果未選取介面則呈暗灰色。|  
|**>>**|加入所有的介面中目前選取的類型程式庫中**可用的型別程式庫**清單。|  
|**<**|移除在目前選取的類別**產生的類別**清單。 呈暗灰色，如果在目前不選取的任何類別**產生的類別**清單。|  
|**<\<**|移除中的所有類別**產生的類別**清單。 如果呈現暗灰色**產生的類別**清單是空的。|  
  
 **產生的類別**  
 指定要從使用新增的介面產生的類別名稱 **>** 或 **>>**   按鈕。 您可以按一下此方塊可選取一個類別，然後使用向上或向下鍵捲動清單，檢視中的每個類別名稱`Class`方塊及檔案名稱中的**檔案** 方塊中，當您按一下時，精靈會產生**完成**。 在此方塊中，您可以一次選取一個類別。  
  
 您可以移除類別選取這份清單中，然後按一下 **<** 。 您不需要，可以移除所有的類別，產生的類別 方塊中選取一個類別依序按一下 **<<** ，移除所有的類別中**產生的類別**方塊。  
  
 `Class`  
 指定在選取的類別名稱**產生的類別**方塊，精靈會新增當您按一下**完成**。 您可以編輯該名稱在`Class`方塊。  
  
 **檔案**  
 設定新類別的標頭檔的名稱。 根據預設，這個名稱根據您在中提供的名稱**產生的類別**。 按一下省略符號按鈕，將檔案名稱儲存到您選擇的位置，或將類別宣告附加至現有的檔案。 如果您選擇現有的檔案，精靈會無法將其儲存到選取的位置直到您按一下**完成**精靈中。  
  
 精靈不會覆寫檔案。 如果當您按一下 選取現有的檔案名稱**完成**，精靈會提示您是否要在類別宣告附加至檔案的內容。 按一下**是**附加檔案，按一下 **否**返回精靈並指定另一個檔案名稱。  
  
## <a name="see-also"></a>請參閱  
 [從類型程式庫的 MFC 類別](../../mfc/reference/adding-an-mfc-class-from-a-type-library.md)   
 [Automation 用戶端：使用型別程式庫](../../mfc/automation-clients-using-type-libraries.md)
