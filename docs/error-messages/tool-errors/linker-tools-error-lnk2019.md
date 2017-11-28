---
title: "連結器工具錯誤 LNK2019 |Microsoft 文件"
ms.custom: 
ms.date: 05/17/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- cpp-tools
ms.tgt_pltfrm: 
ms.topic: error-reference
f1_keywords:
- LNK2019
dev_langs:
- C++
helpviewer_keywords:
- nochkclr.obj
- LNK2019
- _check_commonlanguageruntime_version
ms.assetid: 4392be92-195c-4eb2-bd4d-49cfac3ca291
caps.latest.revision: 39
author: corob-msft
ms.author: corob
manager: ghogen
ms.translationtype: MT
ms.sourcegitcommit: 35b46e23aeb5f4dbfd2a0dd44b906389dd5bfc88
ms.openlocfilehash: 4cb4413b8c0b53b407724dd16083027b89b91b37
ms.contentlocale: zh-tw
ms.lasthandoff: 10/09/2017

---
# <a name="linker-tools-error-lnk2019"></a>連結器工具錯誤 LNK2019
未解析外部符號 '*符號*'函式中參考'*函式*'  
  
編譯程式碼，*函式*讓您參考或呼叫*符號*，但該符號未定義的任何程式庫或物件給連結器指定的檔案。  
  
這則錯誤訊息後面接著嚴重錯誤[LNK1120](../../error-messages/tool-errors/linker-tools-error-lnk1120.md)。 您必須修正若要修正錯誤 LNK1120 所有 LNK2001 和 LNK2019 錯誤。  
  
## <a name="possible-causes"></a>可能的原因  
  
有許多方法，以取得此錯誤，但全部都涉及的函式或變數，連結器無法參考*解決*，或找不到的定義。 編譯器能夠識別時的符號不*宣告*，但不是在未*定義*，因為定義可能是不同原始程式檔或程式庫中。 如果符號為參考，但永遠不會定義，連結器會產生未解析外部符號錯誤。  
  
以下是一些造成 LNK2019 的常見問題：  
  
-   **未連結的目的檔或包含符號定義的文件庫。** 在 Visual Studio 中，請確認來源檔案包含定義會建立並連結為您專案的一部分。 在命令列中，確認編譯時包含定義原始程式檔，確定產生的物件檔案包含在要連結的檔案清單。  
  
-   **符號宣告與符號定義的拼字不同。** 請確認正確的拼字和大小寫用於宣告和定義，而使用或呼叫符號的任一處。  
  
-   **使用了函式，但是類型或參數數目與函式定義不相符。** 函式宣告必須與定義相符。 請確認函式呼叫與宣告相符，而且宣告與定義相符。 叫用樣板函式的程式碼也必須有相符的樣板函式宣告，包含相同的樣板參數做為定義。 如需範本宣告不相符的範例，請參閱範例 LNK2019e.cpp 範例 > 一節中。  
  
-   **已宣告函式或變數，但未定義。** 這通常表示宣告存在於標頭檔，但並未實作任何相符的定義。 若為成員函式或靜態資料成員，實作必須包含類別範圍選取器。 如需範例，請參閱 [Missing Function Body or Variable](../../error-messages/tool-errors/missing-function-body-or-variable.md)。  
  
-   **呼叫慣例在函式宣告和函式定義之間不同。** 呼叫慣例 ([__cdecl](../../cpp/cdecl.md)、 [__stdcall](../../cpp/stdcall.md)、 [__fastcall](../../cpp/fastcall.md)或 [__vectorcall](../../cpp/vectorcall.md)) 會編碼為裝飾名稱的一部分。 確認呼叫慣例相同。  
  
-   **C 檔案中定義了一個符號，但未在 C++ 檔案中使用 extern "C" 宣告。** 編譯為 C 的檔案中所定義的符號之裝飾名稱，不同於 C++ 檔案中所宣告的符號，除非您使用 [extern"C"](../../cpp/using-extern-to-specify-linkage.md) 修飾詞。 請確認宣告與每個符號的編譯連結相符。 同樣地，如果您在 C++ 檔案中定義將由 C 程式使用的符號，請在定義中使用 `extern "C"` 。  
  
-   **符號已定義為靜態，而且稍後由檔案外部參考。** 不同於 C，C++ 中 [全域常數](../../error-messages/tool-errors/global-constants-in-cpp.md) 有 `static` 連結。 若要解決這項限制，您可以在標頭檔中包含 `const` 初始設定，並將該標頭包含在 .cpp 檔案中，或者您可以將變數設為非常數，並使用常數參考來存取。  
  
