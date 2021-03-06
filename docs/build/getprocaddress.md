---
title: GetProcAddress
ms.date: 11/04/2016
f1_keywords:
- GetProcAddress
helpviewer_keywords:
- DLLs [C++], GetProcAddress
- ordinal exports [C++]
- GetProcAddress method
ms.assetid: 48d14ae0-47ea-4c5d-96b1-2c158f1a26af
ms.openlocfilehash: 7b480314d195f50e4867f646208f2d9c70ce9b14
ms.sourcegitcommit: da32511dd5baebe27451c0458a95f345144bd439
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/07/2019
ms.locfileid: "65220802"
---
# <a name="getprocaddress"></a>GetProcAddress

明確連結至 DLL 呼叫的程序[GetProcAddress](/windows/desktop/api/libloaderapi/nf-libloaderapi-getprocaddress)取得 DLL 中匯出的函式的位址。 您可以使用傳回的函式指標來呼叫 DLL 函式。 **GetProcAddress**接受做為參數的 DLL 模組控制代碼 (由其中一個**LoadLibrary**， `AfxLoadLibrary`，或**GetModuleHandle**)，並採用您想要的函式名稱若要呼叫或函式的匯出序數。

因為您呼叫 DLL 函式透過指標，而且沒有編譯時期類型檢查，請確定函式的參數正確無誤，讓您不逾越堆疊上配置的記憶體而造成存取違規。 幫助提供類型安全的方法之一，就是查看匯出的函式的函式原型，並建立相符的函式指標的 typedef。 例如：

```
typedef UINT (CALLBACK* LPFNDLLFUNC1)(DWORD,UINT);
...

HINSTANCE hDLL;               // Handle to DLL
LPFNDLLFUNC1 lpfnDllFunc1;    // Function pointer
DWORD dwParam1;
UINT  uParam2, uReturnVal;

hDLL = LoadLibrary("MyDLL");
if (hDLL != NULL)
{
   lpfnDllFunc1 = (LPFNDLLFUNC1)GetProcAddress(hDLL,
                                           "DLLFunc1");
   if (!lpfnDllFunc1)
   {
      // handle the error
      FreeLibrary(hDLL);
      return SOME_ERROR_CODE;
   }
   else
   {
      // call the function
      uReturnVal = lpfnDllFunc1(dwParam1, uParam2);
   }
}
```

如何指定您想要時呼叫的函式**GetProcAddress**取決於 DLL 的建置方式。

如果您要連結至 DLL 以模組定義 (.def) 檔建置，並列出序數與函式中，您可以只取得匯出序數**匯出**DLL 的.def 檔的區段。 呼叫**GetProcAddress**與匯出序數，而不是函式名稱，會稍微快，如果 DLL 有許多匯出函式，因為匯出序數會被當成 dll 的索引將資料表匯出。 與匯出序數**GetProcAddress**可以找出相比較的 DLL 匯出表中的函式名稱指定的名稱對於直接函式。 不過，您應該呼叫**GetProcAddress**以匯出序數，只有當您可以控制的序數指派.def 檔案中匯出的函式。

## <a name="what-do-you-want-to-do"></a>請您指定選項。

- [將可執行檔連結至 DLL](linking-an-executable-to-a-dll.md#linking-implicitly)

- [將可執行檔連結至 DLL](linking-an-executable-to-a-dll.md#determining-which-linking-method-to-use)

## <a name="what-do-you-want-to-know-more-about"></a>您還想知道關於哪些方面的詳細資訊？

- [LoadLibrary 和 AfxLoadLibrary](loadlibrary-and-afxloadlibrary.md)

- [FreeLibrary](/windows/desktop/api/libloaderapi/nf-libloaderapi-freelibrary)

- [使用 DEF 檔從 DLL 匯出](exporting-from-a-dll-using-def-files.md)

## <a name="see-also"></a>另請參閱

[建立 C /C++在 Visual Studio 中的 Dll](dlls-in-visual-cpp.md)
