---
title: 一般算術轉換
ms.date: 11/04/2016
helpviewer_keywords:
- arithmetic conversions [C++]
- type conversion [C++], arithmetic
- operators [C], arithmetic conversions
- data type conversion [C++], arithmetic
- conversions [C++], arithmetic
- arithmetic operators [C++], type conversions
ms.assetid: bfa49803-0efd-45d0-b987-111412a140d7
ms.openlocfilehash: 729e173c695db3b4970490e84bedfd441e6ff6d3
ms.sourcegitcommit: f4be868c0d1d78e550fba105d4d3c993743a1f4b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/12/2019
ms.locfileid: "56150268"
---
# <a name="usual-arithmetic-conversions"></a>一般算術轉換

大部分的 C 運算子會執行類型轉換，將運算式的運算元轉換為一般類型，或是將短值擴充為電腦作業中使用的整數大小。 C 運算子執行的轉換取決於特定運算子與運算元的類型。 不過，許多運算子會對整數和浮動類型的運算元執行類似轉換。 這些轉換稱為「算術轉換」。 將運算元的值轉換成相容的類型並不會變更其值。

以下摘要說明的算術轉換稱為「一般算術轉換」。 這些步驟僅適用於需要算術類型的二元運算子。 目的是產生一般類型 (也是結果的類型)。 為判斷實際發生的轉換，編譯器會對運算式中的二進位運算套用下列演算法。 下列步驟並非優先順序。

1. 如果任一運算元的類型是 `long double`，就會將另一個運算元轉換成 `long double` 類型。

1. 如果不符合上述條件，而且任一運算元的類型是 **double**，會將另一個運算元轉換為 **double** 類型。

1. 如果不符合上述條件，而且任一運算元的類型是 **float**，會將另一個運算元轉換為 **float** 類型。

1. 如果不符合上述三個條件 (運算元都不是浮動類型)，則會對運算元執行整數轉換，如下所示：

   - 如果任一運算元的類型是 `unsigned long`，就會將另一個運算元轉換成 `unsigned long` 類型。

   - 如果不符合上述條件，而且任一運算元的類型是 **long**，而另一個運算元的類型是 `unsigned int`，則會將兩個運算元都轉換為 `unsigned long` 類型。

   - 如果不符合上述兩個條件，而且任一運算元的類型是 **long**，會將另一個運算元轉換為 **long** 類型。

   - 如果不符合上述三個條件，而且任一運算元的類型是 `unsigned int`，則會將另一個運算元轉換成 `unsigned int` 類型。

   - 如果不符合上述任何條件，會將兩個運算元都轉換成 `int` 類型。

下列程式碼說明這些轉換規則：

```
float   fVal;
double  dVal;
int   iVal;
unsigned long ulVal;

dVal = iVal * ulVal; /* iVal converted to unsigned long
                      * Uses step 4.
                      * Result of multiplication converted to double
                      */
dVal = ulVal + fVal; /* ulVal converted to float
                      * Uses step 3.
                      * Result of addition converted to double
                      */
```

## <a name="see-also"></a>另請參閱

[C 運算子](../c-language/c-operators.md)
