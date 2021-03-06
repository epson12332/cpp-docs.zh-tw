---
title: 事件處理原則 (ATL)
ms.date: 11/04/2016
helpviewer_keywords:
- event handling, implementing
- event handling, advising event sources
- interfaces, event and event sink
- dual interfaces, event interfaces
- event handling, dual event interfaces
ms.assetid: d17ca7cb-54f2-4658-ab8b-b721ac56801d
ms.openlocfilehash: b882a1d356a431f75be1feb6e7bd997abed41c33
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62234767"
---
# <a name="event-handling-principles"></a>事件處理原則

有三個步驟通用於所有的事件處理。 您將需要：

- 在物件上實作事件介面。

- 建議您物件想要接收事件的事件來源。

- 當您的物件不再需要以接收事件時，請取消通知事件來源。

您將實作事件介面的方式將取決於其型別。 Vtable、 dual、 或 dispinterface，可以是事件介面。 已啟動事件來源定義的介面; 的設計工具它由您實作該介面。

> [!NOTE]
>  雖然沒有任何事件介面不可以是雙重的技術原因，但有許多良好的設計以避免雙重介面使用的原因。 不過，這是由設計工具/實作器的事件所做的決策*來源*。 因為您正在從事件的觀點來看`sink`，您需要允許您可能沒有任何選擇的可能性，但實作雙重事件介面。 如需有關介面的詳細資訊，請參閱[雙重介面和 ATL](../atl/dual-interfaces-and-atl.md)。

通知事件來源可以分成三個步驟：

- 查詢的來源物件[IConnectionPointContainer](/windows/desktop/api/ocidl/nn-ocidl-iconnectionpointcontainer)。

- 呼叫[IConnectionPointContainer::FindConnectionPoint](/windows/desktop/api/ocidl/nf-ocidl-iconnectionpointcontainer-findconnectionpoint)傳遞事件介面的 IID，將您感興趣。 如果成功，這會傳回[IConnectionPoint](/windows/desktop/api/ocidl/nn-ocidl-iconnectionpoint)連接點物件上的介面。

- 呼叫[IConnectionPoint::Advise](/windows/desktop/api/ocidl/nf-ocidl-iconnectionpoint-advise)傳遞`IUnknown`事件接收。 如果成功，這會傳回`DWORD`代表的連接 cookie。

一旦您已經順利註冊您要接收事件，就會呼叫物件的事件介面上的方法，根據來源物件所引發的事件。 當您不再需要接收事件時，您可以將 cookie 傳遞至透過的連接點[iconnectionpoint::](/windows/desktop/api/ocidl/nf-ocidl-iconnectionpoint-unadvise)。 這會中斷來源和接收器之間的連線。

請小心避免參考循環處理事件時。

## <a name="see-also"></a>另請參閱

[事件處理](../atl/event-handling-and-atl.md)
