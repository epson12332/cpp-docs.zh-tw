---
title: __func__
ms.date: 10/19/2017
f1_keywords:
- __func__
ms.assetid: a5299b8d-f0ee-4af2-91dd-8fb165e68798
ms.openlocfilehash: eecd3efea6239c92a8bc81c0ed13a9563e5b87d2
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62154291"
---
# <a name="func"></a>__func__

**(C + + 11)** 預先定義的識別碼&#95; &#95;f&#95; &#95;已隱含定義為包含封入函式的非限定和未裝飾名稱的字串。 &#95;&#95;func&#95; &#95;託管的C++標準並不是 Microsoft 擴充功能。

## <a name="syntax"></a>語法

```cpp
__func__
```

## <a name="return-value"></a>傳回值

傳回以 null 結束 const char 陣列的字元，包含函式名稱。

## <a name="example"></a>範例

```cpp
#include <string>
#include <iostream>

namespace Test
{
    struct Foo
    {
        static void DoSomething(int i, std::string s)
        {
           std::cout << __func__ << std::endl; // Output: DoSomething
        }
    };
}

int main()
{
    Test::Foo::DoSomething(42, "Hello");

    return 0;
}
```

## <a name="requirements"></a>需求

C++11