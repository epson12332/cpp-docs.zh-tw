---
title: __readmsr
ms.date: 11/04/2016
f1_keywords:
- __readmsr
helpviewer_keywords:
- Read Model Specific Register
- rdmsr instruction
- __readmsr intrinsic
ms.assetid: 7ab1f8e8-72cb-4ce4-817d-3e728a3c9716
ms.openlocfilehash: 2c866213c452f3b8791bf0fe031a43bb024e91fb
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62262771"
---
# <a name="readmsr"></a>__readmsr

**Microsoft 專屬**

會產生`rdmsr`的指示，它會讀取所指定的模型特定暫存`register`並傳回其值。

## <a name="syntax"></a>語法

```
__int64 __readmsr(
   int register
);
```

#### <a name="parameters"></a>參數

*register*<br/>
[in]讀取模型特定暫存器。

## <a name="return-value"></a>傳回值

指定的暫存器中的值。

## <a name="requirements"></a>需求

|內建|架構|
|---------------|------------------|
|`__readmsr`|x86、x64|

**標頭檔** \<intrin.h >

## <a name="remarks"></a>備註

此函式只適用於核心模式，且此常式僅可作為內建。

如需詳細資訊，請參閱 AMD 文件。

**結束 Microsoft 專屬**

## <a name="see-also"></a>另請參閱

[編譯器內建](../intrinsics/compiler-intrinsics.md)