---
title: LIB 概觀
ms.date: 11/04/2016
f1_keywords:
- Lib
helpviewer_keywords:
- LIB [C++], modes
ms.assetid: e997d423-f574-434f-8b56-25585d137ee0
ms.openlocfilehash: 97d7b8892574fbe485a8d6c5e344e4a77aaf8519
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62320275"
---
# <a name="overview-of-lib"></a>LIB 概觀

LIB 建立標準程式庫、 匯入程式庫和匯出的檔案可搭配[連結](linker-options.md)建置程式時。 從命令提示字元中執行 LIB。

您可以使用程式庫的模式如下：

- [建立或修改 COFF 程式庫](managing-a-library.md)

- [擷取至檔案的成員物件](extracting-a-library-member.md)

- [建立匯出檔案和匯入程式庫](working-with-import-libraries-and-export-files.md)

這些模式是互斥;您可以使用程式庫中只有一個模式，一次。

## <a name="lib-options"></a>Lib 選項

下表列出 lib.exe 的詳細資訊的連結選項。

|選項|描述|
|-|-|
|**/DEF**|建立匯入程式庫和匯出檔案。<br/><br/>如需詳細資訊，請參閱[建置匯入程式庫和匯出檔案](building-an-import-library-and-export-file.md)。|
|**/ERRORREPORT**|   內部錯誤的 lib.exe 的相關資訊傳送到 Microsoft。<br/><br/>如需詳細資訊，請參閱[執行 LIB](running-lib.md)。|
|**/EXPORT**|   匯出函式，從您的程式。<br/><br/>如需詳細資訊，請參閱[建置匯入程式庫和匯出檔案](building-an-import-library-and-export-file.md)。|
|**/EXTRACT**|   建立包含一份現有的程式庫成員的物件 (.obj) 檔案。<br/><br/>如需詳細資訊，請參閱[擷取程式庫成員](extracting-a-library-member.md)。|
|**/INCLUDE**|   加入至符號表中的符號。<br/><br/>如需詳細資訊，請參閱[建置匯入程式庫和匯出檔案](building-an-import-library-and-export-file.md)。|
|**/LIBPATH**|   覆寫環境程式庫路徑。<br/><br/>如需詳細資訊，請參閱[管理程式庫](managing-a-library.md)。|
|**/LIST**|   標準輸出中顯示輸出程式庫的相關資訊。<br/><br/>如需詳細資訊，請參閱[管理程式庫](managing-a-library.md)。|
|**/LTCG**|   會導致要建置使用連結時產生程式碼程式庫。<br/><br/>如需詳細資訊，請參閱[執行 LIB](running-lib.md)。|
|**/MACHINE**|   指定程式的目標平台。<br/><br/>如需詳細資訊，請參閱[執行 LIB](running-lib.md)。|
|**/NAME**|   當建置匯入程式庫時，指定正在建置匯入程式庫 DLL 的名稱。<br/><br/>如需詳細資訊，請參閱[管理程式庫](managing-a-library.md)。|
|**/NODEFAULTLIB**|   解析外部參考時，它會搜尋程式庫清單中移除一或多個預設程式庫。<br/><br/>如需詳細資訊，請參閱[管理程式庫](managing-a-library.md)。|
|**/NOLOGO**|   隱藏顯示的 LIB 著作權訊息和版本號碼，並避免回應的命令檔。<br/><br/>如需詳細資訊，請參閱[執行 LIB](running-lib.md)。|
|**/OUT**|   覆寫預設的輸出檔案名稱。<br/><br/>如需詳細資訊，請參閱[管理程式庫](managing-a-library.md)。|
|**/REMOVE**|   省略輸出程式庫中的物件。<br/><br/>如需詳細資訊，請參閱[管理程式庫](managing-a-library.md)。|
|**/SUBSYSTEM**|   告知作業系統如何執行程式，建立連結至輸出程式庫。<br/><br/>如需詳細資訊，請參閱[管理程式庫](managing-a-library.md)。|
|**/VERBOSE**|   顯示進度的工作階段，包括所加入之.obj 檔的名稱相關的詳細資料。<br/><br/>如需詳細資訊，請參閱[執行 LIB](running-lib.md)。|
|**/WX**|   將警告視為錯誤。<br/><br/>如需詳細資訊，請參閱[執行 LIB](running-lib.md)。|

## <a name="see-also"></a>另請參閱

[LIB 參考](lib-reference.md)<br/>
[LIB 輸入檔](lib-input-files.md)<br/>
[LIB 輸出檔](lib-output-files.md)<br/>
[其他 LIB 輸出](other-lib-output.md)<br/>
[程式庫結構](structure-of-a-library.md)
