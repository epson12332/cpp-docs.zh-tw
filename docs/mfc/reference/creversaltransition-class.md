---
title: CReversalTransition 類別
ms.date: 11/04/2016
f1_keywords:
- CReversalTransition
- AFXANIMATIONCONTROLLER/CReversalTransition
- AFXANIMATIONCONTROLLER/CReversalTransition::CReversalTransition
- AFXANIMATIONCONTROLLER/CReversalTransition::Create
- AFXANIMATIONCONTROLLER/CReversalTransition::m_duration
helpviewer_keywords:
- CReversalTransition [MFC], CReversalTransition
- CReversalTransition [MFC], Create
- CReversalTransition [MFC], m_duration
ms.assetid: e89516be-2d07-4885-95a8-fc278f46e3ad
ms.openlocfilehash: 4bd60ca13ff4a162ddd674e271291a1a3f09a856
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62372123"
---
# <a name="creversaltransition-class"></a>CReversalTransition 類別

封裝反轉的轉換。

## <a name="syntax"></a>語法

```
class CReversalTransition : public CBaseTransition;
```

## <a name="members"></a>成員

### <a name="public-constructors"></a>公用建構函式

|名稱|描述|
|----------|-----------------|
|[CReversalTransition::CReversalTransition](#creversaltransition)|建構反轉轉換物件並初始化其持續時間。|

### <a name="public-methods"></a>公用方法

|名稱|描述|
|----------|-----------------|
|[CReversalTransition::Create](#create)|呼叫轉換程式庫來建立封裝的轉換 COM 物件。 (覆寫[CBaseTransition::Create](../../mfc/reference/cbasetransition-class.md#create)。)|

### <a name="public-data-members"></a>公用資料成員

|名稱|描述|
|----------|-----------------|
|[CReversalTransition::m_duration](#m_duration)|轉換的持續時間。|

## <a name="remarks"></a>備註

反轉的轉換順利變更指定的持續期間內的方向。 最終的值將會是初始的值相同，因此最終的速度的初始速度的負值。 因為所有的轉換會自動清除，所以建議配置它們使用新的運算子。 封裝的 IUIAnimationTransition COM 物件會建立 CAnimationController::AnimateGroup 之前, 則是 NULL。 不會影響這個 COM 物件建立後，請變更成員變數。

## <a name="inheritance-hierarchy"></a>繼承階層

[CObject](../../mfc/reference/cobject-class.md)

[CBaseTransition](../../mfc/reference/cbasetransition-class.md)

[CReversalTransition](../../mfc/reference/creversaltransition-class.md)

## <a name="requirements"></a>需求

**標頭：** afxanimationcontroller.h

##  <a name="create"></a>  CReversalTransition::Create

呼叫轉換程式庫來建立封裝的轉換 COM 物件。

```
virtual BOOL Create(
    IUIAnimationTransitionLibrary* pLibrary,
    IUIAnimationTransitionFactory* \*not used*\);
```

### <a name="parameters"></a>參數

*pLibrary*<br/>
轉換程式庫，也就是負責建立的標準轉換指標。

### <a name="return-value"></a>傳回值

如果轉換成功; 建立，則為 TRUE。否則為 FALSE。

##  <a name="creversaltransition"></a>  CReversalTransition::CReversalTransition

建構反轉轉換物件並初始化其持續時間。

```
CReversalTransition(UI_ANIMATION_SECONDS duration);
```

### <a name="parameters"></a>參數

*duration*<br/>
轉換的持續時間。

##  <a name="m_duration"></a>  CReversalTransition::m_duration

轉換的持續時間。

```
UI_ANIMATION_SECONDS m_duration;
```

## <a name="see-also"></a>另請參閱

[類別](../../mfc/reference/mfc-classes.md)
