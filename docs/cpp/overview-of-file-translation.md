---
title: 檔案轉譯概觀
ms.date: 11/04/2016
helpviewer_keywords:
- file translation [C++], about file translation
- translation [C++]
- translation phases
- files [C++], translation
- programs [C++], lexical conventions of
- preprocessing translation phase
ms.assetid: 5036c7b7-ccff-4e2c-b052-a9ea6c71af87
ms.openlocfilehash: cb8a8fea2411e4eb7de78545f70021f3617b0f52
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62325139"
---
# <a name="overview-of-file-translation"></a>檔案轉譯概觀

C++ 程式 (類似 C 程式) 包含一個或多個檔案。 這些檔案都按下列概念順序轉譯 (實際的順序會依循 "as if" 規則：如果已依照這些步驟進行，則必須進行轉譯)：

1. 語彙 Token 化。 此轉譯階段中會執行字元對應和三併詞處理、行接合，以及 Token 化。

1. 前置處理。 這個轉譯階段會在所參考的附屬原始程式檔`#include`指示詞，處理 「 字串化 」 和 「 字元化 」 指示詞，並執行語彙基元的基元帶入和巨集展開 (請參閱 <<c2> [ 前置處理器指示詞](../preprocessor/preprocessor-directives.md)在 *前置處理器參考 》* 如需詳細資訊)。 前置處理階段產生的結果是一個結合起來，定義一個「轉譯單位」的語彙基元序列。

   前置處理器指示詞一律開頭數字符號 (**#**) 字元 （也就是該行的第一個非泛空白字元字元必須是數字的符號）。 指定行上只能有一個前置處理器指示詞。 例如: 

    ```cpp
    #include <iostream>  // Include text of iostream in
                         //  translation unit.
    #define NDEBUG       // Define NDEBUG (NDEBUG contains empty
                         //  text string).
    ```

1. 程式碼產生。 這個轉譯階段會使用前置處理階段中產生的語彙基元來產生物件程式碼。

   在這個階段中會執行原始程式碼的語法和語意檢查。

請參閱[轉譯階段](../preprocessor/phases-of-translation.md)中*前置處理器參考 》* 如需詳細資訊。

C++ 前置處理器是 ANSI C 語言前置處理器的嚴格超集，不過，C++ 前置處理器在某些情況下有所不同。 下列清單說明 ANSI C 和 C++ 前置處理器之間的一些差異：

- 支援單行註解。 請參閱[註解](../cpp/comments-cpp.md)如需詳細資訊。

- 一個預先定義的巨集`__cplusplus`，定義僅適用於C++。 請參閱[Predefined Macros](../preprocessor/predefined-macros.md)中*前置處理器參考 》* 如需詳細資訊。

- C 前置處理器無法辨識C++運算子： **。**<strong>\*</strong>， **->** <strong>\*</strong>，以及 **::**。 請參閱[運算子](../cpp/cpp-built-in-operators-precedence-and-associativity.md)並[運算式](../cpp/expressions-cpp.md)，如需運算子的詳細資訊。

## <a name="see-also"></a>另請參閱

[語彙慣例](../cpp/lexical-conventions.md)
