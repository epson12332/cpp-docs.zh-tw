---
title: '&lt;codecvt&gt;'
ms.date: 11/04/2016
f1_keywords:
- codecvt
- <codecvt>
helpviewer_keywords:
- codecvt header
ms.assetid: d44ee229-00d5-4761-9b48-0c702122789d
ms.openlocfilehash: 56cd4263d3dcddd23246a05466275b8b7d370b95
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62405205"
---
# <a name="ltcodecvtgt"></a>&lt;codecvt&gt;

定義數個範本類別，以依據 [codecvt](../standard-library/codecvt-class.md) 範本類別描述物件。 這些物件可作為[地區設定 facet](../standard-library/locale-class.md#facet_class) ，以控制類型的值序列之間的轉換`Elem`和一系列的值型別的**char**。

## <a name="syntax"></a>語法

```cpp
#include <codecvt>
```

## <a name="remarks"></a>備註

此標頭中宣告的地區設定 Facet 可在數種字元編碼之間進行轉換。 若是寬字元 (以固定大小的整數形式儲存在程式內)︰

- UCS-4 會在程式內以 Unicode (ISO 10646) 編碼為 32 位元整數。

- UCS-2 會在程式內以 Unicode 編碼為 16 位元整數。

- UTF-16 會在程式內以 Unicode 編碼為一個或兩個 16 位元整數。 (請注意，這並不符合標準 C 或標準 C++ 有效寬字元編碼的所有需求， 但這卻是廣泛使用的情況)。

若是位元組資料流 (儲存在檔案、 傳輸的位元組序列，或儲存在陣列中的程式內**char**):

- UTF-8 會在位元組資料流內以 Unicode 編碼為一或多個 8 位元位元組 (按具決定性的位元組順序)。

- UTF-16LE 會在位元組資料流內以 Unicode 編碼為 UTF-16 (其中每個 16 位元整數會顯示為兩個 8 位元位元組，較不顯著的位元組在前)。

- UTF-16BE 會在位元組資料流內以 Unicode 編碼為 UTF-16 (其中每個 16 位元整數會顯示為兩個 8 位元位元組，較顯著的位元組在前)。

### <a name="enumerations"></a>列舉

|||
|-|-|
|[codecvt_mode](../standard-library/codecvt-enums.md#codecvt_mode)|指定地區設定 Facet 的設定資訊。|

### <a name="classes"></a>類別

|類別|描述|
|-|-|
|[codecvt_utf8](codecvt-utf8-class.md)|代表地區設定 Facet，其可在 UCS-2 或 UCS-4 編碼的寬字元以及 UTF-8 編碼的位元組資料流之間進行轉換。|
|[codecvt_utf8_utf16](codecvt-utf8-utf16-class.md)|代表地區設定 Facet，其可在 UTF-16 編碼的寬字元以及 UTF-8 編碼的位元組資料流之間進行轉換。|
|[codecvt_utf16](codecvt-utf16-class.md)|代表地區設定 Facet，其可在 UCS-2 或 UCS-4 編碼的寬字元以及 UTF-16LE 或 UTF-16BE 編碼的位元組資料流之間進行轉換。|

## <a name="requirements"></a>需求

**標頭：**\<codecvt>

**命名空間：** std

## <a name="see-also"></a>另請參閱

[標頭檔參考](../standard-library/cpp-standard-library-header-files.md)<br/>
