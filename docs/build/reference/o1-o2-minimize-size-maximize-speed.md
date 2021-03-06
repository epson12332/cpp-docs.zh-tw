---
title: /O1、/O2 (最小大小、最快速度)
ms.date: 09/25/2017
f1_keywords:
- /o2
- /o1
helpviewer_keywords:
- maximize speed compiler option [C++]
- minimize size compiler option [C++]
- -O2 compiler option [C++]
- fast code
- small code
- O2 compiler option [C++]
- /O2 compiler option [C++]
- -O1 compiler option [C++]
- O1 compiler option [C++]
- /O1 compiler option [C++]
ms.assetid: 2d1423f5-53d9-44da-8908-b33a351656c2
ms.openlocfilehash: d33fe6bceae09267fd3f79ffe3dc26864e87c764
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62320353"
---
# <a name="o1-o2-minimize-size-maximize-speed"></a>/O1、/O2 (最小大小、最快速度)

選取一組預先定義會影響大小的選項和產生的程式碼的速度。

## <a name="syntax"></a>語法

> /O1 /O2

## <a name="remarks"></a>備註

**/O1**並 **/o2**編譯器選項會設定幾個特定的最佳化選項一次的快速方法。 **/O1**選項會設定個別的最佳化選項，在大部分的情況下建立最小的程式碼。 **/O2**選項會設定在大部分的情況下建立最快的程式碼的選項。 **/O2**選項是發行組建的預設值。 下表顯示特定選項所設定的 **/o1**並 **/o2**:

|選項|相當於|
|------------|-------------------|
|**/ O1** （最小大小）|[/Og](og-global-optimizations.md) [/Os](os-ot-favor-small-code-favor-fast-code.md) [/Oy](oy-frame-pointer-omission.md) [/Ob2](ob-inline-function-expansion.md) [/GF](gf-eliminate-duplicate-strings.md) [/Gy](gy-enable-function-level-linking.md)|
|**/ O2** （最快速度）|[/Og](og-global-optimizations.md) [/Oi](oi-generate-intrinsic-functions.md) [/Ot](os-ot-favor-small-code-favor-fast-code.md) [/Oy](oy-frame-pointer-omission.md) [/Ob2](ob-inline-function-expansion.md) [/GF](gf-eliminate-duplicate-strings.md) [/Gy](gy-enable-function-level-linking.md)|

**/ O1**並 **/o2**互斥。

> [!NOTE]
> **x86 特定**這些選項會隱含使用框架指標省略 ([/Oy](oy-frame-pointer-omission.md)) 選項。

### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>在 Visual Studio 開發環境中設定這個編譯器選項

1. 開啟專案的 [屬性頁]  對話方塊。 如需詳細資訊，請參閱 <<c0> [ 設定C++Visual Studio 中的編譯器和組建屬性](../working-with-project-properties.md)。</c0>

1. 底下**組態屬性**，開啟**C /C++**  ，然後選擇 [**最佳化**] 屬性頁。

1. 修改**最佳化**屬性。

### <a name="to-set-this-compiler-option-programmatically"></a>若要以程式方式設定這個編譯器選項

- 請參閱 <xref:Microsoft.VisualStudio.VCProjectEngine.VCCLCompilerTool.Optimization%2A>。

## <a name="see-also"></a>另請參閱

[/O 選項 (最佳化程式碼)](o-options-optimize-code.md)<br/>
[MSVC 編譯器選項](compiler-options.md)<br/>
[MSVC 編譯器命令列語法](compiler-command-line-syntax.md)<br/>
[/EH (例外狀況處理模型)](eh-exception-handling-model.md)
