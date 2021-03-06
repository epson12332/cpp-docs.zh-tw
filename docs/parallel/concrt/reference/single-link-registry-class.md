---
title: single_link_registry 類別
ms.date: 11/04/2016
f1_keywords:
- single_link_registry
- AGENTS/concurrency::single_link_registry
- AGENTS/concurrency::single_link_registry::single_link_registry
- AGENTS/concurrency::single_link_registry::add
- AGENTS/concurrency::single_link_registry::begin
- AGENTS/concurrency::single_link_registry::contains
- AGENTS/concurrency::single_link_registry::count
- AGENTS/concurrency::single_link_registry::remove
helpviewer_keywords:
- single_link_registry class
ms.assetid: 09540a4e-c34e-4ff9-af49-21b8612b6ab3
ms.openlocfilehash: 20032f393964c8919d2c1a49ec8545400cd9e392
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62160063"
---
# <a name="singlelinkregistry-class"></a>single_link_registry 類別

`single_link_registry` 物件是只管理單一來源或目標區塊的 `network_link_registry`。

## <a name="syntax"></a>語法

```
template<class _Block>
class single_link_registry : public network_link_registry<_Block>;
```

#### <a name="parameters"></a>參數

*_Block*<br/>
區塊資料類型儲存在`single_link_registry`物件。

## <a name="members"></a>成員

### <a name="public-constructors"></a>公用建構函式

|名稱|描述|
|----------|-----------------|
|[single_link_registry](#ctor)|建構 `single_link_registry` 物件。|
|[~ single_link_registry 解構函式](#dtor)|終結`single_link_registry`物件。|

### <a name="public-methods"></a>公用方法

|名稱|描述|
|----------|-----------------|
|[add](#add)|新增連結`single_link_registry`物件。 (覆寫[network_link_registry:: add](network-link-registry-class.md#add)。)|
|[begin](#begin)|傳回迭代器中的第一個項目`single_link_registry`物件。 (覆寫[network_link_registry:: begin](network-link-registry-class.md#begin)。)|
|[contains](#contains)|搜尋`single_link_registry`物件指定的區塊。 (覆寫[network_link_registry:: contains](network-link-registry-class.md#contains)。)|
|[count](#count)|計算中的項目數`single_link_registry`物件。 (覆寫[network_link_registry:: count](network-link-registry-class.md#count)。)|
|[remove](#remove)|移除連結，以從`single_link_registry`物件。 (覆寫[network_link_registry:: remove](network-link-registry-class.md#remove)。)|

## <a name="inheritance-hierarchy"></a>繼承階層

[network_link_registry](network-link-registry-class.md)

`single_link_registry`

## <a name="requirements"></a>需求

**標頭：** agents.h

**命名空間：** concurrency

##  <a name="add"></a> add

新增連結`single_link_registry`物件。

```
virtual void add(_EType _Link);
```

### <a name="parameters"></a>參數

*_Link*<br/>
要加入的區塊的指標。

### <a name="remarks"></a>備註

方法會擲回[invalid_link_target](invalid-link-target-class.md)例外狀況，如果此登錄中已經有一個連結。

##  <a name="begin"></a> begin

傳回迭代器中的第一個項目`single_link_registry`物件。

```
virtual iterator begin();
```

### <a name="return-value"></a>傳回值

迭代器中的第一個項目定址`single_link_registry`物件。

### <a name="remarks"></a>備註

結束狀態會表示`NULL`連結。

##  <a name="contains"></a> 包含

搜尋`single_link_registry`物件指定的區塊。

```
virtual bool contains(_EType _Link);
```

### <a name="parameters"></a>參數

*_Link*<br/>
要搜尋中的區塊的指標`single_link_registry`物件。

### <a name="return-value"></a>傳回值

**真**找不到連結，如果**false**否則。

##  <a name="count"></a> count

計算中的項目數`single_link_registry`物件。

```
virtual size_t count();
```

### <a name="return-value"></a>傳回值

中的項目數`single_link_registry`物件。

##  <a name="remove"></a> 移除

移除連結，以從`single_link_registry`物件。

```
virtual bool remove(_EType _Link);
```

### <a name="parameters"></a>參數

*_Link*<br/>
要移除，如果區塊的指標找到。

### <a name="return-value"></a>傳回值

**真**如果連結已找到並移除**false**否則。

##  <a name="ctor"></a> single_link_registry

建構 `single_link_registry` 物件。

```
single_link_registry();
```

##  <a name="dtor"></a> ~single_link_registry

終結`single_link_registry`物件。

```
virtual ~single_link_registry();
```

### <a name="remarks"></a>備註

方法會擲回[invalid_operation](invalid-operation-class.md)連結移除之前，它會呼叫例外狀況。

## <a name="see-also"></a>另請參閱

[concurrency 命名空間](concurrency-namespace.md)<br/>
[multi_link_registry 類別](multi-link-registry-class.md)
