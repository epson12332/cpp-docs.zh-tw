---
title: Platform::SizeT 實值類別
ms.date: 12/30/2016
ms.topic: reference
f1_keywords:
- VCCORLIB/PlatformSizeT::SizeT constructor
helpviewer_keywords:
- Platform::SizeT Struct
ms.assetid: 0803612c-8ba1-430c-9b7b-1bebae88608d
ms.openlocfilehash: 7f81cb9e1fc2ef7a74cb3878c369e4d7d14e3d90
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62330130"
---
# <a name="platformsizet-value-class"></a>Platform::SizeT 實值類別

表示物件的大小。 SizeT 是不帶正負號的資料類型。

## <a name="syntax"></a>語法

```cpp
public ref class SizeT sealed : ValueType
```

### <a name="members"></a>成員

|成員|描述|
|------------|-----------------|
|[SizeT::SizeT 建構函式](#ctor)|使用指定的值，初始化類別的新執行個體。|

### <a name="requirements"></a>需求

**最低支援用戶端：** Windows 8

**最低支援伺服器：** Windows Server 2012

**命名空間：** Platform

**中繼資料：** platform.winmd

## <a name="ctor"></a>  Sizet:: Sizet 建構函式

使用指定的值來初始化 SizeT 的新執行個體。

### <a name="syntax"></a>語法

```cpp
SizeT( uint32 value1 );   SizeT( void* value2 );
```

### <a name="parameters"></a>參數

*value1*<br/>
32 位元不帶正負號的值。

*value2*<br/>
32 位元不帶正負號之值的指標。

## <a name="see-also"></a>另請參閱

[平台命名空間](../cppcx/platform-namespace-c-cx.md)
