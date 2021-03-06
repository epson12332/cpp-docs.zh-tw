---
title: 判斷要使用哪一個匯出方法
ms.date: 11/04/2016
helpviewer_keywords:
- __declspec(dllexport) keyword [C++]
- exporting DLLs [C++], method comparison
- def files [C++], exporting from DLLs
- .def files [C++], exporting from DLLs
ms.assetid: 66d773ed-935c-45c2-ad03-1a060874b34d
ms.openlocfilehash: 974c32cef87801599ba0d14fd146e84ad874467f
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62273733"
---
# <a name="determine-which-exporting-method-to-use"></a>判斷要使用哪一個匯出方法

您可以使用兩種方式匯出檔案：.def 檔或 `__declspec(dllexport)` 關鍵字。 為了協助您決定針對您的 DLL 使用哪種方式較好，請考慮下列問題：

- 您打算稍後要匯出多個函式嗎？

- 您的 DLL 只由您可以重建的應用程式所使用，或是由您無法重建的應用程式所使用 (例如，由協力廠商所建立的應用程式)？

## <a name="pros-and-cons-of-using-def-files"></a>使用 .def 檔的優缺點

在 .def 檔裡匯出函式，可以讓您控制匯出序數。 當您將匯出函式加入至 DLL 時，可以將較高的序數值 (比其他的匯出函式高) 指派給它們。 當您這樣做時，使用隱含連結的應用程式就不需要重新連結包含新函式的匯入程式庫。 如果您正在設計可供多個應用程式使用的 DLL，這會很方便，因為您可以加入新的功能，也可確保它繼續與已倚賴它的應用程式一起正常運作。 例如，使用 .def 檔建立 MFC DLL。

使用 .def 檔的另一個優點是您可以使用 `NONAME` 屬性來匯出函式。 這麼做只會將序數放在 DLL 的匯出表中。 對於具有大量匯出函式的 DLL，使用 `NONAME` 屬性可以降低 DLL 檔的大小。 如需如何撰寫模組定義陳述式的詳細資訊，請參閱[模組定義陳述式的規則](reference/rules-for-module-definition-statements.md)。 如需序數匯出資訊，請參閱[從根據序數而非依名稱的 DLL 匯出函式](exporting-functions-from-a-dll-by-ordinal-rather-than-by-name.md)。

使用.def 檔的缺點是，如果您要匯出函式中的C++檔案，您必須將裝飾的名稱置於.def 檔案，或使用 extern"C"，以避免名稱裝飾已定義匯出的函式，MSVC 編譯器。

如果您的裝飾的名稱置於.def 檔時，可以取得其使用[DUMPBIN](reference/dumpbin-reference.md)工具或使用連結器[/typedefs/ 對應](reference/map-generate-mapfile.md)選項。 由編譯起產生的裝飾名稱是編譯器特有的名稱，因此如果您將編譯器產生的裝飾名稱放入 .def 檔案中，連結 DLL 的應用程式必須也是使用相同版本的編譯器建置，以便所呼叫應用程式中的裝飾名稱與 DLL 的 .def 檔案中的輸出名稱相符。

## <a name="pros-and-cons-of-using-declspecdllexport"></a>使用 __declspec （dllexport） 的優缺點

使用 `__declspec(dllexport)` 很方便，因為您不必花費心思在維護 .def 檔和取得匯出函式的裝飾名稱上。 不過，這種匯出方法的用處會受限於您願意重建連結應用程式的數目。 如果您使用新的匯出重建 DLL，您也必須重建應用程式，因為匯出 C++ 函式的裝飾名稱，在您使用不同版本的編譯器重建它時可能會變更。

### <a name="what-do-you-want-to-do"></a>請您指定選項。

- [匯出從 DLL 使用。DEF 檔](exporting-from-a-dll-using-def-files.md)

- [使用 __declspec （dllexport） 從 DLL 匯出](exporting-from-a-dll-using-declspec-dllexport.md)

- [匯出和匯入使用 AFX_EXT_CLASS](exporting-and-importing-using-afx-ext-class.md)

- [匯出C++函式以用於 C 語言可執行檔](exporting-cpp-functions-for-use-in-c-language-executables.md)

- [匯出 C 函式，以用於 C 或C++-語言可執行檔](exporting-c-functions-for-use-in-c-or-cpp-language-executables.md)

- [使用 __declspec(dllimport) 匯入至應用程式](importing-into-an-application-using-declspec-dllimport.md)

- [初始化 DLL](run-time-library-behavior.md#initializing-a-dll)

### <a name="what-do-you-want-to-know-more-about"></a>您還想知道關於哪些方面的詳細資訊？

- [匯入和匯出內嵌函式](importing-and-exporting-inline-functions.md)

- [交互匯入](mutual-imports.md)

- [裝飾的名稱](reference/decorated-names.md)

## <a name="see-also"></a>另請參閱

[從 DLL 匯出](exporting-from-a-dll.md)
