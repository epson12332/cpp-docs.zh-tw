---
title: 方向旗標
ms.date: 11/04/2016
f1_keywords:
- c.flags
helpviewer_keywords:
- direction flag
ms.assetid: 0836b4af-dbbb-4ab8-a4b2-156f2e2099e2
ms.openlocfilehash: ead32fa7f09e9dd98130855ecd87ba3b3d454ef5
ms.sourcegitcommit: dedd4c3cb28adec3793329018b9163ffddf890a4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/11/2019
ms.locfileid: "57740151"
---
# <a name="direction-flag"></a>方向旗標

方向旗標是指所有 Intel x86 相容 CPU 專屬的 CPU 旗標。 它會套用至使用 REP (repeat) 前置詞的所有組譯碼指示，例如 MOVS、MOVSD、MOVSW 等。 如果方向旗標已清除，將會增加提供給適用指示的位址。

C 執行階段常式會假設方向旗標已清除。 如果您是以其他函式搭配 C 執行階段函式，則必須確定其他函式不會更動方向旗標，或是會將它還原為原始狀態。 若能在輸入時預期方向旗標已清除，將能使執行階段程式碼更加快速及有效率。

C 執行階段程式庫函式 (例如字串操作和緩衝區操作常式) 將會預期方向旗標已清除。

## <a name="see-also"></a>另請參閱

[CRT 程式庫功能](../c-runtime-library/crt-library-features.md)
