---
title: /openmp （啟用 OpenMP 支援）
ms.date: 04/15/2019
f1_keywords:
- /openmp
- VC.Project.VCCLCompilerTool.OpenMP
helpviewer_keywords:
- /openmp compiler option [C++]
- -openmp compiler option [C++]
ms.assetid: 9082b175-18d3-4378-86a7-c0eb95664e13
ms.openlocfilehash: caa06d89c590abd2b3a74a5a6b118d6ba4acd910
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62320210"
---
# <a name="openmp-enable-openmp-support"></a>/openmp （啟用 OpenMP 支援）

可讓編譯器處理[ `#pragma omp` ](../../preprocessor/omp.md)支援 OpenMP 指示詞。

## <a name="syntax"></a>語法

::: moniker range=">= vs-2019"

> **/openmp**\[**:**__experimental__]

::: moniker-end

::: moniker range="<= vs-2017"

> **/openmp**

::: moniker-end

## <a name="remarks"></a>備註

`#pragma omp` 用來指定[指示詞](../../parallel/openmp/reference/openmp-directives.md)並[子句](../../parallel/openmp/reference/openmp-clauses.md)。 如果 **/openmp**未在編譯中，編譯器會忽略 OpenMP 子句和指示詞指定。 [OpenMP 函式](../../parallel/openmp/reference/openmp-functions.md)呼叫會處理編譯器即使 **/openmp**未指定。

::: moniker range=">= vs-2019"

C++編譯器目前支援 OpenMP 2.0 標準。 不過，Visual Studio 2019 現在也提供 SIMD 功能。 若要使用 SIMD，使用編譯 **/openmp： 實驗性**選項。 此選項可讓這兩個一般 OpenMP 功能，以及其他 OpenMP SIMD 功能無法使用時 **/openmp**切換。

::: moniker-end

藉由使用這兩個編譯的應用程式 **/openmp**並 **/clr**只能在單一應用程式網域的程序中執行。 不支援多個應用程式定義域。 也就是，當模組建構函式 (`.cctor`) 會執行，它會偵測處理程序會使用來編譯 **/openmp**，如果應用程式載入非預設的執行階段。 如需詳細資訊，請參閱 < [appdomain](../../cpp/appdomain.md)， [/clr （Common Language Runtime 編譯）](clr-common-language-runtime-compilation.md)，並[初始化混合組件](../../dotnet/initialization-of-mixed-assemblies.md)。

如果您嘗試將編譯使用這兩個應用程式 **/openmp**並 **/clr**非預設應用程式定義域，<xref:System.TypeInitializationException>偵錯工具，之外擲回例外狀況和`OpenMPWithMultipleAppdomainsException`例外狀況在 偵錯工具會擲回。

在下列情況下，可能也會引發這些例外狀況：

- 如果您的應用程式會使用編譯 **/clr**而非 **/openmp**，且已載入的非預設應用程式定義域，其中的程序包括使用編譯的應用程式 **/openmp**.

- 如果您傳遞您 **/clr**應用程式至公用程式，例如[regasm.exe](/dotnet/framework/tools/regasm-exe-assembly-registration-tool)，其目標組件載入至非預設應用程式定義域。

Common language runtime 的程式碼存取安全性並不適用於 OpenMP 區域。 如果您套用的 CLR 程式碼存取安全性 」 屬性，在平行區域之外，它不會處於作用中平行區域。

Microsoft 不建議您撰寫 **/openmp**應用程式，讓部分信任的呼叫端。 請勿使用<xref:System.Security.AllowPartiallyTrustedCallersAttribute>，或任何 CLR 程式碼存取安全性屬性。

### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>在 Visual Studio 開發環境中設定這個編譯器選項

1. 開啟專案的 [屬性頁]  對話方塊。 如需詳細資訊，請參閱 <<c0> [ 設定C++Visual Studio 中的編譯器和組建屬性](../working-with-project-properties.md)。</c0>

1. 依序展開**組態屬性** > **C /C++** > **語言**屬性頁。

1. 修改**OpenMP 支援**屬性。

### <a name="to-set-this-compiler-option-programmatically"></a>若要以程式方式設定這個編譯器選項

- 請參閱 <xref:Microsoft.VisualStudio.VCProjectEngine.VCCLCompilerTool.OpenMP%2A>。

## <a name="example"></a>範例

下列範例會示範一些與它在啟動之後，使用執行緒集區的執行緒集區啟動的影響。 假設 x64，單一核心，雙處理器，執行緒集區需要大約 16 毫秒啟動。 在那之後，那里是小小額外成本的執行緒集區。

當您編譯使用 **/openmp**，第二個呼叫 test2 絕對不會執行任何時間超過您使用編譯如果 **/openmp-**，因為沒有任何執行緒集區啟動。 百萬個反覆項目，在 **/openmp**版本的速度比 **/openmp-** test2 的第二個呼叫的版本。 在 25 的反覆項目，同時 **/openmp-** 並 **/openmp**版本註冊小於時鐘資料粒度。

如果應用程式中有一個迴圈，而且它會在低於 15 毫秒 （調整您的電腦上的額外負荷），執行 **/openmp**可能不適當。 如果是更高版本，您可能要考慮使用 **/openmp**。

```cpp
// cpp_compiler_options_openmp.cpp
#include <omp.h>
#include <stdio.h>
#include <stdlib.h>
#include <windows.h>

volatile DWORD dwStart;
volatile int global = 0;

double test2(int num_steps) {
   int i;
   global++;
   double x, pi, sum = 0.0, step;

   step = 1.0 / (double) num_steps;

   #pragma omp parallel for reduction(+:sum) private(x)
   for (i = 1; i <= num_steps; i++) {
      x = (i - 0.5) * step;
      sum = sum + 4.0 / (1.0 + x*x);
   }

   pi = step * sum;
   return pi;
}

int main(int argc, char* argv[]) {
   double   d;
   int n = 1000000;

   if (argc > 1)
      n = atoi(argv[1]);

   dwStart = GetTickCount();
   d = test2(n);
   printf_s("For %d steps, pi = %.15f, %d milliseconds\n", n, d, GetTickCount() - dwStart);

   dwStart = GetTickCount();
   d = test2(n);
   printf_s("For %d steps, pi = %.15f, %d milliseconds\n", n, d, GetTickCount() - dwStart);
}
```

## <a name="see-also"></a>另請參閱

[MSVC 編譯器選項](compiler-options.md) \
[MSVC 編譯器的命令列語法](compiler-command-line-syntax.md) \
[在 MSVC 中的 OpenMP](../../parallel/openmp/openmp-in-visual-cpp.md)
