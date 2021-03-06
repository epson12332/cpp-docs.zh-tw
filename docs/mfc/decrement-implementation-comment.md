---
title: --實作註解
ms.date: 11/04/2016
helpviewer_keywords:
- Implementation comment in MFC source files
- comments, MFC
- MFC source files, Implementation comment
- comments, Implementation comments
ms.assetid: 4d799c07-8e71-4a6b-90ab-8282d6ff48ce
ms.openlocfilehash: 377997b66c5b9c005d1e1bee24890b756621b672
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62240733"
---
# <a name="-implementation-comment"></a>// 實作註解

`// Implementation` 區段是所有 MFC 類別宣告最重要的部分。

此區段包含所有實作詳細資料。 成員變數和成員函式二者可能都會出現在此區段中。 這一行以下的所有內容在 MFC 的未來版本中會有所變更。 除非您無法避開它，否則不應該依賴 `// Implementation` 這一行下方的詳細資料。 此外，雖然有些實作技術提示中曾討論過，但在實作行下宣告的成員並未記載。 因為事實上是函式會覆寫被視為實作詳細資料的基底類別實作，所以無論基底類別函式是在哪個區段定義的，覆寫基底類別中的虛擬函式都會包含在此區段中。 一般來說，這些成員是受到保護的，不過並不是始終受保護。

請注意`CStdioFile`底下列出[註解的範例](../mfc/an-example-of-the-comments.md)下宣告的成員`// Implementation`註解可以宣告為**公用**，**保護**，或**私人**。 您應該謹慎使用這些成員，因為它們在未來可能會變更。 宣告成員做為一群**公開**可能需要的類別程式庫實作能正確運作。 不過，這並不表示您可以安全地如其所宣告地使用那些成員。

> [!NOTE]
>  您可能會在 `// Implementation` 註解的上方或下方找到剩餘類型的註解。 不論在上方或下方，它們會均描述在其下宣告的成員類型。 如果它們發生在 `// Implementation` 註解下，您應該假設成員在 MFC 的未來版本中可能會變更。

## <a name="see-also"></a>另請參閱

[使用 MFC 原始程式檔](../mfc/using-the-mfc-source-files.md)<br/>
[註解的範例](../mfc/an-example-of-the-comments.md)<br/>
[建構函式註解](../mfc/decrement-constructors-comment.md)<br/>
[屬性註解](../mfc/decrement-attributes-comment.md)<br/>
[作業註解](../mfc/decrement-operations-comment.md)<br/>
[可覆寫註解](../mfc/decrement-overridables-comment.md)
