---
title: /constexpr （控制 constexpr 評估）
ms.date: 08/15/2017
f1_keywords:
- /constexpr
- -constexpr
helpviewer_keywords:
- /constexpr control constexpr evaluation [C++]
- -constexpr control constexpr evaluation [C++]
- constexpr control constexpr evaluation [C++]
ms.assetid: 76d56784-f5ad-401d-841d-09d1059e8b8c
ms.openlocfilehash: 178acc548fb9c89dcfde104d2a12d85637440e28
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62294248"
---
# <a name="constexpr-control-constexpr-evaluation"></a>/constexpr （控制 constexpr 評估）

使用 **/constexpr**編譯器選項來控制參數**constexpr**在編譯時期評估。

## <a name="syntax"></a>語法

> **/constexpr:depth**<em>N</em>
>  **/constexpr:backtrace**<em>N</em>
>  **/constexpr:steps**<em>N</em>

## <a name="arguments"></a>引數

**深度**<em>N</em>限制的遞迴深度**constexpr**函式引動過程*N*層級。 預設值為 512。

**backtrace**<em>N</em>最多顯示*N* **constexpr**診斷中的評估。 預設值為 10。

**步驟**<em>N</em>終止**constexpr**之後評估*N*步驟。 預設值是 100,000。

## <a name="remarks"></a>備註

**/Constexpr**編譯器選項可控制的編譯時期評估**constexpr**運算式。 評估步驟、 遞迴層級和 backtrace 深度控制上花費太多時間時，防止編譯器**constexpr**評估。 如需詳細資訊**constexpr**語言項目，請參閱[constexpr (C++)](../../cpp/constexpr-cpp.md)。

**/Constexpr**選項會在 Visual Studio 2015 開始提供。

### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>在 Visual Studio 開發環境中設定這個編譯器選項

1. 開啟您的專案**屬性頁** 對話方塊。

2. 底下**組態屬性**，展開**C /C++** 資料夾，然後選擇 [**命令列**] 屬性頁。

3. 輸入任何 **/constexpr**編譯器選項**其他選項** 方塊中。 選擇 **[確定]** 或是**套用**以儲存變更。

### <a name="to-set-this-compiler-option-programmatically"></a>若要以程式方式設定這個編譯器選項

- 請參閱 <xref:Microsoft.VisualStudio.VCProjectEngine.VCCLCompilerTool.AdditionalOptions%2A>。

## <a name="see-also"></a>另請參閱

[MSVC 編譯器選項](compiler-options.md)<br/>
[MSVC 編譯器命令列語法](compiler-command-line-syntax.md)
