---
title: '&lt;string_view&gt;運算子'
ms.date: 04/19/2019
f1_keywords:
- xstring/basic_string_view::operator!=
- xstring/basic_string_view::operator&gt;
- xstring/basic_string_view::operator&gt;=
- xstring/basic_string_view::operator&lt;
- xstring/basic_string_view::operator&lt;&lt;
- xstring/basic_string_view::operator&lt;=
- xstring/basic_string_view::operator+
- xstring/basic_string_view::operator==
helpviewer_keywords:
- std::basic_string_view::operator!=
- std::basic_string_view::operator&gt;
- std::basic_string_view::operator&gt;=
- std::basic_string_view::operator&lt;
- std::basic_string_view::operator&lt;&lt;
- std::basic_string_view::operator&lt;=, std::basic_string_view::operator==
ms.openlocfilehash: 1fbb7faf7d6fc92a053c0f4d47575c5c53c7968e
ms.sourcegitcommit: c6f8e6c2daec40ff4effd8ca99a7014a3b41ef33
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/24/2019
ms.locfileid: "64346916"
---
# <a name="ltstringviewgt-operators"></a>&lt;string_view&gt;運算子

使用這些運算子來比較兩個 string_view 物件，或 string_view 和其他字串物件 (例如[std:: string](basic-string-class.md)，或**char\***) 針對提供的隱含轉換。 

