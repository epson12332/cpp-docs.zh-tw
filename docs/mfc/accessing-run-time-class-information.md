---
title: 存取執行階段類別資訊
ms.date: 11/04/2016
helpviewer_keywords:
- CObject class [MFC], and RTTI
- CObject class [MFC], using IsKindOf method [MFC]
- run time [MFC], class information
- RUNTIME_CLASS macro [MFC]
- CObject class [MFC], using RUNTIME_CLASS macro [MFC]
- RTTI compiler option [MFC]
- CObject class [MFC], accessing run-time class information
- run time [MFC]
- IsKindOf method method [MFC]
- run-time class [MFC], accessing information
- classes [MFC], run-time class information
- run-time class [MFC]
- RUNTIME_CLASS macro, using
ms.assetid: 3445a9af-0bd6-4496-95c3-aa59b964570b
ms.openlocfilehash: 2e4f8685033fc7a8a2f49dafa7ef4e4e019d8989
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62392943"
---
# <a name="accessing-run-time-class-information"></a>存取執行階段類別資訊

本文說明如何在執行階段存取物件之類別的資訊。

> [!NOTE]
>  不使用 MFC[執行階段類型資訊](../cpp/run-time-type-information.md)視覺效果中導入的 (RTTI) 支援C++4.0。

如果您有衍生您的類別，從[CObject](../mfc/reference/cobject-class.md)並用**DECLARE**_**動態**並`IMPLEMENT_DYNAMIC`，則`DECLARE_DYNCREATE`和`IMPLEMENT_DYNCREATE`，或`DECLARE_SERIAL`並`IMPLEMENT_SERIAL`一文中所述的巨集[從 CObject 衍生類別](../mfc/deriving-a-class-from-cobject.md)，則`CObject`類別都能夠在執行階段判斷物件的確切類別。

當需要檢查函式引數的實際類型時，以及當您必須根據物件的類別撰寫特殊用途的程式碼時，這項功能十分實用。 不過，通常不建議使用這種作法，因為這會使虛擬函式的功能重複。

`CObject` 成員函式 `IsKindOf` 可以用來判斷特定物件是否屬於指定的類別，或是否衍生自特定類別。 `IsKindOf` 的引數是一個 `CRuntimeClass` 物件，您可以使用 `RUNTIME_CLASS` 巨集透過類別的名稱來取得該物件。

### <a name="to-use-the-runtimeclass-macro"></a>使用 RUNTIME_CLASS 巨集

1. 針對 `RUNTIME_CLASS` 類別使用 `CObject` 與類別名稱，如下所示：

   [!code-cpp[NVC_MFCCObjectSample#4](../mfc/codesnippet/cpp/accessing-run-time-class-information_1.cpp)]

您很少需要直接存取執行階段類別物件。 一般用法是將執行階段類別物件傳遞至 `IsKindOf` 函式，如下一個程序所示。 `IsKindOf` 函式會測試物件是否屬於特定類別。

#### <a name="to-use-the-iskindof-function"></a>使用 IsKindOf 函式

1. 請確定類別支援執行階段類別。 也就是說，類別必須有已直接或間接衍生自`CObject`並用**DECLARE**_**動態**並`IMPLEMENT_DYNAMIC`，則`DECLARE_DYNCREATE`和`IMPLEMENT_DYNCREATE`，或`DECLARE_SERIAL`並`IMPLEMENT_SERIAL`一文中所述的巨集[從 CObject 衍生類別](../mfc/deriving-a-class-from-cobject.md)。

1. 呼叫該類別之物件的 `IsKindOf` 成員函式，使用 `RUNTIME_CLASS` 巨集產生 `CRuntimeClass` 引數，如下所示：

   [!code-cpp[NVC_MFCCObjectSample#2](../mfc/codesnippet/cpp/accessing-run-time-class-information_2.h)]

   [!code-cpp[NVC_MFCCObjectSample#5](../mfc/codesnippet/cpp/accessing-run-time-class-information_3.cpp)]

    > [!NOTE]
    >  則 IsKindOf 會傳回 **，則為 TRUE**的物件是否為指定的類別或衍生自指定類別的類別成員。 `IsKindOf` 不支援多重繼承或虛擬基底類別，不過您可以視需要為衍生的 MFC 使用多重繼承。

執行階段類別資訊的其中一種用途是動態建立物件。 此程序文章中討論[動態物件建立](../mfc/dynamic-object-creation.md)。

如需詳細資訊，在序列化和執行階段類別資訊，請參閱文章[MFC 中的檔案](../mfc/files-in-mfc.md)並[序列化](../mfc/serialization-in-mfc.md)。

## <a name="see-also"></a>另請參閱

[使用 CObject](../mfc/using-cobject.md)
