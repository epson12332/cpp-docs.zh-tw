---
title: /sdl (啟用其他安全性檢查)
ms.date: 11/26/2018
f1_keywords:
- VC.Project.VCCLCompilerTool.SDLCheck
ms.assetid: 3dcf86a0-3169-4240-9f29-e04a9f535826
ms.openlocfilehash: 0618b796d492395c3e0e5413047ac0260082baff
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62318442"
---
# <a name="sdl-enable-additional-security-checks"></a>/sdl (啟用其他安全性檢查)

加入建議的安全性開發週期 (SDL) 檢查。 這些檢查包括額外的安全性相關警告 (視為錯誤)，以及其他安全程式碼產生功能。

## <a name="syntax"></a>語法

```
/sdl[-]
```

## <a name="remarks"></a>備註

**/sdl**可讓所提供的基準安全性檢查的超集[/GS](gs-buffer-security-check.md) ，並覆寫 **/GS-**。 根據預設， **/sdl**已關閉。 **/sdl-** 停用其他安全性檢查。

## <a name="compile-time-checks"></a>編譯時期檢查

**/sdl**可讓這些警告視為錯誤：

|/sdl 啟用的警告|對應的命令列參數|描述|
|------------------------------|-------------------------------------|-----------------|
|[C4146](../../error-messages/compiler-warnings/compiler-warning-level-2-c4146.md)|/we4146|一元減號運算子套用至不帶正負號的類型，產生不帶正負號的結果。|
|[C4308](../../error-messages/compiler-warnings/compiler-warning-level-2-c4308.md)|/we4308|將負整數常數轉換為 unsigned 類型，產生一個可能無意義的結果。|
|[C4532](../../error-messages/compiler-warnings/compiler-warning-level-1-c4532.md)|/we4532|利用`continue`，`break`或是`goto`中的關鍵字`__finally` / `finally`區塊有未定義的行為異常終止期間。|
|[C4533](../../error-messages/compiler-warnings/compiler-warning-level-1-c4533.md)|/we4533|初始化變數的程式碼不會執行。|
|[C4700](../../error-messages/compiler-warnings/compiler-warning-level-1-and-level-4-c4700.md)|/we4700|使用了未初始化的區域變數。|
|[C4703](../../error-messages/compiler-warnings/compiler-warning-level-4-c4703.md)|/we4703|使用了可能未初始化的本機指標變數。|
|[C4789](../../error-messages/compiler-warnings/compiler-warning-level-1-c4789.md)|/we4789|當使用特定 C 執行階段 (CRT) 函式時發生緩衝區滿溢。|
|[C4995](../../error-messages/compiler-warnings/compiler-warning-level-3-c4995.md)|/we4995|使用函式標記為 pragma[已被取代](../../preprocessor/deprecated-c-cpp.md)。|
|[C4996](../../error-messages/compiler-warnings/compiler-warning-level-3-c4996.md)|/we4996|使用函式標示[已被取代](../../cpp/deprecated-cpp.md)。|

## <a name="runtime-checks"></a>執行階段檢查

當 **/sdl**已啟用，則編譯器會產生程式碼來執行這些檢查，在執行階段：

- 啟用 strict 模式 **/GS**執行階段的緩衝區滿溢偵測，相當於使用編譯`#pragma strict_gs_check(push, on)`。

- 執行有限的指標淨化。 在未涉及取值的運算式中和沒有使用者定義解構函式的類型中，指標參考在呼叫 `delete` 之後設定為非有效位址。 這有助於防止過時的指標參考重複使用。

- 執行類別成員指標初始化。 自動初始化類別成員指標型別**nullptr**在物件具現化 （在建構函式執行之前）。 這有助於避免使用未初始化的指標，建構函式未明確初始化。 稱為編譯器產生的成員指標初始化，只要：

  - 物件未配置的自訂 （使用者定義） `operator new`

  - 物件未配置陣列的一部分 (例如`new A[x]`)

  - 未受管理或匯入類別

  - 此類別具有使用者定義的預設建構函式。

  若要由編譯器所產生的類別初始化函式初始化，成員必須是指標，並不是屬性或常數。

## <a name="remarks"></a>備註

如需詳細資訊，請參閱 <<c0> [ 警告、 /sdl 和改善未初始化的變數偵測](https://cloudblogs.microsoft.com/microsoftsecure/2012/06/06/warnings-sdl-and-improving-uninitialized-variable-detection/)。

#### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>在 Visual Studio 開發環境中設定這個編譯器選項

1. 開啟專案的 [屬性頁]  對話方塊。 如需詳細資訊，請參閱 <<c0> [ 設定C++Visual Studio 中的編譯器和組建屬性](../working-with-project-properties.md)。</c0>

1. 選取  **C /C++** 資料夾。

1. 在 **一般**頁面上，選取 從 選項**SDL 檢查**下拉式清單。

## <a name="see-also"></a>另請參閱

[MSVC 編譯器選項](compiler-options.md)<br/>
[MSVC 編譯器命令列語法](compiler-command-line-syntax.md)
