---
title: SyncLockT 類別
ms.date: 10/03/2018
ms.topic: reference
f1_keywords:
- corewrappers/Microsoft::WRL::Wrappers::Details::SyncLockT
- corewrappers/Microsoft::WRL::Wrappers::Details::SyncLockT::IsLocked
- corewrappers/Microsoft::WRL::Wrappers::Details::SyncLockT::sync_
- corewrappers/Microsoft::WRL::Wrappers::Details::SyncLockT::SyncLockT
- corewrappers/Microsoft::WRL::Wrappers::Details::SyncLockT::~SyncLockT
- corewrappers/Microsoft::WRL::Wrappers::Details::SyncLockT::Unlock
helpviewer_keywords:
- Microsoft::WRL::Wrappers::Details::SyncLockT class
- Microsoft::WRL::Wrappers::Details::SyncLockT::IsLocked method
- Microsoft::WRL::Wrappers::Details::SyncLockT::sync_ data member
- Microsoft::WRL::Wrappers::Details::SyncLockT::SyncLockT, constructor
- Microsoft::WRL::Wrappers::Details::SyncLockT::~SyncLockT, destructor
- Microsoft::WRL::Wrappers::Details::SyncLockT::Unlock method
ms.assetid: a967f6f7-3555-43d1-b210-2bb65d63d15e
ms.openlocfilehash: d27e6ba8601d0e822113bf3a4a65269c89437271
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62398156"
---
# <a name="synclockt-class"></a>SyncLockT 類別

支援 WRL 結構，而且不是直接從您的程式碼使用。

## <a name="syntax"></a>語法

```cpp
template <typename SyncTraits>
class SyncLockT;
```

### <a name="parameters"></a>參數

*SyncTraits*<br/>
可以取得資源的擁有權類型。

## <a name="remarks"></a>備註

代表一種類型，可以採取獨佔或共用資源的擁有權。

`SyncLockT`會使用類別，例如，以協助實作[SRWLock](srwlock-class.md)類別。

## <a name="members"></a>成員

### <a name="public-constructors"></a>公用建構函式

名稱                                      | 描述
----------------------------------------- | ----------------------------------------------------
[SyncLockT::SyncLockT](#synclockt)        | 初始化 `SyncLockT` 類別的新執行個體。
[SyncLockT::~SyncLockT](#tilde-synclockt) | 取消初始化的執行個體`SyncLockT`類別。

### <a name="protected-constructors"></a>受保護的建構函式

名稱                               | 描述
---------------------------------- | ----------------------------------------------------
[SyncLockT::SyncLockT](#synclockt) | 初始化 `SyncLockT` 類別的新執行個體。

### <a name="public-methods"></a>公用方法

名稱                             | 描述
-------------------------------- | --------------------------------------------------------------------------------------------------------------
[SyncLockT::IsLocked](#islocked) | 指出是否目前`SyncLockT`物件擁有資源，也就是，則`SyncLockT`物件*鎖定*。
[SyncLockT::Unlock](#unlock)     | 目前所持有的資源的控制權`SyncLockT`物件，如果有的話。

### <a name="protected-data-members"></a>受保護的資料成員

名稱                      | 描述
------------------------- | -------------------------------------------------------------------
[SyncLockT::sync_](#sync) | 保存所表示之基礎資源`SyncLockT`類別。

## <a name="inheritance-hierarchy"></a>繼承階層

`SyncLockT`

## <a name="requirements"></a>需求

**標頭：** corewrappers.h

**命名空間：** Microsoft::WRL::Wrappers::Details

## <a name="tilde-synclockt"></a>SyncLockT::~SyncLockT

支援 WRL 結構，而且不是直接從您的程式碼使用。

```cpp
~SyncLockT();
```

### <a name="remarks"></a>備註

取消初始化的執行個體`SyncLockT`類別。

此解構函式也會解除鎖定的目前`SyncLockT`執行個體。

## <a name="islocked"></a>SyncLockT::IsLocked

支援 WRL 結構，而且不是直接從您的程式碼使用。

```cpp
bool IsLocked() const;
```

### <a name="return-value"></a>傳回值

**真**如果`SyncLockT`物件已鎖定，否則**false**。

### <a name="remarks"></a>備註

指出是否目前`SyncLockT`物件擁有資源，也就是，則`SyncLockT`物件*鎖定*。

## <a name="sync"></a>SyncLockT::sync_

支援 WRL 結構，而且不是直接從您的程式碼使用。

```cpp
typename SyncTraits::Type sync_;
```

### <a name="remarks"></a>備註

保存所表示之基礎資源`SyncLockT`類別。

## <a name="synclockt"></a>SyncLockT::SyncLockT

支援 WRL 結構，而且不是直接從您的程式碼使用。

```cpp
SyncLockT(
   _Inout_ SyncLockT&& other
);

explicit SyncLockT(
   typename SyncTraits::Type sync = SyncTraits::GetInvalidValue()
);
```

### <a name="parameters"></a>參數

*other*<br/>
右值參考到另一個`SyncLockT`物件。

*sync*<br/>
另一個的參考`SyncLockWithStatusT`物件。

### <a name="remarks"></a>備註

初始化 `SyncLockT` 類別的新執行個體。

第一個建構函式初始化目前`SyncLockT`物件從另一個`SyncLockT`參數所指定的物件*其他*，然後則另`SyncLockT`物件。 第二個建構函式`protected`，並初始化目前`SyncLockT`為無效狀態的物件。

## <a name="unlock"></a>SyncLockT::Unlock

支援 WRL 結構，而且不是直接從您的程式碼使用。

```cpp
void Unlock();
```

### <a name="remarks"></a>備註

目前所持有的資源的控制權`SyncLockT`物件，如果有的話。
