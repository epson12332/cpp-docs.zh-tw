---
title: money_put 類別
ms.date: 11/01/2018
f1_keywords:
- xlocmon/std::money_put
- xlocmon/std::money_put::char_type
- xlocmon/std::money_put::iter_type
- xlocmon/std::money_put::string_type
- xlocmon/std::money_put::do_put
- xlocmon/std::money_put::put
helpviewer_keywords:
- std::money_put [C++]
- std::money_put [C++], char_type
- std::money_put [C++], iter_type
- std::money_put [C++], string_type
- std::money_put [C++], do_put
- std::money_put [C++], put
ms.assetid: f439fd56-c9b1-414c-95e1-66c918c6eee6
ms.openlocfilehash: 346dd4f681432143c954ca125c3862fc6827db60
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62383538"
---
# <a name="moneyput-class"></a>money_put 類別

此樣板類別描述可以做為地區設定 facet 的物件，以控制貨幣值轉換為類型 `CharType` 的序列。

## <a name="syntax"></a>語法

```cpp
template <class CharType,
    class OutputIterator = ostreambuf_iterator<CharType>>
class money_put : public locale::facet;
```

### <a name="parameters"></a>參數

*CharType*<br/>
程式內用於編碼地區設定字元的類型。

*OutputIterator*<br/>
貨幣 put 函式將其輸出寫入其中的迭代器類型。

## <a name="remarks"></a>備註

如同所有地區設定 facet，靜態物件識別碼有初始儲存值零。 第一次嘗試存取它的儲存值時，會在 **id** 中儲存一個唯一的正值。

### <a name="constructors"></a>建構函式

