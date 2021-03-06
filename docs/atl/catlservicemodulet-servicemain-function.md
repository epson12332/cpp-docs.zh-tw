---
title: 'Catlservicemodulet:: Servicemain 函式'
ms.date: 11/04/2016
helpviewer_keywords:
- ServiceMain method
ms.assetid: f21408c1-1919-4dec-88d8-bf5b39ac9808
ms.openlocfilehash: 81cd8fcbdf275063b243e215301eff504a2b5cc6
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62223205"
---
# <a name="catlservicemoduletservicemain-function"></a>Catlservicemodulet:: Servicemain 函式

服務控制管理員 (SCM) 會呼叫`ServiceMain`當您開啟 [服務] 控制台應用程式，選取服務，然後按一下**啟動**。

SCM 之後會呼叫`ServiceMain`，服務必須讓 SCM 處理常式函式。 此函式可讓 SCM 取得服務的狀態並傳遞 （例如暫停或停止） 的特定指示。 SCM 會取得此函式，當服務通過`_Handler`Win32 API 函式[RegisterServiceCtrlHandler](/windows/desktop/api/winsvc/nf-winsvc-registerservicectrlhandlera)。 (`_Handler`靜態成員函式呼叫非靜態成員函式[處理常式](../atl/reference/catlservicemodulet-class.md#handler)。)

在啟動時，服務也應該通知 SCM，它目前的狀態。 其做法是將傳遞至 Win32 API 函式的 SERVICE_START_PENDING [SetServiceStatus](/windows/desktop/api/winsvc/nf-winsvc-setservicestatus)。

`ServiceMain` 然後呼叫`CAtlExeModuleT::InitializeCom`，它會呼叫 Win32 API 函式[CoInitializeEx](/windows/desktop/api/combaseapi/nf-combaseapi-coinitializeex)。 根據預設， `InitializeCom` COINIT_MULTITHREADED 旗標傳遞至函數。 此旗標會指出程式是無限制執行緒的伺服器。

現在，`CAtlServiceModuleT::Run`呼叫來執行服務的主要工作。 `Run` 會繼續執行，直到服務已停止。

## <a name="see-also"></a>另請參閱

[服務](../atl/atl-services.md)<br/>
[CAtlServiceModuleT::ServiceMain](../atl/reference/catlservicemodulet-class.md#servicemain)
