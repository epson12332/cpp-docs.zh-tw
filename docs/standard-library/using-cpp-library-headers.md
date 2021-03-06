---
title: 使用 C++ 程式庫標頭
ms.date: 11/04/2016
helpviewer_keywords:
- headers, naming in C++ include directive
- standard header in C++
- headers
- INCLUDE directive
- headers, C++ Standard Library
- library headers
- C++ Standard Library, headers
ms.assetid: a36e889e-1af2-4cd9-a211-bfc7a3fd8e85
ms.openlocfilehash: b9841d1045a6d2d1126414f1ce4cfc93f9667eef
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62362357"
---
# <a name="using-c-library-headers"></a>使用 C++ 程式庫標頭

您可以透過在 include 指示詞中命名標準標頭來包含其內容。

```cpp
#include <iostream>// include I/O facilities
```

您可以依任何順序包含標準標頭、包含相同的標準標頭超過一次，或是包含兩個以上定義相同巨集或相同類型的標準標頭。 請勿在宣告中包含標準標頭。 在包含標準標頭之前，請勿定義使用相同名稱做為關鍵字的巨集。

C++ 程式庫標頭包含所有它需要定義所需類型的其他 C++ 程式庫標頭。 (不過，請一律在轉譯單位中明確包含任何所需的 C++ 程式庫標頭，以免您針對其實際相依性做出錯誤的判斷。)標準 C 標頭永遠不會包括其他標準標頭。 標準標頭僅宣告或定義此文件中針對它所描述的實體。

程式庫中的每個函式都會在標準標頭中宣告。 不同於標準 C，標準標頭永遠不會提供與遮罩函式宣告並達到相同效果之函式同名的遮罩巨集。 如需有關遮罩巨集的詳細資訊，請參閱 [C++ 程式庫慣例](../standard-library/cpp-library-conventions.md)。

以外的所有名稱**delete 運算子**並**new 運算子**在C++中所定義的程式庫標頭`std`命名空間，或巢狀命名空間中`std`命名空間。 您會參考名稱 `cin` (例如，`std::cin`)。 不過請注意，巨集名稱不會受限於命名空間限定性條件，因此您一律會以不含命名空間限定詞的方式撰寫 `__STD_COMPLEX` 。

在部分轉譯環境，包括C++程式庫標頭可能中宣告的外部名稱帶入`std`全域命名空間，命名空間的個別**使用**宣告每個名稱。 否則，標頭「不會」將任何程式庫名稱引進到目前的命名空間中。

C++標準需要 C 標準標頭宣告命名空間中的所有外部名稱`std`，然後將它們提至個別的全域命名空間**使用**宣告每個名稱。 但是在部分轉譯環境中，C 標準標頭不會包含命名空間宣告，並會直接在全域命名空間中宣告所有名稱。 因此，處理命名空間最方便的方式是遵循兩個規則︰

- 例如，若要在命名空間 `std` 中確實宣告一個傳統上會在 \<stdlib.h> 中宣告的外部名稱，請包含標頭 \<cstdlib>。 請了解該名稱也可能在全域命名空間中宣告。

- 若要在全域命名空間中確實宣告在 \<stdlib.h> 中宣告的外部名稱，請直接包含標頭 \<stdlib.h>。 請了解該名稱也可能在命名空間 `std` 中宣告。

因此，如果您想要呼叫 `std::abort` 以造成異常終止，您應該包含 \<cstdlib>。 如果您想要呼叫 `abort`，您應該包含 \<stdlib.h>。

或者，您可以撰寫宣告︰

```cpp
using namespace std;
```

這會將所有程式庫名稱帶入目前的命名空間。 如果您在所有 include 指示詞之後立即撰寫這個宣告，您會將名稱帶入全域命名空間名稱中。 接下來，您可以忽略轉譯單位其餘部分中的命名空間考量。 您也會避免大多數跨不同轉譯環境的差異。

除非特別指出，否則您不能定義程式內 `std` 命名空間中，或是巢狀於 `std` 命名空間內之命名空間中的名稱。

## <a name="see-also"></a>另請參閱

[C++ 標準程式庫概觀](../standard-library/cpp-standard-library-overview.md)<br/>
[C++ 標準程式庫中的執行緒安全](../standard-library/thread-safety-in-the-cpp-standard-library.md)<br/>
