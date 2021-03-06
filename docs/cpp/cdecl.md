---
title: __cdecl
ms.date: 10/09/2018
f1_keywords:
- __cdecl_cpp
- __cdecl
- _cdecl
- cdecl
helpviewer_keywords:
- __cdecl keyword [C++]
ms.assetid: 1ff1d03e-fb4e-4562-8be1-74f1ad6427f1
ms.openlocfilehash: 298485d310ee4039b13781a8b5cd88a489af3b8b
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62232398"
---
# <a name="cdecl"></a>__cdecl

**Microsoft 專屬**

**__cdecl**是適用於 C 呼叫慣例的預設值和C++程式。 因為呼叫端會清除堆疊，它可以執行`vararg`函式。 **__Cdecl**呼叫慣例會建立較大的可執行檔，比[__stdcall](../cpp/stdcall.md)，因為它需要每個函式呼叫都包含堆疊清除程式碼。 下列清單會顯示這個呼叫慣例的實作。

|項目|實作|
|-------------|--------------------|
|引數傳遞順序|由右至左。|
|堆疊維護責任|呼叫函式會從堆疊取出引數。|
|名稱裝飾慣例|名稱，除非有前置底線字元 (_)\_匯出使用 C 連結的 _cdecl 函式。|
|大小寫轉譯慣例|未執行大小寫轉譯。|

> [!NOTE]
>  如需相關資訊，請參閱[裝飾名稱](../build/reference/decorated-names.md)。

地方 **__cdecl**變數或函式名稱之前的修飾詞。 由於 C 命名和呼叫慣例是預設值，唯一的時候您必須使用 **__cdecl**在 x86 程式碼時，您已指定`/Gv`(vectorcall)、 `/Gz` (stdcall) 或`/Gr`(fastcall)編譯器選項。 [/Gd](../build/reference/gd-gr-gv-gz-calling-convention.md)編譯器選項會強制執行 **__cdecl**呼叫慣例。

在 ARM 和 x64 處理器 **__cdecl**是接受，但通常會忽略編譯器。 ARM 和 x64 的慣例會盡可能在暫存器中傳遞引數，並在堆疊上傳遞後續的引數。 在 x64 程式碼，請使用 **__cdecl**覆寫 **/Gv**編譯器選項，並使用預設的 x64 呼叫慣例。

對於非靜態類別函式，如果函式是以非正規的方式定義，則不需要在非正規定義上指定呼叫慣例修飾詞。 也就是說，對於類別非靜態成員方法而言，宣告時所指定的呼叫慣例是在定義時假設。 如果已指定此類別定義：

```cpp
struct CMyClass {
   void __cdecl mymethod();
};
```

這個：

```cpp
void CMyClass::mymethod() { return; }
```

相當於這個：

```cpp
void __cdecl CMyClass::mymethod() { return; }
```

為了與舊版中，相容性**cdecl**並 **_cdecl**是同義 **__cdecl**除非編譯器選項[/Za\(停用語言擴充功能）](../build/reference/za-ze-disable-language-extensions.md)指定。

## <a name="example"></a>範例

在下列範例中，編譯器收到的指示是針對 `system` 函式使用 C 命名及呼叫慣例。

```cpp
// Example of the __cdecl keyword on function
int __cdecl system(const char *);
// Example of the __cdecl keyword on function pointer
typedef BOOL (__cdecl *funcname_ptr)(void * arg1, const char * arg2, DWORD flags, ...);
```

## <a name="see-also"></a>另請參閱

[引數傳遞和命名慣例](../cpp/argument-passing-and-naming-conventions.md)<br/>
[關鍵字](../cpp/keywords-cpp.md)