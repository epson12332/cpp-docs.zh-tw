---
title: packaged_task 類別
ms.date: 11/04/2016
f1_keywords:
- future/std::packaged_task
- future/std::packaged_task::packaged_task
- future/std::packaged_task::get_future
- future/std::packaged_task::make_ready_at_thread_exit
- future/std::packaged_task::reset
- future/std::packaged_task::swap
- future/std::packaged_task::valid
- future/std::packaged_task::operator()
- future/std::packaged_task::operator bool
ms.assetid: 0a72cbe3-f22a-4bfe-8e50-dcb268c98780
helpviewer_keywords:
- std::packaged_task [C++]
- std::packaged_task [C++], packaged_task
- std::packaged_task [C++], get_future
- std::packaged_task [C++], make_ready_at_thread_exit
- std::packaged_task [C++], reset
- std::packaged_task [C++], swap
- std::packaged_task [C++], valid
ms.openlocfilehash: e759b1bc8cb47c5c943f29545e3b03ee535f3df7
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62370667"
---
# <a name="packagedtask-class"></a>packaged_task 類別

描述「非同步提供者」，它是呼叫簽章為 `Ty(ArgTypes...)` 的呼叫包裝函式。 除了可能的結果外，它的「相關聯非同步狀態」會保存其可呼叫物件的複本。

## <a name="syntax"></a>語法

```cpp
template <class>
class packaged_task;
```

## <a name="members"></a>成員

### <a name="public-constructors"></a>公用建構函式

