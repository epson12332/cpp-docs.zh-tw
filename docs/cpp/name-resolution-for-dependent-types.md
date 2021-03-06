---
title: 相依類型的名稱解析
ms.date: 11/04/2016
ms.assetid: 34066bb4-0c79-4fd8-bda7-539a60a277ab
ms.openlocfilehash: 798cc7067967e8992c32d7c0ced9f647e4877110
ms.sourcegitcommit: da32511dd5baebe27451c0458a95f345144bd439
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/07/2019
ms.locfileid: "65222411"
---
# <a name="name-resolution-for-dependent-types"></a>相依類型的名稱解析

使用**typename**在告訴編譯器將指定的限定的名稱識別類型的樣板定義中的限定名稱。 如需詳細資訊，請參閱 < [typename](../cpp/typename.md)。

```cpp
// template_name_resolution1.cpp
#include <stdio.h>
template <class T> class X
{
public:
   void f(typename T::myType* mt) {}
};

class Yarg
{
public:
   struct myType { };
};

int main()
{
   X<Yarg> x;
   x.f(new Yarg::myType());
   printf("Name resolved by using typename keyword.");
}
```

```Output
Name resolved by using typename keyword.
```

相依名稱的名稱查閱會檢查從樣板定義內容的名稱，這個內容會在下列範例中，尋找`myFunction(char)`— 和範本具現化的內容。在下列範例中，樣板具現化在 main;因此，`MyNamespace::myFunction`是可見的具現化的點，並且可挑選為較佳的相符項目。 如果 `MyNamespace::myFunction` 已重新命名，則會改為呼叫 `myFunction(char)`。

所有名稱都會做為相依名稱解析。 儘管如此，如果可能發生任何衝突，仍建議您使用完整限定名稱。

```cpp
// template_name_resolution2.cpp
// compile with: /EHsc
#include <iostream>
using namespace std;

void myFunction(char)
{
   cout << "Char myFunction" << endl;
}

template <class T> class Class1
{
public:
   Class1(T i)
   {
      // If replaced with myFunction(1), myFunction(char)
      // will be called
      myFunction(i);
}
};

namespace MyNamespace
{
   void myFunction(int)
   {
      cout << "Int MyNamespace::myFunction" << endl;
   }
};

using namespace MyNamespace;

int main()
{
   Class1<int>* c1 = new Class1<int>(100);
}
```

### <a name="output"></a>Output

```Output
Int MyNamespace::myFunction
```

### <a name="template-disambiguation"></a>樣板去除混淆

Visual Studio 2012 會強制執行 C + + 98/03/11 標準規則，以便使用 「 範本 」 關鍵字的去除混淆。 在下列範例中，Visual Studio 2010 會接受不合格的行和相符的程式碼行。  Visual Studio 2012 接受只有相符的程式碼行。

```cpp
#include <iostream>
#include <ostream>
#include <typeinfo>
using namespace std;

template <typename T> struct Allocator {
    template <typename U> struct Rebind {
        typedef Allocator<U> Other;
    };
};

template <typename X, typename AY> struct Container {
    #if defined(NONCONFORMANT)
        typedef typename AY::Rebind<X>::Other AX; // nonconformant
    #elif defined(CONFORMANT)
        typedef typename AY::template Rebind<X>::Other AX; // conformant
    #else
        #error Define NONCONFORMANT or CONFORMANT.
    #endif
};

int main() {
    cout << typeid(Container<int, Allocator<float>>::AX).name() << endl;
}
```

遵循去除混淆規則是必要條件，因為根據預設，C++ 會假設 `AY::Rebind` 不是樣板，因此編譯器會將下列 "`<`" 解譯為小於。 編譯器必須知道 `Rebind` 是樣板，才能將 "`<`" 正確剖析為角括號。

## <a name="see-also"></a>另請參閱

[名稱解析](../cpp/templates-and-name-resolution.md)