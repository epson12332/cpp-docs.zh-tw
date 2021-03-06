---
title: 括號內的運算式
ms.date: 11/04/2016
helpviewer_keywords:
- parentheses
- expression evaluation, evaluation order
- expressions [C++], evaluating
- parentheses, expressions
ms.assetid: b8636147-6982-408c-9e64-29e40678ee43
ms.openlocfilehash: d0105556530161991b46c5ee25cd73f2f995063f
ms.sourcegitcommit: f4be868c0d1d78e550fba105d4d3c993743a1f4b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/12/2019
ms.locfileid: "56149345"
---
# <a name="expressions-in-parentheses"></a>括號內的運算式

您可以將任何運算元包含在括號內，而不會變更括號內運算式的類型或值。 例如，在下列運算式中：

```
( 10 + 5 ) / 5
```

`10 + 5` 前後的括號表示 `10 + 5` 的值會先評估，而且它會變成除法 (**/**) 運算子的左運算元。 `( 10 + 5 ) / 5` 的結果會是 3。 若沒有括號，`10 + 5 / 5` 會評估為 11。

雖然括號會影響運算式中運算元分組的方式，但是無法保證所有情況下的特定評估順序。 例如，下列運算式中的括號和由左至右群組都無法保證 `i` 在任一子運算式中的值為何：

```
( i++ +1 ) * ( 2 + i )
```

編譯器可以依任何順序自由評估乘法的兩邊。 如果 `i` 的初始值為零，則整個運算式會評估為下面這兩個陳述式的其中一個：

```
( 0 + 1 + 1 ) * ( 2 + 1 )
( 0 + 1 + 1 ) * ( 2 + 0 )
```

副作用所造成的例外狀況將在[副作用](../c-language/side-effects.md)中討論。

## <a name="see-also"></a>另請參閱

[C 主要運算式](../c-language/c-primary-expressions.md)
