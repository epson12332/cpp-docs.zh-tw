---
title: 使用 abort
ms.date: 11/04/2016
f1_keywords:
- Abort
helpviewer_keywords:
- abort function
ms.assetid: 3ba39b78-ef74-4a8d-8dee-2d62442de174
ms.openlocfilehash: 0961f6f88f5de4d435fa65e50b9dbdbc478e7608
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62244204"
---
# <a name="using-abort"></a>使用 abort

呼叫[中止](../c-runtime-library/reference/abort.md)函式會導致立即終止。 它會略過初始化全域靜態物件的正常解構流程。 另外也會略過任何使用 `atexit` 函式指定的特殊處理。

## <a name="see-also"></a>另請參閱

[其他終止考量](../cpp/additional-termination-considerations.md)