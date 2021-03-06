---
title: basic_istream 類別
ms.date: 11/04/2016
f1_keywords:
- istream/std::basic_istream
- istream/std::basic_istream::gcount
- istream/std::basic_istream::get
- istream/std::basic_istream::getline
- 'istream/std::basic_istream::'
- istream/std::basic_istream::peek
- istream/std::basic_istream::putback
- istream/std::basic_istream::read
- istream/std::basic_istream::readsome
- istream/std::basic_istream::seekg
- istream/std::basic_istream::sentry
- istream/std::basic_istream::swap
- istream/std::basic_istream::sync
- istream/std::basic_istream::tellg
- istream/std::basic_istream::unget
helpviewer_keywords:
- std::basic_istream [C++]
- std::basic_istream [C++], gcount
- std::basic_istream [C++], get
- std::basic_istream [C++], getline
- std::basic_istream [C++], OVERWRITE
- std::basic_istream [C++], peek
- std::basic_istream [C++], putback
- std::basic_istream [C++], read
- std::basic_istream [C++], readsome
- std::basic_istream [C++], seekg
- std::basic_istream [C++], sentry
- std::basic_istream [C++], swap
- std::basic_istream [C++], sync
- std::basic_istream [C++], tellg
- std::basic_istream [C++], unget
ms.assetid: c7c27111-de6d-42b4-95a3-a7e65259bf17
ms.openlocfilehash: 5e7f6ae0728a7d28af1992cf4186d533f1a97330
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62414161"
---
# <a name="basicistream-class"></a>basic_istream 類別

