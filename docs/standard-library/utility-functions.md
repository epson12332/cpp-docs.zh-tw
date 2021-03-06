---
title: '&lt;utility&gt; 函式'
ms.date: 11/04/2016
f1_keywords:
- utility/std::exchange
- utility/std::forward
- utility/std::make_pair
- utility/std::move
- utility/std::swap
ms.assetid: b1df38cd-3a59-4098-9c81-83342eb719a4
helpviewer_keywords:
- std::exchange [C++]
- std::forward [C++]
- std::make_pair [C++]
- std::move [C++]
- std::swap [C++]
ms.openlocfilehash: 7a061ede19c5c4c181b5fea912b9c6212c583267
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62362363"
---
# <a name="ltutilitygt-functions"></a>&lt;utility&gt; 函式

||||
|-|-|-|
|[exchange](#exchange)|[forward](#forward)|[get 函式 &lt;utility&gt;](#get)|
|[make_pair](#make_pair)|[move](#move)|[swap](#swap)|

## <a name="exchange"></a> exchange

**(C++14)** 指派新值給物件，並傳回其舊值。

```cpp
template <class T, class Other = T>
T exchange(T& val, Other&& new_val)
```

### <a name="parameters"></a>參數

*val*<br/>
將會收到 new_val 值的物件。

*new_val*<br/>
其值會複製或移動到 val 的物件。

### <a name="remarks"></a>備註

對於複雜類型，當可以移動建構函式時，`exchange` 可避免複製舊值，如果它是暫存的物件或已移動，則可避免複製新值，以及使用任何可用的轉換指派運算子接受任何類型做為新值。 Exchange 函式與 [std::swap](../standard-library/algorithm-functions.md#swap) 不同之處在於，左側的引數不會移動或複製到右側的引數。

### <a name="example"></a>範例

下列範例示範如何使用 `exchange`。 在真實世界中，`exchange` 最適用於複製高度耗費資源的大型物件：

```cpp
#include <utility>
#include <iostream>

using namespace std;

struct C
{
   int i;
   //...
};

int main()
{
   // Use brace initialization
   C c1{ 1 };
   C c2{ 2 };
   C result = exchange(c1, c2);
   cout << "The old value of c1 is: " << result.i << endl;
   cout << "The new value of c1 after exchange is: " << c1.i << endl;

   return 0;
}
```

```Output
The old value of c1 is: 1
The new value of c1 after exchange is: 2
```

## <a name="forward"></a>  forward

如果引數是右值或右值參考，有條件地將引數轉型為右值參考。 這會將引數的右值特性還原為轉送函式，以支援完美轉送。

```cpp
template <class Type>    // accepts lvalues
constexpr Type&& forward(typename remove_reference<Type>::type& Arg) noexcept

template <class Type>    // accepts everything else
constexpr Type&& forward(typename remove_reference<Type>::type&& Arg) noexcept
```

### <a name="parameters"></a>參數

|參數|描述|
|---------------|-----------------|
|*Type*|傳入值的型別*Arg*，這可能會不同的型別*Arg*。 通常由轉送函式的樣板引數所決定。|
|*引數*|要轉型的引數。|

### <a name="return-value"></a>傳回值

傳回右值參考*Arg*如果值傳入*Arg*原本是右值或右值參考，否則會傳回*Arg*而不需要修改它的型別。

### <a name="remarks"></a>備註

您必須指定明確的樣板引數呼叫 `forward`。

`forward` 不會轉送它的引數。 相反地，如果引數原本是右值或右值參考，則透過有條件地將引數轉型為右值參考，`forward` 可讓編譯器在具備所轉送引數原始類型的知識下執行多載解析。 轉送函式引數的明顯型別可能與其原始型別不同，例如當右值做為函式引數且繫結至參數名稱時，具有名稱會使其成為左值，不論值是否確實為右值。`forward` 會還原引數的右值特性。

還原引數的原始值右值特性以執行多載解析，稱為「完美轉送」。 完美轉送讓樣板函式接受任何參考類型的引數，並在正確的多載解析需要時還原它的右值特性。 透過完美轉送，您可以保存右值的移動語意，避免必須為只變更其引數參考類型的函式提供多載。

## <a name="get"></a>  get

依索引位置或依類型從 `pair` 物件取得元素。

```cpp
// get reference to element at Index in pair Pr
template <size_t Index, class T1, class T2>
constexpr tuple_element_t<Index, pair<T1, T2>>&
get(pair<T1, T2>& Pr) noexcept;

// get reference to element T1 in pair Pr
template <class T1, class T2>
constexpr T1& get(pair<T1, T2>& Pr) noexcept;

// get reference to element T2 in pair Pr
template <class T2, class T1>
constexpr T2& get(pair<T1, T2>& Pr) noexcept;

// get const reference to element at Index in pair Pr
template <size_t Index, class T1, class T2>
constexpr const tuple_element_t<Index, pair<T1, T2>>&
get(const pair<T1, T2>& Pr) noexcept;

// get const reference to element T1 in pair Pr
template <class T1, class T2>
constexpr const T1& get(const pair<T1, T2>& Pr) noexcept;

// get const reference to element T2 in pair Pr
template <class T2, class T1>
constexpr const T2& get(const pair<T1, T2>& Pr) noexcept;

// get rvalue reference to element at Index in pair Pr
template <size_t Index, class T1, class T2>
constexpr tuple_element_t<Index, pair<T1, T2>>&&
get(pair<T1, T2>&& Pr) noexcept;

// get rvalue reference to element T1 in pair Pr
template <class T1, class T2>
constexpr T1&& get(pair<T1, T2>&& Pr) noexcept;

// get rvalue reference to element T2 in pair Pr
template <class T2, class T1>
constexpr T2&& get(pair<T1, T2>&& Pr) noexcept;
```

### <a name="parameters"></a>參數

*Tuple*<br/>
指定元素的以 0 為基底的索引。

*T1*<br/>
第一個配對項目的類型。

*T2*<br/>
第二個配對項目的類型。

*pr*<br/>
要從中選取的配對。

### <a name="remarks"></a>備註

範本函式各自傳回其 `pair` 引數項目的參考。

索引的多載，如果的值*索引*是函式會傳回的 0`pr.first`如果的值*的索引*為函式會傳回的 1 `pr.second`。 類型 `RI` 是傳回元素的類型。

對於不具有索引參數的多載，要傳回的元素是由類型引數推算。 呼叫`get<T>(Tuple)`會產生編譯器錯誤，如果*pr*包含多於或少於一個項目的 t 型別。

### <a name="example"></a>範例

```cpp
#include <utility>
#include <iostream>
using namespace std;
int main()
{

    typedef pair<int, double> MyPair;

    MyPair c0(9, 3.14);

    // get elements by index
    cout << " " << get<0>(c0);
    cout << " " << get<1>(c0) << endl;

    // get elements by type (C++14)
    MyPair c1(1, 0.27);
    cout << " " << get<int>(c1);
    cout << " " << get<double>(c1) << endl;

    /*
    Output:
    9 3.14
    1 0.27
    */

}
```

## <a name="make_pair"></a>  make_pair

樣板函式，可用來建構 `pair` 類型物件，其中元件類型是根據做為參數傳遞的資料類型自動選擇。

```cpp
template <class T, class U>
pair<T, U> make_pair(T& Val1, U& Val2);

template <class T, class U>
pair<T, U> make_pair(T& Val1, U&& Val2);

template <class T, class U>
pair<T, U> make_pair(T&& Val1, U& Val2);

template <class T, class U>
pair<T, U> make_pair(T&& Val1, U&& Val2);
```

### <a name="parameters"></a>參數

*Val1*<br/>
值，初始化 `pair` 的第一個項目。

*Val2*<br/>
值，初始化 `pair` 的第二個項目。

### <a name="return-value"></a>傳回值

建構的 pair 物件：`pair`< `T`, `U`>( `Val1`, `Val2`)。

### <a name="remarks"></a>備註

`make_pair` 會將 [reference_wrapper 類別](../standard-library/reference-wrapper-class.md)的型別物件轉換為參考型別，並將衰減陣列和函式轉換為指標。

在傳回的 `pair` 物件，`T` 的判斷方式如下:

- 如果輸入類型 `T` 是 `reference_wrapper<X>`，傳回的類型 `T` 是 `X&`。

- 否則，傳回的類型 `T` 為 `decay<T>::type`。 如果不支援 [decay 類別](../standard-library/decay-class.md)，傳回的型別 `T` 會與輸入型別 `T` 相同。

傳回的類型 `U` 同樣是根據輸入類型 `U` 判斷。

`make_pair` 的其中一個優點是，編譯器會自動決定所儲存物件的類型，不需要明確指定。 當您使用 `make_pair<int, int>(1, 2)` 時不要使用明確樣板引數 (例如 `make_pair`)，因為它具有不必要的詳細資訊，並新增可能導致編譯錯誤的複雜右值參考問題。 在這個範例中，正確語法是 `make_pair(1, 2)`。

`make_pair` 協助程式函式也能夠讓您傳遞兩個值給需要成對輸入參數的函式。

### <a name="example"></a>範例

如需如何使用協助程式函式 `make_pair` 宣告並初始化配對的範例，請參閱 [pair 結構](../standard-library/pair-structure.md)。

## <a name="move"></a>  move

無條件地將它的引數轉型為右值參考，因而表示如果其類型已啟用移動，就可以移動它。

```cpp
template <class Type>
constexpr typename remove_reference<Type>::type&& move(Type&& Arg) noexcept;
```

### <a name="parameters"></a>參數

|參數|描述|
|---------------|-----------------|
|*Type*|傳入的引數類型推算類型*Arg*，以及參考摺疊規則。|
|*引數*|要轉型的引數。 雖然的型別*Arg*指定為右值參考，會出現`move`也接受左值引數，因為左值參考可以繫結至右值參考。|

### <a name="return-value"></a>傳回值

`Arg` 做為右值參考，不論它的類型是否為參考類型。

### <a name="remarks"></a>備註

樣板引數*型別*不是明確地指定，但從傳入值的類型推算*Arg*。 型別*型別*根據參考摺疊規則進一步調整。

`move` 不會移動它的引數。 相反地，透過無條件地轉型其引數，這可能會是左值 — 至右值參考，它可讓編譯器後續移動，而不是複製中傳遞的值*Arg*如果其類型已啟用移動。 如果其類型未啟用移動，會複製它。

如果傳入的值*Arg*是左值 — 也就是它具有名稱，或可以取得自己的位址，當移動時，它會失效。 傳入的值未參照*Arg*依名稱或位址已移動之後。

## <a name="swap"></a>  swap

交換兩個 [pair 結構](../standard-library/pair-structure.md)物件的項目。

```cpp
template <class T, class U>
void swap(pair<T, U>& left, pair<T, U>& right);
```

### <a name="parameters"></a>參數

|參數|描述|
|---------------|-----------------|
|*left*|`pair` 類型的物件。|
|*right*|`pair` 類型的物件。|

### <a name="remarks"></a>備註

`swap` 的其中一個優點是，編譯器會自動決定所儲存物件的類型，不需要明確指定。 當您使用 `swap<int, int>(1, 2)` 時不要使用明確樣板引數 (例如 `swap`)，因為它具有不必要的詳細資訊，並新增可能導致編譯錯誤的複雜右值參考問題。

## <a name="see-also"></a>另請參閱

[\<utility>](../standard-library/utility.md)<br/>
