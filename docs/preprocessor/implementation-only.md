---
title: implementation_only
ms.date: 11/04/2016
f1_keywords:
- implementation_only
helpviewer_keywords:
- implementation_only attribute
ms.assetid: d8cabc86-4425-45a0-9587-d57536980088
ms.openlocfilehash: c1435ca74ac2b5a73c308592b1affe6fca097d1b
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62383947"
---
# <a name="implementationonly"></a>implementation_only
**C++特定**

不產生 .tlh 標頭檔 (主要標頭檔)。

## <a name="syntax"></a>語法

```
implementation_only
```

## <a name="remarks"></a>備註

這個檔案包含所有用於公開類型程式庫內容的宣告。 實作包裝函式成員函式時，會產生 .tli 標頭檔並包含在編譯中。

指定這個屬性時，.tli 標頭的內容會在 .tlh 標頭通常使用的相同命名空間中。 此外，不會將成員函式宣告為內嵌。

**Implementation_only**屬性適用於搭配[no_implementation](../preprocessor/no-implementation.md)避開先行編譯標頭 (PCH) 檔案中實作這種屬性。 具有 `#import` 屬性的 `no_implementation` 陳述式是置於用來建立 PCH 的來源範圍中。 產生的 PCH 會供許多原始程式檔使用。 `#import`陳述式搭配**implementation_only** PCH 區域以外的位置，然後使用屬性。 您只能在其中一個原始程式檔中使用此陳述式一次。 如此會產生所有必要的包裝函式成員函式，而不需要額外重新編譯每個原始程式檔。

> [!NOTE]
> **Implementation_only**中其中一個屬性`#import`陳述式必須是用來與另一個`#import`陳述式中，相同的型別程式庫，與`no_implementation`屬性。 否則，就會產生編譯器錯誤。 這是因為所產生的包裝函式類別定義`#import`陳述式搭配`no_implementation`屬性，才能編譯所產生的實作**implementation_only**屬性。

**結束C++特定**

## <a name="see-also"></a>另請參閱

[#import 屬性](../preprocessor/hash-import-attributes-cpp.md)<br/>
[#import 指示詞](../preprocessor/hash-import-directive-cpp.md)