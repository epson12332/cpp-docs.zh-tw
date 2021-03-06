---
title: 例外狀況處理常式
ms.date: 11/04/2016
f1_keywords:
- c.exceptions
helpviewer_keywords:
- exception handling, routines
ms.assetid: f60548c6-850a-4e1e-a79b-a2a6a541ab62
ms.openlocfilehash: 8def356793906074e6fc4b8d7a139ce1915a5f9b
ms.sourcegitcommit: dedd4c3cb28adec3793329018b9163ffddf890a4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/11/2019
ms.locfileid: "57749135"
---
# <a name="exception-handling-routines"></a>例外狀況處理常式

使用 C++ 例外狀況處理函式在程式執行期間從非預期的事件復原。

## <a name="exception-handling-functions"></a>例外狀況處理函式

|功能|使用|
|--------------|---------|
|[_set_se_translator](../c-runtime-library/reference/set-se-translator.md)|以 C++ 類型化例外狀況處理 Win32 例外狀況 (C 結構化例外狀況)|
|[set_terminate](../c-runtime-library/reference/set-terminate-crt.md)|安裝要由 **terminate** 呼叫的專屬終止常式|
|[set_unexpected](../c-runtime-library/reference/set-unexpected-crt.md)|安裝要由 **unexpected** 呼叫的專屬中止函式|
|[terminate](../c-runtime-library/reference/terminate-crt.md)|在擲回例外狀況之後，在某些情況下自動呼叫。 **terminate** 函式呼叫 **abort** 或您使用 **set_terminate** 指定的函式|
|[unexpected](../c-runtime-library/reference/unexpected-crt.md)|呼叫 **terminate** 或您使用 **set_unexpected** 指定的函式。 目前 Microsoft C++ 例外狀況處理實作中未使用 **unexpected** 函式|

## <a name="see-also"></a>另請參閱

[依類別排序的通用 C 執行階段常式](../c-runtime-library/run-time-routines-by-category.md)<br/>
