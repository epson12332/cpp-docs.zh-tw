---
title: 集合 (C++/CX)
ms.date: 11/19/2018
ms.assetid: 914da30b-aac5-4cd7-9da3-a5ac08cdd72c
ms.openlocfilehash: 850ac0f4801a13a5407f8fe008740bbfa21cc02c
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62347330"
---
# <a name="collections-ccx"></a>集合 (C++/CX)

在C++/CX 程式，您可自由使用 Standard Template Library (STL) 容器或任何其他使用者定義的集合型別。 不過，當您集合來回傳遞 Windows 執行階段應用程式二進位介面 (ABI) 之間，比方說，至 XAML 控制項或 JavaScript 用戶端，您必須使用 Windows 執行階段集合型別。

Windows 執行階段定義集合和相關的類型的介面和C++/CX 提供具象C++collection.h 標頭檔案中的實作。 下圖顯示集合型別之間的關聯性：

![C&#43;&#43;&#47;/CX 集合類型的繼承樹狀結構](../cppcx/media/cppcxcollectionsinheritancetree.png "C&#43;&#43;&#47;/CX 集合類型的繼承樹狀結構")

- [Platform::Collections::Vector 類別](../cppcx/platform-collections-vector-class.md) 與 [std::vector 類別](../standard-library/vector-class.md)類似。

- [Platform::Collections::Map 類別](../cppcx/platform-collections-map-class.md) 與 [std::map 類別](../standard-library/map-class.md)類似。

- [Platform::Collections::VectorView 類別](../cppcx/platform-collections-vectorview-class.md) 與[Platform::Collections::MapView 類別](../cppcx/platform-collections-mapview-class.md) 各是 `Vector` 和 `Map`的唯讀版本。

- 迭代器在 [Platform::Collections 命名空間](../cppcx/platform-collections-namespace.md)中定義。 這些迭代器可以滿足 STL 迭代器的需求，並且可讓您針對任何 [Windows::Foundation::Collections](../standard-library/algorithm-functions.md#find)介面類型或  [Platform::Collections](../standard-library/algorithm-functions.md#count_if)具象類型使用 [std::find](/uwp/api/windows.foundation.collections) 、 [std::count_if](../cppcx/platform-collections-namespace.md) 和其他 STL 演算法。 比方說，這表示您可以逐一查看集合中的 Windows 執行階段元件會在 C# 中建立，並對其套用 STL 演算法。

   > [!IMPORTANT]
   > Proxy 迭代器 `VectorIterator` 和 `VectorViewIterator` 會利用 Proxy 物件 `VectoryProxy<T>` 和 `ArrowProxy<T>` 來與 STL 容器搭配使用。 如需詳細資訊，請參閱本文章稍後的＜VectorProxy 元素＞。

- C++/CX 集合類型相同的執行緒安全性保證 STL 容器所支援的支援。

- [Windows::Foundation::Collections::IObservableVector](/uwp/api/Windows.Foundation.Collections.IObservableVector_T_) 和 [Windows::Foundation::Collections::IObservableMap](/uwp/api/Windows.Foundation.Collections.IObservableMap_K_V_) 會定義只要集合變更 (無論變更方式為何) 就會觸發的事件。 藉由實作這些介面，就能讓  [Platform::Collections::Map](../cppcx/platform-collections-map-class.md) 和 [Platform::Collections::Vector](../cppcx/platform-collections-vector-class.md) 與 XAML 集合進行資料繫結。 例如，如果您具有資料繫結至 `Vector` 的 `Grid`，當您將項目加入至集合時，此變更會反映在 Grid UI。

## <a name="vector-usage"></a>向量用法

當您的類別必須將序列容器傳遞至另一個 Windows 執行階段元件時，使用[collections::IVector\<T >](/uwp/api/Windows.Foundation.Collections.IVector_T_)做為參數或傳回型別，以及[collections\<T >](../cppcx/platform-collections-vector-class.md)做為具象實作。 如果您嘗試在公用傳回值或參數中使用 `Vector` 類型，則會引發編譯器錯誤 C3986。 只要將 `Vector` 變更為 `IVector`，就可以修正這個錯誤。

> [!IMPORTANT]
> 如果您在自己的程式中傳遞序列，則使用 `Vector` 或 `std::vector` ，因為這些方法比 `IVector`更有效率。 只有在透過 ABI 傳遞容器時，才應該使用 `IVector` 。
>
> Windows 執行階段類型系統不支援不規則陣列的概念，因此您不能傳遞 Ivector<platform < platform:: array\<T >> 做為傳回的值或方法參數。 若要跨 ABI 傳遞不規則陣列或一組序列中的某個序列，請使用 `IVector<IVector<T>^>`。

`Vector<T>` 提供在集合中新增、移除和存取項目的必要方法，此集合可隱含轉換為 `IVector<T>`。 您也可以在 `Vector<T>`的執行個體上使用 STL 演算法。 下列範例示範一些基本用法。 這裡的 [begin 函式](../cppcx/begin-function.md) 和 [end 函式](../cppcx/end-function.md) 來自 `Platform::Collections` 命名空間，而非 `std` 命名空間。

[!code-cpp[cx_collections#01](../cppcx/codesnippet/CPP/collections/class1.cpp#01)]

如果您有現有的程式碼會使用`std::vector`和您想要在 Windows 執行階段元件中重複使用它，只要使用其中一個`Vector`建構函式會採用`std::vector`或不成對的迭代器，來建構`Vector`其中傳遞之處集合跨 ABI。 下列範例示範如何從 `Vector` 使用 `std::vector`移動建構函式，以提高初始化效率。 在移動作業後，原始 `vec` 變數就不再有效。

[!code-cpp[cx_collections#02](../cppcx/codesnippet/CPP/collections/class1.cpp#02)]

如果您必須在未來透過 ABI 傳遞字串向量，您必須決定最初以 `std::wstring` 型別或 `Platform::String^` 型別建立字串。 如果您必須對字串進行許多處理，則使用 `wstring`。 否則，請以 `Platform::String^` 類型建立字串，以避免稍後進行轉換的成本。 您也必須決定是否要將這些字串放入 `std:vector` 或 `Platform::Collections::Vector` 內部。 一般的作法是，只有在您透過 ABI 傳遞容器時，才使用 `std::vector` ，然後從中建立 `Platform::Vector` 。

## <a name="value-types-in-vector"></a>Vector 中的實值類型

要儲存在 [Platform::Collections::Vector](../cppcx/platform-collections-vector-class.md) 中的所有元素都必須隱含或透過您提供的自訂 [std::equal_to](../standard-library/equal-to-struct.md) 比較子支援相等比較。 所有參考型別及所有純量型別都隱含支援相等比較。 針對非純量實值類型 (例如 [Windows::Foundation::DateTime](/uwp/api/windows.foundation.datetime)) 或自訂比較 (例如 `objA->UniqueID == objB->UniqueID`)，您必須提供自訂函式物件。

## <a name="vectorproxy-elements"></a>VectorProxy 元素

[2&gt;platform::collections::vectoriterator](../cppcx/platform-collections-vectoriterator-class.md)並[vectorviewiterator](../cppcx/platform-collections-vectorviewiterator-class.md)啟用`range for`迴圈和演算法，例如[ivector&lt](../standard-library/algorithm-functions.md#sort) 與[IVector\<T >](/uwp/api/Windows.Foundation.Collections.IVector_T_)容器。 但是，您無法透過 C++ 指標取值存取 `IVector` 項目，只能透過 [GetAt](/uwp/api/windows.foundation.collections.ivector-1.getat) 和 [SetAt](/uwp/api/windows.foundation.collections.ivector-1.setat) 方法存取。 因此，這些迭代器會使用 proxy 類別`Platform::Details::VectorProxy<T>`並`Platform::Details::ArrowProxy<T>`以存取個別的項目，透過__\*__， __->__，以及__\[]__ 運算子，所需的標準程式庫。 嚴格來說，如果指定 `IVector<Person^> vec`，則 `*begin(vec)` 的類型就是 `VectorProxy<Person^>`。 不過，對您的程式碼來說，Proxy 物件永遠都像是不存在一樣。 這些 Proxy 物件沒有記錄在文件中，因為它們僅供迭代器在內部使用，但是了解機制如何運作還是很重要。

當您針對 `range for` 容器使用 `IVector` 迴圈時，請使用 `auto&&` 讓迭代器變數能夠正確繫結至 `VectorProxy` 元素。 如果您使用 `auto` 或 `auto&`，就會引發編譯器警告 C4239，而且警告文字中會提及 `VectoryProxy` 。

下圖顯示針對 `range for` 執行的 `IVector<Person^>`迴圈。 請注意，程式會執行到第 64 行的中斷點停止。 [ **快速監看式** ] 視窗會顯示迭代器變數 `p` 就是擁有 `VectorProxy<Person^>` 和 `m_v` 成員變數的 `m_i` 。 但是，當您針對這個變數呼叫 `GetType` 時，它會將相同的類型傳回給 `Person` 執行個體 `p2`。 因此，雖然 `VectorProxy` 和 `ArrowProxy` 可能會出現在 [ **快速監看式**]、偵錯工具、某些編譯器錯誤或其他位置，但是一般而言，您仍然不必明確為它們撰寫程式碼。

![範圍中的 VectorProxy&#45;架構的 for 迴圈](../cppcx/media/vectorproxy-1.png "範圍中的 VectorProxy&#45;架構的 for 迴圈")

有一種情況下您必須為 Proxy 物件撰寫程式碼，就是必須針對元素執行 `dynamic_cast` 的時候 (例如，當您在 `UIElement` 項目集合中尋找特定類型的 XAML 物件時)。 在這種情況下，您必須先將這個項目轉換為 [Platform::Object](../cppcx/platform-object-class.md)^，然後再執行動態轉換：

```cpp
void FindButton(UIElementCollection^ col)
{
    // Use auto&& to avoid warning C4239
    for (auto&& elem : col)
    {
        Button^ temp = dynamic_cast<Button^>(static_cast<Object^>(elem));
        if (nullptr != temp)
        {
            // Use temp...
        }
    }
}
```

## <a name="map-usage"></a>對應用法

此範例示範如何插入項目，並查閱[std:: map](../cppcx/platform-collections-map-class.md)，然後傳回`Map`為唯讀模式 [Windows::Foundation::Collections::IMapView] / uwp/api /Windows.Foundation.Collections.IMapView_K_V_) 型別。

[!code-cpp[cx_collections#04](../cppcx/codesnippet/CPP/collections/class1.cpp#04)]

一般而言，基於效能考量，在內部對應功能上最好使用 `std::map` 型別。 如果您必須透過 ABI 傳遞容器，請從 [std::map](../cppcx/platform-collections-map-class.md) 建構 [Platform::Collections::Map](../standard-library/map-class.md) ，然後傳回 `Map` 作為 [Windows::Foundation::Collections::IMap](/uwp/api/Windows.Foundation.Collections.IMap_K_V_)。 如果您嘗試在公用傳回值或參數中使用 `Map` 類型，則會引發編譯器錯誤 C3986。 只要將 `Map` 變更為 `IMap`，就可以修正這個錯誤。 在某些情況下，例如，如果不是進行大量搜尋或插入，且您經常透過 ABI 傳遞集合，則一開始便使用 `Platform::Collections::Map` 可耗費較少資源，還能避免轉換 `std::map`時的成本。 在任何情況下，請避免在 `IMap` 上執行查閱和插入作業，因為這些是效能最低的三個類型。 只有在透過 ABI 傳遞容器時，才應該轉換為 `IMap` 。

## <a name="value-types-in-map"></a>Map 中的實值類型

在 [Platform::Collections::Map](../cppcx/platform-collections-map-class.md) 中的項目已排序。 要儲存在 `Map` 中的所有項目都必須隱含或透過您提供的自訂 [stl::less](../standard-library/less-struct.md) 比較子，支援使用嚴格弱式順序的小於比較。 純量類型隱含支援此比較。 針對非純量實值類型 (例如 `Windows::Foundation::DateTime`) 或自訂比較 (例如 `objA->UniqueID < objB->UniqueID`)，您必須提供自訂比較子。

## <a name="collection-types"></a>集合類型

集合分成四種分類：序列集合和關聯集合的可修改版本和唯讀版本。 此外， C++/CX 提供三個迭代器類別，以簡化存取集合，以增強集合。

您可以變更可修改的集合的元素，但只能讀取唯讀集合的元素，又稱為 *檢視 (View)*。 項目[collections](../cppcx/platform-collections-vector-class.md)或是[2&gt;platform::collections::vectorview](../cppcx/platform-collections-vectorview-class.md)可以使用迭代器或集合的存取集合[vector:: getat](../cppcx/platform-collections-vector-class.md#getat)和索引。 可存取關聯集合的項目，請使用集合的[map:: lookup](../cppcx/platform-collections-map-class.md#lookup)和一個索引鍵。

[Platform::Collections::Map 類別](../cppcx/platform-collections-map-class.md)<br/>
可修改的關聯集合。 對應元素是機碼值組。 支援查閱機碼以擷取其關聯值與逐一查看所有機碼值組。

`Map` 和 `MapView` 以 `<K, V, C = std::less<K>>`為樣板，因此，您可以自訂比較子。  此外， `Vector` 和 `VectorView` 以 `<T, E = std::equal_to<T>>` 為樣板，因此，您可以自訂 `IndexOf()`的行為。 這對於值結構的 `Vector` 和 `VectorView` 而言十分重要。 例如，若要建立向量\<Windows::Foundation::DateTime >，您必須提供自訂比較子，因為 DateTime 沒有多載 = = 運算子。

[Platform::Collections::MapView 類別](../cppcx/platform-collections-mapview-class.md)<br/>
`Map`的唯讀版本。

[Platform::Collections::Vector Class](../cppcx/platform-collections-vector-class.md)<br/>
可修改的序列集合。 `Vector<T>` 支援固定時間隨機存取和分期固定時間 [Append](../cppcx/platform-collections-vector-class.md#append) 作業。

[Platform::Collections::VectorView 類別](../cppcx/platform-collections-vectorview-class.md)<br/>
`Vector`的唯讀版本。

[Platform::Collections::InputIterator 類別](../cppcx/platform-collections-inputiterator-class.md)<br/>
滿足 STL 輸入迭代器需求的 STL 迭代器。

[Platform::Collections::VectorIterator 類別](../cppcx/platform-collections-vectoriterator-class.md)<br/>
滿足 STL 可變動隨機存取迭代器需求的 STL 迭代器。

[Platform::Collections::VectorViewIterator 類別](../cppcx/platform-collections-vectorviewiterator-class.md)<br/>
滿足 STL  `const` 隨機存取迭代器需求的 STL 迭代器。

### <a name="begin-and-end-functions"></a>begin() 和 end() 函式

為了簡化使用 STL 來處理`Vector`， `VectorView`， `Map`， `MapView`，和任意`Windows::Foundation::Collections`物件， C++/CX 支援的多載[begin 函式](../cppcx/begin-function.md)並[end 函式](../cppcx/end-function.md)非成員函式。

下表列出可用的迭代器和函式。

|Iterators|函式|
|---------------|---------------|
|[Platform::Collections::VectorIterator\<T>](../cppcx/platform-collections-vectoriterator-class.md)<br /><br /> (在內部儲存[collections::IVector\<T >](/uwp/api/Windows.Foundation.Collections.IVector_T_)和 int)|[begin](../cppcx/begin-function.md)/ [end](../cppcx/end-function.md)([Windows::Foundation::Collections::IVector\<T>](/uwp/api/Windows.Foundation.Collections.IVector_T_))|
|[Platform::Collections::VectorViewIterator\<T>](../cppcx/platform-collections-vectorviewiterator-class.md)<br /><br /> (在內部儲存[IVectorView\<T >](/uwp/api/Windows.Foundation.Collections.IVectorView_T_)^ 和 int)|[開始](../cppcx/begin-function.md)/ [端](../cppcx/end-function.md)([IVectorView\<T >](/uwp/api/Windows.Foundation.Collections.IVectorView_T_)^)|
|[Platform::Collections::InputIterator\<T>](../cppcx/platform-collections-inputiterator-class.md)<br /><br /> (在內部儲存[Iiterator<t\<T >](/uwp/api/Windows.Foundation.Collections.IIterator_T_)^ 和 T)|[開始](../cppcx/begin-function.md)/ [端](../cppcx/end-function.md)([IIterable\<T >](/uwp/api/Windows.Foundation.Collections.IIterable_T_))|
|[Platform::Collections::InputIterator<IKeyValuePair\<K, V>^>](../cppcx/platform-collections-inputiterator-class.md)<br /><br /> (在內部儲存[Iiterator<t\<T >](/uwp/api/Windows.Foundation.Collections.IIterator_T_)^ 和 T)|[開始](../cppcx/begin-function.md)/ [端](../cppcx/end-function.md)([IMap\<K，V >](/uwp/api/Windows.Foundation.Collections.IMap_K_V_)。|
|[Platform::Collections::InputIterator<IKeyValuePair\<K, V>^>](../cppcx/platform-collections-inputiterator-class.md)<br /><br /> (在內部儲存[Iiterator<t\<T >](/uwp/api/Windows.Foundation.Collections.IIterator_T_)^ 和 T)|[開始](../cppcx/begin-function.md)/ [結束](../cppcx/end-function.md)([Windows:: Foundation::Collections::IMapView]/uwp/api/Windows.Foundation.Collections.IMapView_K_V_))|

### <a name="collection-change-events"></a>集合變更事件

`Vector` 和 `Map` 藉由實作變更或重設集合物件時，或者插入、移除或變更集合的任何元素時所發生的事件，來支援 XAML 集合中的資料繫結。 您可以撰寫自己的型別來支援資料繫結，但是您無法繼承自 `Map` 或 `Vector` ，因為這些型別是密封型別。

[Windows::Foundation::Collections::VectorChangedEventHandler](/uwp/api/windows.foundation.collections.vectorchangedeventhandler) 和 [Windows::Foundation::Collections::MapChangedEventHandler](/uwp/api/windows.foundation.collections.mapchangedeventhandler) 委派會為集合變更事件的事件處理常式指定簽章。 [Windows::Foundation::Collections::CollectionChange](/uwp/api/windows.foundation.collections.collectionchange) 公用列舉類別及 `Platform::Collection::Details::MapChangedEventArgs` 和 `Platform::Collections::Details::VectorChangedEventArgs` ref 類別會儲存事件引數，以判斷造成事件的原因。 `*EventArgs`中所定義的型別`Details`命名空間因為您不需要建構或明確地使用它們，當您使用`Map`或`Vector`。

## <a name="see-also"></a>另請參閱

[類型系統](../cppcx/type-system-c-cx.md)<br/>
[視覺化C++語言參考](../cppcx/visual-c-language-reference-c-cx.md)<br/>
[命名空間參考](../cppcx/namespaces-reference-c-cx.md)
