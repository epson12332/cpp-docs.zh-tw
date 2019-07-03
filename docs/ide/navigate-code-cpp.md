---
title: 在 Visual Studio 中巡覽 C++ 程式碼
description: 在 Visual Studio 中使用各種工具來巡覽您的 C++ 程式碼基底。
ms.date: 05/28/2019
ms.openlocfilehash: 5f01307cc82fb1e61ba6fd0c922ea376279fba8b
ms.sourcegitcommit: 65ed563a8a1d4d90f872a2a6edcb086f84ec9f77
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2019
ms.locfileid: "66742034"
---
# <a name="navigate-c-code-in-visual-studio"></a>在 Visual Studio 中巡覽 C++ 程式碼

Visual Studio 提供一套工具，可讓您快速且有效率地巡覽程式碼基底。

## <a name="open-an-included-file"></a>開啟包含的檔案

以滑鼠右鍵按一下 `#include` 指示詞，然後選擇 [移至文件]  ，或將游標停留在該行並按下 **F12**，以開啟檔案。

![C&#43; &#43; [移至文件] 功能表選項](../ide/media/go-to-document.png "移至文件")

## <a name="toggle-headercode-file"></a>切換標頭/程式碼檔

您可以在標頭檔和其對應的原始程式檔之間切換，方法是以滑鼠右鍵按一下檔案中的任何位置，然後選擇 [切換標頭/程式碼檔案]  或按下 **Ctrl + K、Ctrl + O**。

## <a name="go-to-definitiondeclaration"></a>移至定義/宣告

您可以在編輯器中按一下滑鼠右鍵，然後選擇 [移至定義]  ，或按下 **F12**，巡覽至程式碼符號的定義。 您可以同樣地在操作功能表上按一下滑鼠右鍵，或按下 **Ctrl + F12** 來巡覽至宣告。

![C&#43; &#43; 移至定義](../ide/media/go-to-def.png "移至定義")

## <a name="go-to"></a>到

[移至]  係指一組瀏覽功能，每個功能都會根據您指定的篩選條件，提供特定種類的結果。 

您可以使用 **Ctrl + ,** 開啟 [移至]  。 這會在您正在編輯的文件上建立搜尋方塊。

![C&#43;&#43; 移至](../ide/media/go-to-cpp.png "移至")

[移至]  包含這些搜尋篩選條件：

- **移至指定行 (Ctrl + G)** ：快速跳至您目前文件中的不同行
- **移至全部 (Ctrl + ,)** 或 **(Ctrl + T)** ：搜尋結果包含底下所有項目
- **移至檔案 (Ctrl 1、F)** ：搜尋您解決方案中的檔案
- **移至類型 (Ctrl 1、T)** ：搜尋結果包括：
  - 類別、結構、列舉
  - 介面和委派 (僅限受控程式碼)
- **移至成員 (Ctrl 1、M)** ：搜尋結果包括：
  - 全域變數和全域函式
  - 類別成員變數和成員函式
  - 常數
  - 列舉項目
  - 屬性和事件
- **移至符號 (Ctrl 1、S)** ：搜尋結果包括：
  - 移至類型和移至成員的結果
  - 所有剩餘的 C++ 語言建構，包括巨集

當您第一次使用 **Ctrl +** 叫用 [移至]  時，會啟用 [移至全部]  (對搜尋結果沒有篩選條件)。 接著可以使用搜尋文字方塊附近的按鈕，選取您所需的篩選條件。 您可以使用特定篩選條件對應的鍵盤快速鍵來叫用它。 這麼做會開啟 [移至]  搜尋方塊，並預先選取該篩選條件。 所有鍵盤快速鍵都可以進行設定。

若要套用文字篩選條件，請在搜尋查詢開頭使用篩選條件的對應字元，後面接著空格。 ([移至行]  可以選擇性地省略空格。)以下是可用的文字篩選條件：

- 移至全部：(無文字篩選條件)
- 移至行號：：
- 移至檔案：f
- 移至型別：t
- 移至成員：m
- 移至符號：#

下列範例示範使用 'f' 篩選條件的「移至檔案」  作業結果：

![C&#43;&#43; [移至] 功能表](../ide/media/vs2017-go-to-results.png "移至功能表")

若要查看文字篩選條件的清單，請鍵入 ? 後面接著空格。 您也可以使用 [編輯]  功能表存取 [移至]  命令。 這是提醒您自己主要 [移至] 鍵盤快速鍵的另一種方法。

![C&#43;&#43; [移至] 功能表](../ide/media/go-to-menu-cpp.png "移至功能表")

## <a name="find--find-in-files"></a>尋找/檔案中尋找

您可以執行文字搜尋，使用 [尋找] (Ctrl + F)  或 [在檔案中尋找] (Ctrl + Shift + F)  來搜尋解決方案中的任何項目。

尋找範圍可以設定為選取範圍、目前文件、所有開啟的文件、目前專案，或整個解決方案。 您可以使用規則運算式和純文字。 它也會自動在 IDE 中醒目提示所有相符項目。

![C&#43;&#43; 尋找](../ide/media/find-cpp.png "尋找")

[在檔案中尋找]  是 [尋找]  的更強大版本，它會在 [尋找結果]  視窗中顯示結果。 您可以搜尋外部程式碼相依性、依檔案類型篩選等。 

![C&#43;&#43; 在檔案中尋找](../ide/media/find-in-files-cpp.png "在檔案中尋找")

您可以將 [在檔案中尋找]  結果組織成兩個視窗。 您可以同時附加多個搜尋結果。 按一下結果以移至檔案中的該位置。

![C&#43;&#43; 在檔案中尋找](../ide/media/vs2017-find-in-files-results.png "在檔案中尋找")

如需詳細資訊，請參閱 Visual Studio 文件中的[＜在檔案中尋找＞](/visualstudio/ide/find-in-files)。

## <a name="find-all-references"></a>尋找所有參考

若要在程式碼基底中尋找符號的所有使用方式，請將插入號放在符號處或符號之後，然後以滑鼠右鍵按一下並選擇 [尋找所有參考]  。 您可以用許多不同的方式篩選、排序或分組結果。 結果會以累加方式填入。 它們會分類為讀取或寫入，協助您了解解決方案中的是什麼，而非系統標頭或其他程式庫。

![C&#43;&#43; 尋找所有參考](../ide/media/find-all-references-results-cpp.png "尋找所有參考")

您會依下列類別來分組結果：

- 專案接著定義
- 僅定義
- 定義接著專案
- 定義接著路徑
- 定義、專案接著路徑

 #### <a name="filter-results"></a>篩選結果

若要篩選結果，請暫留在資料行，然後按一下快顯的篩選圖示。 您可以從第一個資料行篩選結果，以隱藏您可能不想看到的字串和註解參考等。

![C&#43;&#43; 尋找所有參考篩選條件](../ide/media/find-all-references-filters-cpp.png "尋找所有參考篩選條件")

- **確認的結果**：所搜尋符號的實際程式碼參考。 例如，搜尋稱為 `Size` 的成員函式呼叫會傳回所有 `Size` 參考，這些參考符合定義 `Size` 的類別範圍。

- **未確認的結果**：這個篩選條件預設為關閉，因為它會顯示名稱符合但不是您所搜尋符號之實際參考的符號。 例如，如果您有兩個各自定義成員函式 `Size` 的類別，且您在 `Class1` 物件的參考上搜尋 `Size`，則任何對於 `Class2` 的 `Size` 參考都會顯示為未確認。

- **未處理的結果**：[尋找所有參考]  作業在較大的程式碼基底上可能需要時間完成，因此結果清單會顯示「未處理」的結果。 未處理的結果與所搜尋符號名稱相符，但尚未確認為實際的程式碼參考。 您可以開啟此篩選條件以取得更快的結果。 但請留意，某些結果可能不是實際的參考。

 #### <a name="sort-results"></a>排序結果

您可以按一下任何資料行，依該資料行來排序結果。 您可以再按一下資料行來交換遞增/遞減的順序。

## <a name="navigation-bar"></a>巡覽列

您可以使用編輯器視窗上方的 [瀏覽列]  ，巡覽至檔案中的類型定義，或類型成員。

![C&#43;&#43; 瀏覽列](../ide/media/navbar-cpp.png "瀏覽列")

## <a name="see-also"></a>請參閱

[閱讀並了解 C++ 程式碼](read-and-understand-code-cpp.md)</br>
[編輯並重構 C++ 程式碼](read-and-understand-code-cpp.md)</br>
[使用 Live Share for C++ 共同作業](live-share-cpp.md)