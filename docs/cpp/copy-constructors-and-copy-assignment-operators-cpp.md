---
title: 複製建構函式和複製指派運算子 (C++)
ms.date: 11/04/2016
helpviewer_keywords:
- = operator [C++], copying objects
- assignment statements [C++], copying objects
- assignment operators [C++], for copying objects
- objects [C++], copying
- initializing objects, by copying objects
- copying objects
- assigning values to copy objects
ms.assetid: a94fe1f9-0289-4fb9-8633-77c654002c0d
ms.openlocfilehash: 59f463d103e233a1d9b25da3243a16f67263c815
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62392293"
---
# <a name="copy-constructors-and-copy-assignment-operators-c"></a>複製建構函式和複製指派運算子 (C++)

> [!NOTE]
> 從 C + + 11 開始，支援兩種指派會在語言中：*複製指派*並*移動指派*。 在本文中，除非明確指定，否則「指派」表示複製指派。 如需移動指派的詳細資訊，請參閱 <<c0> [ 移動建構函式和移動指派運算子 (C++)](move-constructors-and-move-assignment-operators-cpp.md)。</c0>
>
> 指派作業和初始化作業都會導致複製物件。

- **指派**:當一個物件的值指派到另一個物件時，會將第一個物件複製到第二個物件。 因此，

    ```cpp
    Point a, b;
    ...
    a = b;
    ```

   會導致 `b` 的值複製到 `a`。

- **初始化**:在宣告新的物件，引數會傳遞至函式的值或傳值方式從函式傳回值時，會進行初始化。

您可以定義類別類型物件的「複製」語意。 例如，請參考這個程式碼：

```cpp
TextFile a, b;
a.Open( "FILE1.DAT" );
b.Open( "FILE2.DAT" );
b = a;
```

上述程式碼可能表示「將 FILE1.DAT 的內容複製到 FILE2.DAT」，也可能表示「忽略 FILE2.DAT 並且讓 `b` 成為 FILE1.DAT 的第二個控制代碼」。 您必須將適當的複製語意附加至每一個類別，如下所示。

- 使用指派運算子**運算子 =** 為傳回型別，而且參數所傳遞的類別類型的參考一起**const**參考 — 例如`ClassName& operator=(const ClassName& x);`。

- 使用複製建構函式。

如果您未宣告複製建構函式，則編譯器會產生一個成員複製建構函式。  如果您未宣告複製指派建構函式，則編譯器會產生一個成員複製指派運算子。 宣告複製建構函式不會隱藏編譯器產生的複製指派運算子，反之亦然。 如果您實作任一種，建議您一併實作另一種，如此程式碼的意義才會明確。

複製建構函式接受類型引數<em>類別名稱</em><strong>&</strong>，其中*類別名稱*是為其定義建構函式的類別名稱。 例如: 

```cpp
// spec1_copying_class_objects.cpp
class Window
{
public:
    Window( const Window& ); // Declare copy constructor.
    // ...
};

int main()
{
}
```

> [!NOTE]
> 讓複製建構函式的引數的型別**const** <em>類別名稱</em><strong>&</strong>盡可能。 這樣可避免複製建構函式意外變更做為複製來源的物件。 它也可讓您複製從**const**物件。

## <a name="compiler-generated-copy-constructors"></a>編譯器產生的複製建構函式

編譯器產生的複製建構函式，例如使用者定義的複製建構函式具有類型的單一引數 」 參考*類別名稱*。 」 所有的基底類別和成員類別將複製建構函式宣告為接受單一引數的型別時，發生例外狀況**const** <em>類別名稱</em><strong>&</strong>。 在此情況下，編譯器產生的複製建構函式的引數是也**const**。

當複製建構函式的引數類型不是時**const**，藉由複製初始化**const**物件會產生錯誤。 反向執行則不成立：如果引數**const**，您可以藉由複製不是物件來初始化**const**。

編譯器產生的指派運算子遵循相同的模式與**const。** 它們接受單一引數型別的<em>類別名稱</em><strong>&</strong>除非所有基底和成員類別中的指派運算子不接受引數的型別**const** <em>類別名稱</em><strong>&</strong>。 在此情況下，類別產生的指派運算子會接受**const**引數。

> [!NOTE]
> 虛擬基底類別是由複製建構函式進行初始化、由編譯器所產生或使用者所定義時，只會在建構時初始化一次。

這些影響類似複製建構函式的影響。 當引數類型不是時**const**，從指派**const**物件會產生錯誤。 反向執行則不成立：如果**const**的值指派給值不是**const**，指派會成功。

如需有關多載的指派運算子的詳細資訊，請參閱 <<c0> [ 指派](../cpp/assignment.md)。