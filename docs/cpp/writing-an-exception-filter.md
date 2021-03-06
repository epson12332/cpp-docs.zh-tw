---
title: 撰寫例外狀況篩選條件
ms.date: 11/04/2016
helpviewer_keywords:
- exception handling [C++], filters
ms.assetid: 47fc832b-a707-4422-b60a-aaefe14189e5
ms.openlocfilehash: 2bc159247604877fb22ff6084e1fda36946561a1
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62209373"
---
# <a name="writing-an-exception-filter"></a>撰寫例外狀況篩選條件

您可以藉由跳至例外狀況處理常式的層級或繼續執行的方式處理例外狀況。 除了使用例外狀況處理常式程式碼來處理例外狀況並繼續之外，您可以使用*篩選*清除 此問題，然後傳回-1，而不清除堆疊中繼續正常流程。

> [!NOTE]
>  某些例外狀況無法繼續執行。 如果*篩選*會評估為-1 的這類例外狀況，系統就會引發新的例外狀況。 當您呼叫[RaiseException](https://msdn.microsoft.com/library/windows/desktop/ms680552)，您判斷例外狀況是否會繼續。

例如，下列程式碼會使用中的函式呼叫*篩選*運算式： 這個函式會處理問題，則會傳回-1，若要繼續一般控制流程：

```cpp
// exceptions_Writing_an_Exception_Filter.cpp
#include <windows.h>
int main() {
   int Eval_Exception( int );

   __try {}

   __except ( Eval_Exception( GetExceptionCode( ))) {
      ;
   }

}
void ResetVars( int ) {}
int Eval_Exception ( int n_except ) {
   if ( n_except != STATUS_INTEGER_OVERFLOW &&
      n_except != STATUS_FLOAT_OVERFLOW )   // Pass on most exceptions
   return EXCEPTION_CONTINUE_SEARCH;

   // Execute some code to clean up problem
   ResetVars( 0 );   // initializes data to 0
   return EXCEPTION_CONTINUE_EXECUTION;
}
```

它是個不錯的主意，使用中的函式呼叫*篩選器*運算式每當*篩選*需要執行任何複雜的動作。 評估運算式會讓函式執行，在這個案例中是 `Eval_Exception`。

請注意，使用[GetExceptionCode](/windows/desktop/Debug/getexceptioncode)判斷例外狀況。 您必須在 filter 本身內呼叫這個函式。 `Eval_Exception` 無法呼叫`GetExceptionCode`，但是它必須擁有例外狀況代碼傳遞給它。

除非例外狀況是整數或浮點溢位，否則這個處理常式會將控制項傳遞至另一個處理常式。 如果是，處理常式會呼叫函式 (`ResetVars` 只是範例，不是應用程式開發介面函式) 重設部分全域變數。 *陳述式區塊 2*，在此範例空的可以永遠不會執行，因為`Eval_Exception`永遠不會傳回 EXCEPTION_EXECUTE_HANDLER (1)。

使用函式呼叫是處理複雜的篩選條件運算式時理想的通用技術。 另外兩項實用的 C 語言功能為：

- 條件運算子

- 逗號運算子

條件運算子通常很有用，因為它可以用來檢查特定傳回碼，然後傳回兩個不同值的其中一個。 比方說，下列程式碼中的篩選條件的例外狀況是 STATUS_INTEGER_OVERFLOW 時，才會辨識例外狀況：

```cpp
__except( GetExceptionCode() == STATUS_INTEGER_OVERFLOW ? 1 : 0 ) {
```

這個案例中條件運算子的目的主要在於避免混淆，因為下列程式碼會產生相同的結果：

```cpp
__except( GetExceptionCode() == STATUS_INTEGER_OVERFLOW ) {
```

條件運算子是比較好用的情況下，您可以篩選在評估為-1，EXCEPTION_CONTINUE_EXECUTION。

逗號運算子可讓您在單一運算式內執行多項獨立的運算。 這個效果大致上與執行多個陳述式，然後傳回最後一個運算式的值相同。 例如，下列程式碼會將例外狀況代碼儲存在變數中，然後進行測試：

```cpp
__except( nCode = GetExceptionCode(), nCode == STATUS_INTEGER_OVERFLOW )
```

## <a name="see-also"></a>另請參閱

[撰寫例外狀況處理常式](../cpp/writing-an-exception-handler.md)<br/>
[結構化例外狀況處理 (C/C++)](../cpp/structured-exception-handling-c-cpp.md)