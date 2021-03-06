---
title: bad_cast 例外狀況
ms.date: 11/04/2016
f1_keywords:
- bad_cast
- bad_cast_cpp
helpviewer_keywords:
- exceptions [C++], bad_cast
- bad_cast keyword [C++]
ms.assetid: 31eae1e7-d8d5-40a0-9fef-64a6a4fc9021
ms.openlocfilehash: 028fa8cc90b33aca6a37fb3b7f58b8c5fad81bd7
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62284769"
---
# <a name="badcast-exception"></a>bad_cast 例外狀況

**Bad_cast**所擲回例外狀況**dynamic_cast**的失敗是參考型別轉型運算子。

## <a name="syntax"></a>語法

```
catch (bad_cast)
   statement
```

## <a name="remarks"></a>備註

介面**bad_cast**是：

```cpp
class bad_cast : public exception {
public:
   bad_cast(const char * _Message = "bad cast");
   bad_cast(const bad_cast &);
   virtual ~bad_cast();
};
```

下列程式碼包含範例的失敗**dynamic_cast** ，則會擲回**bad_cast**例外狀況。

```cpp
// expre_bad_cast_Exception.cpp
// compile with: /EHsc /GR
#include <typeinfo.h>
#include <iostream>

class Shape {
public:
   virtual void virtualfunc() const {}
};

class Circle: public Shape {
public:
   virtual void virtualfunc() const {}
};

using namespace std;
int main() {
   Shape shape_instance;
   Shape& ref_shape = shape_instance;
   try {
      Circle& ref_circle = dynamic_cast<Circle&>(ref_shape);
   }
   catch (bad_cast b) {
      cout << "Caught: " << b.what();
   }
}
```

擲回例外狀況是因為所轉型的物件 (圖形) 不是衍生自指定的轉換類型 (圓形)。 若要避免例外狀況，請將這些宣告加入至 `main`：

```cpp
Circle circle_instance;
Circle& ref_circle = circle_instance;
```

再反向轉換中的意義**嘗試**封鎖，如下所示：

```cpp
Shape& ref_shape = dynamic_cast<Shape&>(ref_circle);
```

## <a name="see-also"></a>另請參閱

[dynamic_cast 運算子](../cpp/dynamic-cast-operator.md)<br/>
[關鍵字](../cpp/keywords-cpp.md)<br/>
[C++ 例外狀況處理](../cpp/cpp-exception-handling.md)