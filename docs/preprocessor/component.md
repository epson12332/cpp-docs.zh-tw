---
title: 元件
ms.date: 04/08/2019
f1_keywords:
- vc-pragma.component
- component_CPP
helpviewer_keywords:
- component pragma
- pragmas, component
ms.assetid: 7b66355e-3201-4c14-8190-f4a2a81a604a
ms.openlocfilehash: 4870860650a39d27639ad18100ba37ba14aa15c0
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62366910"
---
# <a name="component"></a>元件

控制瀏覽資訊或從原始程式檔內的相依性資訊的集合。

## <a name="syntax"></a>語法

> **#pragma component( browser,** { **on** | **off** }[**,** **references** [**,** *name* ]] **)** \
> **#pragma 元件 (minrebuild 上** | **關閉)** \
> **#pragma 元件 (mintypeinfo 上** | **關閉)**

## <a name="remarks"></a>備註

### <a name="browser"></a>瀏覽器

您可以開啟或關閉收集功能，而且可以指定要在收集的資訊中忽略的特定名稱。

使用開啟或關閉來控制收集 pragma 前方的瀏覽資訊。 例如: 

```cpp
#pragma component(browser, off)
```

讓編譯器停止收集瀏覽資訊。

> [!NOTE]
> 若要開啟的瀏覽資訊，請使用這個 pragma，收集[瀏覽資訊必須先啟用](../build/reference/building-browse-information-files-overview.md)。

`references`可以使用選項，包含或不含*名稱*引數。 使用`references`而不需要*名稱*開啟或關閉參考的收集 （其他瀏覽資訊仍繼續收集，不過）。 例如: 

```cpp
#pragma component(browser, off, references)
```

讓編譯器停止收集參考資訊。

使用`references`具有*名稱*並`off`防止參考*名稱*不會出現在瀏覽資訊視窗。 使用這個語法會忽略您沒有興趣的名稱和類型，並可減少瀏覽資訊檔的大小。 例如: 

```cpp
#pragma component(browser, off, references, DWORD)
```

會忽略為 DWORD 從該點之後的參考。 您可以開啟使用收集的 DWORD 參考回到`on`:

```cpp
#pragma component(browser, on, references, DWORD)
```

這是唯一的方法可以繼續收集參考*名稱*; 您必須明確開啟任何*名稱*，您已關閉。

若要避免前置處理器展開*名稱*（例如擴充 NULL 為 0），將 雙引號括住：

```cpp
#pragma component(browser, off, references, "NULL")
```

### <a name="minimal-rebuild"></a>最少重建

已被取代[/Gm （啟用最少重建）](../build/reference/gm-enable-minimal-rebuild.md)功能需要編譯器建立並儲存C++類別會佔用磁碟空間的相依性資訊。 若要節省磁碟空間，您可以使用`#pragma component( minrebuild, off )`每當您不需要收集相依性資訊，比方說，不會變更的標頭檔中。 插入`#pragma component(minrebuild, on)`之後上一步 若要開啟相依性集合不變的類別。

### <a name="reduce-type-information"></a>減少類型資訊

`mintypeinfo`選項可減少指定區域的偵錯資訊。 這項資訊的容量相當可觀，會影響到 .pdb 和 .obj 檔案。 您無法在 mintypeinfo 區域中偵錯類別和結構。 使用 mintypeinfo 選項可避免下列警告：

```cmd
LINK : warning LNK4018: too many type indexes in PDB "filename", discarding subsequent type information
```

如需詳細資訊，請參閱 < [/Gm （啟用最少重建）](../build/reference/gm-enable-minimal-rebuild.md)編譯器選項。

## <a name="see-also"></a>另請參閱

[Pragma 指示詞和 __Pragma 關鍵字](../preprocessor/pragma-directives-and-the-pragma-keyword.md)