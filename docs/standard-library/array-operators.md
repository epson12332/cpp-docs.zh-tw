---
title: "&lt;array&gt; 運算子 | Microsoft Docs"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- array/std::array::operator!=
- array/std::array::operator<
- array/std::array::operator<=
- array/std::array::operator>
- array/std::array::operator>=
- array/std::array::operator==
dev_langs:
- C++
ms.assetid: c8f46282-f179-4909-9a01-639cb8e18c27
caps.latest.revision: 12
manager: ghogen
ms.translationtype: MT
ms.sourcegitcommit: 65f4e356ad0d46333b0d443d0fd6ac0b9f2b6f58
ms.openlocfilehash: e4854303bc80603ccbdf908aefc31f304487fb1a
ms.contentlocale: zh-tw
ms.lasthandoff: 10/03/2017

---
# <a name="ltarraygt-operators"></a>&lt;array&gt; 運算子
\<array> 標頭包含這些 `array` 非成員比較範本函式。  
  
||||  
|-|-|-|  
|[operator!=](#op_neq)|[operator&gt;](#op_gt)|[operator&gt;=](#op_gt_eq)|  
|[operator&lt;](#op_lt)|[operator&lt;=](#op_lt_eq)|[operator==](#op_eq_eq)|  
  
##  <a name="op_neq"></a> operator!=  
 陣列比較，不相等。  
  
```  
template <Ty, std::size_t N>  
bool operator!=(
    const array<Ty, N>& left,  
    const array<Ty, N>& right);
```  
  
### <a name="parameters"></a>參數  
 `Ty`  
 元素的類型。  
  
 `N`  
 陣列的大小。  
  
 `left`  
 要比較的左容器。  
  
 `right`  
 要比較的右容器。  
  
### <a name="remarks"></a>備註  
 此範本函式會傳回 `!(left == right)`。  
  
### <a name="example"></a>範例  
  
```cpp  
// std__array__operator_ne.cpp   
// compile with: /EHsc   
#include <array>   
#include <iostream>   
  
typedef std::array<int, 4> Myarray;   
int main()   
    {   
    Myarray c0 = {0, 1, 2, 3};   
  
// display contents " 0 1 2 3"   
    for (Myarray::const_iterator it = c0.begin();   
        it != c0.end(); ++it)   
        std::cout << " " << *it;   
    std::cout << std::endl;   
  
    Myarray c1 = {4, 5, 6, 7};   
  
// display contents " 4 5 6 7"   
    for (Myarray::const_iterator it = c1.begin();   
        it != c1.end(); ++it)   
        std::cout << " " << *it;   
    std::cout << std::endl;   
  
// display results of comparisons   
    std::cout << std::boolalpha << " " << (c0 != c0);   
    std::cout << std::endl;   
    std::cout << std::boolalpha << " " << (c0 != c1);   
    std::cout << std::endl;   
  
    return (0);   
    }   
```  
  
```Output  
0 1 2 3  
4 5 6 7  
false  
true  
```  
  
##  <a name="op_lt"></a> operator&lt;  
 陣列比較，小於。  
  
```  
template <Ty, std::size_t N>  
bool operator<(
    const array<Ty, N>& left,  
    const array<Ty, N>& right);
```  
  
### <a name="parameters"></a>參數  
 `Ty`  
 元素的類型。  
  
 `N`  
 陣列的大小。  
  
 `left`  
 要比較的左容器。  
  
 `right`  
 要比較的右容器。  
  
### <a name="remarks"></a>備註  
 此範本函式會多載 `operator<` 來比較範本類別 [array 類別](../standard-library/array-class-stl.md)的兩個物件。 函式會傳回 `lexicographical_compare(left.begin(), left.end(), right.begin())`。  
  
### <a name="example"></a>範例  
  
```cpp  
// std__array__operator_lt.cpp   
// compile with: /EHsc   
#include <array>   
#include <iostream>   
  
typedef std::array<int, 4> Myarray;   
int main()   
    {   
    Myarray c0 = {0, 1, 2, 3};   
  
// display contents " 0 1 2 3"   
    for (Myarray::const_iterator it = c0.begin();   
        it != c0.end(); ++it)   
        std::cout << " " << *it;   
    std::cout << std::endl;   
  
    Myarray c1 = {4, 5, 6, 7};   
  
// display contents " 4 5 6 7"   
    for (Myarray::const_iterator it = c1.begin();   
        it != c1.end(); ++it)   
        std::cout << " " << *it;   
    std::cout << std::endl;   
  
// display results of comparisons   
    std::cout << std::boolalpha << " " << (c0 < c0);   
    std::cout << std::endl;   
    std::cout << std::boolalpha << " " << (c0 < c1);   
    std::cout << std::endl;   
  
    return (0);   
    }  
  
```  
  
```Output  
0 1 2 3  
4 5 6 7  
false  
true  
```  
  
##  <a name="op_lt_eq"></a> operator&lt;=  
 陣列比較，小於或相等。  
  
```  
template <Ty, std::size_t N>  
bool operator<=(
    const array<Ty, N>& left,  
    const array<Ty, N>& right);
```  
  
### <a name="parameters"></a>參數  
 `Ty`  
 元素的類型。  
  
 `N`  
 陣列的大小。  
  
 `left`  
 要比較的左容器。  
  
 `right`  
 要比較的右容器。  
  
### <a name="remarks"></a>備註  
 此範本函式會傳回 `!(right < left)`。  
  
### <a name="example"></a>範例  
  
```cpp  
// std__array__operator_le.cpp   
// compile with: /EHsc   
#include <array>   
#include <iostream>   
  
typedef std::array<int, 4> Myarray;   
int main()   
    {   
    Myarray c0 = {0, 1, 2, 3};   
  
// display contents " 0 1 2 3"   
    for (Myarray::const_iterator it = c0.begin();   
        it != c0.end(); ++it)   
        std::cout << " " << *it;   
    std::cout << std::endl;   
  
    Myarray c1 = {4, 5, 6, 7};   
  
// display contents " 4 5 6 7"   
    for (Myarray::const_iterator it = c1.begin();   
        it != c1.end(); ++it)   
        std::cout << " " << *it;   
    std::cout << std::endl;   
  
// display results of comparisons   
    std::cout << std::boolalpha << " " << (c0 <= c0);   
    std::cout << std::endl;   
    std::cout << std::boolalpha << " " << (c1 <= c0);   
    std::cout << std::endl;   
  
    return (0);   
    }  
  
```  
  
```Output  
0 1 2 3  
4 5 6 7  
true  
false  
```  
  
##  <a name="op_eq_eq"></a> operator==  
 陣列比較，相等。  
  
```  
template <Ty, std::size_t N>  
bool operator==(
    const array<Ty, N>& left,  
    const array<Ty, N>& right);
```  
  
### <a name="parameters"></a>參數  
 `Ty`  
 元素的類型。  
  
 `N`  
 陣列的大小。  
  
 `left`  
 要比較的左容器。  
  
 `right`  
 要比較的右容器。  
  
### <a name="remarks"></a>備註  
 此範本函式會多載 `operator==` 來比較範本類別 [array 類別](../standard-library/array-class-stl.md)的兩個物件。 函式會傳回 `equal(left.begin(), left.end(), right.begin())`。  
  
### <a name="example"></a>範例  
  
```cpp  
// std__array__operator_eq.cpp   
// compile with: /EHsc   
#include <array>   
#include <iostream>   
  
typedef std::array<int, 4> Myarray;   
int main()   
    {   
    Myarray c0 = {0, 1, 2, 3};   
  
// display contents " 0 1 2 3"   
    for (Myarray::const_iterator it = c0.begin();   
        it != c0.end(); ++it)   
        std::cout << " " << *it;   
    std::cout << std::endl;   
  
    Myarray c1 = {4, 5, 6, 7};   
  
// display contents " 4 5 6 7"   
    for (Myarray::const_iterator it = c1.begin();   
        it != c1.end(); ++it)   
        std::cout << " " << *it;   
    std::cout << std::endl;   
  
// display results of comparisons   
    std::cout << std::boolalpha << " " << (c0 == c0);   
    std::cout << std::endl;   
    std::cout << std::boolalpha << " " << (c0 == c1);   
    std::cout << std::endl;   
  
    return (0);   
    }  
  
```  
  
```Output  
0 1 2 3  
4 5 6 7  
true  
false  
```  
  
##  <a name="op_gt"></a> operator&gt;  
 陣列比較，大於。  
  
```  
template <Ty, std::size_t N>  
bool operator>(
    const array<Ty, N>& left,  
    const array<Ty, N>& right);
```  
  
### <a name="parameters"></a>參數  
 `Ty`  
 元素的類型。  
  
 `N`  
 陣列的大小。  
  
 `left`  
 要比較的左容器。  
  
 `right`  
 要比較的右容器。  
  
### <a name="remarks"></a>備註  
 此範本函式會傳回 `(right < left)`。  
  
### <a name="example"></a>範例  
  
```cpp  
// std__array__operator_gt.cpp   
// compile with: /EHsc   
#include <array>   
#include <iostream>   
  
typedef std::array<int, 4> Myarray;   
int main()   
    {   
    Myarray c0 = {0, 1, 2, 3};   
  
// display contents " 0 1 2 3"   
    for (Myarray::const_iterator it = c0.begin();   
        it != c0.end(); ++it)   
        std::cout << " " << *it;   
    std::cout << std::endl;   
  
    Myarray c1 = {4, 5, 6, 7};   
  
// display contents " 4 5 6 7"   
    for (Myarray::const_iterator it = c1.begin();   
        it != c1.end(); ++it)   
        std::cout << " " << *it;   
    std::cout << std::endl;   
  
// display results of comparisons   
    std::cout << std::boolalpha << " " << (c0 > c0);   
    std::cout << std::endl;   
    std::cout << std::boolalpha << " " << (c1 > c0);   
    std::cout << std::endl;   
  
    return (0);   
    }  
  
```  
  
```Output  
0 1 2 3  
4 5 6 7  
false  
true  
```  
  
##  <a name="op_gt_eq"></a> operator&gt;=  
 陣列比較，大於或相等。  
  
```  
template <Ty, std::size_t N>  
bool operator>=(
    const array<Ty, N>& left,  
    const array<Ty, N>& right);
```  
  
### <a name="parameters"></a>參數  
 `Ty`  
 元素的類型。  
  
 `N`  
 陣列的大小。  
  
 `left`  
 要比較的左容器。  
  
 `right`  
 要比較的右容器。  
  
### <a name="remarks"></a>備註  
 此範本函式會傳回 `!(left < right)`。  
  
### <a name="example"></a>範例  
  
```cpp  
// std__array__operator_ge.cpp   
// compile with: /EHsc   
#include <array>   
#include <iostream>   
  
typedef std::array<int, 4> Myarray;   
int main()   
    {   
    Myarray c0 = {0, 1, 2, 3};   
  
// display contents " 0 1 2 3"   
    for (Myarray::const_iterator it = c0.begin();   
        it != c0.end(); ++it)   
        std::cout << " " << *it;   
    std::cout << std::endl;   
  
    Myarray c1 = {4, 5, 6, 7};   
  
// display contents " 4 5 6 7"   
    for (Myarray::const_iterator it = c1.begin();   
        it != c1.end(); ++it)   
        std::cout << " " << *it;   
    std::cout << std::endl;   
  
// display results of comparisons   
    std::cout << std::boolalpha << " " << (c0 >= c0);   
    std::cout << std::endl;   
    std::cout << std::boolalpha << " " << (c0 >= c1);   
    std::cout << std::endl;   
  
    return (0);   
    }  
  
```  
  
```Output  
0 1 2 3  
4 5 6 7  
true  
false  
```  
  
## <a name="see-also"></a>另請參閱  
 [\<array>](../standard-library/array.md)

