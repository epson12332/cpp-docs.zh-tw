---
title: 函式主體
ms.date: 11/04/2016
helpviewer_keywords:
- functions [C], syntax
- variables, function syntax
- function definitions, function body
- function body
ms.assetid: f7e74822-fac8-4dc8-8f3a-2b1611da4640
ms.openlocfilehash: c227640e45943fb57b1029a4f03329241d1d6b34
ms.sourcegitcommit: f4be868c0d1d78e550fba105d4d3c993743a1f4b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/12/2019
ms.locfileid: "56146862"
---
# <a name="function-body"></a>函式主體

「函式主體」是複合陳述式，其中包含指定函式功能的陳述式。

## <a name="syntax"></a>語法

*function-definition*:<br/>
&nbsp;&nbsp;&nbsp;&nbsp;*declaration-specifiers*<sub>opt</sub> *attribute-seq*<sub>opt</sub> *宣告子* *declaration-list*<sub>opt</sub> *compound-statement*

/\* *attribute-seq* 是 Microsoft 專有 \*/

*compound-statement*: /\* 函式主體 \*/<br/>
&nbsp;&nbsp;&nbsp;&nbsp;**{** *declaration-list*<sub>opt</sub> *statement-list*<sub>opt</sub> **}**

除非另外指定，否則在函式主體中宣告的變數 (稱為「區域變數」) 均具有 **auto** 儲存類別。 呼叫函式時，會建立區域變數儲存區並執行區域初始化。 執行控制權會傳遞至 *compound-statement* 中的第一個陳述式，並且繼續到執行 **return** 陳述式或遇到函式主體的結尾為止。 然後，控制權會回到呼叫該函式的點。

如果函式應傳回值，必須執行包含運算式的 **return** 陳述式。 如果未執行 **return** 陳述式或 **return** 陳述式不包含運算式，則函式的傳回值會是未定義的。

## <a name="see-also"></a>另請參閱

[C 函式定義](../c-language/c-function-definitions.md)
