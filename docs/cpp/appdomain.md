---
title: appdomain
ms.date: 11/04/2016
f1_keywords:
- appdomain_cpp
helpviewer_keywords:
- appdomain __declspec keyword
- __declspec keyword [C++], appdomain
ms.assetid: 29d843cb-cb6b-4d1b-a48d-d928a877234d
ms.openlocfilehash: 3f83841565eb6a097f306129fe8f6d121f837c27
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62184487"
---
# <a name="appdomain"></a>appdomain

指定 Managed 應用程式的每個應用程式定義域都應該有自己的特定全域變數或靜態成員變數複本。 請參閱[應用程式定義域和視覺效果C++](../dotnet/application-domains-and-visual-cpp.md)如需詳細資訊。

每個應用程式定義域都有自己的 per-appdomain 變數複本。 組件載入應用程式定義域時，appdomain 變數的建構函式就會執行，而應用程式定義域卸載時，解構函式就會執行。

如果您希望 Common Language Runtime 中某個處理序內的所有應用程式定義域共用全域變數，請使用 `__declspec(process)` 修飾詞。 `__declspec(process)` 作用中的下的預設值是[/clr](../build/reference/clr-common-language-runtime-compilation.md)。 **/Clr: pure**並 **/clr: safe**編譯器選項是在 Visual Studio 2015 中已被取代，而且不支援的 Visual Studio 2017 中。

`__declspec(appdomain)` 只適用於當其中一個 **/clr**編譯器選項使用。 只有全域變數、靜態成員變數或靜態區域變數可以擁有 `__declspec(appdomain)` 標記。 將 `__declspec(appdomain)` 套用至 Managed 類型的靜態成員會發生錯誤，因為這些成員會固定出現這類行為。

使用`__declspec(appdomain)`類似於使用[執行緒區域儲存區 (TLS)](../parallel/thread-local-storage-tls.md)。 執行緒擁有自己的儲存區，應用程式定義域也一樣。 使用 `__declspec(appdomain)` 可確保全域變數在針對這個應用程式建立的每個應用程式定義域中擁有自己的儲存區。

若要混合使用處理序專屬和 appdomain 專屬變數; 的限制請參閱[程序](../cpp/process.md)如需詳細資訊。

例如，在程式啟動時，會先初始化所有處理序專屬變數，然後才會初始化所有 per-appdomain 變數。 因此，當處理序專屬變數初始化時，它就無法依據任何應用程式定義域專屬變數的值。 不建議您混合使用 (指派) appdomain 專屬和處理序專屬變數。

如需如何在特定應用程式定義域中呼叫的函式的資訊，請參閱[call_in_appdomain 函式](../dotnet/call-in-appdomain-function.md)。

## <a name="example"></a>範例

```cpp
// declspec_appdomain.cpp
// compile with: /clr
#include <stdio.h>
using namespace System;

class CGlobal {
public:
   CGlobal(bool bProcess) {
      Counter = 10;
      m_bProcess = bProcess;
      Console::WriteLine("__declspec({0}) CGlobal::CGlobal constructor", m_bProcess ? (String^)"process" : (String^)"appdomain");
   }

   ~CGlobal() {
      Console::WriteLine("__declspec({0}) CGlobal::~CGlobal destructor", m_bProcess ? (String^)"process" : (String^)"appdomain");
   }

   int Counter;

private:
   bool m_bProcess;
};

__declspec(process) CGlobal process_global = CGlobal(true);
__declspec(appdomain) CGlobal appdomain_global = CGlobal(false);

value class Functions {
public:
   static void change() {
      ++appdomain_global.Counter;
   }

   static void display() {
      Console::WriteLine("process_global value in appdomain '{0}': {1}",
         AppDomain::CurrentDomain->FriendlyName,
         process_global.Counter);

      Console::WriteLine("appdomain_global value in appdomain '{0}': {1}",
         AppDomain::CurrentDomain->FriendlyName,
         appdomain_global.Counter);
   }
};

int main() {
   AppDomain^ defaultDomain = AppDomain::CurrentDomain;
   AppDomain^ domain = AppDomain::CreateDomain("Domain 1");
   AppDomain^ domain2 = AppDomain::CreateDomain("Domain 2");
   CrossAppDomainDelegate^ changeDelegate = gcnew CrossAppDomainDelegate(&Functions::change);
   CrossAppDomainDelegate^ displayDelegate = gcnew CrossAppDomainDelegate(&Functions::display);

   // Print the initial values of appdomain_global in all appdomains.
   Console::WriteLine("Initial value");
   defaultDomain->DoCallBack(displayDelegate);
   domain->DoCallBack(displayDelegate);
   domain2->DoCallBack(displayDelegate);

   // Changing the value of appdomain_global in the domain and domain2
   // appdomain_global value in "default" appdomain remain unchanged
   process_global.Counter = 20;
   domain->DoCallBack(changeDelegate);
   domain2->DoCallBack(changeDelegate);
   domain2->DoCallBack(changeDelegate);

   // Print values again
   Console::WriteLine("Changed value");
   defaultDomain->DoCallBack(displayDelegate);
   domain->DoCallBack(displayDelegate);
   domain2->DoCallBack(displayDelegate);

   AppDomain::Unload(domain);
   AppDomain::Unload(domain2);
}
```

```Output
__declspec(process) CGlobal::CGlobal constructor
__declspec(appdomain) CGlobal::CGlobal constructor
Initial value
process_global value in appdomain 'declspec_appdomain.exe': 10
appdomain_global value in appdomain 'declspec_appdomain.exe': 10
__declspec(appdomain) CGlobal::CGlobal constructor
process_global value in appdomain 'Domain 1': 10
appdomain_global value in appdomain 'Domain 1': 10
__declspec(appdomain) CGlobal::CGlobal constructor
process_global value in appdomain 'Domain 2': 10
appdomain_global value in appdomain 'Domain 2': 10
Changed value
process_global value in appdomain 'declspec_appdomain.exe': 20
appdomain_global value in appdomain 'declspec_appdomain.exe': 10
process_global value in appdomain 'Domain 1': 20
appdomain_global value in appdomain 'Domain 1': 11
process_global value in appdomain 'Domain 2': 20
appdomain_global value in appdomain 'Domain 2': 12
__declspec(appdomain) CGlobal::~CGlobal destructor
__declspec(appdomain) CGlobal::~CGlobal destructor
__declspec(appdomain) CGlobal::~CGlobal destructor
__declspec(process) CGlobal::~CGlobal destructor
```

## <a name="see-also"></a>另請參閱

[__declspec](../cpp/declspec.md)<br/>
[關鍵字](../cpp/keywords-cpp.md)