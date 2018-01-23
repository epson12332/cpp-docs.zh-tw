---
title: "開啟檔案 |Microsoft 文件"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: cpp-windows
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: C++
helpviewer_keywords:
- Open member functions [MFC]
- CFile class [MFC], variable
- opening files, in MFC
- Open calls [MFC]
- Open method, CFile class [MFC]
- examples [MFC], opening files
- opening files, handling exceptions
- exception handling [MFC], when opening files
- files [MFC], opening
- file objects [MFC]
- MFC, file operations
- opening files [MFC]
- exception handling [MFC], opening files
ms.assetid: a991b8ec-b04a-4766-b47e-7485b5dd0b01
caps.latest.revision: "11"
author: mikeblome
ms.author: mblome
manager: ghogen
ms.workload: cplusplus
ms.openlocfilehash: 3ebc650aa4a3f13a0cbc9d9b0026d948d64ae8b4
ms.sourcegitcommit: 8fa8fdf0fbb4f57950f1e8f4f9b81b4d39ec7d7a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="opening-files"></a>開啟檔案
在 MFC 中，最常見的開啟檔案方式是一個兩階段的程序。  
  
#### <a name="to-open-a-file"></a>開啟檔案  
  
1.  建立檔案物件，而不指定路徑或使用權限旗標。  
  
     您通常會藉由宣告建立檔案物件[CFile](../mfc/reference/cfile-class.md)堆疊框架上的變數。  
  
2.  呼叫[開啟](../mfc/reference/cfile-class.md#open)提供路徑和使用權限旗標的 「 檔案 」 物件的成員函式。  
  
     如果已成功開啟檔案，`Open` 會傳回非零值，如果無法開啟指定的檔案則會傳回 0。 `Open` 成員函式的原型如下：  
  
     `virtual BOOL Open( LPCTSTR lpszFileName, UINT nOpenFlags, CFileException* pError = NULL );`  
  
     開啟旗標指定您要為檔案指定的使用權限，例如唯讀。 可能的旗標值會在 `CFile` 類別中定義為列舉常數，使其符合 "`CFile::`" 的格式，如 `CFile::modeRead`。 如果您要建立檔案，請使用 `CFile::modeCreate` 旗標。  
  
 下列範例顯示如何建立具有讀取/寫入權限的新檔案 (取代任何具有相同路徑的舊檔案)：  
  
 [!code-cpp[NVC_MFCFiles#1](../atl-mfc-shared/reference/codesnippet/cpp/opening-files_1.cpp)]  
  
> [!NOTE]
>  這個範例會建立並開啟檔案。 如果發生問題，則 `Open` 可能會在它的最後一個參數中傳回 `CFileException` 物件，如下所示。 `TRACE` 巨集會列印檔案名稱和表示失敗原因的代碼。 如果需要更詳細的錯誤報告，您可以呼叫 `AfxThrowFileException` 函式。  
  
## <a name="see-also"></a>請參閱  
 [CFile 類別](../mfc/reference/cfile-class.md)   
 [CFile::Open](../mfc/reference/cfile-class.md#open)   
 [檔案](../mfc/files-in-mfc.md)
