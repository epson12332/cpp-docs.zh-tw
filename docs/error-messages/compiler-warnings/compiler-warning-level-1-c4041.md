---
title: 編譯器警告 (層級 1) C4041
ms.date: 11/04/2016
f1_keywords:
- C4041
helpviewer_keywords:
- C4041
ms.assetid: 107ee9fd-4b88-4f22-a18f-a20726831095
ms.openlocfilehash: 6e1f2a2396447038f6a117f66d4002bea7fd7486
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62151314"
---
# <a name="compiler-warning-level-1-c4041"></a>編譯器警告 (層級 1) C4041

編譯器限制 : 瀏覽器資訊超出編譯器上限，已終止輸出

瀏覽器資訊超過編譯器限制。

這個警告可能是使用 [/FR](../../build/reference/fr-fr-create-dot-sbr-file.md) (包含區域變數的瀏覽器資訊) 進行編譯所造成。

### <a name="to-fix-by-using-the-following-possible-solutions"></a>使用下列可能的解決方式來進行修正

1. 使用 /Fr (未含區域變數的瀏覽器資訊) 進行編譯。

1. 停用瀏覽器輸出 (不使用 /FR 或 /Fr 進行編譯)。