---
title: 編譯器錯誤 C2659
ms.date: 11/04/2016
f1_keywords:
- C2659
helpviewer_keywords:
- C2659
ms.assetid: b0883600-4d27-4ca7-a931-8ca6bd48654d
ms.openlocfilehash: 1b44ef825626f60e9ae6c6e8600953959fcd7b3a
ms.sourcegitcommit: 28eae422049ac3381c6b1206664455dbb56cbfb6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/31/2019
ms.locfileid: "66449224"
---
# <a name="compiler-error-c2659"></a>編譯器錯誤 C2659

'operator' : 當做左運算元

函式在指定運算子的左邊。 這個錯誤最常見的原因是當開發人員要將運算子左方的識別項當做變數時，編譯器已將其剖析為函式。 如需詳細資訊，請參閱維基百科文章[最常困擾剖析](https://en.wikipedia.org/wiki/Most_vexing_parse)。 此範例顯示容易混淆的函式宣告和變數定義：

```
// C2659a.cpp
// Compile using: cl /W4 /EHsc C2659a.cpp
#include <string>
using namespace std;

int main()
{
   string string1(); // string1 is a function returning string
   string string2{}; // string2 is a string initialized to empty

   string1 = "String 1"; // C2659
   string2 = "String 2";
}
```

若要解決這個問題，請變更識別項的宣告，使其不會被解析為函式宣告。

當函式具有無法在指定運算子左方運算式中使用的類型時，也可能會發生錯誤 C2659。 此範例會在程式碼指派函式指標至函式時產生 C2659：

```
// C2659b.cpp
// Compile using: cl /W4 /EHsc C2659b.cpp
int func0(void) { return 42; }
int (*func1)(void);

int main()
{
   func1 = func0;
   func0 = func1; // C2659
}
```