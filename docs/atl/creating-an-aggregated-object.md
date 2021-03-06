---
title: 建立彙總的物件
ms.date: 11/04/2016
helpviewer_keywords:
- aggregation [C++], creating aggregated objects
- aggregate objects [C++], creating
ms.assetid: fc29d7aa-fd53-4276-9c2f-37379f71b179
ms.openlocfilehash: 4be8d0e852da91b58125dc01d44eed4560b2b8d9
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62250754"
---
# <a name="creating-an-aggregated-object"></a>建立彙總的物件

彙總委派`IUnknown`呼叫中，提供外部物件的指標`IUnknown`內部物件。

## <a name="to-create-an-aggregated-object"></a>若要建立彙總的物件

1. 新增`IUnknown`指向您的類別物件，並將它初始化為 NULL 的建構函式。

1. 覆寫[跖](../atl/reference/ccomobjectrootex-class.md#finalconstruct)來建立彙總。

1. 使用`IUnknown`指標，在步驟 1 中定義為第二個參數，如[COM_INTERFACE_ENTRY_AGGREGATE](reference/com-interface-entry-macros.md#com_interface_entry_aggregate)巨集。

1. 覆寫[FinalRelease](../atl/reference/ccomobjectrootex-class.md#finalrelease)釋放`IUnknown`指標。

> [!NOTE]
> 如果您使用，並發行期間的彙總物件的介面`FinalConstruct`，您應該加入[DECLARE_PROTECT_FINAL_CONSTRUCT](reference/aggregation-and-class-factory-macros.md#declare_protect_final_construct)類別物件定義的巨集。

## <a name="see-also"></a>另請參閱

[ATL COM 物件的基本概念](../atl/fundamentals-of-atl-com-objects.md)
