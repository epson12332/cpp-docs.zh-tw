---
title: /ENTRY (進入點符號)
ms.date: 11/04/2016
f1_keywords:
- /entry
- VC.Project.VCLinkerTool.EntryPointSymbol
helpviewer_keywords:
- starting address
- -ENTRY linker option
- /ENTRY linker option
- ENTRY linker option
ms.assetid: 26c62ba2-4f52-4882-a7bd-7046a0abf445
ms.openlocfilehash: 0f3604ef75ce10928463c088e423615886555eda
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62293208"
---
# <a name="entry-entry-point-symbol"></a>/ENTRY (進入點符號)

```
/ENTRY:function
```

## <a name="arguments"></a>引數

*function*<br/>
指定使用者定義啟動的函式位址的.exe 檔或 DLL。

## <a name="remarks"></a>備註

/ENTRY 選項會指定進入點函式做為.exe 檔或 DLL 的開始位址。

此函式必須定義為使用`__stdcall`呼叫慣例。 參數和傳回值取決於如果程式是主控台應用程式、 windows 應用程式或 DLL。 建議您讓連結器設定的進入點，以便正確地初始化 C 執行階段程式庫和C++針對靜態物件的建構函式會執行。

根據預設，開始的位址會是 C 執行階段程式庫函式的名稱。 連結器會選取它的屬性的程式，根據下表所示。

|函式名稱|預設值|
|-------------------|-----------------|
|**mainCRTStartup** (或**wmainCRTStartup**)|使用 /subsystem: console; 的應用程式呼叫`main`(或`wmain`)|
|**WinMainCRTStartup** (或**wWinMainCRTStartup**)|應用程式使用 /SUBSYSTEM:**WINDOWS**; 呼叫`WinMain`(或`wWinMain`)，這必須定義為使用 `__stdcall`|
|**_DllMainCRTStartup**|DLL;呼叫`DllMain`若有的話，它必須定義為使用 `__stdcall`|

如果[/DLL](dll-build-a-dll.md)或是[/SUBSYSTEM](subsystem-specify-subsystem.md)未指定選項，連結器將會取決於是否子系統和項目點`main`或`WinMain`定義。

函式`main`， `WinMain`，和`DllMain`是三種形式的使用者定義的進入點。

/ENTRY 到指定的函式時建立的受控映像，必須具有的簽章 (LPVOID *var1*，DWORD *var2*，LPVOID *var3*)。

如需如何定義您自己`DllMain`進入點，請參閱 < [Dll 和視覺效果C++執行階段程式庫行為](../run-time-library-behavior.md)。

### <a name="to-set-this-linker-option-in-the-visual-studio-development-environment"></a>在 Visual Studio 開發環境中設定這個連結器選項

1. 開啟專案的 [屬性頁]  對話方塊。 如需詳細資訊，請參閱 <<c0> [ 設定C++Visual Studio 中的編譯器和組建屬性](../working-with-project-properties.md)。</c0>

1. 按一下 **連結器**資料夾。

1. 按一下 **進階**屬性頁。

1. 修改**進入點**屬性。

### <a name="to-set-this-linker-option-programmatically"></a>若要以程式設計方式設定這個連結器選項

- 請參閱 <xref:Microsoft.VisualStudio.VCProjectEngine.VCLinkerTool.EntryPointSymbol%2A>。

## <a name="see-also"></a>另請參閱

[MSVC 連結器參考](linking.md)<br/>
[MSVC 連結器選項](linker-options.md)
