---
title: network_link_registry 類別
ms.date: 11/04/2016
f1_keywords:
- network_link_registry
- AGENTS/concurrency::network_link_registry
- AGENTS/concurrency::network_link_registry::add
- AGENTS/concurrency::network_link_registry::begin
- AGENTS/concurrency::network_link_registry::contains
- AGENTS/concurrency::network_link_registry::count
- AGENTS/concurrency::network_link_registry::remove
helpviewer_keywords:
- network_link_registry class
ms.assetid: 3e7b4097-09f1-4252-964e-b15b8f7f7fc6
ms.openlocfilehash: 2537ed857651b5210b104a270b3d827246b8339a
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62385228"
---
# <a name="networklinkregistry-class"></a>network_link_registry 類別

`network_link_registry` 抽象基底類別會管理來源和目標區塊之間的連結。

## <a name="syntax"></a>語法

```
template<class _Block>
class network_link_registry;
```

#### <a name="parameters"></a>參數

*_Block*<br/>
區塊資料類型儲存在`network_link_registry`。

## <a name="members"></a>成員

### <a name="public-typedefs"></a>公用 Typedefs

|名稱|描述|
|----------|-----------------|
|`const_pointer`|此類型提供的指標`const`中的項目`network_link_registry`物件。|
|`const_reference`|提供的參考型別`const`項目儲存在`network_link_registry`供讀取和執行 const 作業的物件。|
|`iterator`|類型，提供迭代器可以讀取或修改任何項目中的`network_link_registry`物件。|
|`type`|此類型代表儲存在區塊型別`network_link_registry`物件。|

### <a name="public-methods"></a>公用方法

|名稱|描述|
|----------|-----------------|
|[add](#add)|當在衍生類別中覆寫時，將加入的連結`network_link_registry`物件。|
|[begin](#begin)|當在衍生類別中覆寫時，會傳回迭代器中的第一個項目`network_link_registry`物件。|
|[contains](#contains)|當在衍生類別中覆寫時，會搜尋`network_link_registry`物件指定的區塊。|
|[count](#count)|當在衍生類別中覆寫時，會傳回中的項目數`network_link_registry`物件。|
|[remove](#remove)|當在衍生類別中覆寫時，會移除指定的區塊，從`network_link_registry`物件。|

## <a name="remarks"></a>備註

`network link registry`並不安全的並行存取。

## <a name="inheritance-hierarchy"></a>繼承階層

`network_link_registry`

## <a name="requirements"></a>需求

**標頭：** agents.h

**命名空間：** concurrency

##  <a name="add"></a> add

當在衍生類別中覆寫時，將加入的連結`network_link_registry`物件。

```
virtual void add(_EType _Link) = 0;
```

### <a name="parameters"></a>參數

*_Link*<br/>
要加入的區塊的指標。

##  <a name="begin"></a> begin

當在衍生類別中覆寫時，會傳回迭代器中的第一個項目`network_link_registry`物件。

```
virtual iterator begin() = 0;
```

### <a name="return-value"></a>傳回值

迭代器中的第一個項目定址`network_link_registry`物件。

### <a name="remarks"></a>備註

迭代器的結束狀態會由`NULL`連結。

##  <a name="contains"></a> 包含

當在衍生類別中覆寫時，會搜尋`network_link_registry`物件指定的區塊。

```
virtual bool contains(_EType _Link) = 0;
```

### <a name="parameters"></a>參數

*_Link*<br/>
在搜尋區塊的指標`network_link_registry`物件。

### <a name="return-value"></a>傳回值

**真**找不到此區塊，如果**false**否則。

##  <a name="count"></a> count

當在衍生類別中覆寫時，會傳回中的項目數`network_link_registry`物件。

```
virtual size_t count() = 0;
```

### <a name="return-value"></a>傳回值

中的項目數`network_link_registry`物件。

##  <a name="remove"></a> 移除

當在衍生類別中覆寫時，會移除指定的區塊，從`network_link_registry`物件。

```
virtual bool remove(_EType _Link) = 0;
```

### <a name="parameters"></a>參數

*_Link*<br/>
要移除，如果區塊的指標找到。

### <a name="return-value"></a>傳回值

**真**如果連結已找到並移除**false**否則。

## <a name="see-also"></a>另請參閱

[concurrency 命名空間](concurrency-namespace.md)<br/>
[single_link_registry 類別](single-link-registry-class.md)<br/>
[multi_link_registry 類別](multi-link-registry-class.md)
