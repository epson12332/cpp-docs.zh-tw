---
title: ISource 類別
ms.date: 11/04/2016
f1_keywords:
- ISource
- AGENTS/concurrency::ISource
- AGENTS/concurrency::ISource::accept
- AGENTS/concurrency::ISource::acquire_ref
- AGENTS/concurrency::ISource::consume
- AGENTS/concurrency::ISource::link_target
- AGENTS/concurrency::ISource::release
- AGENTS/concurrency::ISource::release_ref
- AGENTS/concurrency::ISource::reserve
- AGENTS/concurrency::ISource::unlink_target
- AGENTS/concurrency::ISource::unlink_targets
helpviewer_keywords:
- ISource class
ms.assetid: c7b73463-42f6-4dcc-801a-81379b12d35a
ms.openlocfilehash: 5b0704f3d666eca08bafb33f9236709478d347d8
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62301873"
---
# <a name="isource-class"></a>ISource 類別

`ISource` 類別是所有來源區塊的介面。 來源區塊會將訊息傳播至 `ITarget` 區塊。

## <a name="syntax"></a>語法

```
template<class T>
class ISource;
```

#### <a name="parameters"></a>參數

*T*<br/>
來源區塊所產生的訊息內裝載的資料型別。

## <a name="members"></a>成員

### <a name="public-typedefs"></a>公用 Typedefs

|名稱|描述|
|----------|-----------------|
|`source_type`|類型別名`T`。|

### <a name="public-constructors"></a>公用建構函式