||||
|-|-|-|
|[operator!=](#op_neq)|[operator&gt;](#op_gt)|[operator&gt;=](#op_gt_eq)|
|[operator&lt;](#op_lt)|[operator&lt;&lt;](#op_lt_lt)|[operator&lt;=](#op_lt_eq)|
|[operator==](#op_eq_eq)|[operator""sv](#op_sv)|

## <a name="op_neq"></a> 運算子 ！ =

測試運算子左邊的物件是否不等於右邊的物件。

```cpp
template <class CharType, class Traits>
bool operator!=(
    const basic_string_view<CharType, Traits>& left,
    const basic_string_view<CharType, Traits>& right);

template <class CharType, class Traits>
bool operator!=(
    const basic_string_view<CharType, Traits>& left,
    convertible_string_type right);

template <class CharType, class Traits>
bool operator!=(
    convertible_string_type left,
    const basic_string_view<CharType, Traits>& right);
```

### <a name="parameters"></a>參數

*left*<br/>
任何轉換的字串型別或型別的物件`basic_string_view`進行比較。

*right*<br/>
任何轉換的字串型別或型別的物件`basic_string_view`進行比較。

### <a name="return-value"></a>傳回值

**真**如果運算子左邊的物件在詞典編纂上等於右邊的物件，否則為不是**false**。

### <a name="remarks"></a>備註

隱含的轉換必須從其中*convertible_string_type*到另一端 string_view。 

比較為基礎的成對辭典編纂比較字元序列。 如果有相同數目的項目，且項目都相等，則兩個物件相等。 反之則為不相等。

## <a name="op_eq_eq"></a> 運算子 = =

測試運算子左邊的物件是否等於右邊的物件。

```cpp
template <class CharType, class Traits>
bool operator==(
    const basic_string_view<CharType, Traits>& left,
    const basic_string_view<CharType, Traits>& right);

template <class CharType, class Traits>
bool operator==(
    const basic_string_view<CharType, Traits>& left,
    convertible_string_type right);

template <class CharType, class Traits>
bool operator==(
    convertible_string_type left,
    const basic_string_view<CharType, Traits>& right);
```

### <a name="parameters"></a>參數

*left*<br/>
任何轉換的字串型別或型別的物件`basic_string_view`進行比較。

*right*<br/>
任何轉換的字串型別或型別的物件`basic_string_view`進行比較。

### <a name="return-value"></a>傳回值

**真**詞典編纂上等於右邊的物件，否則為運算子左邊的物件是否**false**。

### <a name="remarks"></a>備註

隱含的轉換必須從其中*convertible_string_type*到另一端 string_view。 

比較為基礎的成對辭典編纂比較字元序列。 如果有相同數目的項目，且項目都相等，則兩個物件相等。


## <a name="op_lt"></a> 運算子&lt;

測試運算子左邊的物件是否小於右邊的 sidestring_view 上的物件
```cpp
template <class CharType, class Traits>
bool operator<(
    const basic_string_view<CharType, Traits>& left,
    const basic_string_view<CharType, Traits>& right);

template <class CharType, class Traits>
bool operator<(
    const basic_string_view<CharType, Traits>& left,
    convertible_string_type right);

template <class CharType, class Traits>
bool operator<(
    convertible_string_type left,
    const basic_string_view<CharType, Traits>& right);
```

### <a name="parameters"></a>參數

*left*<br/>
任何轉換的字串型別或型別的物件`basic_string_view`進行比較。

*right*<br/>
任何轉換的字串型別或型別的物件`basic_string_view`進行比較。

### <a name="return-value"></a>傳回值

**真**如果運算子左邊的物件詞典編纂上小於右邊; 物件否則**false**。

### <a name="remarks"></a>備註

隱含的轉換必須從其中*convertible_string_type*到另一端 string_view。 

比較為基礎的成對辭典編纂比較字元序列。 遇到第一個不相等的成對字元時，會傳回該比較的結果。 如果找不到任何不相等的字元，但一個序列較短，較短的序列小於較長的以外。 換句話說，「 貓 」 有 「 貓 」、 「 小於。

### <a name="example"></a>範例

```cpp
#include <string>
#include <string_view>

using namespace std;

int main()
{
    string_view sv1 { "ABA" };
    string_view sv2{ "ABAC" };
    string_view sv3{ "ABAD" };
    string_view sv4{ "ABACE" };

    bool result = sv2 > sv1; // true
    result = sv3 > sv2; // true
    result = sv3 != sv1; // true
    result = sv4 < sv3; // true because `C` < `D`
}
```

## <a name="op_lt_eq"></a> 運算子&lt;=

測試運算子左邊的物件是否小於或等於右邊的物件。

```cpp
template <class CharType, class Traits>
bool operator<=(
    const basic_string_view<CharType, Traits>& left,
    const basic_string_view<CharType, Traits>& right);

template <class CharType, class Traits>
bool operator<=(
    const basic_string_view<CharType, Traits>& left,
    convertible_string_type right);

template <class CharType, class Traits>
bool operator<=(
    convertible_string_type left,
    const basic_string_view<CharType, Traits>& right);
```

### <a name="parameters"></a>參數

*left*<br/>
任何轉換的字串型別或型別的物件`basic_string_view`進行比較。

*right*<br/>
任何轉換的字串型別或型別的物件`basic_string_view`進行比較。

### <a name="return-value"></a>傳回值

**真**如果運算子左邊的物件是詞典編纂上小於或等於右邊的物件，，否則為**false**。

### <a name="remarks"></a>備註

請參閱[運算子&lt;](#op_lt)。

## <a name="op_lt_lt"></a> 運算子&lt;&lt;

將 string_view 寫入至輸出資料流中。

```cpp
template <class CharType, class Traits>
inline basic_ostream<CharType, Traits>& operator<<(
    basic_ostream<CharType, Traits>& Ostr, const basic_string_view<CharType, Traits> Str);
```

### <a name="parameters"></a>參數

*Ostr*<br/>
要寫入輸出資料流。

*Str*<br/>
要輸入至輸出資料流 string_view。

### <a name="return-value"></a>傳回值

要寫入輸出資料流。

### <a name="remarks"></a>備註

使用這個運算子來將 string_view 的內容插入至輸出資料流，例如使用[std:: cout](iostream.md#cout)。

## <a name="op_gt"></a> 運算子&gt;

測試運算子左邊的物件是否大於右邊的物件。

```cpp
template <class CharType, class Traits>
bool operator>(
    const basic_string_view<CharType, Traits>& left,
    const basic_string_view<CharType, Traits>& right);

template <class CharType, class Traits>
bool operator>(
    const basic_string_view<CharType, Traits>& left,
    convertible_string_type right);

template <class CharType, class Traits>
bool operator>(
    convertible_string_type left,
    const basic_string_view<CharType, Traits>& right);
```

### <a name="parameters"></a>參數

*left*<br/>
任何轉換的字串型別或型別的物件`basic_string_view`進行比較。

*right*<br/>
任何轉換的字串型別或型別的物件`basic_string_view`進行比較。

### <a name="return-value"></a>傳回值

**真**詞典編纂上大於右邊的 string_view 物件; 否則為運算子左邊的物件是否**false**。

### <a name="remarks"></a>備註

請參閱[運算子&lt;](#op_lt)。

## <a name="op_gt_eq"></a> 運算子&gt;=

測試運算子左邊的物件是否大於或等於右邊的物件。

```cpp
template <class CharType, class Traits>
bool operator>=(
    const basic_string_view<CharType, Traits>& left,
    const basic_string_view<CharType, Traits>& right);

template <class CharType, class Traits>
bool operator>=(
    const basic_string_view<CharType, Traits>& left,
    convertible_string_type right);

template <class CharType, class Traits>
bool operator>=(
    convertible_string_type left,
    const basic_string_view<CharType, Traits>& right);
```

### <a name="parameters"></a>參數

*left*<br/>
任何轉換的字串型別或型別的物件`basic_string_view`進行比較。

*right*<br/>
任何轉換的字串型別或型別的物件`basic_string_view`進行比較。

### <a name="return-value"></a>傳回值

**真**詞典編纂上大於或等於右邊的物件，否則為運算子左邊的物件是否**false**。

### <a name="remarks"></a>備註

請參閱[運算子&lt;](#op_lt)。

## <a name="op_sv"></a> 運算子""sv (string_view 常值)

建構 string_view，以從字串常值。 需要命名空間`std::literals::string_view_literals`。 

### <a name="example"></a>範例

```cpp

using namespace std;
using namespace literals::string_view_literals;

    string_view sv{ "Hello"sv };
    wstring_view wsv{ L"Hello"sv };
    u16string_view sv16{ u"Hello"sv };
    u32string_view sv32{ U"Hello"sv };
```

## <a name="see-also"></a>另請參閱

[\<string_view>](../standard-library/string-view.md)<br/>
