---
title: 編譯器錯誤 C2212
ms.date: 11/04/2016
f1_keywords:
- C2212
helpviewer_keywords:
- C2212
ms.assetid: 3fdab304-272c-4d07-bfd4-fad75170e536
ms.openlocfilehash: a632aaf9809cd306354320a21cb03b993d60a95f
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62400418"
---
# <a name="compiler-error-c2212"></a>編譯器錯誤 C2212

'identifier': __based 不提供函式指標

函式的指標不可以宣告為`__based`。 如果您需要的程式碼為基礎的資料，請使用`__declspec`關鍵字或`data_seg`pragma。