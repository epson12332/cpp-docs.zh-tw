---
title: /Zc:auto (推算變數類型)
ms.date: 02/28/2018
f1_keywords:
- /Zc:auto
helpviewer_keywords:
- -Zc compiler options (C++)
- Deduce variable type (C++)
- /Zc compiler options (C++)
- Zc compiler options (C++)
ms.assetid: 5f5bc102-44c3-4688-bbe1-080594dcee5c
ms.openlocfilehash: 9609bc484310fbc9999182add384eb4e438378bf
ms.sourcegitcommit: 7d64c5f226f925642a25e07498567df8bebb00d4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/08/2019
ms.locfileid: "65446237"
---
# <a name="zcauto-deduce-variable-type"></a>/Zc:auto (推算變數類型)

**/Zc: auto [-]** 編譯器選項會指示編譯器使用方式[auto 關鍵字](../../cpp/auto-keyword.md)來宣告變數。 如果您指定 [預設] 選項中， **/zc: auto**，編譯器會推斷所宣告的變數，從其初始化運算式的類型。 如果您指定 **/Zc:auto-**，編譯器會自動儲存類別將變數配置。

## <a name="syntax"></a>語法

> **/Zc:auto**[**-**]

## <a name="remarks"></a>備註

C++ 標準為 `auto` 關鍵字定義了原始和修訂的意義。 在 Visual Studio 2010 之前的關鍵字會宣告自動儲存類別; 中的變數也就是一個變數具有區域存留期。 從 Visual Studio 2010 開始，關鍵字會推斷變數，以從宣告的初始化運算式的型別。 使用  **/zc: auto [-]** 編譯器選項來告訴編譯器使用的原始或修訂的意義`auto`關鍵字。 **/Zc: auto**選項預設為開啟。 [/Permissive--](permissive-standards-conformance.md)選項不會變更預設值 **/zc: auto**。

編譯器會發出適當的診斷訊息，如果您使用`auto`關鍵字與牴觸的目前 **/zc: auto**編譯器選項。 如需詳細資訊，請參閱 < [auto 關鍵字](../../cpp/auto-keyword.md)。 如需有關具有視覺效果的一致性問題C++，請參閱[非標準行為](../../cpp/nonstandard-behavior.md)。

### <a name="to-set-this-compiler-option-in-visual-studio"></a>在 Visual Studio 中設定這個編譯器選項

1. 開啟專案的 [屬性頁]  對話方塊。 如需詳細資訊，請參閱 <<c0> [ 設定C++Visual Studio 中的編譯器和組建屬性](../working-with-project-properties.md)。</c0>

1. 選取 **組態屬性** > **C /C++** > **命令列**屬性頁。

1. 新增 **/zc: auto**或是 **/Zc:auto-** 來**其他選項：** 窗格。

## <a name="see-also"></a>另請參閱

[/Zc (一致性)](zc-conformance.md)<br/>
[auto 關鍵字](../../cpp/auto-keyword.md)
