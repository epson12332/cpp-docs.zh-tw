---
title: Visual Studio 中的 C++ 專案的 MSBuild 內部項目
ms.date: 05/16/2019
helpviewer_keywords:
- MSBuild overview
ms.assetid: dd258f6f-ab51-48d9-b274-f7ba911d05ca
ms.openlocfilehash: b3348320a1468fea03f39e43cc847f1085f3d319
ms.sourcegitcommit: a10c9390413978d36b8096b684d5ed4cf1553bc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/17/2019
ms.locfileid: "65837224"
---
# <a name="msbuild-internals-for-c-projects"></a>C++ 專案的 MSBuild 內部項目

當您在 IDE 中設定專案屬性，然後儲存專案時，Visual Studio 會將專案設定寫入至您的專案檔。 專案檔中包含對您的專案而言唯一的設定，但不包含建置專案所需的所有設定。 專案檔含有 `Import` 元素，其中包含其他*支援檔案*的網路。 支援檔案中包含建置專案所需的其餘屬性、目標和設定。

支援檔案中大部分的目標和屬性的唯一用途皆為實作建置系統。 以下這一節將討論您在 MSBuild 命令列上可指定的一些有用的目標和屬性。 若要探索更多目標和屬性，請瀏覽支援檔案目錄中的檔案。

## <a name="support-file-directories"></a>支援檔案目錄

根據預設，主要的 Visual Studio 支援檔案會位於下列目錄中。 Microsoft Visual Studio 下的目錄供 Visual Studio 2017 和更新版本使用，而 MSBuild 下的目錄則供 Visual Studio 2015 和更早版本使用。

|Directory|說明|
|---------------|-----------------|
|*drive*:\Program Files *(x86)* \Microsoft Visual Studio\\*year*\\*edition*\Common7\IDE\VC\VCTargets\ <br /><br />*drive*:\Program Files *(x86)* \MSBuild\Microsoft.Cpp (x86)\v4.0\\*version*\ |包含目標所使用的主要目標檔案 (.targets) 和屬性檔案 (.props)。 根據預設，$(VCTargetsPath) 巨集會參考這個目錄。|
|*drive*:\Program Files *(x86)* \Microsoft Visual Studio\\*year*\\*edition*\Common7\IDE\VC\VCTargets\Platforms\\*platform*\ <br /><br />*drive*:\Program Files *(x86)* \MSBuild\Microsoft.Cpp\v4.0\\*version*\Platforms\\*platform*\ |包含平台特定的目標和屬性檔案，會覆寫其上層目錄中的目標和屬性。 此目錄也包含一個 DLL，會定義此目錄中的目標所使用的工作。<br /><br /> *platform* 預留位置代表 ARM、Win32 或 x64 子目錄。|
|*drive*:\Program Files *(x86)* \Microsoft Visual Studio\\*year*\\*edition*\Common7\IDE\VC\VCTargets\Platforms\\*platform*\PlatformToolsets\\*toolset*\ <br /><br />*drive*:\Program Files *(x86)* \MSBuild\Microsoft.Cpp\v4.0\\*version*\Platforms\\*platform*\PlatformToolsets\\*toolset*\ <br /><br />*drive*:\Program Files *(x86)* \MSBuild\Microsoft.Cpp\v4.0\Platforms\\*platform*\PlatformToolsets\\*toolset*\ |包含可讓組建使用指定的 *toolset* 產生 C++ 應用程式的目錄。<br /><br /> Visual Studio 2017 和更新版本會使用 *year* 和 *edition* 預留位置。 Visual Studio 2012 的 *version* 預留位置為 V110、Visual Studio 2013 的預留位置為 V120、Visual Studio 2015 的預留位置為 V140、Visual Studio 2017 的預留位置為 V141，Visual Studio 2019 的預留位置為 V142。 *platform* 預留位置代表 ARM、Win32 或 x64 子目錄。 *toolset* 預留位置代表 toolset 子目錄，例如，v140 代表會使用 Visual Studio 2015 工具組建置 Windows 應用程式，v120_xp 代表會使用 Visual Studio 2013 工具組建置 Windows XP 應用程式。<br /><br />可讓組建產生 Visual Studio 2008 或 Visual Studio 2010 應用程式的目錄所在的路徑不包含 *version*，而 *platform* 預留位置代表 Itanium、Win32 或 x64 子目錄。 *toolset* 預留位置代表 v90 或 v100 工具組子目錄。|

## <a name="support-files"></a>支援檔案

支援檔案目錄包含具有下列副檔名的檔案：

|副檔名|說明|
|---------------|-----------------|
|.targets|包含 `Target` XML 元素，會指定目標所執行的工作。 也可能包含 `PropertyGroup`、`ItemGroup`、`ItemDefinitionGroup` 和使用者定義的 `Item` 元素，用來檔案和命令列選項指派給工作參數。<br /><br /> 如需詳細資訊，請參閱 [Target 元素 (MSBuild)](/visualstudio/msbuild/target-element-msbuild)。|
|.props|包含 `Property Group` 和使用者定義的 `Property` XML 元素，會指定在建置期間使用的檔案和參數設定。<br /><br /> 也可能包含指定其他設定的 `ItemDefinitionGroup` 和使用者定義 `Item` XML 元素。 定義於項目定義群組中的項目類似於屬性，但無法從命令列存取。 Visual Studio 專案檔通常會使用項目來代表設定，而不是使用屬性。<br /><br /> 如需詳細資訊，請參閱 [ItemGroup 元素 (MSBuild)](/visualstudio/msbuild/itemgroup-element-msbuild)、 
[ItemDefinitionGroup 元素 (MSBuild)](/visualstudio/msbuild/itemdefinitiongroup-element-msbuild) 和 [Item 元素 (MSBuild)](/visualstudio/msbuild/item-element-msbuild)。|
|.xml|包含會宣告和初始化 IDE 使用者介面元素 (例如屬性工作表和屬性頁) 以及文字方塊和清單方塊控制項的 XML 元素。<br /><br /> .xml 檔案可直接支援 IDE，而非 MSBuild。 不過，IDE 屬性的值會指派給組建屬性和項目。<br /><br /> 大部分的 .xml 檔案會位於地區設定特定子目錄中。 例如，English-US 區域的檔案會位於 $(VCTargetsPath)\1033\\ 中。|

