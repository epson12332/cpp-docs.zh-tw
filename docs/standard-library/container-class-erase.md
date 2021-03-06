---
title: 容器類別::erase
ms.date: 11/04/2016
helpviewer_keywords:
- erase method
ms.assetid: abc091c5-5a80-4bd8-93a8-a2d9bde2efec
ms.openlocfilehash: 0ef4db1c14942fc896f10095ff2331648d27c820
ms.sourcegitcommit: da32511dd5baebe27451c0458a95f345144bd439
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/07/2019
ms.locfileid: "65221633"
---
# <a name="container-classerase"></a>容器類別::erase

> [!NOTE]
> 本主題位於 MicrosoftC++中所用容器的無作用範例文件C++標準程式庫。 如需詳細資訊，請參閱 [C++ 標準程式庫容器](../standard-library/stl-containers.md)。

插入元素。

## <a name="syntax"></a>語法

```

    iterator erase(
    iterator _Where);

iterator erase(
    iterator first,
    iterator last);
```

## <a name="remarks"></a>備註

第一個成員函式會移除所指向之受控制序列的項目 *_Where*。 第二個成員函式會移除 [`first`, `last`) 範圍中受控制序列中的元素。 兩者皆會傳回迭代器，其指定任何移除的元素之後的第一個剩餘元素；如果沒有這個元素，則為 [end](../standard-library/container-class-end.md)。

只有當複製作業擲回例外狀況時，成員函式才會擲回例外狀況。

## <a name="see-also"></a>另請參閱

[範例容器類別](../standard-library/sample-container-class.md)<br/>
