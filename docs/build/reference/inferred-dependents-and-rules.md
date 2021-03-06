---
title: 推斷相依和規則
ms.date: 11/04/2016
helpviewer_keywords:
- rules, inferred
- inferred dependents in NMAKE
- inferred rules in NMAKE
- dependents, inferred
ms.assetid: 9381e74a-53d9-445c-836d-0ff7ef6112d9
ms.openlocfilehash: b9c3055db0cc173999e1737986166eb334dcf96c
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62269904"
---
# <a name="inferred-dependents-and-rules"></a>推斷相依和規則

如果適用的推斷規則存在，NMAKE 就會假設為目標的推斷的相依。 如果，套用規則：

- *toext*符合目標的延伸模組。

- *fromext*有目標的基底名稱和檔案的副檔名存在於目前或指定目錄中的相符項目。

- *fromext*處於[。尾碼](dot-directives.md); 沒有其他*fromext*比對規則中有較高 **。後置詞**優先順序。

- 具有較高的任何明確的相依 **。後置詞**優先順序。

推斷相依項目可能會造成非預期的副作用。 如果目標的描述區塊包含命令，NMAKE 就會執行這些命令，而不是命令中的規則。

## <a name="see-also"></a>另請參閱

[推斷規則](inference-rules.md)
