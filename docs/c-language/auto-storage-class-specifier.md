---
title: auto 儲存類別指定名稱
ms.date: 11/04/2016
ms.assetid: 8e73f57e-aa92-4e41-91ea-5c8ad2a2b332
ms.openlocfilehash: 6bd36fd534602a5a4df95047a830058e8c5ef163
ms.sourcegitcommit: f4be868c0d1d78e550fba105d4d3c993743a1f4b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/12/2019
ms.locfileid: "56147005"
---
# <a name="auto-storage-class-specifier"></a>auto 儲存類別指定名稱

**auto** 儲存類別指定名稱會宣告自動變數，也就是具有本機存留期的變數。 **auto** 變數只能在其宣告所在的區塊中看見。 **auto** 變數的宣告可以包含初始設定式，如[初始化](../c-language/initialization.md)中所述。 由於具有 **auto** 儲存類別的變數不會自動初始化，因此您應該在宣告這些變數時明確地將它們初始化，或者在區塊內的陳述式中為它們指派初始值。 未初始化的 **auto** 變數值為未定義 (如果已指定初始設定式，則 **auto** 或 **register** 儲存類別的區域變數會在每次進入範圍時初始化)。

內部 **static** 變數 (具有區域或區塊範圍的靜態變數) 可以使用任何外部或 **static** 項目的位址初始化，但是無法使用另一個 **auto** 項目的位址初始化，因為 **auto** 項目的位址不是常數。

## <a name="see-also"></a>另請參閱

[auto 關鍵字](../cpp/auto-keyword.md)
