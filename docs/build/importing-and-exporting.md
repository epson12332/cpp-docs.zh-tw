---
title: 匯入和匯出
ms.date: 05/06/2019
helpviewer_keywords:
- DLLs [C++], importing
- exporting DLLs [C++]
- importing DLLs [C++]
- DLLs [C++], exporting from
- __declspec(dllimport) keyword [C++]
ms.assetid: 7c44c2aa-2117-4cec-9615-a65bfd3f8f7b
ms.openlocfilehash: 03931f7f128ab0666890bb8e76677db67dda8fc7
ms.sourcegitcommit: da32511dd5baebe27451c0458a95f345144bd439
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/07/2019
ms.locfileid: "65220636"
---
# <a name="importing-and-exporting"></a>匯入和匯出

您可以將公用符號匯入的應用程式，或使用兩種方法從 DLL 匯出函式：

- 建置 DLL 時使用模組定義 (.def) 檔

- 使用關鍵字 **__declspec （dllimport)** 或是 **__declspec （dllexport)** 主應用程式中的函式定義中

## <a name="using-a-def-file"></a>使用.def 檔

模組定義 (.def) 檔案是文字檔，其中包含一或多個模組陳述式，說明 DLL 的各種屬性。 如果您不要使用 **__declspec （dllimport)** 或是 **__declspec （dllexport)** 來匯出 DLL 的函式，則 DLL 就需要.def 檔。

您可以使用.def 檔，來[匯入應用程式](importing-using-def-files.md)上，或者[從 DLL 匯出](exporting-from-a-dll-using-def-files.md)。

## <a name="using-declspec"></a>使用 __declspec

您不需要使用 **__declspec （dllimport)** 對於您的程式碼編譯是否正確，但這種方式可讓編譯器產生更好的程式碼。 編譯器可產生更好的程式碼，因為它可以判斷是否函式的 DLL 中存在，可讓編譯器產生程式碼，會略過通常會跨越 DLL 界限的函式呼叫中出現的間接取值層級。 不過，您必須使用 **__declspec （dllimport)** 匯入 DLL 中使用的變數。

使用適當的.def 檔的 [匯出] 區段中， **__declspec （dllexport)** 並非必要。 **__declspec （dllexport)** 已加入至提供簡單的方式，從.exe 或.dll 檔案匯出函式，而不使用.def 檔。

Win32 可攜式執行檔格式被設計來最小化必須接觸到，若要修正匯入的頁面數目。 若要這樣做，就會將任何程式的所有匯入位址稱為 「 匯入位址表格的一個位置中。 這可讓載入器時存取這些匯入修改一個或兩個頁面。

## <a name="what-do-you-want-to-do"></a>請您指定選項。

- [匯入至應用程式](importing-into-an-application-using-declspec-dllimport.md)

- [從 DLL 匯出](exporting-from-a-dll.md)

## <a name="see-also"></a>另請參閱

[建立 C /C++在 Visual Studio 中的 Dll](dlls-in-visual-cpp.md)
