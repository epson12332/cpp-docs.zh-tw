---
title: 資源識別項 （符號） (C++)
ms.date: 02/14/2019
f1_keywords:
- vc.editors.symbol.identifiers
helpviewer_keywords:
- symbols [C++], resource identifiers
- symbols [C++], creating
- resource symbols
- symbols [C++], editing
- resource editors [C++], resource symbols
ms.assetid: 8fccc09a-0237-4a65-b9c4-57d60c59e324
ms.openlocfilehash: 0b19ff0d1c709616868d47c172ff4cf8c6931b82
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62387873"
---
# <a name="resource-identifiers-symbols-c"></a>資源識別項 （符號） (C++)

符號是資源識別碼 (ID)，由兩個部分組成，符號名稱 （字串） 對應至符號值 （整數），例如：

```
IDC_EDITNAME = 5100
```

符號名稱最常稱為識別項。

符號為您的原始程式碼中出現的資源和使用者介面物件，以及當您在資源編輯器中使用上述項目時，提供描述性參考。 您可以使用 [[資源符號]](../windows/viewing-resource-symbols.md)對話方塊，在一個方便的位置檢視及操作符號。

當您的應用程式大小和複雜性提高時，其資源和符號數目也會增加。 追蹤分散於多個檔案的大量符號可能會很困難。 **資源符號**對話方塊藉由提供集中工具，您可透過它來簡化符號管理：

- [建立符號](../windows/creating-new-symbols.md)

- [管理符號](../windows/changing-a-symbol-or-symbol-name-id.md)

- [檢視預先定義的符號 ID](../windows/predefined-symbol-ids.md)

當您建立新的資源或資源物件時，[[資源編輯器]](../windows/resource-editors.md) 會提供資源的預設名稱 (例如 `IDC_RADIO1`) 並為其指派值。 名稱加值的定義會儲存在`Resource.h`檔案。

> [!NOTE]
> 當您將資源或資源物件從一個 .rc 檔複製到另一個檔案時，Visual C++ 可能會變更已傳送資源的符號值，或符號名稱和值，以避免與現有檔案中的符號名稱或值相衝突。

## <a name="requirements"></a>需求

Win32

## <a name="see-also"></a>另請參閱

[使用資源檔](../windows/working-with-resource-files.md)<br/>
[資源檔](../windows/resource-files-visual-studio.md)<br/>
[資源編輯器](../windows/resource-editors.md)<br/>