---
title: CLocalHeap 類別
ms.date: 11/04/2016
f1_keywords:
- CLocalHeap
- ATLMEM/ATL::CLocalHeap
- ATLMEM/ATL::CLocalHeap::Allocate
- ATLMEM/ATL::CLocalHeap::Free
- ATLMEM/ATL::CLocalHeap::GetSize
- ATLMEM/ATL::CLocalHeap::Reallocate
helpviewer_keywords:
- CLocalHeap class
ms.assetid: 1ffa87a5-5fc8-4f8d-8809-58e87e963bd2
ms.openlocfilehash: 53288bea8a50f62437eab4dd81d5d816abf78f44
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62258828"
---
# <a name="clocalheap-class"></a>CLocalHeap 類別

這個類別會實作[IAtlMemMgr](../../atl/reference/iatlmemmgr-class.md)使用 Win32 本機堆積函式。

> [!IMPORTANT]
>  此類別和其成員不能在 Windows 執行階段中執行的應用程式。

## <a name="syntax"></a>語法

```
class CLocalHeap : public IAtlMemMgr
```

## <a name="members"></a>成員

### <a name="public-methods"></a>公用方法

|名稱|描述|
|----------|-----------------|
|[CLocalHeap::Allocate](#allocate)|呼叫這個方法來配置記憶體區塊。|
|[CLocalHeap::Free](#free)|呼叫這個方法來釋放此記憶體管理員所配置的記憶體區塊。|
|[CLocalHeap::GetSize](#getsize)|呼叫這個方法，以取得此記憶體管理員所配置的記憶體區塊配置的大小。|
|[CLocalHeap::Reallocate](#reallocate)|呼叫這個方法來重新配置此記憶體管理員所配置的記憶體。|

## <a name="remarks"></a>備註

`CLocalHeap` 實作使用 Win32 本機堆積函式的記憶體配置函式。

> [!NOTE]
>  本機堆積函式會低於其他記憶體管理函式，並不會提供許多功能。 因此，應該使用新的應用程式[堆積函式](/windows/desktop/Memory/heap-functions)。 中會有這些[CWin32Heap](../../atl/reference/cwin32heap-class.md)類別。

## <a name="example"></a>範例

範例，請參閱[IAtlMemMgr](../../atl/reference/iatlmemmgr-class.md)。

## <a name="inheritance-hierarchy"></a>繼承階層

`IAtlMemMgr`

`CLocalHeap`

## <a name="requirements"></a>需求

**標頭：** atlmem.h

##  <a name="allocate"></a>  CLocalHeap::Allocate

呼叫這個方法來配置記憶體區塊。

```
virtual __declspec(allocator) void* Allocate(size_t nBytes) throw();
```

### <a name="parameters"></a>參數

*nBytes*<br/>
在新記憶體區塊中要求的位元組數目。

### <a name="return-value"></a>傳回值

傳回新配置記憶體區塊開頭的指標。

### <a name="remarks"></a>備註

呼叫[clocalheap:: Free](#free)或是[clocalheap:: Reallocate](#reallocate)釋放這個方法所配置的記憶體。

使用實作[LocalAlloc](/windows/desktop/api/winbase/nf-winbase-localalloc)搭配 LMEM_FIXED 旗標參數。

##  <a name="free"></a>  Clocalheap:: Free

呼叫這個方法來釋放此記憶體管理員所配置的記憶體區塊。

```
virtual void Free(void* p) throw();
```

### <a name="parameters"></a>參數

*p*<br/>
此記憶體管理員先前所配置之記憶體的指標。 NULL 是有效的值，且沒有任何作用。

### <a name="remarks"></a>備註

使用實作[LocalFree](/windows/desktop/api/winbase/nf-winbase-localfree)。

##  <a name="getsize"></a>  CLocalHeap::GetSize

呼叫這個方法，以取得此記憶體管理員所配置的記憶體區塊配置的大小。

```
virtual size_t GetSize(void* p) throw();
```

### <a name="parameters"></a>參數

*p*<br/>
此記憶體管理員先前所配置之記憶體的指標。

### <a name="return-value"></a>傳回值

傳回配置的記憶體區塊大小，以位元組為單位。

### <a name="remarks"></a>備註

使用實作[LocalSize](/windows/desktop/api/winbase/nf-winbase-localsize)。

##  <a name="reallocate"></a>  CLocalHeap::Reallocate

呼叫這個方法來重新配置此記憶體管理員所配置的記憶體。

```
virtual __declspec(allocator) void* Reallocate(void* p, size_t nBytes) throw();
```

### <a name="parameters"></a>參數

*p*<br/>
此記憶體管理員先前所配置之記憶體的指標。

*nBytes*<br/>
在新記憶體區塊中要求的位元組數目。

### <a name="return-value"></a>傳回值

傳回新配置記憶體區塊開頭的指標。

### <a name="remarks"></a>備註

呼叫[clocalheap:: Free](#free)釋放這個方法所配置的記憶體。

使用實作[LocalReAlloc](/windows/desktop/api/winbase/nf-winbase-localrealloc)。

## <a name="see-also"></a>另請參閱

[類別概觀](../../atl/atl-class-overview.md)<br/>
[CComHeap 類別](../../atl/reference/ccomheap-class.md)<br/>
[CWin32Heap 類別](../../atl/reference/cwin32heap-class.md)<br/>
[CGlobalHeap 類別](../../atl/reference/cglobalheap-class.md)<br/>
[CCRTHeap 類別](../../atl/reference/ccrtheap-class.md)<br/>
[IAtlMemMgr 類別](../../atl/reference/iatlmemmgr-class.md)
