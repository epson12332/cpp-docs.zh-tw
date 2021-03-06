---
title: 目前時間：一般用途類別
ms.date: 11/04/2016
helpviewer_keywords:
- time, setting current
- current time, CTime object
- procedures, getting current time
- initializing objects, with the current time
- time, getting current
ms.assetid: c39e6775-6a92-4b27-95a7-5c86ed371d8a
ms.openlocfilehash: e883a47243feb7ad1555748ffdda9b8ae9594644
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62236210"
---
# <a name="current-time-general-purpose-classes"></a>目前時間：一般用途類別

下列程序示範如何建立`CTime`物件，並將它初始化與目前的時間。

### <a name="to-get-the-current-time"></a>若要取得目前的時間

1. 配置`CTime`物件，如下所示：

   [!code-cpp[NVC_ATLMFC_Utilities#171](../atl-mfc-shared/codesnippet/cpp/current-time-general-purpose-classes_1.cpp)]

   > [!NOTE]
   > 未初始化`CTime`物件不會初始化為正確的時間。

1. 呼叫`CTime::GetCurrentTime`函式可從作業系統取得目前的時間。 此函數會傳回`CTime`物件，可用來設定的值`CTime`、，如下所示：

   [!code-cpp[NVC_ATLMFC_Utilities#172](../atl-mfc-shared/codesnippet/cpp/current-time-general-purpose-classes_2.cpp)]

   由於`GetCurrentTime`的靜態成員函式，從`CTime`類別，您必須限定其名稱與類別和範圍解析運算子的名稱 (`::`)， `CTime::GetCurrentTime()`。

當然，所述的兩個步驟之前可以合併成單一的程式陳述式，如下所示：

[!code-cpp[NVC_ATLMFC_Utilities#173](../atl-mfc-shared/codesnippet/cpp/current-time-general-purpose-classes_3.cpp)]