|建構函式|描述|
|-|-|
|[money_put](#money_put)|`money_put` 類型物件的建構函式。|

### <a name="typedefs"></a>Typedefs

|類型名稱|描述|
|-|-|
|[char_type](#char_type)|類型，用來描述由地區設定使用的字元。|
|[iter_type](#iter_type)|描述輸出迭代器的類型。|
|[string_type](#string_type)|類型，描述包含 `CharType` 類型字元的字串。|

### <a name="member-functions"></a>成員函式

|成員函式|描述|
|-|-|
|[do_put](#do_put)|虛擬函式，呼叫以將數字或字串轉換為代表貨幣值的字元序列。|
|[put](#put)|將數字或字串轉換為代表貨幣值的字元序列。|

## <a name="requirements"></a>需求

**標頭︰**\<locale>

**命名空間：** std

## <a name="char_type"></a>  money_put::char_type

類型，用來描述由地區設定使用的字元。

```cpp
typedef CharType char_type;
```

### <a name="remarks"></a>備註

此類型與樣板參數 **CharType** 同義。

## <a name="do_put"></a>  money_put::do_put

虛擬函式，呼叫以將數字或字串轉換為代表貨幣值的字元序列。

```cpp
virtual iter_type do_put(
    iter_type next,
    bool _Intl,
    ios_base& _Iosbase,
    CharType _Fill,
    const string_type& val) const;

virtual iter_type do_put(
    iter_type next,
    bool _Intl,
    ios_base& _Iosbase,
    CharType _Fill,
    long double val) const;
```

### <a name="parameters"></a>參數

*next*<br/>
迭代器，定址對象是所插入字串的第一個元素。

*_Intl*<br/>
布林值，指出序列中預期的貨幣符號類型：如果是國際，即為 **true**，如果是國內，則為 **false**。

*_Iosbase*<br/>
格式旗標，已設定時，表示貨幣符號為選用；否則，必須指定貨幣符號。

*_Fill*<br/>
間距所使用的字元。

*val*<br/>
要轉換的字串物件。

### <a name="return-value"></a>傳回值

輸出迭代器，定址對象是所產生之最後一個元素的後面一個位置。

### <a name="remarks"></a>備註

第一個虛擬的受保護的成員函式會產生開始的循序元素*下一步*產生貨幣輸出欄位從[string_type](#string_type)物件*val*。 所控制的序列*val*必須開始一個或多個小數位數，選擇性地加上減號 （-），以代表總額。 此函式會傳回迭代器，此迭代器指定所產生之貨幣輸出欄位後的第一個元素。

第二個受保護的虛擬成員函式的行為與第一個相同除了其第一個有效的轉換*val*為一連串十進位數字，選擇性地加上負號，然後將轉換為上述該序列。

貨幣輸出欄位的格式會由 [locale facet](../standard-library/locale-class.md#facet_class) fac (由 [use_facet](../standard-library/locale-functions.md#use_facet) < [moneypunct](../standard-library/moneypunct-class.md)\< **CharType**, **intl**> >( **iosbase**. [getloc](../standard-library/ios-base-class.md#getloc)) 有效呼叫所傳回) 決定。

尤其是：

- **fac**. [pos_format](../standard-library/moneypunct-class.md#pos_format) 會決定為非負數值產生欄位元件時的順序。

- **fac**. [neg_format](../standard-library/moneypunct-class.md#neg_format) 會決定為負數值產生欄位元件時的順序。

- **fac**. [curr_symbol](../standard-library/moneypunct-class.md#curr_symbol) 會決定要為貨幣符號產生的元素序列。

- **fac**. [positive_sign](../standard-library/moneypunct-class.md#positive_sign) 會決定要為正號產生的元素序列。

- **fac**. [negative_sign](../standard-library/moneypunct-class.md#negative_sign) 會決定要為負號產生的元素序列。

- **fac**. [grouping](../standard-library/moneypunct-class.md#grouping) 會決定任何小數點左邊數字分組的方式。

- **fac**. [thousands_sep](../standard-library/moneypunct-class.md#thousands_sep) 會決定任何小數點左邊分隔數字群組的元素。

- **fac**. [decimal_point](../standard-library/moneypunct-class.md#decimal_point) 會決定將整數與任何小數分隔的元素。

- **fac**. [frac_digits](../standard-library/moneypunct-class.md#frac_digits) 會決定任何小數點右邊的有效小數數目。

如果正負號字串 ( **fac**. `negative_sign` 或 **fac**. `positive_sign`) 有多個元素，將只會在格式模式中與 **money_base::sign** 相等之元素出現的位置，產生第一個元素，其中該格式模式為 ( **fac**. `neg_format` 或 **fac**. `pos_format`)。 所有其餘元素則是在貨幣輸入欄位的結尾產生。

如果 **iosbase**. [flags](../standard-library/ios-base-class.md#flags) & [showbase](../standard-library/ios-functions.md#showbase) 不為零，字串 **fac**. `curr_symbol` 就會在格式模式中與 **money_base::symbol** 相等之元素出現的位置產生。 否則，不會產生任何貨幣符號。

如果 **fac**. **grouping** (其第一個元素的值為 CHAR_MAX) 未施加任何千分號條件約束，就不會有任何 **fac**. `thousands_sep` 執行個體在貨幣輸出欄位的值部分 (格式模式中與 **money_base::value** 相等之元素出現的位置) 產生。 如果 **fac**. `frac_digits` 為零，則在十進位數字之後不會產生任何 **fac**. `decimal_point` 執行個體。 否則，產生的貨幣輸出欄位會將低序位 **fac**. `frac_digits` 十進位數字放在小數點右邊。

系統會針對所有數字輸出欄位進行填補，但有例外，就是如果 **iosbase**. **flags** & **iosbase**. [internal](../standard-library/ios-functions.md#internal) 不為零，便會在格式模式中與 **money_base::space** 相等之元素出現的位置，於該元素未出現的情況下，產生任何內部填補字元。 否則，內部填補字元會出現在已產生的序列之前。 填補字元為 **fill**。

函式會呼叫 **iosbase**. **width**(0) 將欄位寬度重設為零。

### <a name="example"></a>範例

請參閱 [put](#put) 的範例，其中會由 **put** 呼叫此虛擬成員函式。

## <a name="iter_type"></a>  money_put::iter_type

描述輸出迭代器的類型。

```cpp
typedef OutputIterator iter_type;
```

### <a name="remarks"></a>備註

此類型與範本參數 **OutputIterator** 同義。

## <a name="money_put"></a>  money_put::money_put

`money_put` 類型物件的建構函式。

```cpp
explicit money_put(size_t _Refs = 0);
```

### <a name="parameters"></a>參數

*_Refs*<br/>
整數值，用來指定物件的記憶體管理類型。

### <a name="remarks"></a>備註

可能值 *_Refs*參數和其意義如下：

- 0：物件的存留期由包含該物件的地區設定來管理。

- 1：物件的存留期必須以手動方式管理。

- \> 1： 未定義這些值。

無法提供任何直接範例，因為解構函式受到保護。

建構函式會以 **locale::**[facet](../standard-library/locale-class.md#facet_class)( `_Refs`) 將其基底物件初始化。

## <a name="put"></a>  money_put::put

將數字或字串轉換為代表貨幣值的字元序列。

```cpp
iter_type put(
    iter_type next,
    bool _Intl,
    ios_base& _Iosbase,
    CharType _Fill,
    const string_type& val) const;

iter_type put(
    iter_type next,
    bool _Intl,
    ios_base& _Iosbase,
    CharType _Fill,
    long double val) const;
```

### <a name="parameters"></a>參數

*next*<br/>
迭代器，定址對象是所插入字串的第一個元素。

*_Intl*<br/>
布林值，指出序列中預期的貨幣符號類型：如果是國際，即為 **true**，如果是國內，則為 **false**。

*_Iosbase*<br/>
格式旗標，已設定時，表示貨幣符號為選用；否則，必須指定貨幣符號。

*_Fill*<br/>
間距所使用的字元。

*val*<br/>
要轉換的字串物件。

### <a name="return-value"></a>傳回值

輸出迭代器，定址對象是所產生之最後一個元素的後面一個位置。

### <a name="remarks"></a>備註

兩個成員函式都會傳回 [do_put](#do_put)( `next`, `_Intl`, `_Iosbase`, `_Fill`, `val`)。

### <a name="example"></a>範例

```cpp
// money_put_put.cpp
// compile with: /EHsc
#include <locale>
#include <iostream>
#include <sstream>

int main()
{
    std::locale loc( "german_germany" );
    std::basic_stringstream<char> psz;

    psz.imbue(loc);
    psz.flags(psz.flags() | std::ios_base::showbase); // force the printing of the currency symbol
    std::use_facet<std::money_put<char> >(loc).put(std::basic_ostream<char>::_Iter(psz.rdbuf()), true, psz, ' ', 100012);
    if (psz.fail())
        std::cout << "money_put() FAILED" << std::endl;
    else
        std::cout << "money_put() = \"" << psz.rdbuf()->str() << "\"" << std::endl;
}
```

```Output
money_put() = "EUR1.000,12"
```

## <a name="string_type"></a>  money_put::string_type

類型，描述包含 `CharType` 類型字元的字串。

```cpp
typedef basic_string<CharType, Traits, Allocator> string_type;
```

### <a name="remarks"></a>備註

此類型描述 [basic_string](../standard-library/basic-string-class.md) 範本類別的特製化，其中此類別的物件可儲存來自來源序列的元素序列。

## <a name="see-also"></a>另請參閱

[\<locale>](../standard-library/locale.md)<br/>
[facet 類別](../standard-library/locale-class.md#facet_class)<br/>
[C++ 標準程式庫中的執行緒安全](../standard-library/thread-safety-in-the-cpp-standard-library.md)<br/>
