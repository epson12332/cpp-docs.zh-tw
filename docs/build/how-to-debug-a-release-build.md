---
title: HOW TO：偵錯發行組建
ms.date: 11/04/2016
helpviewer_keywords:
- debugging [C++], release builds
- release builds, debugging
ms.assetid: d333e4d1-4e6c-4384-84a9-cb549702da25
ms.openlocfilehash: 6d93fac4e980085c322acb55e6f8758e6cea0a00
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62188960"
---
# <a name="how-to-debug-a-release-build"></a>HOW TO：偵錯發行組建

您可以偵錯應用程式的發行組建。

### <a name="to-debug-a-release-build"></a>若要偵錯發行組建

1. 開啟**屬性頁**專案 對話方塊。 如需詳細資訊，請參閱 <<c0> [ 設定C++Visual Studio 中的編譯器和組建屬性](working-with-project-properties.md)。</c0>

1. 按一下  **C /C++** 節點。 設定**偵錯資訊格式**要[C7 相容 (/ Z7)](reference/z7-zi-zi-debug-information-format.md)或是**程式資料庫 (/Zi)**。

1. 依序展開**連結器**然後按一下**一般**節點。 設定**啟用累加連結**要[否 (/ /INCREMENTAL: NO)](reference/incremental-link-incrementally.md)。

1. 選取 **偵錯**節點。 設定**產生偵錯資訊**要[是 (/debug)](reference/debug-generate-debug-info.md)。

1. 選取 **最佳化**節點。 設定**參考**要[/opt: ref](reference/opt-optimizations.md)並**啟用 COMDAT 摺疊**至[/opt: icf](reference/opt-optimizations.md)。

1. 您現在可以偵錯發行組建的應用程式。 若要發現問題，逐步執行程式碼 （或使用 Just In Time 偵錯），直到您找出發生失敗的位置，然後判斷不正確的參數或程式碼。

   如果應用程式是在偵錯組建中，但在發行組建會失敗，其中一個編譯器最佳化可能會公開於原始碼的缺失。 若要找出問題，請停用的每個原始程式碼檔案所選取的最佳化直到您找出檔案，並且會造成問題的最佳化功能。 （若要加速此程序，您可以將檔案分割成兩個群組、 停用最佳化其中一個群組，而且當您在群組中，找到問題時繼續進行分割，直到您分辨出問題檔案）。

   您可以使用[/RTC](reference/rtc-run-time-error-checks.md)嘗試公開偵錯組建中的這類錯誤。

   如需詳細資訊，請參閱 <<c0> [ 最佳化您的程式碼](optimizing-your-code.md)。

## <a name="see-also"></a>另請參閱

[解決發行組建的問題](fixing-release-build-problems.md)
