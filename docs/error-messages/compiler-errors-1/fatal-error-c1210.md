---
title: 嚴重錯誤 C1210
ms.date: 11/04/2016
f1_keywords:
- C1210
helpviewer_keywords:
- C1210
ms.assetid: e2208309-c284-425c-a7e8-48e96e66f35b
ms.openlocfilehash: a90ca3e3b55642f1a6cd847997b83e4b7db46818
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62385845"
---
# <a name="fatal-error-c1210"></a>嚴重錯誤 C1210

> 所安裝的執行階段版本不支援 /clr:pure 和 /clr:safe

**/Clr: pure**並 **/clr: safe**編譯器選項是在 Visual Studio 2015 中已被取代，而且不支援的 Visual Studio 2017 中。

如果您有目前版本的編譯器，但 Common Language Runtime 來自舊版本，就會發生 C1210。

編譯器的某個功能可能無法在執行階段的舊版本上運作。

若要解決 C1210，請安裝要與編譯器搭配使用的 Common Language Runtime 版本。