描述一個物件，該物件可控制如何從具有 `Elem` 類型 (也稱為 [char_type](../standard-library/basic-ios-class.md#char_type)) 之元素的資料流緩衝區擷取元素和編碼物件；其中該類型的字元特性是由 *Tr* 類別 (也稱為 [traits_type](../standard-library/basic-ios-class.md#traits_type)) 所決定。

## <a name="syntax"></a>語法

```cpp
template <class Elem, class Tr = char_traits<Elem>>
class basic_istream : virtual public basic_ios<Elem, Tr>
```

## <a name="remarks"></a>備註

大部分多載 [operator>>](#op_gt_gt) 的成員函式為格式化的輸入函式。 它們遵循下列模式：

```cpp
iostate state = goodbit;
const sentry ok(*this);

if (ok)
{
    try
    {
        /*extract elements and convert
            accumulate flags in state.
            store a successful conversion*/
    }
    catch (...)
    {
        try
        {
            setstate(badbit);

        }
        catch (...)
        {
        }
        if ((exceptions()& badbit) != 0)
            throw;
    }
}
setstate(state);

return (*this);
```

許多其他的成員函式為未經格式化的輸入函式。 它們遵循下列模式：

```cpp
iostate state = goodbit;
count = 0;    // the value returned by gcount
const sentry ok(*this, true);

if (ok)
{
    try
    {
        /* extract elements and deliver
            count extracted elements in count
            accumulate flags in state */
    }
    catch (...)
    {
        try
        {
            setstate(badbit);

        }
        catch (...)
        {
        }
        if ((exceptions()& badbit) != 0)
            throw;
    }
}
setstate(state);
```

這兩個群組的函式呼叫[setstate](../standard-library/basic-ios-class.md#setstate)(`eofbit`) 如果在擷取元素時遇到檔案結尾。

`basic_istream`< `Elem`, *Tr*> 類別的物件會儲存：

- [basic_ios](../standard-library/basic-ios-class.md)< `Elem`, *Tr*> 類別的虛擬公開基底物件`.`

- 最後一個未格式化的輸入作業之擷取計數 (稱為`count`中先前的程式碼)。

## <a name="example"></a>範例

若要深入了解輸入資料流，請參閱 [basic_ofstream 類別](../standard-library/basic-ifstream-class.md)的範例。

### <a name="constructors"></a>建構函式

|建構函式|描述|
|-|-|
|[basic_istream](#basic_istream)|建構類型 `basic_istream` 的物件。|

### <a name="member-functions"></a>成員函式

|成員函式|描述|
|-|-|
|[gcount](#gcount)|傳回最後一個未經格式化的輸入期間，讀取的字元數。|
|[get](#get)|從輸入資料流讀取一或多個字元。|
|[getline](#getline)|從輸入資料流讀取一行。|
|[ignore](#ignore)|導致從目前的讀取位置略過一些項目。|
|[peek](#peek)|傳回要讀取的下一個字元。|
|[putback](#putback)|將指定的字元放入資料流。|
|[read](#read)|從資料流讀取指定的字元數，並將其儲存在陣列中。|
|[readsome](#readsome)|只從緩衝區讀取。|
|[seekg](#seekg)|移動資料流中的讀取位置。|
|[sentry](#sentry)|此巢狀類別會描述物件，該物件的宣告會建構格式化的輸入函式以及未經格式化的輸入函式。|
|[swap](#swap)|以 `basic_istream` 物件交換所提供的 `basic_istream` 物件參數。|
|[sync](#sync)|同步處理與資料流緩衝區的資料流相關聯的輸入裝置。|
|[tellg](#tellg)|回報在資料流中目前的讀取位置。|
|[unget](#unget)|將最近讀取的字元放回資料流。|

### <a name="operators"></a>運算子

|運算子|描述|
|-|-|
|[operator>>](#op_gt_gt)|呼叫輸入資料流上的函式，或從輸入資料流讀取經格式化的資料。|
|[operator=](#op_eq)|將位於運算子右側的 `basic_istream` 指派給此物件。 這是一個移動指派，涉及不會留下複本的 `rvalue` 參考。|

## <a name="requirements"></a>需求

**標頭︰**\<istream>

**命名空間：** std

## <a name="basic_istream"></a>  basic_istream::basic_istream

建構類型 `basic_istream` 的物件。

```cpp
explicit basic_istream(
    basic_streambuf<Elem, Tr>* strbuf,
    bool _Isstd = false);

basic_istream(basic_istream&& right);
```

### <a name="parameters"></a>參數

*strbuf*<br/>
[basic_streambuf](../standard-library/basic-streambuf-class.md) 類型的物件。

*_Isstd*<br/>
**true**如果這是標準的資料流; 否則**false**。

*right*<br/>
要複製的 `basic_istream` 物件。

### <a name="remarks"></a>備註

第一個建構函式會藉由呼叫 [init](../standard-library/basic-ios-class.md#init)(_S `trbuf`) 初始化基底類別。 它也會在擷取計數中儲存零。 如需此擷取計數的詳細資訊，請參閱 [basic_istream 類別](../standard-library/basic-istream-class.md)概觀主題的＜備註＞一節。

第二個建構函式會藉由呼叫 `move( right)` 初始化基底類別。 它也會在擷取計數中儲存 _R `ight.gcount()`，並在 _R `ight` 的擷取計數中儲存零。

### <a name="example"></a>範例

若要深入了解輸入資料流，請參閱 [basic_ifstream::basic_ifstream](../standard-library/basic-ifstream-class.md#basic_ifstream) 的範例。

## <a name="gcount"></a>  basic_istream::gcount

傳回最後一個未經格式化的輸入期間，讀取的字元數。

```cpp
streamsize gcount() const;
```

### <a name="return-value"></a>傳回值

擷取計數。

### <a name="remarks"></a>備註

請使用 [basic_istream:: get](#get) 來讀取未格式化的字元。

### <a name="example"></a>範例

```cpp
// basic_istream_gcount.cpp
// compile with: /EHsc
#include <iostream>
using namespace std;

int main( )
{
   cout << "Type the letter 'a': ";

   ws( cin );
   char c[10];

   cin.get( &c[0],9 );
   cout << c << endl;

   cout << cin.gcount( ) << endl;
}
```

```Input
a
```

```Output
Type the letter 'a': a
1
```

## <a name="get"></a>  basic_istream::get

從輸入資料流讀取一或多個字元。

```cpp
int_type get();

basic_istream<Elem, Tr>& get(Elem& Ch);
basic_istream<Elem, Tr>& get(Elem* str, streamsize count);
basic_istream<Elem, Tr>& get(Elem* str, streamsize count, Elem Delim);

basic_istream<Elem, Tr>& get(basic_streambuf<Elem, Tr>& strbuf);
basic_istream<Elem, Tr>& get(basic_streambuf<Elem, Tr>& strbuf, Elem Delim);
```

### <a name="parameters"></a>參數

*count*<br/>
要從 `strbuf` 中讀取的字元數。

*Delim*<br/>
如果發生之前應終止讀取的字元*計數*。

*str*<br/>
要在其中寫入的字串。

*Ch*<br/>
要取得的字元。

*strbuf*<br/>
要在其中寫入的緩衝區。

### <a name="return-value"></a>傳回值

無參數格式的 get 會將讀取的元素當做整數或檔案結尾傳回。 其餘格式會傳回資料流 (* `this`)。

### <a name="remarks"></a>備註

這些未格式化之輸入函式的第一個函式會盡可能擷取一個元素，就像是傳回 `rdbuf`-> `sbumpc` 一樣。 否則會傳回 **traits_type::**[eof](../standard-library/char-traits-struct.md#eof)。 如果函式未不擷取任何元素，則會呼叫[setstate](../standard-library/basic-ios-class.md#setstate)(`failbit`)。

第二個函式會以相同方式來擷取 [int_type](../standard-library/basic-ios-class.md#int_type) 元素 `meta`。 如果 `meta` 與 **traits_type::eof** 比較的結果相等，則此函式會呼叫 `setstate`( **failbit**)。 否則，它會將 **traits_type::**[to_char_type](../standard-library/char-traits-struct.md#to_char_type)( `meta`) 儲存在 `Ch` 中。 此函式會傳回 **\*this**。

第三個函式會傳回 **get**(_ *Str*, `count`, `widen`('\ **n**'))。

第四個函式最多會擷取*計數*-1 的項目並將它們儲存在 _ 開頭的陣列中*Str*。 它一律會在所儲存的任何已擷取元素之後儲存 `char_type`。 為了進行測試，在下列情況下會停止擷取：

- 到達檔案結尾時。

- 在函式擷取比較為相等的項目*Delim*，在此情況下的項目放回受控制序列。

- 在函式擷取*計數*-1 的項目。

如果此函式未擷取任何元素，則會呼叫 `setstate`( **failbit**)。 在任何情況下，它都會傳回 **\*this**。

第五個函式會傳回 **get**( **strbuf**, `widen`('\ **n**'))。

第六個函式會擷取項目，並將其插入`strbuf`。 到達檔案結尾時，或是遇到與 _ *Delim* 比較為相等的元素 (不會擷取此元素) 時，會停止擷取。 如果插入失敗或擲回例外狀況 (會攔截但不會再次擲回)，也會停止，而不會擷取有問題的元素。 如果此函式未擷取任何元素，則會呼叫 `setstate`( **failbit**)。 在任何情況下，此函式都會傳回 **\*this**。

### <a name="example"></a>範例

```cpp
// basic_istream_get.cpp
// compile with: /EHsc
#include <iostream>
using namespace std;

int main( )
{
   char c[10];

   c[0] = cin.get( );
   cin.get( c[1] );
   cin.get( &c[2],3 );
   cin.get( &c[4], 4, '7' );

   cout << c << endl;
}
```

```Output
1111
```

## <a name="getline"></a>  basic_istream::getline

從輸入資料流取得一行。

```cpp
basic_istream<Elem, Tr>& getline(
    char_type* str,
    streamsize count);

basic_istream<Elem, Tr>& getline(
    char_type* str,
    streamsize count,
    char_type Delim);
```

### <a name="parameters"></a>參數

*count*<br/>
要從 `strbuf` 中讀取的字元數。

*Delim*<br/>
如果發生之前應終止讀取的字元*計數*。

*str*<br/>
要在其中寫入的字串。

### <a name="return-value"></a>傳回值

資料流 ( **\*this**)。

### <a name="remarks"></a>備註

這些未格式化之輸入函式的第一個輸入函式會傳回 **getline**(_ *Str*, `count`, `widen`(' `\`**n**'))。

第二個函式最多會擷取*計數*-1 的項目並將它們儲存在 _ 開頭的陣列中*Str*。 它一律會在所儲存的任何已擷取元素之後儲存字串結束字元。 為了進行測試，在下列情況下會停止擷取：

- 到達檔案結尾時。

- 在函式擷取比較為相等的項目*Delim*，在此情況下的項目不會放回或附加至受控制序列。

- 在函式擷取*計數*-1 的項目。

如果函式未不擷取任何元素或*計數*-1 項目，會呼叫[setstate](../standard-library/basic-ios-class.md#setstate)(`failbit`)。 在任何情況下，它都會傳回 **\*this**。

### <a name="example"></a>範例

```cpp
// basic_istream_getline.cpp
// compile with: /EHsc
#include <iostream>
using namespace std;

int main( )
{
   char c[10];

   cin.getline( &c[0], 5, '2' );
   cout << c << endl;
}
```

```Output
121
```

## <a name="ignore"></a>  basic_istream::ignore

導致從目前的讀取位置略過一些項目。

```cpp
basic_istream<Elem, Tr>& ignore(
    streamsize count = 1,
    int_type Delim = traits_type::eof());
```

### <a name="parameters"></a>參數

*count*<br/>
要從目前的讀取位置略過的元素數目。

*Delim*<br/>
項目，如果發生計數、 會導致`ignore`返回並讓之後的所有項目*Delim*讀取。

### <a name="return-value"></a>傳回值

資料流 ( **\*this**)。

### <a name="remarks"></a>備註

未格式化的輸入函式最多會擷取*計數*項目，並捨棄它們。 如果*計數*equals **numeric_limits\<int >:: max**，不過，它會被視為任意大。 會及早停止擷取或項目上的檔案結尾`Ch`使得**traits_type::**[to_int_type](../standard-library/char-traits-struct.md#to_int_type)( `Ch`) 的比較結果相等*Delim* （其中也會擷取）。 此函式會傳回 **\*this**。

### <a name="example"></a>範例

```cpp
// basic_istream_ignore.cpp
// compile with: /EHsc
#include <iostream>
int main( )
{
   using namespace std;
   char chararray[10];
   cout << "Type 'abcdef': ";
   cin.ignore( 5, 'c' );
   cin >> chararray;
   cout << chararray;
}
```

```Output
Type 'abcdef': abcdef
def
```

## <a name="op_gt_gt"></a>  basic\_istream::operator>>

呼叫輸入資料流上的函式，或從輸入資料流讀取經格式化的資料。

```cpp
basic_istream& operator>>(basic_istream& (* Pfn)(basic_istream&));
basic_istream& operator>>(ios_base& (* Pfn)(ios_base&));
basic_istream& operator>>(basic_ios<Elem, Tr>& (* Pfn)(basic_ios<Elem, Tr>&));
basic_istream& operator>>(basic_streambuf<Elem, Tr>* strbuf);
basic_istream& operator>>(bool& val);
basic_istream& operator>>(short& val);
basic_istream& operator>>(unsigned short& val);
basic_istream& operator>>(int& val);
basic_istream& operator>>(unsigned int& val);
basic_istream& operator>>(long& val);
basic_istream& operator>>(unsigned long& val);
basic_istream& operator>>(long long& val);
basic_istream& operator>>(unsigned long long& val);
basic_istream& operator>>(void *& val);
basic_istream& operator>>(float& val);
basic_istream& operator>>(double& val);
basic_istream& operator>>(long double& val);
```

### <a name="parameters"></a>參數

*Pfn*<br/>
函式指標。

*strbuf*<br/>
`stream_buf` 類型的物件。

*val*<br/>
要從資料流中讀取的值。

### <a name="return-value"></a>傳回值

資料流 ( **\*this**)。

### <a name="remarks"></a>備註

\<Istream > 標頭也會定義數個全域擷取運算子。 如需詳細資訊，請參閱 [operator>> (\<istream>)](../standard-library/istream-operators.md#op_gt_gt)。

第一個成員函式可確保 **istr** >> `ws` 格式的運算式呼叫 [ws](../standard-library/istream-functions.md#ws)( **istr**)，然後傳回 **\*this**。 第二個和第三個函式可確保其他操作工具 (例如 [hex](../standard-library/ios-functions.md#hex)) 具有類似的行為。 其餘函式會構成格式化的輸入函式。

函式：

```cpp
basic_istream& operator>>(
    basic_streambuf<Elem, Tr>* strbuf);
```

擷取項目，如果 _ *Strbuf*不是 null 指標，並將其插入*strbuf*。 到達檔案結尾時，會停止擷取。 如果插入失敗或擲回例外狀況 (會攔截但不會再次擲回)，也會停止，而不會擷取有問題的元素。 如果函式未不擷取任何元素，則會呼叫[setstate](../standard-library/basic-ios-class.md#setstate)(`failbit`)。 在任何情況下，此函式都會傳回 **\*this**。

函式：

```cpp
basic_istream& operator>>(bool& val);
```

會藉由呼叫 [use_facet](../standard-library/basic-filebuf-class.md#open) < `num_get`\< **Elem**, **InIt**>( [getloc](../standard-library/ios-base-class.md#getloc)). [get](../standard-library/ios-base-class.md#getloc)( **InIt**( [rdbuf](../standard-library/basic-ios-class.md#rdbuf)), `Init`(0), **\*this**, `getloc`, `val`) 擷取欄位，並將其轉換為布林值。 其中的 **InIt** 會定義為 [istreambuf_iterator](../standard-library/istreambuf-iterator-class.md)\< **Elem**, **Tr**>。 此函式會傳回 **\*this**。

函式：

```cpp
basic_istream& operator>>(short& val);
basic_istream& operator>>(unsigned short& val);
basic_istream& operator>>(int& val);
basic_istream& operator>>(unsigned int& val);
basic_istream& operator>>(long& val);
basic_istream& operator>>(unsigned long& val);
basic_istream& operator>>(long long& val);
basic_istream& operator>>(unsigned long long& val);
basic_istream& operator>>(void *& val);
```

會藉由呼叫 `use_facet`< `num_get`\< **Elem**, **InIt**>( `getloc`). [get](#get)( **InIt**( `rdbuf`), `Init`(0), **\*this**, `getloc`, `val`) 擷取欄位，並將其轉換為數值。 在這裡， **InIt**定義為`istreambuf_iterator` \< **Elem**， **Tr**>，以及`val`類型**長**， **unsigned long**，或**void** <strong>\*</strong>視。

如果已轉換的值無法表示為型別`val`，函式會呼叫[setstate](../standard-library/basic-ios-class.md#setstate)(`failbit`)。 在任何情況下，此函式都會傳回 **\*this**。

函式：

```cpp
basic_istream& operator>>(float& val);
basic_istream& operator>>(double& val);
basic_istream& operator>>(long double& val);
```

會藉由呼叫 `use_facet`< `num_get`\< **Elem**, **InIt**>( `getloc`). **get**( **InIt**( `rdbuf`), `Init`(0), **\*this**, `getloc`, `val`) 擷取欄位，並將其轉換為數值。 在這裡，`InIt`定義為`istreambuf_iterator` \< **Elem**， **Tr**>，並`val`具有型別**double**或**長double**視。

如果無法以 `val` 類型表示已轉換的值，此函式會呼叫 `setstate`( **failbit**)。 在任何情況下，它都會傳回 **\*this**。

### <a name="example"></a>範例

```cpp
// istream_basic_istream_op_is.cpp
// compile with: /EHsc
#include <iostream>

using namespace std;

ios_base& hex2( ios_base& ib )
{
   ib.unsetf( ios_base::dec );
   ib.setf( ios_base::hex );
   return ib;
}

basic_istream<char, char_traits<char> >& somefunc(basic_istream<char, char_traits<char> > &i)
{
   if ( i == cin )
   {
      cerr << "i is cin" << endl;
   }
   return i;
}

int main( )
{
   int i = 0;
   cin >> somefunc;
   cin >> i;
   cout << i << endl;
   cin >> hex2;
   cin >> i;
   cout << i << endl;
}
```

## <a name="op_eq"></a>  basic_istream::operator=

將位於運算子右側的 `basic_istream` 指派給此物件。 這是一個移動指派，涉及不會留下複本的 `rvalue` 參考。

```cpp
basic_istream& operator=(basic_istream&& right);
```

### <a name="parameters"></a>參數

*right*<br/>
`basic_ifstream` 物件的 `rvalue` 參考。

### <a name="return-value"></a>傳回值

傳回 *this。

### <a name="remarks"></a>備註

這個成員運算子會呼叫 swap `( right)`。

## <a name="peek"></a>  basic_istream::peek

傳回要讀取的下一個字元。

```cpp
int_type peek();
```

### <a name="return-value"></a>傳回值

要讀取的下一個字元。

### <a name="remarks"></a>備註

此未格式化的輸入函式會盡可能擷取一個元素，就像是傳回 `rdbuf` -> [sgetc](../standard-library/basic-streambuf-class.md#sgetc) 一樣。 否則會傳回 **traits_type::**[eof](../standard-library/char-traits-struct.md#eof)。

### <a name="example"></a>範例

```cpp
// basic_istream_peek.cpp
// compile with: /EHsc
#include <iostream>
using namespace std;

int main( )
{
   char c[10], c2;
   cout << "Type 'abcde': ";

   c2 = cin.peek( );
   cin.getline( &c[0], 9 );

   cout << c2 << " " << c << endl;
}
```

```Input
abcde
```

```Output
Type 'abcde': abcde
a abcde
```

## <a name="putback"></a>  basic_istream::putback

將指定的字元放入資料流。

```cpp
basic_istream<Elem, Tr>& putback(
    char_type Ch);
```

### <a name="parameters"></a>參數

*Ch*<br/>
要放回資料流的字元。

### <a name="return-value"></a>傳回值

資料流 ( **\*this**)。

### <a name="remarks"></a>備註

[未格式化的輸入函式](../standard-library/basic-istream-class.md)放回*Ch*，如果可能的話，請如同呼叫[rdbuf](../standard-library/basic-ios-class.md#rdbuf)`->`[sputbackc](../standard-library/basic-streambuf-class.md#sputbackc)。 如果 rdbuf 為 null 指標，或呼叫`sputbackc`會傳回**traits_type::**[eof](../standard-library/char-traits-struct.md#eof)，函式呼叫[setstate](../standard-library/basic-ios-class.md#setstate)(`badbit`)。 在任何情況下，它都會傳回 **\*this**。

### <a name="example"></a>範例

```cpp
// basic_istream_putback.cpp
// compile with: /EHsc
#include <iostream>
using namespace std;

int main( )
{
   char c[10], c2, c3;

   c2 = cin.get( );
   c3 = cin.get( );
   cin.putback( c2 );
   cin.getline( &c[0], 9 );
   cout << c << endl;
}
```

```Output
qwq
```

## <a name="read"></a>  basic_istream::read

從資料流讀取指定的字元數，並將其儲存在陣列中。

此方法有賴於呼叫者檢查傳遞的值是否正確，因此可能不安全。

```cpp
basic_istream<Elem, Tr>& read(
    char_type* str,
    streamsize count);
```

### <a name="parameters"></a>參數

*str*<br/>
要讀取其中字元的陣列。

*count*<br/>
要讀取的字元數。

### <a name="return-value"></a>傳回值

資料流 ( `*this`)。

### <a name="remarks"></a>備註

未格式化的輸入函式最多會擷取*計數*項目並將它們儲存在 _ 開頭的陣列中`Str`。 會及早停止擷取檔案結尾，情況下，函數會呼叫所在[setstate](../standard-library/basic-ios-class.md#setstate)(`failbit`)。 在任何情況下，它都會傳回 `*this`。

### <a name="example"></a>範例

```cpp
// basic_istream_read.cpp
// compile with: /EHsc
#include <iostream>
using namespace std;

int main()
{
    char c[10];
    int count = 5;

    cout << "Type 'abcde': ";

    // Note: cin::read is potentially unsafe, consider
    // using cin::_Read_s instead.
    cin.read(&c[0], count);
    c[count] = 0;

    cout << c << endl;
}
```

```Input
abcde
```

```Output
Type 'abcde': abcde
abcde
```

## <a name="readsome"></a>  basic_istream::readsome

讀取指定數目的字元值。

此方法有賴於呼叫者檢查傳遞的值是否正確，因此可能不安全。

```cpp
streamsize readsome(
    char_type* str,
    streamsize count);
```

### <a name="parameters"></a>參數

*str*<br/>
`readsome` 要在其中儲存所讀取字元的陣列。

*count*<br/>
要讀取的字元數。

### <a name="return-value"></a>傳回值

實際讀取的字元數 [gcount](#gcount)。

### <a name="remarks"></a>備註

此未格式化的輸入函式最多會擷取*計數*項目，從輸入資料流，並將它們儲存在陣列中*str*。

此函式不會等候輸入。 它會讀取任何可用的資料。

### <a name="example"></a>範例

```cpp
// basic_istream_readsome.cpp
// compile with: /EHsc /W3
#include <iostream>
using namespace std;

int main( )
{
   char c[10];
   int count = 5;

   cout << "Type 'abcdefgh': ";

   // cin.read blocks until user types input.
   // Note: cin::read is potentially unsafe, consider
   // using cin::_Read_s instead.
   cin.read(&c[0], 2);

   // Note: cin::readsome is potentially unsafe, consider
   // using cin::_Readsome_s instead.
   int n = cin.readsome(&c[0], count);  // C4996
   c[n] = 0;
   cout << n << " characters read" << endl;
   cout << c << endl;
}
```

## <a name="seekg"></a>  basic_istream::seekg

移動資料流中的讀取位置。

```cpp
basic_istream<Elem, Tr>& seekg(pos_type pos);

basic_istream<Elem, Tr>& seekg(off_type off, ios_base::seekdir way);
```

### <a name="parameters"></a>參數

*pos*<br/>
要在其中移動讀取指標的絕對位置。

*off*<br/>
若要移動讀取的指標相對於位移*方式*。

*way*<br/>
其中一個 [ios_base::seekdir](../standard-library/ios-base-class.md#seekdir) 列舉。

### <a name="return-value"></a>傳回值

資料流 ( **\*this**)。

### <a name="remarks"></a>備註

第一個成員函式會執行絕對搜尋，第二個成員函式會執行相對搜尋。

> [!NOTE]
> 請勿對文字檔案使用第二個成員函式，因為標準 C++ 不支援在文字檔案中執行相對搜尋。

如果[失敗](../standard-library/basic-ios-class.md#fail)為 false，第一個成員函式呼叫**newpos** = [rdbuf](../standard-library/basic-ios-class.md#rdbuf) -> [pubseekpos](../standard-library/basic-streambuf-class.md#pubseekpos)( `pos`)，某些`pos_type`暫存物件`newpos`。 如果`fail`為 false，第二個函式會呼叫**newpos** = **rdbuf** -> [pubseekoff](../standard-library/basic-streambuf-class.md#pubseekoff)( `off`， `way`). 在任一情況下，如果 ( `off_type`) **newpos** = = ( `off_type`)(-1) （置放作業失敗），函式呼叫`istr`。 [setstate](../standard-library/basic-ios-class.md#setstate)(`failbit`)。 兩個函式都會傳回 **\*this**。

如果 [fail](../standard-library/basic-ios-class.md#fail) 為 true，成員函式不會執行任何動作。

### <a name="example"></a>範例

```cpp
// basic_istream_seekg.cpp
// compile with: /EHsc
#include <iostream>
#include <fstream>

int main ( )
{
   using namespace std;
   ifstream file;
   char c, c1;

   file.open( "basic_istream_seekg.txt" );
   file.seekg(2);   // seek to position 2
   file >> c;
   cout << c << endl;
}
```

## <a name="sentry"></a>  basic_istream::sentry

此巢狀類別描述一個物件，該物件的宣告會建構格式化和未格式化的輸入函式。

class sentry { public: explicit sentry( basic_istream\<Elem, Tr>& _Istr, bool _Noskip = false); operator bool() const; };

### <a name="remarks"></a>備註

如果 `_Istr.`[good](../standard-library/basic-ios-class.md#good) 為 true，此建構函式會：

- 呼叫 `_Istr`。 [tie](../standard-library/basic-ios-class.md#tie) -> [flush](../standard-library/basic-ostream-class.md#flush) (如果 `_Istr` `tie` 不是 null 指標)

- 有效呼叫 [ws](../standard-library/istream-functions.md#ws)( `_Istr`) (如果 `_Istr` [flags](../standard-library/ios-base-class.md#flags)**&**[skipws](../standard-library/ios-functions.md#skipws) 為非零值)

如果在任何這類準備之後，`_Istr` `good` 為 false，建構函式呼叫`_Istr`。 [setstate](../standard-library/basic-ios-class.md#setstate)(`failbit`)。 在任何情況下，此建構函式都會將 `_Istr` `good` 在  `status`。 稍後呼叫`operator bool`提供此預存的值。

## <a name="swap"></a>  basic_istream::swap

交換兩個 `basic_istream` 物件的內容。

```cpp
void swap(basic_istream& right);
```

### <a name="parameters"></a>參數

*right*<br/>
`basic_istream` 物件的 lvalue 參考。

### <a name="remarks"></a>備註

此成員函式會呼叫 [basic_ios::swap](../standard-library/basic-ios-class.md#swap)`(right)`。 它也會交換擷取計數使用的擷取計數*右*。

## <a name="sync"></a>  basic_istream::sync

同步處理與資料流緩衝區的資料流相關聯的輸入裝置。

```cpp
int sync();
```

### <a name="return-value"></a>傳回值

如果 [rdbuf](../standard-library/basic-ios-class.md#rdbuf) 為 null 指標，此函式會傳回 -1。 否則會呼叫 `rdbuf` -> [pubsync](../standard-library/basic-streambuf-class.md#pubsync)。 如果傳回-1，函式會呼叫[setstate](../standard-library/basic-ios-class.md#setstate)(`badbit`) 並傳回-1。 否則，此函式會傳回零。

## <a name="tellg"></a>  basic_istream::tellg

回報在資料流中目前的讀取位置。

```cpp
pos_type tellg();
```

### <a name="return-value"></a>傳回值

在資料流中的目前位置。

### <a name="remarks"></a>備註

如果 [fail](../standard-library/basic-ios-class.md#fail) 為 false，此成員函式會傳回 [rdbuf](../standard-library/basic-ios-class.md#rdbuf) -> [pubseekoff](../standard-library/basic-streambuf-class.md#pubseekoff)(0, `cur`, **in**)。 否則會傳回 `pos_type`(-1)。

### <a name="example"></a>範例

```cpp
// basic_istream_tellg.cpp
// compile with: /EHsc
#include <iostream>
#include <fstream>

int main()
{
    using namespace std;
    ifstream file;
    char c;
    streamoff i;

    file.open("basic_istream_tellg.txt");
    i = file.tellg();
    file >> c;
    cout << c << " " << i << endl;

    i = file.tellg();
    file >> c;
    cout << c << " " << i << endl;
}
```

## <a name="unget"></a>  basic_istream::unget

將最近讀取的字元放回資料流。

```cpp
basic_istream<Elem, Tr>& unget();
```

### <a name="return-value"></a>傳回值

資料流 ( **\*this**)。

### <a name="remarks"></a>備註

[未格式化的輸入函式](../standard-library/basic-istream-class.md)會盡可能將上一個元素放回資料流，就像是呼叫 `rdbuf` -> [sungetc](../standard-library/basic-streambuf-class.md#sungetc) 一樣。 如果[rdbuf](../standard-library/basic-ios-class.md#rdbuf)為 null 指標，或如果呼叫`sungetc`會傳回**traits_type::**[eof](../standard-library/basic-ios-class.md#eof)，函式呼叫[setstate](../standard-library/basic-ios-class.md#setstate)(`badbit`). 在任何情況下，它都會傳回 **\*this**。

如需 `unget` 何以失敗的資訊，請參閱 [basic_streambuf::sungetc](../standard-library/basic-streambuf-class.md#sungetc)。

### <a name="example"></a>範例

```cpp
// basic_istream_unget.cpp
// compile with: /EHsc
#include <iostream>
using namespace std;

int main( )
{
   char c[10], c2;

   cout << "Type 'abc': ";
   c2 = cin.get( );
   cin.unget( );
   cin.getline( &c[0], 9 );
   cout << c << endl;
}
```

```Input
abc
```

```Output
Type 'abc': abc
abc
```

## <a name="see-also"></a>另請參閱

[C++ 標準程式庫中的執行緒安全](../standard-library/thread-safety-in-the-cpp-standard-library.md)<br/>
[iostream 程式設計](../standard-library/iostream-programming.md)<br/>
[iostream 慣例](../standard-library/iostreams-conventions.md)<br/>
