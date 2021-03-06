---
title: 將類型和成員設為已被取代 (C++/CX)
ms.date: 12/30/2016
ms.assetid: b20b01c1-a439-4ff0-8cf3-d7280c492813
ms.openlocfilehash: 7f488dfa522c0b48c75150d40584b0946baae806
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62301496"
---
# <a name="deprecating-types-and-members-ccx"></a>將類型和成員設為已被取代 (C++/CX)

在C++/CX，生產者與取用者使用的 Windows 執行階段型別和成員取代[Deprecated](/uwp/api/windows.foundation.metadata.deprecatedattribute)支援屬性。 如果您使用的 API 已套用這個屬性，您會收到一個編譯時期警告訊息，表示 API 已被取代，此外建議替代的 API 以供使用。 在您的公用類型和方法，可以套用這個屬性並提供自訂訊息。

> [!CAUTION]
> [Deprecated](/uwp/api/windows.foundation.metadata.deprecatedattribute)是只能與 Windows 執行階段類型的屬性。 如果是 Standard C++ 類別和成員，請使用 [__declspec(deprecated)](../cpp/deprecated-cpp.md)。

### <a name="example"></a>範例

下列範例示範如何 (例如在 Windows 執行階段元件中) 將您的公用 API 設為已被取代。 第二個參數，其類型為 [Windows:Foundation::Metadata::DeprecationType](/uwp/api/windows.foundation.metadata.deprecationtype) ，指定 API 正要被取代或移除。 目前只支援 DeprecationType::Deprecated 值。 屬性中的第三個參數指定要套用屬性的 [Windows::Foundation::Metadata::Platform](/uwp/api/windows.foundation.metadata.platformattribute) 。

```

namespace wfm = Windows::Foundation::Metadata;

public ref class Bicycle sealed
{

public:
    property double Speed;

    [wfm::Deprecated("Use the Speed property to compute the angular speed of the wheel", wfm::DeprecationType::Deprecate, 0x0)]
    double ComputeAngularVelocity();
};
```

## <a name="supported-targets"></a>支援的目標

下表列出可套用 Deprecated 屬性的建構：

| |
|-|
|XAML 控制項|
|Delegate - 委派|
|Event - 事件|
|列舉欄位|
|enum|
|struct|
|方法|
|Class - 類別|
|interface|
|屬性|
|結構欄位|
|參數化建構函式|

## <a name="see-also"></a>另請參閱

[類型系統](../cppcx/type-system-c-cx.md)<br/>
[視覺化C++語言參考](../cppcx/visual-c-language-reference-c-cx.md)<br/>
[命名空間參考](../cppcx/namespaces-reference-c-cx.md)