|名稱|描述|
|----------|-----------------|
|[packaged_task](#packaged_task)|建構 `packaged_task` 物件。|
|[packaged_task::~packaged_task 解構函式](#dtorpackaged_task_destructor)|終結 `packaged_task` 物件。|

### <a name="public-methods"></a>公用方法

|名稱|描述|
|----------|-----------------|
|[get_future](#get_future)|傳回 [future](../standard-library/future-class.md) 物件，該物件具有相同的相關聯非同步狀態。|
|[make_ready_at_thread_exit](#make_ready_at_thread_exit)|呼叫儲存在相關聯非同步狀態中的可呼叫物件，並以不可部分完成的方式儲存傳回的值。|
|[reset](#reset)|取代相關聯的非同步狀態。|
|[swap](#swap)|交換指定之物件的相關聯非同步狀態。|
|[valid](#valid)|指定物件是否具有相關的非同步狀態。|

### <a name="public-operators"></a>公用運算子

|名稱|描述|
|----------|-----------------|
|[packaged_task::operator=](#op_eq)|從指定的物件轉移相關聯的非同步狀態。|
|[packaged_task::operator()](#op_call)|呼叫儲存在相關聯非同步狀態中的可呼叫物件，以不可部分完成的方式儲存傳回的值，並將狀態設定為「就緒」。|
|[packaged_task::operator bool](#op_bool)|指定物件是否具有相關聯的非同步狀態。|

## <a name="requirements"></a>需求

**標頭：** \<未來 >

**命名空間：** std

## <a name="get_future"></a>  packaged_task::get_future

傳回類型 `future<Ty>` 的物件，該物件具有相同的「相關聯非同步狀態」。

```cpp
future<Ty> get_future();
```

### <a name="remarks"></a>備註

如果 `packaged_task` 物件沒有相關聯的非同步狀態，則這個方法會擲回含有 `no_state` 錯誤碼的 [future_error](../standard-library/future-error-class.md)。

如果已經針對具有同一個相關聯的非同步狀態的 `packaged_task` 物件呼叫這個方法，方法會擲回具有錯誤碼 `future_already_retrieved` 的 `future_error`。

## <a name="make_ready_at_thread_exit"></a>  packaged_task::make_ready_at_thread_exit

呼叫儲存在「相關聯非同步狀態」中的可呼叫物件，並以不可部分完成的方式儲存傳回的值。

```cpp
void make_ready_at_thread_exit(ArgTypes... args);
```

### <a name="remarks"></a>備註

如果 `packaged_task` 物件沒有相關聯的非同步狀態，則這個方法會擲回含有 `no_state` 錯誤碼的 [future_error](../standard-library/future-error-class.md)。

如果已經針對具有同一個相關聯的非同步狀態的 `packaged_task` 物件呼叫這個方法或 [make_ready_at_thread_exit](#make_ready_at_thread_exit)，方法會擲回具有錯誤碼 `promise_already_satisfied` 的 `future_error`。

否則，此運算子會呼叫 `INVOKE(fn, args..., Ty)`，其中 *fn* 是儲存在相關聯非同步狀態中的可呼叫物件。 任何傳回的值會以不可部分完成的方式儲存為相關聯非同步狀態的傳回結果。

與 [packaged_task::operator()](#op_call) 相反，除非呼叫之執行緒中所有的執行緒區域物件皆已終結，否則相關聯的非同步狀態不會設定為 `ready`。 通常，除非呼叫的執行緒結束，否則被封鎖於相關聯非同步狀態的執行緒不會解除封鎖。

## <a name="op_eq"></a>  packaged_task::operator=

從指定的物件轉移「相關聯的非同步狀態」。

```cpp
packaged_task& operator=(packaged_task&& Right);
```

### <a name="parameters"></a>參數

*右邊*<br/>
`packaged_task` 物件。

### <a name="return-value"></a>傳回值

`*this`

### <a name="remarks"></a>備註

作業之後，*右*不再具有相關聯的非同步狀態。

## <a name="op_call"></a>  packaged_task::operator()

呼叫儲存在「相關聯非同步狀態」中的可呼叫物件，以不可部分完成的方式儲存傳回的值，並將狀態設定為「就緒」。

```cpp
void operator()(ArgTypes... args);
```

### <a name="remarks"></a>備註

如果 `packaged_task` 物件沒有相關聯的非同步狀態，則這個方法會擲回含有 `no_state` 錯誤碼的 [future_error](../standard-library/future-error-class.md)。

如果已經針對具有同一個相關聯的非同步狀態的 `packaged_task` 物件呼叫這個方法或 [make_ready_at_thread_exit](#make_ready_at_thread_exit)，方法會擲回具有錯誤碼 `promise_already_satisfied` 的 `future_error`。

否則，此運算子會呼叫 `INVOKE(fn, args..., Ty)`，其中 *fn* 是儲存在相關聯非同步狀態中的可呼叫物件。 任何傳回的值會以不可部分完成的方式儲存為相關聯非同步狀態的傳回結果，並將狀態設為就緒。 如此一來，封鎖於相關聯非同步狀態上的所有執行緒都會解除封鎖。

## <a name="op_bool"></a>  packaged_task::operator bool

指定物件是否具有 `associated asynchronous state`。

```cpp
operator bool() const noexcept;
```

### <a name="return-value"></a>傳回值

**true**如果物件有相關聯的非同步狀態; 否則**false**。

## <a name="packaged_task"></a>  packaged_task::packaged_task 建構函式

建構 `packaged_task` 物件。

```cpp
packaged_task() noexcept;
packaged_task(packaged_task&& Right) noexcept;
template <class Fn>
   explicit packaged_task(Fn&& fn);

template <class Fn, class Alloc>
   explicit packaged_task(
      allocator_arg_t, const Alloc& alloc, Fn&& fn);
```

### <a name="parameters"></a>參數

*右邊*<br/>
`packaged_task` 物件。

*alloc*<br/>
記憶體配置器。 如需詳細資訊，請參閱 [\<allocators>](../standard-library/allocators-header.md)。

*fn*<br/>
函式物件。

### <a name="remarks"></a>備註

第一個建構函式會建構沒有「相關聯的非同步狀態」的 `packaged_task` 物件。

第二個建構函式建構`packaged_task`物件，並將轉移相關聯的非同步狀態，從*右*。 作業之後，*右*不再具有相關聯的非同步狀態。

第三個建構函式建構`packaged_task`物件具有一份*fn*儲存在其相關聯的非同步狀態。

第四個建構函式建構`packaged_task`物件具有一份*fn*儲存在其相關聯的非同步狀態，並使用`alloc`進行記憶體配置。

## <a name="dtorpackaged_task_destructor"></a>  packaged_task::~packaged_task 解構函式

終結 `packaged_task` 物件。

```cpp
~packaged_task();
```

### <a name="remarks"></a>備註

如果「相關聯的非同步狀態」不是「就緒」，解構函式會將具有錯誤碼 `broken_promise` 的 [future_error](../standard-library/future-error-class.md) 例外狀況在相關聯的非同步狀態中儲存為結果，且封鎖於相關聯非同步狀態上的所有執行緒都會解除封鎖。

## <a name="reset"></a>  packaged_task::reset

使用新的「相關聯非同步狀態」來取代現有的相關聯非同步狀態。

```cpp
void reset();
```

### <a name="remarks"></a>備註

實際上，這個方法會執行 `*this = packaged_task(move(fn))`，其中 *fn* 是儲存於此物件之相關聯非同步狀態中的函式物件。 因此，會清除物件的狀態，並且可以像在新建構的物件上一樣地呼叫 [get_future](#get_future)、[operator()](#op_call) 和 [make_ready_at_thread_exit](#make_ready_at_thread_exit)。

## <a name="swap"></a>  packaged_task::swap

交換指定之物件的相關聯非同步狀態。

```cpp
void swap(packaged_task& Right) noexcept;
```

### <a name="parameters"></a>參數

*右邊*<br/>
`packaged_task` 物件。

## <a name="valid"></a>  packaged_task::valid

指定物件是否具有 `associated asynchronous state`。

```cpp
bool valid() const;
```

### <a name="return-value"></a>傳回值

**true**如果物件有相關聯的非同步狀態; 否則**false**。

## <a name="see-also"></a>另請參閱

[標頭檔參考](../standard-library/cpp-standard-library-header-files.md)<br/>
[\<future>](../standard-library/future.md)<br/>
