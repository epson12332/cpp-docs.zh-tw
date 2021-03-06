---
title: constexpr (C++)
ms.date: 04/06/2018
f1_keywords:
- constexpr_cpp
ms.assetid: c6458ccb-51c6-4a16-aa61-f69e6f4e04f7
ms.openlocfilehash: 3ab3b75589864c95cb345be57db39c028a02f8db
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62399092"
---
# <a name="constexpr-c"></a>constexpr (C++)

關鍵字**constexpr**已在 c++11 中引進，並在 c++14 中改進。 這表示*常數運算式*。 像是**const**，它可以套用至變數，所以如果任何程式碼嘗試修改的值，則會引發編譯器錯誤。 不同於**const**， **constexpr**也可以套用至函式和類別建構函式。 **constexpr**表示的值或傳回值，保持不變，可能的話，會在編譯時期計算。

A **constexpr**只要 const 整數是必要的例如在樣板引數和陣列宣告中使用整數值。 和時間可以計算出的值，而不是執行階段編譯時期，它可以協助您的程式執行速度更快，並使用較少的記憶體。

若要限制的編譯時期常數的計算，以及其可能的影響，在編譯時間複雜性，C + + 14 標準需要常數運算式中的型別，要[常值類型](trivial-standard-layout-and-pod-types.md#literal_types)。

## <a name="syntax"></a>語法

> **constexpr** *常值型別* *識別碼* **=** *常數運算式* **;** 
>  **constexpr** *常值型別* *識別碼* **{** *常數運算式* **}** **;** 
>  **constexpr** *常值型別* *識別碼* **(** *params* **)** **;** 
>  **constexpr** *ctor* **(** *params* **)** **;**

## <a name="parameters"></a>參數

*params*<br/>
一或多個參數，其中每個必須是常值的型別，而且必須是本身是常數運算式。

## <a name="return-value"></a>傳回值

Constexpr 變數或函式必須傳回[常值型別](trivial-standard-layout-and-pod-types.md#literal_types)。

## <a name="constexpr-variables"></a>constexpr 變數

Const 和 constexpr 變數之間的主要差異是 const 變數的初始化可以延遲，直到執行階段。 Constexpr 變數必須在編譯時期初始化。  所有的 constexpr 變數都是常數。

- 變數可以使用宣告**constexpr**，如果它具有常值的型別，並已初始化。 如果建構函式執行初始化，則建構函式必須宣告為**constexpr**。

- 如果所參考的物件已由常數運算式初始化，而且在初始化期間叫用的任何隱含轉換也是常數運算式，則參考可以宣告為 constexpr。

- 所有宣告**constexpr**變數或函式必須**constexpr**規範。

```cpp
constexpr float x = 42.0;
constexpr float y{108};
constexpr float z = exp(5, 3);
constexpr int i; // Error! Not initialized
int j = 0;
constexpr int k = j + 1; //Error! j not a constant expression
```

## <a name="constexpr_functions"></a> constexpr 函式

A **constexpr**函式是在編譯時期時使用的程式碼需要它，您可以計算其傳回的值。 使用程式碼需要傳回值在編譯時期，比方說，初始化**constexpr**變數，或提供非類型樣板引數。 其引數為當**constexpr**的值， **constexpr**函式會產生編譯時間常數。 當呼叫與非**constexpr**引數，或當其值不是在編譯時期的必要項目，像是一般函式的執行階段產生的值。 (這種雙行為讓您不必撰寫**constexpr**和非位**constexpr**相同的函式的版本。)

A **constexpr**函式或建構函式會以隱含方式**內嵌**。

Constexpr 函式，套用下列規則：

- A **constexpr**函式必須接受並傳回僅[常值類型](trivial-standard-layout-and-pod-types.md#literal_types)。

- A **constexpr**函式可以是遞迴。

- 它不能[虛擬](../cpp/virtual-cpp.md)。 如果封入類別有任何虛擬基底類別建構函式無法定義為 constexpr。

- 主體可以定義為 `= default` 或 `= delete`。

- 主體不可以包含**goto**陳述式或 try 區塊。

- 非 constexpr 範本的明確特製化可以宣告為**constexpr**:

- 明確特製化**constexpr**範本並沒有同時**constexpr**:

下列規則適用於**constexpr**函式在 Visual Studio 2017 和更新版本：

- 它可能包含**如果**和**切換**陳述式，以及所有迴圈陳述式，包括**如**、 以範圍為基礎，**雖然**，和**請勿-雖然**。

- 它可能包含區域變數宣告、 但變數必須初始化，必須為常值的型別，而且不能是靜態或執行緒區域。 在本機宣告的變數並不一定要 const，可能會變動。

- Constexpr 非靜態成員函式不需要是隱含 const。

```cpp
constexpr float exp(float x, int n)
{
    return n == 0 ? 1 :
        n % 2 == 0 ? exp(x * x, n / 2) :
        exp(x * x, (n - 1) / 2) * x;
};
```

> [!TIP]
> 在 Visual Studio 偵錯工具時偵錯非最佳化偵錯組建，您可以告訴是否**constexpr**函式會在編譯時期將中斷點放評估。 如果叫用中斷點，便已在執行階段呼叫此函式。  否則便是在編譯時期呼叫函式。

## <a name="extern-constexpr"></a>extern constexpr

[/Zc: externconstexpr](../build/reference/zc-externconstexpr.md)編譯器選項可讓編譯器套用[外部連結](../c-language/external-linkage.md)宣告使用變數**extern constexpr**。 在舊版的 Visual Studio，並依預設或如果 **/Zc:externConstexpr-** 指定時，Visual Studio 會套用到的內部連結**constexpr**變數，即使**extern**使用關鍵字。 **/Zc: externconstexpr**選項是從 Visual Studio 2017 Update 15.6 中推出。 和預設為關閉。 /Permissive-option 不會啟用 /zc: externconstexpr。

## <a name="example"></a>範例

下列範例所示**constexpr**變數、 函數及使用者定義型別。 在 main （），最後一行陳述**constexpr**成員函式 getvalue （） 是執行階段呼叫，因為值不一定要在編譯時期為已知。

```cpp
#include <iostream>

using namespace std;

// Pass by value
constexpr float exp(float x, int n)
{
    return n == 0 ? 1 :
        n % 2 == 0 ? exp(x * x, n / 2) :
        exp(x * x, (n - 1) / 2) * x;
};

// Pass by reference
constexpr float exp2(const float& x, const int& n)
{
    return n == 0 ? 1 :
        n % 2 == 0 ? exp2(x * x, n / 2) :
        exp2(x * x, (n - 1) / 2) * x;
};

// Compile-time computation of array length
template<typename T, int N>
constexpr int length(const T(&ary)[N])
{
    return N;
}

// Recursive constexpr function
constexpr int fac(int n)
{
    return n == 1 ? 1 : n*fac(n - 1);
}

// User-defined type
class Foo
{
public:
    constexpr explicit Foo(int i) : _i(i) {}
    constexpr int GetValue()
    {
        return _i;
    }
private:
    int _i;
};

int main()
{
    // foo is const:
    constexpr Foo foo(5);
    // foo = Foo(6); //Error!

    // Compile time:
    constexpr float x = exp(5, 3);
    constexpr float y { exp(2, 5) };
    constexpr int val = foo.GetValue();
    constexpr int f5 = fac(5);
    const int nums[] { 1, 2, 3, 4 };
    const int nums2[length(nums) * 2] { 1, 2, 3, 4, 5, 6, 7, 8 };

    // Run time:
    cout << "The value of foo is " << foo.GetValue() << endl;

}
```

## <a name="requirements"></a>需求

Visual Studio 2015

## <a name="see-also"></a>另請參閱

[宣告和定義](../cpp/declarations-and-definitions-cpp.md)<br/>
[const](../cpp/const-cpp.md)
