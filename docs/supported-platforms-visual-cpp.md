---
title: "支援的平台 (Visual C++) | Microsoft Docs"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: cpp-tools
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: C++
helpviewer_keywords:
- Visual C++, platforms supported
- platforms [C++]
ms.assetid: 0d893056-4008-411a-b3d1-5f57fd7da95c
caps.latest.revision: "22"
author: mikeblome
ms.author: mblome
manager: ghogen
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
ms.openlocfilehash: 78fac089c9b21825bfb014fe6f26776bac58bd93
ms.sourcegitcommit: ebec1d449f2bd98aa851667c2bfeb7e27ce657b2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/24/2017
---
# <a name="supported-platforms-visual-c"></a>支援的平台 (Visual C++)

使用 [!INCLUDE[vsprvs](assembler/masm/includes/vsprvs_md.md)] 所建置的應用程式可以在各種平台上做為目標執行，如下所示。  
  
|作業系統|x86|x64|ARM|  
|----------------------|---------|---------|---------|  
|Windows XP|X*|X*||  
|[!INCLUDE[WinXPSvr](build/includes/winxpsvr_md.md)]|X*|X*||  
|Windows Vista|X|X||  
|Windows Server 2008|X|X||  
|Windows 7|X|X||  
|Windows Server 2012 R2|X|X||  
|Windows 8|X|X|X|  
|Windows 8.1|X|X|X|  
|Windows 10|X|X|X|  
|Android **|X|X|X|  
|iOS **|X|X|X|  
|Linux ***|X|X|X|  
  
\* 您可使用 Visual Studio 2017、Visual Studio 2015、Visual Studio 2013 和 Visual Studio 2012 Update 1 或更新版本所隨附的 Windows XP 平台工具組，建置 Windows XP 與 [!INCLUDE[WinXPSvr](build/includes/winxpsvr_md.md)] 專案。 如需如何使用這個平台工具組的相關資訊，請參閱[為 Windows XP 設定程式](build/configuring-programs-for-windows-xp.md)。 如需變更平台工具組的其他資訊，請參閱[如何：修改目標 Framework 和平台工具組](build/how-to-modify-the-target-framework-and-platform-toolset.md)。  
  
\*\* 您可在 Visual Studio 安裝程式 (或是在 Visual Studio 2015 安裝程式中的選用**適用於跨平台行動裝置應用程式開發的 Visual C++** 元件) 中，安裝**使用 C++ 進行行動裝置開發**的工作負載，將 iOS 或 Android 平台設為目標。 如需指示，請參閱[安裝適用於跨平台行動裝置開發的 Visual C++](/visualstudio/cross-platform/install-visual-cpp-for-cross-platform-mobile-development)。 若要建置 iOS 程式碼，您必須具有 Mac 電腦，並且符合其他需求。 如需必要條件清單和安裝指示，請參閱[安裝和設定工具以使用 iOS 建置](/visualstudio/cross-platform/install-and-configure-tools-to-build-using-ios)。 您可以配合目標硬體來建置 x86 或 ARM 程式碼。 使用 x86 組態為 iOS 模擬器、Microsoft Visual Studio Emulator for Android 和一些 Android 裝置進行建置。 使用 ARM 組態為 iOS 裝置和大部分 Android 裝置進行建置。  
  
\*\*\* 您可在 Visual Studio 安裝程式中，安裝**使用 C++ 進行 Linux 開發**工作負載，將 Linux 平台設為目標。 如需指示，請參閱[下載、安裝及設定 Linux 工作負載](linux/download-install-and-setup-the-linux-development-workload.md)。 因為此工具組會編譯您在目標電腦上的可執行檔，所以可針對任何支援的架構進行建置。  

如需如何設定目標平台組態的資訊，請參閱[如何：將 Visual C++ 專案設定為以 64 位元 (x64) 平台為目標](build/how-to-configure-visual-cpp-projects-to-target-64-bit-platforms.md)。  
  
## <a name="see-also"></a>另請參閱  

[Visual Studio 版本中的 Visual C++ 工具和功能](ide/visual-cpp-tools-and-features-in-visual-studio-editions.md)   
[快速入門](/visualstudio/ide/getting-started-with-visual-cpp-in-visual-studio)