---
title: HOW TO：定義和使用列舉在C++/CLI
ms.date: 11/04/2016
helpviewer_keywords:
- enum class, specifying underlying types
ms.assetid: df8f2b91-b9d2-4fab-9be4-b1d58b8bc570
ms.openlocfilehash: 9787b7b96f83b2926c65209254c88eb56fe1a8ab
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62387379"
---
# <a name="how-to-define-and-consume-enums-in-ccli"></a>HOW TO：定義和使用列舉在C++/CLI

本主題討論中的列舉C++/CLI。

## <a name="specifying-the-underlying-type-of-an-enum"></a>指定列舉的基礎類型

根據預設，會列舉的基礎型別`int`。  不過，您可以在其中指定的類型是帶正負號或不帶正負號的形式`int`， `short`， `long`， `__int32`，或`__int64`。  您也可以使用`char`。

```
// mcppv2_enum_3.cpp
// compile with: /clr
public enum class day_char : char {sun, mon, tue, wed, thu, fri, sat};

int main() {
   // fully qualified names, enumerator not injected into scope
   day_char d = day_char::sun, e = day_char::mon;
   System::Console::WriteLine(d);
   char f = (char)d;
   System::Console::WriteLine(f);
   f = (char)e;
   System::Console::WriteLine(f);
   e = day_char::tue;
   f = (char)e;
   System::Console::WriteLine(f);
}
```

**輸出**

```Output
sun
0
1
2
```

## <a name="how-to-convert-between-managed-and-standard-enumerations"></a>如何將 managed 和標準列舉間轉換

列舉與整數類資料類型; 間沒有標準轉換需要轉型。

```
// mcppv2_enum_4.cpp
// compile with: /clr
enum class day {sun, mon, tue, wed, thu, fri, sat};
enum {sun, mon, tue, wed, thu, fri, sat} day2; // unnamed std enum

int main() {
   day a = day::sun;
   day2 = sun;
   if ((int)a == day2)
   // or...
   // if (a == (day)day2)
      System::Console::WriteLine("a and day2 are the same");
   else
      System::Console::WriteLine("a and day2 are not the same");
}
```

**輸出**

```Output
a and day2 are the same
```

## <a name="operators-and-enums"></a>運算子和列舉

下列運算子會在列舉中有效C++/CLI:

|運算子|
|--------------|
|== != \< > \<= >=|
|+ -|
|&#124; ^ & ~|
|++ --|
|sizeof|

運算子&#124;^ & ~ + +-具有基礎類型，不包括 bool 的整數資料只會針對列舉所定義。  這兩個運算元必須是列舉型別。

編譯器會執行任何靜態或動態檢查結果的列舉作業;作業可能會導致不在列舉的有效列舉值的範圍中的值。

> [!NOTE]
>  C++11 引進列舉類別類型在 unmanaged 程式碼也就是明顯不同於中的 managed 的列舉類別C++/CLI。 特別是，C + + 11 列舉類別類型不支援做為 managed 的列舉類別類型中相同的運算子C++/CLI，以及C++/CLI 的原始程式碼必須提供 managed 列舉中的存取範圍規範類別宣告以區別來自unmanaged (C + + 11) 列舉類別宣告。 如需有關列舉類別，在C++/CLI， C++/CX，以及 C + + 11，請參閱[列舉類別](../extensions/enum-class-cpp-component-extensions.md)。

```
// mcppv2_enum_5.cpp
// compile with: /clr
private enum class E { a, b } e, mask;
int main() {
   if ( e & mask )   // C2451 no E->bool conversion
      ;

   if ( ( e & mask ) != 0 )   // C3063 no operator!= (E, int)
      ;

   if ( ( e & mask ) != E() )   // OK
      ;
}
```

```
// mcppv2_enum_6.cpp
// compile with: /clr
private enum class day : int {sun, mon};
enum : bool {sun = true, mon = false} day2;

int main() {
   day a = day::sun, b = day::mon;
   day2 = sun;

   System::Console::WriteLine(sizeof(a));
   System::Console::WriteLine(sizeof(day2));
   a++;
   System::Console::WriteLine(a == b);
}
```

**輸出**

```Output
4
1
True
```

## <a name="see-also"></a>另請參閱

[enum 類別](../extensions/enum-class-cpp-component-extensions.md)
