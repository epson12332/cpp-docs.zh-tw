---
title: "類別庫概觀 |Microsoft 文件"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: cpp-windows
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: vc.classes.mfc
dev_langs: C++
helpviewer_keywords:
- grouping MFC classes
- MFC, class library
- classes [MFC], MFC
- class libraries, MFC
- class libraries
ms.assetid: 9b0e3152-ac39-4f52-91b4-f20aa3a674aa
caps.latest.revision: "12"
author: mikeblome
ms.author: mblome
manager: ghogen
ms.openlocfilehash: 014e1792a3431fee8dad673d17afdb84ef620936
ms.sourcegitcommit: ebec1d449f2bd98aa851667c2bfeb7e27ce657b2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/24/2017
---
# <a name="class-library-overview"></a>類別庫概觀
本概觀分類，並說明在 Microsoft Foundation 類別庫 (MFC) 9.0 版的類別。 在 MFC 中，同時採用兩者，類別會構成應用程式架構，適用於 Windows API 撰寫的應用程式的架構。 填入您的應用程式特有的程式碼為您的程式設計工作。  
  
 程式庫的類別會介紹下列類別：  
  
-   [根類別：CObject](../mfc/root-class-cobject.md)  
  
-   [MFC 應用程式架構類別](../mfc/mfc-application-architecture-classes.md)  
  
    -   [應用程式和執行緒支援類別](../mfc/application-and-thread-support-classes.md)  
  
    -   [命令路由類別](../mfc/command-routing-classes.md)  
  
    -   [文件類別](../mfc/document-classes.md)  
  
    -   [檢視類別 (架構)](../mfc/view-classes-architecture.md)  
  
    -   [框架視窗類別 (架構)](../mfc/frame-window-classes-architecture.md)  
  
    -   [文件樣板類別](../mfc/document-template-classes.md)  
  
-   [視窗、對話方塊和控制項類別](../mfc/window-dialog-and-control-classes.md)  
  
    -   [框架視窗類別 (Windows)](../mfc/frame-window-classes-windows.md)  
  
    -   [檢視類別 (Windows)](../mfc/view-classes-windows.md)  
  
    -   [對話方塊類別](../mfc/dialog-box-classes.md)  
  
    -   [控制項類別](../mfc/control-classes.md)  
  
    -   [控制列類別](../mfc/control-bar-classes.md)  
  
-   [繪圖和列印類別](../mfc/drawing-and-printing-classes.md)  
  
    -   [輸出 (裝置內容) 類別](../mfc/output-device-context-classes.md)  
  
    -   [繪圖工具類別](../mfc/drawing-tool-classes.md)  
  
-   [簡單資料類型類別](../mfc/simple-data-type-classes.md)  
  
-   [陣列、清單和對應類別](../mfc/array-list-and-map-classes.md)  
  
    -   [陣列、清單和對應的樣板類別](../mfc/template-classes-for-arrays-lists-and-maps.md)  
  
    -   [立即可用的陣列類別](../mfc/ready-to-use-array-classes.md)  
  
    -   [立即可用的清單類別](../mfc/ready-to-use-list-classes.md)  
  
    -   [立即可用的對應類別](../mfc/ready-to-use-map-classes.md)  
  
-   [檔案和資料庫類別](../mfc/file-and-database-classes.md)  
  
    -   [檔案 I/O 類別](../mfc/file-i-o-classes.md)  
  
    -   [DAO 類別](../mfc/dao-classes.md)  
  
    -   [ODBC 類別](../mfc/odbc-classes.md)  
  
    -   [OLE DB 類別](../mfc/ole-db-classes.md)  
  
-   [網際網路和網路類別](../mfc/internet-and-networking-classes.md)  
  
    -   [Windows Sockets 類別](../mfc/windows-sockets-classes.md)  
  
    -   [Win32 網際網路類別](../mfc/win32-internet-classes.md)  
  
-   [OLE 類別](../mfc/ole-classes.md)  
  
    -   [OLE 容器類別](../mfc/ole-container-classes.md)  
  
    -   [OLE 伺服器類別](../mfc/ole-server-classes.md)  
  
    -   [OLE 拖放和資料傳輸類別](../mfc/ole-drag-and-drop-and-data-transfer-classes.md)  
  
    -   [OLE 通用對話方塊類別](../mfc/ole-common-dialog-classes.md)  
  
    -   [OLE Automation 類別](../mfc/ole-automation-classes.md)  
  
    -   [OLE 控制項類別](../mfc/ole-control-classes.md)  
  
    -   [主動式文件類別](../mfc/active-document-classes.md)  
  
    -   [OLE 相關類別](../mfc/ole-related-classes.md)  
  
-   [偵錯和例外狀況類別](../mfc/debugging-and-exception-classes.md)  
  
    -   [偵錯支援類別](../mfc/debugging-support-classes.md)  
  
    -   [例外狀況類別](../mfc/exception-classes.md)  
  
 區段[一般類別設計原理](../mfc/general-class-design-philosophy.md)說明 MFC 程式庫的設計方式。  
  
 如需架構的概觀，請參閱[使用類別來撰寫 Windows 應用程式](../mfc/using-the-classes-to-write-applications-for-windows.md)。 有些上面所列的類別是一般用途的類別，可用於外部架構，並提供有用的抽象概念，例如集合、 例外狀況、 檔案和字串。  
  
 若要查看繼承的類別，請使用[類別階層架構圖表](../mfc/hierarchy-chart.md)。  
  
 除了本概觀中所列出的類別，MFC 程式庫包含許多全域函式、 全域變數和巨集。 沒有概觀，以及詳細的清單，這些主題中的 < [MFC 巨集和全域](../mfc/reference/mfc-macros-and-globals.md)，其中依照依字母順序排列參考的 MFC 類別。  
  
## <a name="see-also"></a>另請參閱  
 [MFC 傳統型應用程式](../mfc/mfc-desktop-applications.md)
