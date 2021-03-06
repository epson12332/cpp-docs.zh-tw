---
title: 編譯器錯誤 C2666
ms.date: 11/04/2016
f1_keywords:
- C2666
helpviewer_keywords:
- C2666
ms.assetid: 78364d15-c6eb-439a-9088-e04a0176692b
ms.openlocfilehash: 4a1d46f3b000b5054564b05ca2c3c94a9e7b6398
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62386872"
---
# <a name="compiler-error-c2666"></a>編譯器錯誤 C2666

'identifier': 數字的多載具有類似的轉換

多載函式或運算子模稜兩可。   型式參數清單可能會太類似編譯器無法解析模稜兩可。  若要解決這個錯誤，明確轉換一或多個實際的參數。

下列範例會產生 C2666:

```
// C2666.cpp
struct complex {
   complex(double);
};

void h(int,complex);
void h(double, double);

int main() {
   h(3,4);   // C2666
}
```

這項錯誤也會導致針對 Visual Studio.NET 2003年所進行的編譯器一致性工作：

- 二元運算子，以及使用者定義的指標類型轉換

- 限定性條件轉換不是身分識別轉換相同

以二元運算子\<，>， \<= 和 > =、 傳遞參數現在會隱含地轉換成運算元的類型如果參數的型別定義使用者定義轉換運算子，將轉換成運算元的類型。 目前沒有模稜兩可的可能性。

在 Visual Studio.NET 2003年和 Visual Studio.NET 版本，視覺效果中有效的程式碼的C++，呼叫類別運算子，明確地使用函式語法。

## <a name="example"></a>範例

```
// C2666b.cpp
#include <string.h>
#include <stdio.h>

struct T
{
    T( const T& copy )
    {
        m_str = copy.m_str;
    }

    T( const char* str )
    {
        int iSize = (strlen( str )+ 1);
        m_str = new char[ iSize ];
        if (m_str)
            strcpy_s( m_str, iSize, str );
    }

    bool operator<( const T& RHS )
    {
        return m_str < RHS.m_str;
    }

    operator char*() const
    {
        return m_str;
    }

    char* m_str;
};

int main()
{
    T str1( "ABCD" );
    const char* str2 = "DEFG";

    // Error - Ambiguous call to operator<()
    // Trying to convert str1 to char* and then call
    // operator<( const char*, const char* )?
    //  OR
    // trying to convert str2 to T and then call
    // T::operator<( const T& )?

    if( str1 < str2 )   // C2666

    if ( str1.operator < ( str2 ) )   // Treat str2 as type T
        printf_s("str1.operator < ( str2 )\n");

    if ( str1.operator char*() < str2 )   // Treat str1 as type char*
        printf_s("str1.operator char*() < str2\n");
}
```

## <a name="example"></a>範例

下列範例會產生 C2666

```
// C2666c.cpp
// compile with: /c

enum E
{
    E_A,   E_B
};

class A
{
    int h(const E e) const {return 0; }
    int h(const int i) { return 1; }
    // Uncomment the following line to resolve.
    // int h(const E e) { return 0; }

    void Test()
    {
        h(E_A);   // C2666
        h((const int) E_A);
        h((int) E_A);
    }
};
```