|名稱|描述|
|----------|-----------------|
|[~ ISource 解構函式](#dtor)|終結`ISource`物件。|

### <a name="public-methods"></a>公用方法

|名稱|描述|
|----------|-----------------|
|[accept](#accept)|當在衍生類別中覆寫時，會接受一則訊息，由此`ISource`區塊中，將擁有權傳送給呼叫者。|
|[acquire_ref](#acquire_ref)|當在衍生類別中覆寫時，取得此參考計數`ISource`區塊，以防止刪除。|
|[consume](#consume)|當在衍生類別中覆寫時，會使用先前由此訊息`ISource`區塊和目標，將擁有權傳送給呼叫者已成功保留。|
|[link_target](#link_target)|當在衍生類別中覆寫時，目標區塊連結至這`ISource`區塊。|
|[release](#release)|當在衍生類別中覆寫時，釋放先前成功的訊息保留。|
|[release_ref](#release_ref)|當在衍生類別中覆寫時，釋放此參考計數`ISource`區塊。|
|[reserve](#reserve)|當在衍生類別中覆寫時，會保留先前由此訊息`ISource`區塊。|
|[unlink_target](#unlink_target)|當在衍生類別中覆寫時，取消連結的目標區塊，從這個`ISource`如果封鎖先前連結中找到。|
|[unlink_targets](#unlink_targets)|當在衍生類別中覆寫時，取消連結所有的目標區塊，從這個`ISource`區塊。|

## <a name="remarks"></a>備註

如需詳細資訊，請參閱 <<c0> [ 非同步訊息區](../../../parallel/concrt/asynchronous-message-blocks.md)。

## <a name="inheritance-hierarchy"></a>繼承階層

`ISource`

## <a name="requirements"></a>需求

**標頭：** agents.h

**命名空間：** concurrency

##  <a name="accept"></a> 接受

當在衍生類別中覆寫時，會接受一則訊息，由此`ISource`區塊中，將擁有權傳送給呼叫者。

```
virtual message<T>* accept(
    runtime_object_identity _MsgId,
    _Inout_ ITarget<T>* _PTarget) = 0;
```

### <a name="parameters"></a>參數

*_MsgId*<br/>
`runtime_object_identity`提供的`message`物件。

*_PTarget*<br/>
正在呼叫的目標區塊的指標`accept`方法。

### <a name="return-value"></a>傳回值

指標，呼叫者現在擁有的訊息。

### <a name="remarks"></a>備註

`accept`時所提供的訊息，方法由目標呼叫`ISource`區塊。 訊息指標傳回可能不同於傳遞至另一個`propagate`方法的`ITarget`封鎖，如果此來源決定要建立一份訊息。

##  <a name="acquire_ref"></a> acquire_ref

當在衍生類別中覆寫時，取得此參考計數`ISource`區塊，以防止刪除。

```
virtual void acquire_ref(_Inout_ ITarget<T>* _PTarget) = 0;
```

### <a name="parameters"></a>參數

*_PTarget*<br/>
正在呼叫這個方法的目標區塊的指標。

### <a name="remarks"></a>備註

這個方法會呼叫`ITarget`物件所要連結到這個來源期間，`link_target`方法。

##  <a name="consume"></a> 使用

當在衍生類別中覆寫時，會使用先前由此訊息`ISource`區塊和目標，將擁有權傳送給呼叫者已成功保留。

```
virtual message<T>* consume(
    runtime_object_identity _MsgId,
    _Inout_ ITarget<T>* _PTarget) = 0;
```

### <a name="parameters"></a>參數

*_MsgId*<br/>
`runtime_object_identity`的保留`message`物件。

*_PTarget*<br/>
正在呼叫的目標區塊的指標`consume`方法。

### <a name="return-value"></a>傳回值

指標`message`物件，呼叫者現在會有的擁有權。

### <a name="remarks"></a>備註

`consume`方法是類似`accept`，但必須一律加上呼叫`reserve`傳回**true**。

##  <a name="dtor"></a> ~ISource

終結`ISource`物件。

```
virtual ~ISource();
```

##  <a name="link_target"></a> link_target

當在衍生類別中覆寫時，目標區塊連結至這`ISource`區塊。

```
virtual void link_target(_Inout_ ITarget<T>* _PTarget) = 0;
```

### <a name="parameters"></a>參數

*_PTarget*<br/>
正在連結到此目標區塊的指標`ISource`區塊。

##  <a name="release"></a> 版本

當在衍生類別中覆寫時，釋放先前成功的訊息保留。

```
virtual void release(
    runtime_object_identity _MsgId,
    _Inout_ ITarget<T>* _PTarget) = 0;
```

### <a name="parameters"></a>參數

*_MsgId*<br/>
`runtime_object_identity`的保留`message`物件。

*_PTarget*<br/>
正在呼叫的目標區塊的指標`release`方法。

##  <a name="release_ref"></a> release_ref

當在衍生類別中覆寫時，釋放此參考計數`ISource`區塊。

```
virtual void release_ref(_Inout_ ITarget<T>* _PTarget) = 0;
```

### <a name="parameters"></a>參數

*_PTarget*<br/>
正在呼叫這個方法的目標區塊的指標。

### <a name="remarks"></a>備註

這個方法會呼叫`ITarget`要從這個來源取消連結的物件。 來源區塊允許釋放任何資源保留給目標區塊。

##  <a name="reserve"></a> 保留

當在衍生類別中覆寫時，會保留先前由此訊息`ISource`區塊。

```
virtual bool reserve(
    runtime_object_identity _MsgId,
    _Inout_ ITarget<T>* _PTarget) = 0;
```

### <a name="parameters"></a>參數

*_MsgId*<br/>
`runtime_object_identity`提供的`message`物件。

*_PTarget*<br/>
正在呼叫的目標區塊的指標`reserve`方法。

### <a name="return-value"></a>傳回值

**真**已成功保留訊息，如果**false**否則。 保留失敗可能有許多原因，包括：訊息已經保留或已由另一個目標接受、來源拒絕保留等等。

### <a name="remarks"></a>備註

在您呼叫後`reserve`，如果成功，您必須呼叫`consume`或`release`以便採取或分別放棄訊息，因此擁有。

##  <a name="unlink_target"></a> unlink_target

當在衍生類別中覆寫時，取消連結的目標區塊，從這個`ISource`如果封鎖先前連結中找到。

```
virtual void unlink_target(_Inout_ ITarget<T>* _PTarget) = 0;
```

### <a name="parameters"></a>參數

*_PTarget*<br/>
正在從這個連結的目標區塊的指標`ISource`區塊。

##  <a name="unlink_targets"></a> unlink_targets

當在衍生類別中覆寫時，取消連結所有的目標區塊，從這個`ISource`區塊。

```
virtual void unlink_targets() = 0;
```

## <a name="see-also"></a>另請參閱

[concurrency 命名空間](concurrency-namespace.md)<br/>
[ITarget 類別](itarget-class.md)
