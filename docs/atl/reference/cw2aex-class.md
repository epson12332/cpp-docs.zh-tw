---
title: CW2AEX 類別
ms.date: 11/04/2016
f1_keywords:
- CW2AEX
- ATLCONV/ATL::CW2AEX
- ATLCONV/ATL::CW2AEX::CW2AEX
- ATLCONV/ATL::CW2AEX::m_psz
- ATLCONV/ATL::CW2AEX::m_szBuffer
helpviewer_keywords:
- CW2AEX class
ms.assetid: 44dc2cf5-dd30-440b-a9b9-b21b43f49843
ms.openlocfilehash: 97b398dd80bb38b1579458ae0b8b65f082458e23
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62277161"
---
# <a name="cw2aex-class"></a>CW2AEX 類別

這個類別會使用字串轉換巨集 CT2AEX、 CW2TEX、 CW2CTEX，和 CT2CAEX 和 typedef CW2A。

> [!IMPORTANT]
>  此類別和其成員不能在 Windows 執行階段中執行的應用程式。

## <a name="syntax"></a>語法

```
template<int t_nBufferLength = 128>
class CW2AEX
```

#### <a name="parameters"></a>參數

*t_nBufferLength*<br/>
轉譯程序中使用的緩衝區大小。 預設長度為 128 位元組。

## <a name="members"></a>成員

### <a name="public-constructors"></a>公用建構函式

|名稱|描述|
|----------|-----------------|
|[CW2AEX::CW2AEX](#cw2aex)|建構函式。|
|[CW2AEX::~CW2AEX](#dtor)|解構函式。|

### <a name="public-operators"></a>公用運算子

|名稱|描述|
|----------|-----------------|
|[CW2AEX::operator LPSTR](#operator_lpstr)|轉換運算子。|

### <a name="public-data-members"></a>公用資料成員

|名稱|描述|
|----------|-----------------|
|[CW2AEX::m_psz](#m_psz)|儲存在來源字串資料成員。|
|[CW2AEX::m_szBuffer](#m_szbuffer)|靜態緩衝區，用來儲存已轉換的字串。|

## <a name="remarks"></a>備註

除非需要額外的功能，使用 CT2AEX、 CW2TEX、 CW2CTEX、 CT2CAEX 或 CW2A 程式碼中。

這個類別包含固定大小的靜態緩衝區可用來儲存轉換的結果。 如果結果太大而無法放入靜態緩衝區，類別配置的記憶體使用**malloc**，當物件超出範圍時，即釋放記憶體。 這可確保，不同於文字轉換巨集可在舊版的 ATL，這個類別能夠安全地在迴圈中使用，而且它不會堆疊溢位。

如果類別嘗試失敗與堆積上配置記憶體時，它會呼叫`AtlThrow`E_OUTOFMEMORY 引數。

根據預設，ATL 轉換類別和巨集會使用目前的執行緒 ANSI 字碼頁轉換。 如果您想要覆寫特定轉換，行為，請做為類別的建構函式的第二個參數指定的字碼頁。

下列巨集根據此類別：

- CT2AEX

- CW2TEX

- CW2CTEX

- CT2CAEX

下列的 typedef 根據此類別：

- CW2A

如需這些文字轉換巨集的討論，請參閱 < [ATL 和 MFC 字串轉換巨集](string-conversion-macros.md)。

## <a name="example"></a>範例

請參閱[ATL 和 MFC 字串轉換巨集](string-conversion-macros.md)如需使用這些字串轉換巨集的範例。

## <a name="requirements"></a>需求

**標頭：** atlconv.h

##  <a name="cw2aex"></a>  CW2AEX::CW2AEX

建構函式。

```
CW2AEX(LPCWSTR psz, UINT nCodePage) throw(...);
CW2AEX(LPCWSTR psz) throw(...);
```

### <a name="parameters"></a>參數

*psz*<br/>
要轉換的文字字串。

*nCodePage*<br/>
使用的字碼頁來執行轉換。 請參閱 Windows SDK 函式的程式碼頁面參數討論[MultiByteToWideChar](/windows/desktop/api/stringapiset/nf-stringapiset-multibytetowidechar)如需詳細資訊。

### <a name="remarks"></a>備註

配置轉譯程序中使用的緩衝區。

##  <a name="dtor"></a>  CW2AEX::~CW2AEX

解構函式。

```
~CW2AEX() throw();
```

### <a name="remarks"></a>備註

釋放配置的緩衝區。

##  <a name="m_psz"></a>  CW2AEX::m_psz

儲存在來源字串資料成員。

```
LPSTR m_psz;
```

##  <a name="m_szbuffer"></a>  CW2AEX::m_szBuffer

靜態緩衝區，用來儲存已轉換的字串。

```
char m_szBuffer[t_nBufferLength];
```

##  <a name="operator_lpstr"></a>  CW2AEX::operator LPSTR

轉換運算子。

```
operator LPSTR() const throw();
```

### <a name="return-value"></a>傳回值

當輸入 LPSTR，傳回文字字串。

## <a name="see-also"></a>另請參閱

[CA2AEX 類別](../../atl/reference/ca2aex-class.md)<br/>
[CA2CAEX 類別](../../atl/reference/ca2caex-class.md)<br/>
[CA2WEX 類別](../../atl/reference/ca2wex-class.md)<br/>
[CW2CWEX 類別](../../atl/reference/cw2cwex-class.md)<br/>
[CW2WEX 類別](../../atl/reference/cw2wex-class.md)<br/>
[類別概觀](../../atl/atl-class-overview.md)
