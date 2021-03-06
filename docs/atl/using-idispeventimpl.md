---
title: 使用 IDispEventImpl (ATL)
ms.date: 11/04/2016
helpviewer_keywords:
- IDispEventImpl class, using
ms.assetid: 82d53b61-9d0d-45c5-aff9-2fafa468a9ca
ms.openlocfilehash: c532164788d359c7834759de01407d49c19463ca
ms.sourcegitcommit: c6f8e6c2daec40ff4effd8ca99a7014a3b41ef33
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/24/2019
ms.locfileid: "64341486"
---
# <a name="using-idispeventimpl"></a>使用 IDispEventImpl

當使用`IDispEventImpl`來處理事件，您必須：

- 衍生您的類別，從[IDispEventImpl](../atl/reference/idispeventimpl-class.md)。

- 將事件接收對應新增至您的類別。

- 將項目新增至事件接收對應使用[SINK_ENTRY](reference/composite-control-macros.md#sink_entry)或是[SINK_ENTRY_EX](reference/composite-control-macros.md#sink_entry_ex)巨集。

- 實作您想要處理的方法。

- 通知與取消通知的事件來源。

## <a name="example"></a>範例

下列範例示範如何處理`DocumentChange`事件引發的 Word**應用程式**物件。 此事件上定義為方法`ApplicationEvents`dispinterface。

此範例是來自[ATLEventHandling 範例](../overview/visual-cpp-samples.md)。

```cpp
[ uuid(000209F7-0000-0000-C000-000000000046), hidden ]
dispinterface ApplicationEvents {
properties:
methods:
    [id(0x00000001), restricted, hidden]
    void Startup();

    [id(0x00000002)]
    void Quit();

    [id(0x00000003)]
    void DocumentChange();
};
```

此範例會使用`#import`從 Word 的型別程式庫產生必要的標頭檔。 如果您想要與其他版本的 Word 中使用此範例中，您必須指定正確的 mso dll 檔案。 例如，Office 2000 提供 mso9.dll 和 OfficeXP 提供 mso.dll。 此程式碼被簡化從 stdafx.h 中：

[!code-cpp[NVC_ATL_EventHandlingSample#1](../atl/codesnippet/cpp/using-idispeventimpl_1.h)]

下列程式碼會出現在 NotSoSimple.h。 相關的程式碼註解所註明：

[!code-cpp[NVC_ATL_EventHandlingSample#2](../atl/codesnippet/cpp/using-idispeventimpl_2.h)]

## <a name="see-also"></a>另請參閱

[事件處理](../atl/event-handling-and-atl.md)<br/>
[ATLEventHandling 範例](../overview/visual-cpp-samples.md)
