---
title: mem_fun1_ref_t 類別
ms.date: 02/21/2019
f1_keywords:
- functional/std::mem_fun1_ref_t
helpviewer_keywords:
- mem_fun1_ref_t class
ms.assetid: 7d6742f6-19ba-4523-b3c8-0e5b8f11464f
ms.openlocfilehash: d4f0f2064ac6771e2c351b70097137fed12c8262
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62412874"
---
# <a name="memfun1reft-class"></a>mem_fun1_ref_t 類別

配接器類別，可讓`non_const`接受單一引數時，當作二元函式物件以參考引數初始化呼叫成員函式。 在 C + + 11 中，在 c++17 中移除已被取代。

## <a name="syntax"></a>語法

```cpp
template <class Result, class Type, class Arg>
class mem_fun1_ref_t : public binary_function<Type, Arg, Result> {
    explicit mem_fun1_ref_t(
    Result (Type::* _Pm)(Arg));

    Result operator()(
    Type& left,
    Arg right) const;

};
```

### <a name="parameters"></a>參數

*_Pm*<br/>
要轉換成函式物件之 `Type` 類別的成員函式指標。

*left*<br/>
物件， *_Pm*上呼叫成員函式。

*right*<br/>
提供給引數 *_Pm*。

## <a name="return-value"></a>傳回值

具適應性的二元函式。

## <a name="remarks"></a>備註

此範本類別會儲存一份 *_Pm*，它必須是類別的成員函式的指標`Type`，私用成員物件中。 它會定義其成員函式`operator()`做為傳回 (**左**。\*`_Pm`) (**右**)。

## <a name="example"></a>範例

通常並不直接使用 `mem_fun1_ref_t` 的建構函式，而協助程式函式 `mem_fun_ref` 可用來調整成員函式。 如需如何使用成員函式配接器的範例，請參閱 [mem_fun_ref](../standard-library/functional-functions.md#mem_fun_ref)。

## <a name="requirements"></a>需求

**標頭：**\<functional>

**命名空間：** std

## <a name="see-also"></a>另請參閱

[C++ 標準程式庫中的執行緒安全](../standard-library/thread-safety-in-the-cpp-standard-library.md)<br/>
[C++ 標準程式庫參考](../standard-library/cpp-standard-library-reference.md)<br/>
