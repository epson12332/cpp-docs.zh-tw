---
title: 循序評估運算子
ms.date: 11/04/2016
helpviewer_keywords:
- operators [C++], sequential-evaluation
- sequential-evaluation operator
- comma operator
ms.assetid: 587514f4-c8e2-44e9-81a8-7a553ce1453a
ms.openlocfilehash: 2cbffc51fb7113ae442dbfcd1db01bbf27a67746
ms.sourcegitcommit: f4be868c0d1d78e550fba105d4d3c993743a1f4b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/12/2019
ms.locfileid: "56149124"
---
# <a name="sequential-evaluation-operator"></a>循序評估運算子

循序評估運算子 (也稱為「逗號運算子」) 是由左至右依序評估其兩個運算元。

## <a name="syntax"></a>語法

*expression*：<br/>
&nbsp;&nbsp;&nbsp;&nbsp;*assignment-expression*<br/>
&nbsp;&nbsp;&nbsp;&nbsp;*expression* **,** *assignment-expression*

循序評估運算子的左運算元會評估為 `void` 運算式。 此作業的結果會是與右運算元相同的值與類型。 各個運算元可以為任何類型。 循序評估運算子不會在其運算元之間執行類型轉換，因此，它不會產生左值。 在第一個運算元之後有一個序列點，表示會先完成左運算元評估的所有副作用，再開始評估右運算元。 如需詳細資訊，請參閱[序列點](../c-language/c-sequence-points.md)。

循序評估運算子通常用來在只允許一個運算式的內容中評估兩個以上的運算式。

逗號可以在內容中當做分隔符號使用。 不過，您必須謹慎避免混淆做為分隔符號使用的逗號，以及做為運算子使用的逗號，這兩種用法完全不同。

## <a name="example"></a>範例

此範例將示範循序評估運算子：

```
for ( i = j = 1; i + j < 20; i += i, j-- );
```

在此範例中，會對 **for** 陳述式的第三個運算式中每一個運算元獨立進行評估。 左運算元 `i += i` 會先評估，然後再評估右運算元 `j--`。

```
func_one( x, y + 2, z );
func_two( (x--, y + 2), z );
```

在 `func_one` 的函式呼叫中，會傳遞三個以逗號分隔的引數：`x`、`y + 2` 和 `z`。 在 `func_two` 的函式呼叫中，括號會強制編譯器將第一個逗號解譯為循序求值運算子。 這個函式呼叫會傳遞兩個引數至 `func_two`。 第一個引數是循序求值運算 `(x--, y + 2)` 的結果，具有 `y + 2` 運算式的值和類型，而第二個引數為 `z`。

## <a name="see-also"></a>另請參閱

[逗號運算子：,](../cpp/comma-operator.md)
