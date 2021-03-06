---
title: for each, in
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- cliext::foreach
- for
- each
- in
helpviewer_keywords:
- for each keyword [C++]
ms.assetid: 0c3a364b-2747-43f3-bb8d-b7d3b7023f79
ms.openlocfilehash: b1dfe3a32f88c0e9456e3d73c31c533911f8d3ac
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62404451"
---
# <a name="for-each-in"></a>for each, in

逐一查看陣列或集合。 此非標準關鍵字在 C++/CLI 和原生 C++ 專案中皆可用。 但是，不建議使用。 請考慮使用標準[範圍架構 for 陳述式 (C++)](../cpp/range-based-for-statement-cpp.md)改為。

## <a name="all-runtimes"></a>所有執行階段

### <a name="syntax"></a>語法

> **每個 (** *型別**識別碼***中***運算式* **) {**<br/>
> &nbsp;&nbsp;&nbsp;&nbsp;*陳述式*<br/>
> **}**

### <a name="parameters"></a>參數

*type*<br/>
`identifier` 的類型。

*identifier*<br/>
表示集合項目的反覆項目變數。  當`identifier`已[追蹤參考運算子](../extensions/tracking-reference-operator-cpp-component-extensions.md)，您可以修改項目。

*expression*<br/>
陣列運算式或集合。 集合項目必須如此，編譯器才能將其轉換為 `identifier` 類型。

*statements*<br/>
要執行的一個或多個陳述式。

### <a name="remarks"></a>備註

`for each` 陳述式可用來逐一查看集合。 您可以修改集合中的項目，不過，您無法加入或刪除項目。

*陳述式*會針對陣列或集合中的每個項目執行。 在完成集合中所有項目的反覆項目之後，程式控制權會轉移到 `for each` 區塊之後的下一個陳述式。

`for each` 並`in`都[內容相關性關鍵字](../extensions/context-sensitive-keywords-cpp-component-extensions.md)。

如需詳細資訊：

- [使用 for each 反覆查看 C++ 標準程式庫集合](../dotnet/iterating-over-stl-collection-by-using-for-each.md)

- [如何：每個逐一查看陣列](../dotnet/how-to-iterate-over-arrays-with-for-each.md)

- [如何：每個反覆查看泛型集合與](../dotnet/how-to-iterate-over-a-generic-collection-with-for-each.md)

- [如何：每個反覆查看使用者定義的集合，與](../dotnet/how-to-iterate-over-a-user-defined-collection-with-for-each.md)

## <a name="windows-runtime"></a>Windows 執行階段

### <a name="requirements"></a>需求

編譯器選項： **/ZW**

### <a name="example"></a>範例

本範例示範如何使用 `for each` 逐一查看字串。

```cpp
// for_each_string1.cpp
// compile with: /ZW
#include <stdio.h>
using namespace Platform;

ref struct MyClass {
   property String^ MyStringProperty;
};

int main() {
   String^ MyString = ref new String("abcd");

   for each ( char c in MyString )
      wprintf("%c", c);

   wprintf("/n");

   MyClass^ x = ref new MyClass();
   x->MyStringProperty = "Testing";

   for each( char c in x->MyStringProperty )
      wprintf("%c", c);
}
```

**輸出**

```Output
abcd

Testing
```

## <a name="common-language-runtime"></a>Common Language Runtime

**備註**

CLR 語法是相同**所有執行階段**語法中，除非，如下所示。

*expression*<br/>
Managed 陣列運算式或集合。 集合項目必須如此，編譯器可以將它從轉換<xref:System.Object>要*識別碼*型別。

*運算式*評估為類型可實作<xref:System.Collections.IEnumerable>， <xref:System.Collections.Generic.IEnumerable%601>，或定義的類型`GetEnumerator`方法會傳回型別實作<xref:System.Collections.IEnumerator>宣告所有中所定義的方法或`IEnumerator`.

### <a name="requirements"></a>需求

編譯器選項： **/clr**

### <a name="example"></a>範例

本範例示範如何使用 `for each` 逐一查看字串。

```cpp
// for_each_string2.cpp
// compile with: /clr
using namespace System;

ref struct MyClass {
   property String ^ MyStringProperty;
};

int main() {
   String ^ MyString = gcnew String("abcd");

   for each ( Char c in MyString )
      Console::Write(c);

   Console::WriteLine();

   MyClass ^ x = gcnew MyClass();
   x->MyStringProperty = "Testing";

   for each( Char c in x->MyStringProperty )
      Console::Write(c);
}
```

**輸出**

```Output
abcd

Testing
```

## <a name="see-also"></a>另請參閱

[執行階段平台的元件延伸模組](../extensions/component-extensions-for-runtime-platforms.md)
