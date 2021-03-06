---
title: 並行執行階段逐步解說
ms.date: 11/04/2016
helpviewer_keywords:
- walkthroughs [Concurrency Runtime]
- Concurrency Runtime, walkthroughs
ms.assetid: 7374c5e9-54eb-44bf-9ed9-5e190cfd290b
ms.openlocfilehash: d176049bb3b03ae0f55170e45e20e7c2c0e322ff
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62296486"
---
# <a name="concurrency-runtime-walkthroughs"></a>並行執行階段逐步解說

這一節以案例為基礎的主題示範如何使用多個並行執行階段的功能。

## <a name="in-this-section"></a>本節內容

[逐步解說：使用工作和 XML HTTP 要求進行連線](../../parallel/concrt/walkthrough-connecting-using-tasks-and-xml-http-requests.md)<br/>
示範如何使用[IXMLHTTPRequest2](/windows/desktop/api/msxml6/nn-msxml6-ixmlhttprequest2)並[IXMLHTTPRequest2Callback](/windows/desktop/api/msxml6/nn-msxml6-ixmlhttprequest2callback)介面，以及將 HTTP GET 和 POST 要求傳送至通用 Windows 平台 (UWP) 應用程式中的 web 服務的工作。

[逐步解說：建立代理程式型的應用程式](../../parallel/concrt/walkthrough-creating-an-agent-based-application.md)<br/>
描述如何建立基本的代理程式型應用程式。

[逐步解說：建立資料流程代理程式](../../parallel/concrt/walkthrough-creating-a-dataflow-agent.md)<br/>
示範如何建立代理程式為基礎的應用程式為基礎的資料流程，而不是在控制流程。

[逐步解說：建立影像處理網路](../../parallel/concrt/walkthrough-creating-an-image-processing-network.md)<br/>
示範如何建立執行映像處理的非同步訊息區的網路。

[逐步解說：實作 Future](../../parallel/concrt/walkthrough-implementing-futures.md)<br/>
示範如何以非同步方式計算值供日後使用。

[逐步解說：使用聯結以預防死結](../../parallel/concrt/walkthrough-using-join-to-prevent-deadlock.md)<br/>
使用哲學家用餐問題，說明如何使用[concurrency:: join](../../parallel/concrt/reference/join-class.md)類別避免應用程式中的死結。

[逐步解說：從使用者介面執行緒移除工作](../../parallel/concrt/walkthrough-removing-work-from-a-user-interface-thread.md)<br/>
示範如何改善繪製 Mandelbrot 碎形的 MFC 應用程式的效能。

[逐步解說：在啟用 COM 的應用程式中使用並行執行階段](../../parallel/concrt/walkthrough-using-the-concurrency-runtime-in-a-com-enabled-application.md)<br/>
示範如何使用並行執行階段中使用元件物件模型 (COM) 的應用程式。

[逐步解說：改寫現有程式碼以使用輕量型工作](../../parallel/concrt/walkthrough-adapting-existing-code-to-use-lightweight-tasks.md)<br/>
顯示如何調整現有的程式碼使用 Windows API 來建立和執行使用輕量型工作的執行緒。

[逐步解說：建立自訂訊息區](../../parallel/concrt/walkthrough-creating-a-custom-message-block.md)<br/>
描述如何建立依優先順序排序內送訊息的自訂訊息區塊類型。

## <a name="related-sections"></a>相關章節

[並行執行階段](../../parallel/concrt/concurrency-runtime.md)<br/>
介紹並行程式設計架構，視覺效果C++。
