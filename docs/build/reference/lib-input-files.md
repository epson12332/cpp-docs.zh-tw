---
title: LIB 輸入檔
ms.date: 11/04/2016
f1_keywords:
- Lib
helpviewer_keywords:
- input files, LIB
ms.assetid: e1236f0d-cd90-446b-b900-f311f456085c
ms.openlocfilehash: 648871464dbc99972b8ca40579046347727e81cf
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62269384"
---
# <a name="lib-input-files"></a>LIB 輸入檔

LIB 所預期的輸入的檔而定的模式，其中它在使用下, 表所示。

|模式|輸入|
|----------|-----------|
|預設值 （建立或修改程式庫）|COFF 物件 (.obj) 檔案，COFF 程式庫 (.lib)，32 位元的物件模型的格式 (OMF) 物件 (.obj) 檔案|
|擷取的成員具有 /EXTRACT|COFF 程式庫 (.lib)|
|建立匯出檔案，並匯入 /DEF 程式庫|模組定義 (.def) 檔、 COFF 物件 (.obj) 檔案、 COFF 程式庫 (.lib)、 32 位元 OMF 目的檔 (.obj)|

> [!NOTE]
>  16 位元版本的程式庫所建立的 OMF 程式庫不能做為 LIB 的 32 位元版本的輸入。

## <a name="see-also"></a>另請參閱

[LIB 概觀](overview-of-lib.md)
