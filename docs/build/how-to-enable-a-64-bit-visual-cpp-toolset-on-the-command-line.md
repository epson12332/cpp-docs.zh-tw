---
title: 作法：在命令列上啟用 64 位元 MSVC 工具組
ms.date: 05/16/2019
helpviewer_keywords:
- x64 [C++]
- 64-bit compiler [C++], command line usage
- 64-bit compiler [C++], toolset enabling at command line
- command line [C++], 64-bit compiler
- Itanium [C++], command-line compiler
- IPF
- Itanium [C++]
- IPF, command-line compiler
- x64 [C++], command-line compiler
ms.assetid: 4da93a19-e20d-4778-902a-5eee9a6a90b5
ms.openlocfilehash: 24dd6355578e8e9e00064ccfdf31bc51b7fd12ec
ms.sourcegitcommit: a10c9390413978d36b8096b684d5ed4cf1553bc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/17/2019
ms.locfileid: "65836980"
---
# <a name="how-to-enable-a-64-bit-x64-hosted-msvc-toolset-on-the-command-line"></a>作法：在命令列上啟用 64 位元、x64 架構的 MSVC 工具組

Visual Studio 包含 C++編譯器、連結器和其他工具，可用來建立您可以在 32 位元、64 位元或 ARM 型 Windows 作業系統上執行的平台特定應用程式版本。 其他選擇性的 Visual Studio 工作負載可讓您使用 C++ 工具將其他平台設為目標，例如 iOS、Android 和 Linux。 預設組建架構會使用 32 位元、x86 架構的工具來建置 32 位元、x86 原生 Windows 程式碼。 不過，您的電腦可能是 64 位元。 當您建置適用於 x86、x64 或 ARM 處理器的程式碼時，您可以使用 64 位元、x64 架構的工具組，以善用 64 位元程式碼可用的處理器和記憶體空間。

> [!NOTE]
> 如需各個 Visual Studio 版本隨附之特定工具的相關資訊，請參閱 [Visual Studio 版本中的 Visual C++ 工具和功能](../overview/visual-cpp-tools-and-features-in-visual-studio-editions.md)。
>
> 如需如何使用 Visual Studio IDE 建立 64 位元應用程式的詳細資訊，請參閱[如何：將 Visual C++ 專案設定為以 64 位元 x64 平台為目標](how-to-configure-visual-cpp-projects-to-target-64-bit-platforms.md)。

當您在 Visual Studio 安裝程式中安裝 C++ 工作負載時，一律會安裝 32 位元、x86 架構的原生和跨平台編譯器工具來建置 x86 和 x64 程式碼。 如果您納入通用 Windows 平台工作負載，則也會安裝 x86 架構的跨平台編譯器工具來建置 ARM 程式碼。 如果您在 64 位元、x64 處理器上安裝這些工作負載，您也將取得可建置 x86、x64 和 ARM 程式碼的 64 位元原生和跨平台編譯器工具。 32 位元和 64 位元工具會產生相同的程式碼，但是 64 位元工具對於先行編譯標頭符號和整個程式最佳化 ([/GL](reference/gl-whole-program-optimization.md) 和 [/LTCG](reference/ltcg-link-time-code-generation.md)) 選項可支援較多的記憶體。 如果在使用 32 位元工具時受限於記憶體限制，請嘗試使用 64 位元工具。

## <a name="use-a-64-bit-hosted-developer-command-prompt-shortcut"></a>使用 64 位元架構的開發人員命令提示字元捷徑

當 Visual Studio 安裝在 64 位元的 Windows 作業系統上時，64 位元、x64 架構的原生和跨平台編譯器會有額外的開發人員命令提示字元捷徑可供使用。 若要在 Windows 10 上存取這些命令提示字元，請在 [開始] 功能表上開啟您的 Visual Studio 版本的資料夾 (例如 **Visual Studio 2019**)，然後選擇其中一個 x64 原生或跨平台工具開發人員命令提示字元。 若要在 Windows 8 上存取這些命令提示字元，請開啟 [開始] 畫面上的 [所有應用程式]。 在已安裝的 Visual Studio 版本的標題下方，開啟 **Visual Studio** 資料夾 (在舊版的 Visual Studio 中，其名稱可能是 **Visual Studio Tools**)。 在舊版 Windows 上選擇 [開始]，展開 [所有程式]，然後開啟您的 **Visual Studio** 版本的資料夾 (在舊版的 Visual Studio 上為 **Visual Studio Tools**)。 如需詳細資訊，請參閱[開發人員命令提示字元捷徑](building-on-the-command-line.md#developer_command_prompt_shortcuts)。

## <a name="use-vcvarsallbat-to-set-a-64-bit-hosted-build-architecture"></a>使用 Vcvarsall.bat 設定 64 位元架構的組建架構

藉由執行 vcvarsall.bat 命令檔，任何原生或跨平台編譯器工具的組建組態均可在命令列上使用。 此命令檔會設定可在現有的命令提示字元視窗中啟用特定組建架構的路徑和環境變數。 如需特定指示，請參閱[開發人員命令檔位置](building-on-the-command-line.md#developer_command_file_locations)。

## <a name="see-also"></a>另請參閱

[設定適用於 64 位元、x64 目標的 C++ 專案](configuring-programs-for-64-bit-visual-cpp.md)<br/>
