---
title: hash 類別
ms.date: 11/04/2016
f1_keywords:
- functional/std::hash
- bitset/std::hash
- memory/std::hash
- string/std::hash
- system_error/std::hash
- thread/std::hash
- typeindex/std::hash
- vector/std::hash
- XSTDDEF/std::hash
- xstring/std::hash
helpviewer_keywords:
- std::hash [C++]
- std::hash [C++]
- std::hash [C++]
- std::hash [C++]
- std::hash [C++]
- std::hash [C++]
- std::hash [C++]
- std::hash [C++]
- std::hash [C++]
ms.assetid: e1b500c6-a5c8-4f6f-ad33-7ec52eb8e2e4
ms.openlocfilehash: 2f7206e3764df384004b78e6df2127833a784f70
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62405088"
---
# <a name="hash-class"></a>hash 類別

計算值的雜湊碼。

## <a name="syntax"></a>語法

```cpp
template <class Ty>
struct hash {
    size_t operator()(Ty val) const;
};
```

## <a name="remarks"></a>備註

函式物件會定義雜湊函式，適用於將 *Ty* 類型的值對應到索引值的分佈。 成員 `operator()` 會傳回 *val* 的雜湊碼，適合用來與範本類別 `unordered_map`、`unordered_multimap`、`unordered_set` 及 `unordered_multiset` 搭配使用。 標準程式庫提供適用於基本類型的特製化：*Ty*可以是任何純量類型，包括指標類型和列舉類型。 此外，還有適用於程式庫類型 `string`、`wstring`、`u16string`、`u32string`、`string_view`、`wstring_view`、`u16string_view`、`u32string_view`、`bitset`、`error_code`、`error_condition`、`optional`、`shared_ptr`、`thread`、`type_index`、`unique_ptr`、`variant` 及 `vector<bool>` 的特製化。

## <a name="example"></a>範例

```cpp
// std__functional__hash.cpp
// compile with: /EHsc
#include <functional>
#include <iostream>
#include <unordered_set>

int main()
    {
    std::unordered_set<int, std::hash<int> > c0;
    c0.insert(3);
    std::cout << *c0.find(3) << std::endl;

    return (0);
    }
```

```Output
3
```

## <a name="requirements"></a>需求

**標頭：**\<functional>

**命名空間：** std

## <a name="see-also"></a>另請參閱

[<unordered_map>](../standard-library/unordered-map.md)<br/>
[unordered_multimap 類別](../standard-library/unordered-multimap-class.md)<br/>
[unordered_multiset 類別](../standard-library/unordered-multiset-class.md)<br/>
[<unordered_set>](../standard-library/unordered-set.md)<br/>
