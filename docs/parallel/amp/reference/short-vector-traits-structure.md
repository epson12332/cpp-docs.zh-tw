---
title: short_vector_traits 結構
ms.date: 11/04/2016
f1_keywords:
- short_vector_traits
- AMP_SHORT_VECTORS/short_vector_traits
- AMP_SHORT_VECTORS/Concurrency::graphics::short_vector_traits::short_vector_traits
- AMP_SHORT_VECTORS/Concurrency::graphics::short_vector_traits::size Constant
ms.assetid: cd9492da-9e02-4a6e-9d50-b61252cdb460
ms.openlocfilehash: c407c42e5c6a7035e911218ecb41c2da62967787
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62351140"
---
# <a name="shortvectortraits-structure"></a>short_vector_traits 結構

short_vector_traits 允許擷取時，基礎的向量長度和短向量類型的純量類型或純量類型

## <a name="syntax"></a>語法

```
template<
    typename T
>
struct short_vector_traits;
template<>
struct short_vector_traits<unsigned int>;
template<>
struct short_vector_traits<uint_2>;
template<>
struct short_vector_traits<uint_3>;
template<>
struct short_vector_traits<uint_4>;
template<>
struct short_vector_traits<int>;
template<>
struct short_vector_traits<int_2>;
template<>
struct short_vector_traits<int_3>;
template<>
struct short_vector_traits<int_4>;
template<>
struct short_vector_traits<float>;
template<>
struct short_vector_traits<float_2>;
template<>
struct short_vector_traits<float_3>;
template<>
struct short_vector_traits<float_4>;
template<>
struct short_vector_traits<unorm>;
template<>
struct short_vector_traits<unorm_2>;
template<>
struct short_vector_traits<unorm_3>;
template<>
struct short_vector_traits<unorm_4>;
template<>
struct short_vector_traits<norm>;
template<>
struct short_vector_traits<norm_2>;
template<>
struct short_vector_traits<norm_3>;
template<>
struct short_vector_traits<norm_4>;
template<>
struct short_vector_traits<double>;
template<>
struct short_vector_traits<double_2>;
template<>
struct short_vector_traits<double_3>;
template<>
struct short_vector_traits<double_4>;
```

#### <a name="parameters"></a>參數

`T`

## <a name="members"></a>成員

### <a name="public-typedefs"></a>公用 Typedefs

|名稱|描述|
|----------|-----------------|
|`value_type`||

### <a name="public-constructors"></a>公用建構函式

|名稱|描述|
|----------|-----------------|
|[short_vector_traits:: short_vector_traits 建構函式](#ctor)||

### <a name="public-constants"></a>公用常數

|名稱|描述|
|----------|-----------------|
|[short_vector_traits:: size 常數](#size)||

## <a name="inheritance-hierarchy"></a>繼承階層

`short_vector_traits`

## <a name="requirements"></a>需求

**標頭：** amp_short_vectors.h

**命名空間：** Concurrency:: graphics

##  <a name="ctor"></a>  short_vector_traits:: short_vector_traits 建構函式

```
short_vector_traits();
```

##  <a name="size"></a>  short_vector_traits:: size 常數

```
static int const size = 1;
```

## <a name="see-also"></a>另請參閱

[Concurrency::graphics 命名空間](concurrency-graphics-namespace.md)
