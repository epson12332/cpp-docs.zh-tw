---
title: ATL Active Server Page 元件精靈
ms.date: 05/09/2019
helpviewer_keywords:
- ASP components, creating in ATL
ms.assetid: 5a5cb904-dbbf-44ea-ad3d-2ddd14c1d3c5
ms.openlocfilehash: a78beeab663ef1b467cdec32ca51132e8134a9b2
ms.sourcegitcommit: fc1de63a39f7fcbfe2234e3f372b5e1c6a286087
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/15/2019
ms.locfileid: "65707044"
---
# <a name="atl-active-server-page-component-wizard"></a>ATL Active Server Page 元件精靈

::: moniker range="vs-2019"

Visual Studio 2019 及更新版本中未提供此精靈。

::: moniker-end

::: moniker range="<=vs-2017"

此精靈可將 Active Server Pages (ASP) 元件插入至專案。 Microsoft Internet Information Services (IIS) 會使用 ASP 元件，作為其已增強網頁程式開發架構的一部分。

使用此精靈，您可以指定元件的執行緒模式及其彙總支援。 您也可以指定錯誤資訊介面、連接點，以及無限制執行緒封送處理器。

## <a name="remarks"></a>備註

從 Visual Studio 2008 開始，此精靈所產生的註冊指令碼會在 **HKEY_CURRENT_USER** 而非 **HKEY_LOCAL_MACHINE** 下方註冊它的 COM 元件。 若要修改此行為，請設定 ATL 精靈的 [為所有使用者註冊元件] 選項。

## <a name="names"></a>名稱

指定要新增至專案的物件、介面和類別名稱。 除了**簡短名稱**，所有其他方塊均可單獨編輯。 如果您變更**簡短名稱**的文字，該變更即會反映於此頁面的所有其他方塊名稱中。

如果您在 [COM] 區段中變更 **Coclass** 名稱，則變更會反映於 [型別] 和 [ProgID] 方塊中，但**介面**名稱不會變更。 此命名行為旨在讓您開發控制項時，能夠輕鬆地識別所有名稱。

### <a name="c"></a>C++

提供針對物件所建立的 C++ 類別相關資訊。

- **簡短名稱**

   設定物件的根名稱。 您提供的名稱可決定 `Class` 和 **Coclass** 名稱、**.cpp 檔案**和 **.h 檔案**名稱、**介面**名稱、**型別**名稱，以及 **ProgID** (但前提是您並未個別變更這些欄位)。

- **.h 檔案**

   設定新物件類別的標頭檔名稱。 根據預設，此名稱會以您在 [簡短名稱] 中提供的名稱為基礎。 按一下省略符號按鈕，將檔案名稱儲存至您選擇的位置，或將類別宣告附加至現有的檔案。 如果您選取現有的檔案，在您按一下精靈中的 [完成] 之前，精靈不會將它儲存至選取的位置。

   精靈不會覆寫檔案。 如果您選取現有檔案的名稱，當您按一下 [完成] 時，精靈會提示您指出是否應該將類別宣告附加至檔案的內容。 按一下 [是] 可附加檔案，按一下 [否] 可返回精靈並指定另一個檔案名稱。

- **類別**

   設定要建立的類別名稱。 此名稱會以您在**簡短名稱**中提供的名稱為基礎，前面加上 'C'，此為類別名稱的一般前置詞。

- **.cpp 檔**

   設定新物件類別的實作檔名稱。 根據預設，此名稱會以您在 [簡短名稱] 中提供的名稱為基礎。 按一下省略符號按鈕，將檔案名稱儲存至您選擇的位置。 在您按一下精靈中的 [完成] 之前，檔案不會儲存至選取的位置。

   精靈不會覆寫檔案。 如果您選取現有檔案的名稱，當您按一下 [完成] 時，精靈會提示您指出是否應該將類別實作附加至檔案的內容。 按一下 [是] 可附加檔案，按一下 [否] 可返回精靈並指定另一個檔案名稱。

- **使用屬性**

   指出物件是否會使用屬性。 如果您要將物件新增至屬性化的 ATL 專案，則此選項已選取且無法變更。 也就是說，您只能將屬性化的物件新增至透過屬性支援建立的專案。

   如果您針對不含屬性支援的 ATL 專案選取此選項，精靈會提示您指定是否要將屬性支援新增至專案。

   根據預設，針對未屬性化的專案，在您設定此選項後新增的任何物件都會指定為屬性化 (已選取核取方塊)。 您可以清除此方塊以新增未使用屬性的物件。

   如需詳細資訊，請參閱[應用程式設定，ATL 專案精靈](../../atl/reference/application-settings-atl-project-wizard.md)和[屬性的基本機制](../../windows/basic-mechanics-of-attributes.md)。

### <a name="com"></a>COM

提供物件 COM 功能的相關資訊。

- **Coclass**

   設定元件類別的名稱，其中包含物件所支援的介面清單。 如果您的專案或此物件會使用屬性，您就無法變更此選項，因為 ATL 未包含 **coclass** 屬性。

- **Type**

   設定將出現在 coclass 登錄中的物件描述。

- **Interface**

   設定您為物件建立的介面。 此介面包含您的自訂方法。

- **ProgID**

   設定容器可使用的名稱，而不是物件的 CLSID。

::: moniker-end

## <a name="see-also"></a>另請參閱

[ATL Active Server Page 元件](../../atl/reference/adding-an-atl-active-server-page-component.md)
