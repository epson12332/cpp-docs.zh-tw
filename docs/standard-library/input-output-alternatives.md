---
title: 輸入 / 輸出替代項目
ms.date: 05/07/2019
helpviewer_keywords:
- I/O [C++], alternatives
ms.assetid: 9f8401c7-d90d-4285-8918-63573df74a80
ms.openlocfilehash: 5fb98714a96dedf725ea17332d7c1627e3390896
ms.sourcegitcommit: da32511dd5baebe27451c0458a95f345144bd439
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/07/2019
ms.locfileid: "65221398"
---
# <a name="inputoutput-alternatives"></a>輸入/輸出替代項目

MicrosoftC++編譯器會提供 I/O 程式設計中的多個替代方案：

- C 執行階段程式庫直接、無緩衝 I/O。

- ANSI C 執行階段程式庫資料流 I/O。

- 主控台和連接埠直接 I/O。

- MFC 程式庫。

- Microsoft C++ 標準程式庫。

iostream 類別適用於緩衝、格式化的文字 I/O。 如果您需要 C++ 程式設計介面，且決定不使用 Microsoft Foundation Class (MFC) 程式庫，則也可以將它們用於無緩衝或二進位 I/O。 iostream 類別是 C 執行階段函式的物件導向 I/O 替代方案。

您可以將 iostream 類別與 Microsoft Windows 作業系統搭配使用。 資料流和檔案資料流在運作方面沒有限制，但字元模式資料流物件物件 `cin`、`cout`、`cerr` 及 `clog` 與 Windows 圖形化使用者介面並不一致。 您也可以衍生與 Windows 環境直接互動的自訂資料流類別。

## <a name="see-also"></a>另請參閱

[什麼是資料流](../standard-library/what-a-stream-is.md)<br/>
