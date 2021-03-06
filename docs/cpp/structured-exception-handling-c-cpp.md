---
title: Structured Exception Handling (C/C++)
ms.date: 08/14/2018
helpviewer_keywords:
- termination handlers [C++], handling exceptions in C++
- structured exception handling [C++]
- try-catch keyword [C++], exception handlers
- C++ exception handling, termination handlers
- try-catch keyword [C++], termination handlers
- C++ exception handling, exception handlers
ms.assetid: dd3b647d-c269-43a8-aab9-ad1458712976
ms.openlocfilehash: e948d941afa1459623619e385aa67b1c60490245
ms.sourcegitcommit: da32511dd5baebe27451c0458a95f345144bd439
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/07/2019
ms.locfileid: "65221955"
---
# <a name="structured-exception-handling-cc"></a>Structured Exception Handling (C/C++)

結構化例外狀況處理 (SEH) 是依正常程序處理特定例外狀況程式碼的情況下，例如硬體故障，C 的 Microsoft 擴充功能。 雖然 Windows 和 MicrosoftC++支援 SEH，我們建議您使用 ISO 標準C++例外狀況處理，因為它可讓您的程式碼，更可攜性和彈性。 不過，若要維護現有的程式碼或針對特定類型的程式，您仍然必須使用 SEH。

**Microsoft 專有的：**

## <a name="grammar"></a>文法

*try-except-statement* :<br/>
&nbsp;&nbsp;&nbsp;&nbsp;**__try** *compound-statement* **__except** **(** *expression* **)** *compound-statement*

*try finally-陳述式*:<br/>
&nbsp;&nbsp;&nbsp;&nbsp;**__try** *compound-statement* **__finally** *compound-statement*

## <a name="remarks"></a>備註

使用 SEH，您可以確保，例如記憶體區塊和檔案的資源會釋出正確執行意外終止。 您也可以處理特定問題 — 比方說，沒有足夠的記憶體 — 使用簡潔的結構化程式碼，不會依賴**goto**陳述式，或傳回碼的複雜測試。

本文中參照的 try-except 和 try-finally 陳述式是 C 語言的 Microsoft 擴充功能。 它們支援 SEH，讓應用程式在終止執行的事件之後取得程式的控制權。 雖然 SEH 與 C++ 原始程式檔搭配運作，但它不是專為 C++ 所設計。 如果您使用在 SEHC++您使用編譯的計劃[/EHa 或 /EHsc](../build/reference/eh-exception-handling-model.md)選項，則解構函式的呼叫本機物件，但其他執行行為可能不是您的預期。 如需圖例，請參閱本文稍後的範例。 在大部分情況下，而不是 SEH 我們建議您使用 ISO 標準[C++例外狀況處理](../cpp/try-throw-and-catch-statements-cpp.md)，而 MicrosoftC++編譯器也支援。 使用 C++ 例外狀況處理，確保您的程式碼更具可攜性，而且您可以處理任何類型的例外狀況。

如果您有使用 SEH 的 C 程式碼時，您可以混合使用C++使用的程式碼C++例外狀況處理。 如需資訊，請參閱[處理中的結構化例外狀況C++ ](../cpp/exception-handling-differences.md)。

有兩種 SEH 機制：

- [例外狀況處理常式](../cpp/writing-an-exception-handler.md)，或 **__except**區塊，可回應或關閉例外狀況。

- [終止處理常式](../cpp/writing-a-termination-handler.md)，或 **__finally**一律呼叫時，是否發生例外狀況或不會導致終止的區塊。

這兩種處理常式不同，但透過稱為「回溯堆疊」的處理序密切相關。 結構化例外狀況發生時，Windows 會尋找目前作用中的最近安裝例外狀況處理常式。 處理常式可以執行下列三項事項的其中一項：

- 無法辨識例外狀況，並將控制權傳給其他處理常式。

- 辨識例外狀況，但關閉它。

- 辨識例外狀況，並處理它。

可辨識例外狀況的例外狀況處理常式可能不在例外狀況發生時正在執行的函式中。 在某些情況下，它可能在堆疊上更高的函式中。 目前執行中函式和堆疊框架上的所有其他函式都會終止。 在此過程中，堆疊是 「 回溯 」 堆疊; 亦即，從堆疊清除終止函式的非靜態區域變數。

回溯堆疊時，作業系統會呼叫您為每個函式所撰寫的任何終止處理常式。 透過使用終止處理常式，您可以清除因異常終止而仍然保持開啟的資源。 如果您已經進入重要區段，您可以在終止處理常式中結束它。 如果程式即將關閉，您可以執行其他環境維護工作 (例如關閉和移除暫存檔案)。

## <a name="next-steps"></a>後續步驟

- [撰寫例外狀況處理常式](../cpp/writing-an-exception-handler.md)

- [撰寫終止處理常式](../cpp/writing-a-termination-handler.md)

- [使用 C++ 處理結構化例外狀況](../cpp/exception-handling-differences.md)

## <a name="example"></a>範例

如前所述，解構函式會呼叫區域物件，如果您使用中的 SEH 的C++程式，並使用編譯 **/EHa**或是 **/EHsc**選項。 不過，如果您同時使用 C++ 例外狀況，則在執行期間的行為可能會不如預期。 此範例示範這些行為的差異。

```cpp
#include <stdio.h>
#include <Windows.h>
#include <exception>

class TestClass
{
public:
    ~TestClass()
    {
        printf("Destroying TestClass!\r\n");
    }
};

__declspec(noinline) void TestCPPEX()
{
#ifdef CPPEX
    printf("Throwing C++ exception\r\n");
    throw std::exception("");
#else
    printf("Triggering SEH exception\r\n");
    volatile int *pInt = 0x00000000;
    *pInt = 20;
#endif
}

__declspec(noinline) void TestExceptions()
{
    TestClass d;
    TestCPPEX();
}

int main()
{
    __try
    {
        TestExceptions();
    }
    __except(EXCEPTION_EXECUTE_HANDLER)
    {
        printf("Executing SEH __except block\r\n");
    }

    return 0;
}
```

如果您使用 **/EHsc**若要編譯此程式碼，但本機測試控制項巨集`CPPEX`會未定義，沒有任何執行`TestClass`解構函式，則輸出看起來像這樣：

```Output
Triggering SEH exception
Executing SEH __except block
```

如果您使用 **/EHsc**編譯程式碼和`CPPEX`使用定義`/DCPPEX`(以便C++會擲回例外狀況)，則`TestClass`解構函式執行，並輸出看起來像這樣：

```Output
Throwing C++ exception
Destroying TestClass!
Executing SEH __except block
```

如果您使用 **/EHa**編譯的程式碼`TestClass`解構函式執行，不論是否擲回例外狀況使用`std::throw`或使用 SEH 來觸發例外狀況，也就是是否`CPPEX`定義或不。 輸出顯示如下：

```Output
Throwing C++ exception
Destroying TestClass!
Executing SEH __except block
```

如需詳細資訊，請參閱 [/EH (例外狀況處理模型)](../build/reference/eh-exception-handling-model.md)。

**結束 Microsoft 專屬**

## <a name="see-also"></a>另請參閱

[例外狀況處理](../cpp/exception-handling-in-visual-cpp.md)<br/>
[關鍵字](../cpp/keywords-cpp.md)<br/>
[\<exception>](../standard-library/exception.md)<br/>
[錯誤和例外狀況處理](../cpp/errors-and-exception-handling-modern-cpp.md)<br/>
[結構化的例外處理 (Windows)](https://msdn.microsoft.com/library/windows/desktop/ms680657.aspx)
