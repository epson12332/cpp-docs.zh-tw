---
title: add_volatile 類別
ms.date: 11/04/2016
f1_keywords:
- type_traits/std::add_volatile
helpviewer_keywords:
- add_volatile class
- add_volatile
ms.assetid: cde57277-d764-402d-841e-97611ebaab14
ms.openlocfilehash: ff48b1848e2d7631d789621a5ef845d04d8e8821
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62411132"
---
# <a name="addvolatile-class"></a>add_volatile 類別

可讓**volatile**類型從指定的型別。

## <a name="syntax"></a>語法

```cpp
template <class Ty>
struct add_volatile;

template <class T>
using add_volatile_t = typename add_volatile<T>::type;
```

### <a name="parameters"></a>參數

*T*<br/>
要修改的類型。

## <a name="remarks"></a>備註

執行個體`add_volatile<T>`有一個成員**typedef** `type`也就是說*T*如果*T*為參考、 函式或 volatile 限定類型，否則為**volatile** *T*。別名`add_volatile_t`是存取成員的捷徑**typedef** `type`。

## <a name="example"></a>範例

```cpp
#include <type_traits>
#include <iostream>

int main()
{
    std::add_volatile_t<int> *p = (volatile int *)0;

    p = p;  // to quiet "unused" warning
    std::cout << "add_volatile<int> == "
        << typeid(*p).name() << std::endl;

    return (0);
}
```

```Output
add_volatile<int> == int
```

## <a name="requirements"></a>需求

**標頭：**\<type_traits>

**命名空間：** std

## <a name="see-also"></a>另請參閱

[<type_traits>](../standard-library/type-traits.md)<br/>
[remove_volatile 類別](../standard-library/remove-volatile-class.md)<br/>
