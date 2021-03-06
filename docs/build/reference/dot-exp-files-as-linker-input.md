---
title: .Exp 檔做為連結器輸入
ms.date: 11/04/2016
helpviewer_keywords:
- exporting functions
- import libraries, linker files
- linking [C++], exports
- exporting functions, information about exported functions
- exporting data, export (.exp) files
- functions [C++], exporting
- .exp files [C++]
- EXP files
ms.assetid: 399f5636-0a4d-462e-b500-5f5b9ae5ad22
ms.openlocfilehash: 0f2f5c22752d6d938700228fc208c21b8f32cc7b
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62293663"
---
# <a name="exp-files-as-linker-input"></a>.Exp 檔做為連結器輸入

匯出 (.exp) 檔案包含匯出函式和資料的項目的相關資訊。 當程式庫建立匯入程式庫時，它也會建立.exp 檔。 當您連結至匯出和匯入從另一個程式，直接或間接的程式，您可以使用.exp 檔。 如果您連結.exp 檔，連結不會產生匯入程式庫，因為它假設 LIB 已經建立一個。 如需有關.exp 檔案和匯入程式庫的詳細資訊，請參閱[使用 匯入程式庫和匯出檔案](working-with-import-libraries-and-export-files.md)。

## <a name="see-also"></a>另請參閱

[LINK 輸入檔](link-input-files.md)<br/>
[MSVC 連結器選項](linker-options.md)
