---
title: make_public
ms.date: 11/04/2016
f1_keywords:
- vc-pragma.make_public
- make_public_CPP
helpviewer_keywords:
- pragmas, make_public
- make_public pragma
ms.assetid: c3665f4d-268a-4932-9661-c37c8ae6a341
ms.openlocfilehash: d569758f90b9e55f65ad13517f86dea41d151ca8
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62371759"
---
# <a name="makepublic"></a>make_public
表示原生類型應該具有公用組件存取範圍。

## <a name="syntax"></a>語法

```
#pragma make_public(type)
```

### <a name="parameters"></a>參數

*型別*是您想要具有公用組件存取範圍的類型名稱。

## <a name="remarks"></a>備註

**make_public**適用於當您想要參考原生型別是來自您無法變更之.h 檔案。 如果您要在具有公用組件存取範圍類型的公用函式簽章中使用原生類型，原生類型必須同時具有公用組件存取範圍，否則編譯器會發出警告。

**make_public**必須在全域範圍指定，而且只有在從該點是在其宣告的原始程式檔的結尾。

原生型別可能是隱含或明確私用;請參閱[型別可視性](../dotnet/how-to-define-and-consume-classes-and-structs-cpp-cli.md#BKMK_Type_visibility)如需詳細資訊。

## <a name="examples"></a>範例

下列範例是 .h 檔案的內容，其中包含兩個原生結構的定義。

```cpp
// make_public_pragma.h
struct Native_Struct_1 { int i; };
struct Native_Struct_2 { int i; };
```

下列程式碼範例會使用標頭檔，並顯示除非您明確標記為 public，原生結構使用**make_public**，當您嘗試使用中的原生結構時，編譯器會產生一則警告在公用 managed 類型的公用函式簽章。

```cpp
// make_public_pragma.cpp
// compile with: /c /clr /W1
#pragma warning (default : 4692)
#include "make_public_pragma.h"
#pragma make_public(Native_Struct_1)

public ref struct A {
   void Test(Native_Struct_1 u) {u.i = 0;}   // OK
   void Test(Native_Struct_2 u) {u.i = 0;}   // C4692
};
```

## <a name="see-also"></a>另請參閱

[Pragma 指示詞和 __Pragma 關鍵字](../preprocessor/pragma-directives-and-the-pragma-keyword.md)