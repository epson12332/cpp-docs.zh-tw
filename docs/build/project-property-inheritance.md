---
title: Visual Studio 專案中的屬性繼承 - C++
ms.date: 05/16/2019
helpviewer_keywords:
- C++ projects, property inheritance
ms.openlocfilehash: 472700226ffc1f265f6fab84dbd44fca651b3c87
ms.sourcegitcommit: a10c9390413978d36b8096b684d5ed4cf1553bc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/17/2019
ms.locfileid: "65837409"
---
# <a name="property-inheritance-in-visual-studio-projects"></a>Visual Studio 專案中的屬性繼承

Visual Studio 專案系統是以 MSBuild 為基礎，可定義用於建置任何類型專案的檔案格式和規則。 MSBuild 會管理針對多個組態與平台建置時所產生的大部分複雜性，但是您需要稍微了解其運作方式。 如果您想要定義自訂組態，或建立可重複使用的屬性集以便共用或匯入多個專案，這一點特別重要。

## <a name="the-vcxproj-file-props-files-and-targets-files"></a>.vcxproj 檔案、.props 檔案和 .targets 檔案

專案屬性會直接儲存在專案檔 (*.vcxproj) 中，或儲存在專案檔所匯入且提供預設值的其他 .targets 或 .props 檔案中。 若為 Visual Studio 2015，這些檔案位於 **\Program Files (x86)\MSBuild\Microsoft.Cpp\v4.0\V140**。 若為 Visual Studio 2017 或 Visual Studio 2019，這些檔案位於 **\\Program Files (x86)\\Microsoft Visual Studio\\&lt;2017 或 2019>\\_edition_\\Common7\\IDE\\VC\\VCTargets**，其中 _edition_ 是安裝的 Visual Studio 版本。 屬性也會儲存在您可能新增至自己專案的任何自訂 .props 檔案中。 除非您非常了解 MSBuild，否則強烈建議您不要手動編輯這些檔案，並改為在 IDE 中使用屬性頁來修改所有屬性，特別是那些參與繼承的屬性。

如先前所示，相同組態的相同屬性可能會在這些不同的檔案中指派不同的值。 當您建置專案時，MSBuild 引擎會以妥善定義的順序 (如下所述) 評估專案檔與所有匯入的檔案。 評估每個檔案時，任何在該檔案中定義的屬性值都會覆寫現有值。 任何未指定的值則會從稍早所評估的檔案繼承。 因此，當您使用屬性頁設定屬性時，請務必也要注意設定的位置。 如果在 .props 檔案中將屬性設定為 "X"，但此屬性在專案檔中設定為 "Y"，則專案將在屬性設定為 "Y" 的情況下建置。 如果相同屬性在專案項目 (例如 .cpp 檔案) 上設定為 "Z"，則 MSBuild 引擎會使用 "Z" 值。 

以下是基本繼承樹狀結構：

1. MSBuild CPP Toolset 的預設設定 (..\Program Files\MSBuild\Microsoft.Cpp\v4.0\Microsoft.Cpp.Default.props，由 .vcxproj 檔案匯入)。

2. 屬性工作表

3. .vcxproj 檔案  (可以覆寫預設及屬性工作表設定)。

4. 項目中繼資料

> [!TIP]
> 在屬性頁中，以 `bold` 表示的屬性是在目前內容中定義的。 以一般字型表示的屬性是繼承的。

## <a name="view-an-expanded-project-file-with-all-imported-values"></a>檢視展開的專案檔和所有匯入的值

有時候，檢視展開的檔案以判斷指定的屬性值如何繼承，十分有用。 若要檢視展開的版本，請在 Visual Studio 命令提示字元輸入下列命令  (將預留位置檔案名稱變更為您要使用的名稱)。

**msbuild /pp:** *temp* **.txt** *myapp* **.vcxproj**

除非您熟悉 MSBuild，不然展開的專案檔可能很龐大，而且難以了解。 以下是專案檔的基本結構：

1. 基本專案屬性，IDE 不會公開這些屬性。

2. 匯入 Microsoft.cpp.default.props，這會定義一些與工具組無關的基本屬性。

3. 全域組態屬性 (在 [組態概觀] 頁面上公開為 **PlatformToolset** 和 **Project** 預設屬性)。 這些屬性會決定 Microsoft.cpp.props 在下一個步驟中匯入哪些工具組和內建屬性工作表。

4. 匯入 Microsoft.cpp.props，這會設定大部分的專案預設值。

5. 匯入所有屬性工作表，包括 .user 檔案。 這些屬性工作表可能會覆寫除了 **PlatformToolset** 和 **Project** 預設屬性以外的所有屬性。

6. 剩餘的專案組態屬性。 這些值可以覆寫屬性工作表上已設定的屬性。

7. 項目 (檔案) 以及其中繼資料。 這些項目永遠握有 MSBuild 評估規則的最後決定權，即使是在其他屬性和匯入之前出現。

如需詳細資訊，請參閱 [MSBuild 屬性](/visualstudio/msbuild/msbuild-properties)。

## <a name="build-configurations"></a>組建組態

組態只是已指定名稱的任意一組屬性。 Visual Studio 提供一些偵錯和發行組態，每個都會針對偵錯組建或發行組建適當地設定各種屬性。 您可以使用 [組態管理員]，將自訂組態定義為針對組建之特定類別來分組屬性的便利方式。 

若要深入了解組建組態，請依據您的設定，選擇 [檢視 &#124;  屬性管理員] 或 [檢視 &#124; 其他視窗 &#124; 屬性管理員] 來開啟 [屬性管理員]。 **屬性管理員**包含專案中每個組態/平台配對的節點。 每個節點下都是屬性工作表 (.props 檔案) 的節點，可為該組態設定一些特定屬性。

![屬性管理員](media/property-manager.png "屬性管理員")

如果您移至 [屬性頁] 中的 [一般] 窗格，並將 [字元集] 屬性設定為 [未設定] 而非 [使用 Unicode]，然後按一下 [確定]，[屬性管理員] 會顯示目前的組態沒有 [Unicode 支援] 屬性工作表，但它仍會用於其他組態。

如需有關屬性管理員和屬性工作表的詳細資訊，請參閱[共用或重複使用 Visual StudioC++ 專案設定](create-reusable-property-configurations.md)。

> [!TIP]
> .user 檔案是一項舊版功能，建議您將其刪除，以根據組態/平台將屬性正確分組。