-   **未定義類別的靜態成員。** 靜態類別成員必須具有唯一的定義，否則將違反單一定義規則。 無法以內嵌進行定義的靜態類別成員，必須使用其完整名稱在一個來源檔案中加以定義。 如果未完全定義，則連結器會產生 LNK2019。  
  
-   **建置相依性只定義為方案中的專案相依性。** 在舊版的 Visual Studio 中，此層級的相依性已經足夠。 不過，從 Visual Studio 2010 開始，Visual Studio 需要[專案對專案參考](/visualstudio/ide/managing-references-in-a-project)。 如果您的專案沒有專案對專案間的參考，您就有可能會收到這個連結器錯誤。 加入專案對專案間的參考來修正此問題。  
  
-   **您使用 Windows 應用程式設定來建置主控台應用程式**。 如果錯誤訊息類似於**WinMain 函式中所參考的未解析外部符號**`function_name`，使用連結**/subsystem: console**而不是**/subsystem: windows**. 如需此設定的詳細資訊，以及如何在 Visual Studio 中設定此屬性的指示，請參閱 [/SUBSYSTEM (Specify Subsystem)](../../build/reference/subsystem-specify-subsystem.md)。  
  
-   **您可以使用不同的編譯器選項，在不同的原始程式檔中用於函式內嵌。** 若使用在 .cpp 檔案中定義的內嵌函式，且又在不同的原始程式檔中混用函式內嵌編譯器選項，則可能會導致 LNK2019。 如需詳細資訊，請參閱 [Function Inlining Problems](../../error-messages/tool-errors/function-inlining-problems.md)。  
  
-   **您可在其範圍外部使用自動變數。** 自動 (函式範圍) 變數只能在該函式的範圍內使用。 不能將這些變數宣告為 `extern` ，也不能在其他原始程式檔中加以使用。 如需範例，請參閱 [Automatic (Function Scope) Variables](../../error-messages/tool-errors/automatic-function-scope-variables.md)。  
  
-   **您呼叫內建函式，或傳遞至內建函式的引數類型在您的目標架構上並不支援。** 例如，如果您使用 AVX2 內建，但未指定 [/ARCH:AVX2](../../build/reference/arch-x86.md) 編譯器選項，則編譯器會假設此內建為外部函式。 編譯器會產生具有相同名稱的外部符號呼叫做為內建，而非產生內嵌指令。 當連結器嘗試找出此遺漏函式的定義時，就會產生 LNK2019。 請確認您只使用內建和目標架構支援的型別。  
  
-   **混合程式碼會使用原生 wchar\_t 不的程式碼。** 根據預設，於 Visual C++ 2005 中完成的 C++ 語言一致性工作讓 `wchar_t` 成為原生類型。 您必須使用 [/Zc:wchar_t-](../../build/reference/zc-wchar-t-wchar-t-is-native-type.md) 編譯器選項，以產生與使用舊版 Visual C++ 所編譯程式庫檔及目的檔相容的程式碼。 如果不是所有檔案使用相同的已都編譯**/Zc:wchar\_t**類型參考可能不會解析成相容的類型的設定。 在編譯時，請更新所使用的類型，或使用一致的 `wchar_t` 設定，以確認所有程式庫檔或目的檔中的 **/Zc:wchar_t** 類型都相容。  
  
## <a name="diagnosis-tools"></a>診斷工具    
  
很難判斷為什麼連結器無法找到特定的符號定義。 問題通常出在於，並未包含的程式碼包含在您的組建定義，或建置選項建立了不同裝飾外部符號的名稱。 有些工具和選項可協助您診斷 LNK2019 錯誤。  
  
-   [/VERBOSE](../../build/reference/verbose-print-progress-messages.md) 連結器選項可協助您判斷連結器會參考哪些檔案。 這可以協助您確認包含符號定義的檔案是否已包含在您的建置中。  
  
-   DUMPBIN 公用程式的 [/EXPORTS](../../build/reference/dash-exports.md) 和 [/SYMBOLS](../../build/reference/symbols.md) 選項可協助您探索哪些符號定義在 .DLL 和物件或程式庫檔案中。 請確認匯出的裝飾名稱與連結器搜尋的裝飾名稱相符。  
  
