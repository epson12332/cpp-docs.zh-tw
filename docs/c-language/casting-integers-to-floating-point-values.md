---
title: 將整數轉型為浮點值
ms.date: 11/04/2016
helpviewer_keywords:
- integers, casting to floating-point values
ms.assetid: 81fd5b7d-15eb-4c11-a8c8-e1621ff54fd3
ms.openlocfilehash: 8fa013668278fae82bcb2bb9eb1f2aec3cb61581
ms.sourcegitcommit: f4be868c0d1d78e550fba105d4d3c993743a1f4b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/12/2019
ms.locfileid: "56152868"
---
# <a name="casting-integers-to-floating-point-values"></a>將整數轉型為浮點值

**ANSI 3.2.1.3**：當整數轉換成無法正確地表示原始值的浮點數時，其截斷的方向

當整數轉型成無法正確地表示其值的浮點值時，會將其值捨入 (向上或向下捨入) 為最接近的適當值。

例如，將 **unsigned long**(具有 32 位元精確度) 轉型為 **float** (其尾數具有 23 位元精確度) 時，會將數字捨入至最接近 256 的倍數。 **long** 值 4,294,966,913 到 4,294,967,167 都會捨入為 **float** 值 4,294,967,040。

## <a name="see-also"></a>另請參閱

[浮點數學](../c-language/floating-point-math.md)
