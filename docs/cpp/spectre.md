---
title: spectre
ms.date: 1/23/2018
f1_keywords:
- spectre_cpp
- spectre
- nomitigation
helpviewer_keywords:
- __declspec keyword (C++), spectre
- spectre __declspec keyword
ms.openlocfilehash: 2377a3c23be1e27bfe4f2df23eb00823635fa05d
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62267254"
---
# <a name="spectre"></a>spectre

**Microsoft 專屬**

會告知編譯器不要插入 Spectre 變異 1 推測性執行的屏障指示函式。

## <a name="syntax"></a>語法

> **__declspec( spectre(nomitigation) )**

## <a name="remarks"></a>備註

[/Qspectre](../build/reference/qspectre.md)編譯器選項會導致編譯器插入推測性執行的屏障指示分析指出 Spectre 變異 1 安全性弱點的存在。 發出的特定指示取決於處理器。 雖然這些指示應該擁有對程式碼大小或效能的影響最小，可能是您的程式碼不會受到這項弱點，而且需要最大效能。

專家 analysis 可能會判斷函式是安全從 Spectre 變異 1 界限檢查略過缺失。 在此情況下，您可以藉由套用隱藏的函式中的風險降低程式碼產生`__declspec(spectre(nomitigation))`函式宣告。

> [!CAUTION]
> **/Qspectre**推測性執行的屏障指示提供重要的安全性保護，且對效能造成的影響微乎其微。 因此，除了在少數函式的效能為重要考量，以及函式已知為安全的情況以外，建議您不要抑制這些檢查。

## <a name="example"></a>範例

下列程式碼顯示如何使用 `__declspec(spectre(nomitigation))`。

```cpp
// compile with: /c /Qspectre
static __declspec(spectre(nomitigation))
int noSpectreIssues() {
    // No Spectre variant 1 vulnerability here
    // ...
    return 0;
}

int main() {
    noSpectreIssues();
    return 0;
}
```

**結束 Microsoft 專屬**

## <a name="see-also"></a>另請參閱

[__declspec](../cpp/declspec.md)<br/>
[關鍵字](../cpp/keywords-cpp.md)<br/>
[/Qspectre](../build/reference/qspectre.md)