-   UNDNAME 公用程式可以顯示裝飾名稱之對等的未裝飾外部符號。  
## <a name="examples"></a>範例  
  
以下是幾個會造成 LNK2019 錯誤的範例程式碼，以及如何修正此錯誤的相關資訊。  
  
### <a name="a-symbol-is-declared-but-not-defined"></a>符號已宣告但未定義  
  
在此範例中，外部變數已宣告但未定義：  
  
```cpp  
// LNK2019.cpp  
// Compile by using: cl /EHsc /W4 LNK2019.cpp  
// LNK2019 expected  
extern char B[100];   // B is not available to the linker  
int main() {  
   B[0] = ' ';   // LNK2019  
}  
```  
  
以下是另一個範例，其中宣告變數和函式為`extern`但不提供定義：  
  
```cpp  
// LNK2019c.cpp  
// Compile by using: cl /EHsc LNK2019c.cpp  
// LNK2019 expected  
extern int i;  
extern void g();  
void f() {  
   i++;  
   g();  
}  
int main() {}  
```  
  
除非`i`和`g`所定義的其中一個檔案包含在組建中，連結器會產生 LNK2019。 您可以包含原始碼檔案來修正此問題，其中包含此定義做為編譯的一部分。 或者，您可以傳遞的.obj 檔案或.lib 檔案，包含要連結器的定義。  
  
### <a name="a-static-data-member-is-declared-but-not-defined"></a>靜態資料成員已宣告但未定義  
  
LNK2019 也可能在靜態資料成員已宣告但未定義時發生。 下列範例會產生 LNK2019，並示範如何修正此問題。  
  
```cpp  
// LNK2019b.cpp  
// Compile by using: cl /EHsc LNK2019b.cpp  
// LNK2019 expected  
struct C {  
   static int s;  
};  
  
// Uncomment the following line to fix the error.  
// int C::s;  
  
int main() {  
   C c;  
   C::s = 1;  
}  
```  
  
### <a name="declaration-parameters-do-not-match-definition"></a>宣告參數與定義不相符  
  
叫用樣板函式的程式碼必須具有對應的樣板函式宣告。 宣告必須包含相同的樣板參數做為定義。 下列範例會在使用者定義的運算子上產生 LNK2019，並示範如何修正此問題。  
  
```cpp  
// LNK2019e.cpp  
// compile by using: cl /EHsc LNK2019e.cpp  
// LNK2019 expected  
#include <iostream>  
using namespace std;  
  
template<class T> class   
Test {  
   // The operator<< declaration does not match the definition below:  
   friend ostream& operator<<(ostream&, Test&);  
   // To fix, replace the line above with the following:  
   // template<typename T> friend ostream& operator<<(ostream&, Test<T>&);  
};  
  
template<typename T>  
ostream& operator<<(ostream& os, Test<T>& tt) {  
   return os;  
}  
  
int main() {  
   Test<int> t;  
   cout << "Test: " << t << endl;   // LNK2019 unresolved external  
}  
```  
  
### <a name="inconsistent-wchart-type-definitions"></a>不一致的 wchar_t 類型定義  
  
這個範例會建立 DLL，具有會使用匯出`WCHAR`，這會解析為`wchar_t`。  
  
```cpp  
// LNK2019g.cpp  
// compile with: cl /EHsc /LD LNK2019g.cpp  
#include "windows.h"  
// WCHAR resolves to wchar_t  
__declspec(dllexport) void func(WCHAR*) {}  
```  
  
下一個範例在前一個範例中，使用 DLL，並且會產生 LNK2019，因為類型不帶正負號 short * 和 WCHAR\*不相同。  
  
```cpp  
// LNK2019h.cpp  
// compile by using: cl /EHsc LNK2019h LNK2019g.lib  
// LNK2019 expected  
__declspec(dllimport) void func(unsigned short*);  
  
int main() {  
   func(0);  
}  
```  
  
 若要修正這個錯誤，變更`unsigned short`至`wchar_t`或`WCHAR`，或藉由編譯 LNK2019g.cpp **/Zc:wchar_t-**。  
  
## <a name="additional-resources"></a>其他資源  
  
如需 LNK2001 可能原因和解決方案的詳細資訊，請參閱 Stack Overflow 的問題[什麼是未定義參考/未解析外部符號錯誤及如何修正問題？](http://stackoverflow.com/q/12573816/2002113)。  