## <a name="user-targets-and-properties"></a>使用者目標和屬性

若要在命令列上最有效地使用 MSBuild，最好先知道哪些屬性和目標有用且相關。 大部分屬性和目標都有助於實作 Visual Studio 建置系統，但無法與使用者產生關聯。 本節說明一些有用的使用者導向屬性和目標。

### <a name="platformtoolset-property"></a>PlatformToolset 屬性

`PlatformToolset` 屬性會決定要在組建中使用的 MSVC 工具組。 依預設會使用目前的工具組。 設定這個屬性時，屬性的值會與常值字串串連來而形成目錄的路徑，且其中包含為特定平台建置專案所需的屬性和目標檔案。 必須安裝平台工具組，才能使用該平台工具組版本來建置。

例如，將 `PlatformToolset` 屬性設為 `v140`，會使用 Visual Studio 2015 工具和程式庫來建置您的應用程式：

`msbuild myProject.vcxproj /p:PlatformToolset=v140`

### <a name="preferredtoolarchitecture-property"></a>PreferredToolArchitecture 屬性

`PreferredToolArchitecture` 屬性會決定要在組建中使用 32 位元還是 64 位元編譯器和工具。 此屬性不會影響輸出平台架構或組態。 根據預設，若未設定此屬性，MSBuild 將會使用 x86 版本的編譯器和工具。

例如，將 `PreferredToolArchitecture` 屬性設為 `x64`，會使用 64 位元編譯器和工具來建置您的應用程式：

`msbuild myProject.vcxproj /p:PreferredToolArchitecture=x64`

### <a name="useenv-property"></a>UseEnv 屬性

根據預設，目前專案的平台特定設定會覆寫 PATH、INCLUDE、LIB、LIBPATH、CONFIGURATION 和 PLATFORM 等環境變數。 將 `UseEnv` 屬性設為 **true**，可保證不會覆寫環境變數。

`msbuild myProject.vcxproj /p:UseEnv=true`

### <a name="targets"></a>目標

Visual Studio 支援檔案中有數百個目標。 不過，大部分都是使用者可忽略的系統導向目標。 大部分系統目標都會以底線 (_) 開頭，或具有以 "PrepareFor"、"Compute"、"Before"、"After"、"Pre" 或 "Post" 開頭的名稱。

下表列出數個有用的使用者導向目標。

|Target|說明|
|------------|-----------------|
|BscMake|執行 Microsoft Browse Information Maintenance Utility 工具 (bscmake.exe)。|
|組建|建置專案。<br /><br /> 這是專案的預設目標。|
|ClCompile|執行 MSVC 編譯器工具 (cl.exe)。|
|清除|刪除暫存檔和中繼組建檔案。|
|Lib|執行 Microsoft 32 位元程式庫管理員工具 (lib.exe)。|
|連結|執行 MSVC 連結器工具 (link.exe)。|
|ManifestResourceCompile|從資訊清單中擷取資源清單，然後執行 Microsoft Windows 資源編譯器工具 (rc.exe)。|
|Midl|執行 Microsoft 介面定義語言 (MIDL) 編譯器工具 (midl.exe)。|
|重建|清除並建置您的專案。|
|ResourceCompile|執行 Microsoft Windows 資源編譯器工具 (rc.exe)。|
|XdcMake|執行 XML 文件工具 (xdcmake.exe)。|
|Xsd|執行 XML 結構描述定義工具 (xsd.exe)。 請參閱下列注意事項。|

> [!NOTE]
> 在 Visual Studio 2017 和更新版本中，**xsd** 檔案的 C++ 專案支援已過時。 您仍然可以將 **CppCodeProvider.dll** 手動新增至 GAC 來使用 **Microsoft.VisualC.CppCodeProvider**。

## <a name="see-also"></a>另請參閱

[MSBuild 工作參考](/visualstudio/msbuild/msbuild-task-reference)<br/>
[BscMake 工作](/visualstudio/msbuild/bscmake-task)<br/>
[CL 工作](/visualstudio/msbuild/cl-task)<br/>
[CPPClean 工作](/visualstudio/msbuild/cppclean-task)<br/>
[LIB 工作](/visualstudio/msbuild/lib-task)<br/>
[Link 工作](/visualstudio/msbuild/link-task)<br/>
[MIDL 工作](/visualstudio/msbuild/midl-task)<br/>
[MT 工作](/visualstudio/msbuild/mt-task)<br/>
[RC 工作](/visualstudio/msbuild/rc-task)<br/>
[SetEnv 工作](/visualstudio/msbuild/setenv-task)<br/>
[VCMessage 工作](/visualstudio/msbuild/vcmessage-task)<br/>
[XDCMake 工作](/visualstudio/msbuild/xdcmake-task)<br/>
