---
title: strstream 類別
ms.date: 11/04/2016
f1_keywords:
- strstream/std::strstream::freeze
- strstream/std::strstream::pcount
- strstream/std::strstream::rdbuf
- strstream/std::strstream::str
helpviewer_keywords:
- std::strstream [C++], freeze
- std::strstream [C++], pcount
- std::strstream [C++], rdbuf
- std::strstream [C++], str
ms.assetid: 63f3be31-9e36-42b1-9715-a474a5997e2a
ms.openlocfilehash: 9494f7ee2508df1971d56c94b929a7212bedb254
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62412289"
---
# <a name="strstream-class"></a>strstream 類別

描述一個物件，該物件可控制如何使用類別 [strstreambuf](../standard-library/strstreambuf-class.md) 的資料流緩衝區來插入及擷取項目和編碼物件。

## <a name="syntax"></a>語法

```cpp
class strstream : public iostream
```

## <a name="remarks"></a>備註

此物件會儲存類別 `strstreambuf` 的物件。

> [!NOTE]
> 這個類別已被取代。 請考慮改用 [stringstream](../standard-library/sstream-typedefs.md#stringstream) 或 [wstringstream](../standard-library/sstream-typedefs.md#wstringstream)。

### <a name="constructors"></a>建構函式

|建構函式|描述|
|-|-|
|[strstream](#strstream)|建構類型 `strstream` 的物件。|

### <a name="member-functions"></a>成員函式

|成員函式|描述|
|-|-|
|[freeze](#freeze)|導致資料流緩衝區無法在資料流緩衝區作業中使用。|
|[pcount](#pcount)|傳回寫入至受控制序列的元素計數。|
|[rdbuf](#rdbuf)|將指標傳回至資料流的相關 `strstreambuf` 物件。|
|[str](#str)|呼叫 [freeze](../standard-library/strstreambuf-class.md#freeze)，然後傳回指向受控制序列開頭的指標。|

## <a name="requirements"></a>需求

**標頭：**\<strstream>

**命名空間：** std

## <a name="freeze"></a>  strstream::freeze

導致資料流緩衝區無法在資料流緩衝區作業中使用。

```cpp
void freeze(bool _Freezeit = true);
```

### <a name="parameters"></a>參數

*_Freezeit*<br/>
A **bool**指出您是否要凍結的資料流。

### <a name="remarks"></a>備註

成員函式會呼叫 [rdbuf](#rdbuf) -> [freeze](../standard-library/strstreambuf-class.md#freeze)(_ *Freezeit*)。

### <a name="example"></a>範例

請參閱[strstreambuf:: freeze](../standard-library/strstreambuf-class.md#freeze)如需範例，會使用`freeze`。

## <a name="pcount"></a>  strstream::pcount

傳回寫入至受控制序列的元素計數。

```cpp
streamsize pcount() const;
```

### <a name="return-value"></a>傳回值

寫入受控制序列的項目數。

### <a name="remarks"></a>備註

成員函式會傳回 [rdbuf](#rdbuf) -> [pcount](../standard-library/strstreambuf-class.md#pcount)。

### <a name="example"></a>範例

如需使用 pcount 的範例，請參閱 [strstreambuf::pcount](../standard-library/strstreambuf-class.md#pcount)。

## <a name="rdbuf"></a>  strstream::rdbuf

傳回指向資料流相關 strstreambuf 物件的指標。

```cpp
strstreambuf *rdbuf() const
```

### <a name="return-value"></a>傳回值

指向資料流相關 strstreambuf 物件的指標。

### <a name="remarks"></a>備註

此成員函式會傳回類型的預存資料流緩衝區的位址`pointer`要[strstreambuf](../standard-library/strstreambuf-class.md)。

### <a name="example"></a>範例

如需使用 `rdbuf` 的範例，請參閱 [strstreambuf::pcount](../standard-library/strstreambuf-class.md#pcount)。

## <a name="str"></a>  strstream::str

呼叫 [freeze](../standard-library/strstreambuf-class.md#freeze)，然後傳回指向受控制序列開頭的指標。

```cpp
char *str();
```

### <a name="return-value"></a>傳回值

指向受控制序列開頭的指標。

### <a name="remarks"></a>備註

成員函式會傳回 [rdbuf](#rdbuf) -> [str](../standard-library/strstreambuf-class.md#str)。

### <a name="example"></a>範例

請參閱[strstreambuf:: str](../standard-library/strstreambuf-class.md#str)如需範例，會使用`str`。

## <a name="strstream"></a>  strstream::strstream

建構類型 `strstream` 的物件。

```cpp
strstream();

strstream(char* ptr,
    streamsize count,
    ios_base::openmode _Mode = ios_base::in | ios_base::out);
```

### <a name="parameters"></a>參數

*count*<br/>
緩衝區的大小。

*_Mode*<br/>
緩衝區的輸入和輸出模式。 如需詳細資訊，請參閱 [ios_base::openmode](../standard-library/ios-base-class.md#openmode)。

*ptr*<br/>
緩衝區。

### <a name="remarks"></a>備註

這兩個建構函式初始化基底類別，藉由呼叫[streambuf](../standard-library/streambuf-typedefs.md#streambuf)( **sb**)，其中`sb`是類別的預存的物件[strstreambuf](../standard-library/strstreambuf-class.md)。 第一個建構函式也會初始化`sb`藉由呼叫[strstreambuf](../standard-library/strstreambuf-class.md#strstreambuf)。 第二個建構函式會使用下列其中一種方法來初始化基底類別：

- 如果`_Mode`  &  **ios_base:: app**= = 0，然後*ptr*必須指定陣列的第一個項目`count`項目，以及建構函式呼叫`strstreambuf`( `ptr`, `count`, `ptr`).

- 否則，請*ptr*必須指定 count 項目之陣列包含 C 字串的第一個項目所指定的第一個元素*ptr*，並建構函式呼叫`strstreambuf`( `ptr`, `count`, `ptr` + `strlen`( `ptr`) ).

## <a name="see-also"></a>另請參閱

[iostream](../standard-library/istream-typedefs.md#iostream)<br/>
[C++ 標準程式庫中的執行緒安全](../standard-library/thread-safety-in-the-cpp-standard-library.md)<br/>
[iostream 程式設計](../standard-library/iostream-programming.md)<br/>
[iostream 慣例](../standard-library/iostreams-conventions.md)<br/>
