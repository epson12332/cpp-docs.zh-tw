---
title: 設定命令列建置的路徑和環境變數
ms.custom: conceptual
ms.date: 05/06/2019
helpviewer_keywords:
- environment variables [C++]
- VCVARS32.bat file
- cl.exe compiler [C++], environment variables
- LINK tool [C++], environment variables
- PATH reserved word
- INCLUDE reserved word
- LINK tool [C++], path
- LIB environment variable
- compiling source code [C++], from command line
- environment variables [C++], CL compiler
ms.assetid: 99389528-deb5-43b9-b99a-03c8773ebaf4
ms.openlocfilehash: 30dadf365186ae74144a3225889c08eedfb89b47
ms.sourcegitcommit: da32511dd5baebe27451c0458a95f345144bd439
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/07/2019
ms.locfileid: "65217611"
---
# <a name="set-the-path-and-environment-variables-for-command-line-builds"></a>設定命令列建置的路徑和環境變數

Microsoft C++ (MSVC) 命令列建置工具需要安裝和組建組態的客製化的數個環境變數。 當C++Visual Studio 安裝程式安裝工作負載，它會建立自訂的命令檔或設定所需的環境變數的批次檔案。 安裝程式然後會使用這些命令檔案來建立 Windows 開始 功能表開啟 開發人員命令提示字元 視窗的快速鍵。 這些快速鍵設定環境變數以供特定建置組態。 當您想要使用命令列工具時，您可以執行其中一個捷徑，或您可以開啟純文字的命令提示字元 視窗，然後執行其中一個要自行設定組建設定環境的自訂命令檔。 如需詳細資訊，請參閱 <<c0> [ 使用 MSVC 工具組，從命令列](building-on-the-command-line.md)。

MSVC 命令列工具使用的路徑、 TMP、 INCLUDE、 LIB 和 LIBPATH 環境變數，並也使用您已安裝的工具、 平台和 Sdk 的特定其他環境變數。 甚至是簡單的 Visual Studio 安裝可能設定 20 個或多個環境變數。 由於這些環境變數的值專屬於您的安裝，而且您選擇的組建組態，而且可以變更產品更新或升級，我們強烈建議您使用開發人員命令提示字元捷徑或其中一個自訂設定，而不是自己設定這些 Windows 環境中的命令檔。

若要查看哪些環境變數所設定的開發人員命令提示字元捷徑，您可以使用 SET 命令。 開啟純文字的命令提示字元視窗，並擷取基準的 SET 命令的輸出。 開啟開發人員命令提示字元視窗，並擷取輸出的 SET 命令的比較。 例如 Visual Studio IDE 內建的 diff 工具可用來比較的環境變數，並請參閱什麼由開發人員命令提示字元設定。 編譯器和連結器所使用之特定環境變數的詳細資訊，請參閱[CL 環境變數](reference/cl-environment-variables.md)。

> [!NOTE]
>  數個命令列工具或工具選項，可能需要系統管理員權限。 如果您有權限問題，當您使用它們時，我們建議您開啟開發人員命令提示字元視窗中，使用**系統管理員身分執行**選項。 在 Windows 10 中，以滑鼠右鍵按一下以開啟 [命令提示字元] 視窗的捷徑功能表，然後選擇**更多**，**系統管理員身分執行**。

## <a name="see-also"></a>另請參閱

[從命令列使用 MSVC 工具組](building-on-the-command-line.md)<br/>
[MSVC 連結器參考](reference/linking.md)<br/>
[MSVC 連結器選項](reference/linker-options.md)<br/>
[MSVC 編譯器參考](reference/compiling-a-c-cpp-program.md)<br/>
[MSVC 編譯器選項](reference/compiler-options.md)
