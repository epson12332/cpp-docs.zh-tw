---
title: /H (限制外部名稱的長度)
ms.date: 09/05/2018
f1_keywords:
- /h
helpviewer_keywords:
- public name length
- /H compiler option [C++]
- H compiler option [C++]
- external names
- -H compiler option [C++]
ms.assetid: de701dd3-ed04-4c88-8195-960d2520ec2e
ms.openlocfilehash: bdd3da8d3a5165262c00bc3475122e31f5770726
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62270387"
---
# <a name="h-restrict-length-of-external-names"></a>/H (限制外部名稱的長度)

已取代。 限制外部名稱的長度。

## <a name="syntax"></a>語法

> **/H**<em>number</em>

## <a name="arguments"></a>引數

*number*<br/>
指定在程式中所允許的外部名稱的最大長度。

## <a name="remarks"></a>備註

根據預設，外部 （公用） 名稱的長度為 2047 個字元。 這適用於 C 和C++程式。 使用 **/H**只能減少識別項的允許長度上限，不能增加它。 之間的空格 **/H**並*數目*是選擇性的。

如果程式包含的外部名稱的長度超過*數字*，額外的字元會被忽略。 如果您編譯的程式，而不需要 **/H** ，而且如果識別項包含超過 2047 個字元，編譯器會產生[嚴重錯誤 C1064](../../error-messages/compiler-errors-1/fatal-error-c1064.md)。

長度的限制包括任何編譯器建立的前置底線 (**\_**) 或 at 符號 (**\@**)。 這些字元是識別項的一部分，且需要大量的位置。

- 編譯器會新增前置底線 (**\_**) 來修改名稱`__cdecl`（預設值） 和`__stdcall`呼叫慣例和前置字元 @ 記號 (**\@**) 來修改名稱`__fastcall`呼叫慣例。

- 編譯器會將引數大小資訊附加至名稱修改`__fastcall`並`__stdcall`呼叫慣例，並將型別資訊C++名稱。

您可能會發現 **/H**很有用：

- 當您建立混合語言或可攜式的程式。

- 當您使用外部識別項的長度限制的工具。

- 當您想要限制的符號偵錯組建中所使用的空間量。

下列範例示範如何使用 **/H**實際引發錯誤，如果識別項長度太多限制：

```cpp
// compiler_option_H.cpp
// compile with: /H5
// processor: x86
// LNK2005 expected
void func1(void);
void func2(void);

int main() { func1(); }

void func1(void) {}
void func2(void) {}
```

您也必須使用時請小心 **/H**預先定義的編譯器識別項的選項。 如果最大的識別項長度太小，某些預先定義的識別碼會無法解析，以及特定的程式庫函式呼叫。 比方說，如果`printf`會使用函式和選項 **/H5**指定在編譯時期，符號 **_prin**將會建立以參考`printf`，，這將會找不到在 程式庫。

利用 **/H**與不相容[/GL （整個程式最佳化）](gl-whole-program-optimization.md)。

**/H** Visual Studio 2005 起已被取代選項; 最大長度限制已經增加並 **/H**不再需要。 如需已被取代的編譯器選項的清單，請參閱 <<c0>  **已取代及移除的編譯器選項**中[依分類排列的編譯器選項](compiler-options-listed-by-category.md)。

### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>在 Visual Studio 開發環境中設定這個編譯器選項

1. 開啟專案的 [屬性頁]  對話方塊。 如需詳細資訊，請參閱 <<c0> [ 設定C++Visual Studio 中的編譯器和組建屬性](../working-with-project-properties.md)。</c0>

1. 選取 **組態屬性** > **C /C++** > **命令列**屬性頁。

1. 輸入中的編譯器選項**其他選項** 方塊中。

### <a name="to-set-this-compiler-option-programmatically"></a>若要以程式方式設定這個編譯器選項

- 請參閱 <xref:Microsoft.VisualStudio.VCProjectEngine.VCCLCompilerTool.AdditionalOptions%2A>。

## <a name="see-also"></a>另請參閱

[MSVC 編譯器選項](compiler-options.md)<br/>
[MSVC 編譯器命令列語法](compiler-command-line-syntax.md)
