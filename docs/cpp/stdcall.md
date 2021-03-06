---
title: __stdcall
ms.date: 10/10/2018
f1_keywords:
- __stdcall_cpp
- __stdcall
- _stdcall
helpviewer_keywords:
- __stdcall keyword [C++]
ms.assetid: e212594b-1827-4d07-9527-7d412b300df8
ms.openlocfilehash: b9efac6f729a78db945ff3bd9ab16ebe315b7a5a
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62266955"
---
# <a name="stdcall"></a>__stdcall

**Microsoft 專屬**

**__Stdcall**呼叫慣例用於呼叫 Win32 API 函式。 被呼叫端會清除堆疊，因此編譯器會建立`vararg`函式 **__cdecl**。 使用這個呼叫慣例的函式需要函式原型。

## <a name="syntax"></a>語法

> *return-type* **\_\_stdcall** *function-name*[**(** *argument-list* **)**]

## <a name="remarks"></a>備註

下列清單會顯示這個呼叫慣例的實作。

|項目|實作|
|-------------|--------------------|
|引數傳遞順序|由右至左。|
|引數傳遞慣例|以傳值方式，除非傳遞指標或參考類型。|
|堆疊維護責任|被呼叫函式會從堆疊快顯其本身的引數。|
|名稱裝飾慣例|名稱前面會加底線 (_)。 名稱後面加上 @ 符號，再接著引數清單中的位元組數目 (十進位)。 因此，宣告為 `int func( int a, double b )` 的函式會裝飾為如下：`_func@12`|
|大小寫轉譯慣例|None|

[/Gz](../build/reference/gd-gr-gv-gz-calling-convention.md)編譯器選項會指定 **__stdcall**所有未明確宣告為具有不同呼叫慣例的函式。

為了與舊版中，相容性 **_stdcall**同義 **__stdcall**除非編譯器選項[/Za\(停用語言擴充功能)](../build/reference/za-ze-disable-language-extensions.md)是指定此項目。

使用宣告的函式 **__stdcall**修飾詞的傳回值做為使用宣告的函式的相同方式[__cdecl](../cpp/cdecl.md)。

在 ARM 和 x64 處理器 **__stdcall**會接受並忽略編譯器; 在 ARM 和 x64 架構，依照慣例，引數會傳入暫存器，如果可能的話，和在堆疊上傳遞後續的引數。

對於非靜態類別函式，如果函式是以非正規的方式定義，則不需要在非正規定義上指定呼叫慣例修飾詞。 也就是說，對於類別非靜態成員方法而言，宣告時所指定的呼叫慣例是在定義時假設。 如果已指定此類別定義，

```cpp
struct CMyClass {
   void __stdcall mymethod();
};
```

this

```cpp
void CMyClass::mymethod() { return; }
```

相當於這個

```cpp
void __stdcall CMyClass::mymethod() { return; }
```

## <a name="example"></a>範例

在下列範例中，使用 **__stdcall**造成所有`WINAPI`函式類型被當成標準呼叫處理：

```cpp
// Example of the __stdcall keyword
#define WINAPI __stdcall
// Example of the __stdcall keyword on function pointer
typedef BOOL (__stdcall *funcname_ptr)(void * arg1, const char * arg2, DWORD flags, ...);
```

## <a name="see-also"></a>另請參閱

[引數傳遞和命名慣例](../cpp/argument-passing-and-naming-conventions.md)<br/>
[關鍵字](../cpp/keywords-cpp.md)