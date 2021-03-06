---
title: if 陳述式 (C)
ms.date: 11/04/2016
f1_keywords:
- else
- if
helpviewer_keywords:
- if keyword [C]
- else clauses
- else keyword [C]
- if keyword [C], if statement syntax
- nested statements
ms.assetid: d7fc16a0-fdbc-4f39-b596-76e1ca4ad4a5
ms.openlocfilehash: b6df50d483a6e2958de3100a07c18b89b0c4f12f
ms.sourcegitcommit: f4be868c0d1d78e550fba105d4d3c993743a1f4b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/12/2019
ms.locfileid: "56152608"
---
# <a name="if-statement-c"></a>if 陳述式 (C)

**if** 陳述式可控制條件分支。 如果運算式的值為非零值，就會執行 **if** 陳述式的主體。 **if** 陳述式的語法有兩種形式。

## <a name="syntax"></a>語法

*selection-statement*: **if (**  *expression*  **)**  *statement*

**if (**  *expression*  **)**  *statement*  **else**  *statement*

在兩種形式的 **if** 陳述式中，都會評估運算式 (可以有任何值，但結構除外)，包括所有副作用。

在第一種形式的語法中，如果 *expression* 為 true (非零值)，就會執行 *statement*。 如果 *expression* 是 false，則會忽略 *statement*。 在第二種形式的語法 (使用 **else**) 中，如果 *expression* 為 false，就會執行第二個 *statement*。 在這兩種形式中，除非其中一個陳述式包含 **break**、**continue** 或 `goto`，否則控制權會從 **if** 陳述式傳至程式中的下一個陳述式。

以下是 **if** 陳述式的範例：

```
if ( i > 0 )
    y = x / i;
else
{
    x = i;
    y = f( x );
}
```

在此範例中，如果 `y = x/i;` 大於 0，就會執行 `i` 陳述式。 如果 `i` 小於或等於 0，則會將 `i` 指派給 `x`，而將 `f( x )` 指派給 `y`。 請注意，構成 **if** 子句的陳述式會以分號結束。

撰寫巢狀 **if** 陳述式和 **else** 子句時，請使用大括號將陳述式和子句群組成複合陳述式，以便釐清您的意圖。 如果沒有使用大括號，編譯器會在每個 **else** 和缺少 **else** 但最接近的 **if** 之間建立關聯性，以解決模棱兩可的問題。

```
if ( i > 0 )           /* Without braces */
    if ( j > i )
        x = j;
    else
        x = i;
```

本範例中，是在 **else** 子句和內部的 **if** 陳述式之間建立關聯性。 如果 `i` 小於或等於 0，則不會指派任何值給 `x`。

```
if ( i > 0 )
{                      /* With braces */
    if ( j > i )
        x = j;
}
else
    x = i;
```

在這個範例中，括住內部 **if** 陳述式的大括號會使 **else** 子句成為外部 **if** 陳述式的一部分。 如果 `i` 小於或等於 0，會將 `i` 指派給 `x`。

## <a name="see-also"></a>另請參閱

[if-else 陳述式 (C++)](../cpp/if-else-statement-cpp.md)
