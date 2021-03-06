---
title: 定義和慣例
ms.date: 11/04/2016
helpviewer_keywords:
- nonterminals definition
ms.assetid: f9b3cf5f-6a7c-4a10-9b18-9d4a43efdaeb
ms.openlocfilehash: 0ff3f8b447e29f0da59405a7c0286d7a696b4613
ms.sourcegitcommit: f4be868c0d1d78e550fba105d4d3c993743a1f4b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/12/2019
ms.locfileid: "56152465"
---
# <a name="definitions-and-conventions"></a>定義和慣例

終端是語法定義的端點。 沒有其他解決方式。 終端包括一組保留字和使用者定義的識別項。

非終端是語法中的預留位置，會在此語法摘要中的其他地方定義。 定義可以是遞迴式。

選擇性的元件會以下標的 <sub>opt</sub> 表示。 例如，套用至物件的

> **{** *運算式*<sub>opt</sub> **}**

表示放在大括號中的選擇性運算式。

語法慣例會針對語法的不同元件使用不同的字型屬性。 符號和字型如下：

|屬性|描述|
|---------------|-----------------|
|*nonterminal*|斜體類型表示非終端項。|
|**const**|粗體類型的終端項為必須依下述方式輸入的常值保留字和符號。 此內容中的字元一律區分大小寫。|
|<sub>opt</sub>|後面接著非終端項的 <sub>opt</sub> 一律為選擇項。|
|預設字樣|這個字樣中描述或列出的集合中的字元可用來作為 C 陳述式中的終端。|

接著非終端項的冒號 (**:**) 會引入其定義。 除非前面加上「one of」字樣，否則替代定義另列於其他行。

## <a name="see-also"></a>另請參閱

[C 語言語法摘要](../c-language/c-language-syntax-summary.md)
