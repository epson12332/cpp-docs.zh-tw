---
title: 嚴重錯誤 C1005
ms.date: 11/04/2016
f1_keywords:
- C1005
helpviewer_keywords:
- C1005
ms.assetid: 150daf8e-a38a-4669-9c1a-a05b5a1f65ef
ms.openlocfilehash: a84791367656729b1cbd50ca180368f6c01531a4
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62383187"
---
# <a name="fatal-error-c1005"></a>嚴重錯誤 C1005

字串太大超過緩衝區

編譯器中繼檔案中的字串造成緩衝區溢位。

當您傳遞至 [/Fd](../../build/reference/fd-program-database-file-name.md) 或 [/Yl](../../build/reference/yl-inject-pch-reference-for-debug-library.md) 編譯器選項的參數大於 256 個位元組時，可能會取得這項錯誤。