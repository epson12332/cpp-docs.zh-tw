---
title: '&lt;m > (C++文件註解)'
ms.date: 11/04/2016
f1_keywords:
- <summary>
- summary
helpviewer_keywords:
- <summary> C++ XML tag
- summary C++ XML tag
ms.assetid: cdeeefbb-1339-45d6-9002-10042a9a2726
ms.openlocfilehash: 68bb8b7c269b3406438e5cf21dde7179f7e67646
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62318182"
---
# <a name="ltsummarygt"></a>&lt;summary&gt;

\<summary> 標記應該用來描述類型或類型成員。 使用 [\<remarks>](remarks-visual-cpp.md) 新增類型描述的補充資訊。

## <a name="syntax"></a>語法

```
<summary>description</summary>
```

#### <a name="parameters"></a>參數

*description*<br/>
物件的摘要。

## <a name="remarks"></a>備註

\<summary> 標記的文字是 IntelliSense 中型別的唯一資訊來源，也會顯示在[物件瀏覽器](/visualstudio/ide/viewing-the-structure-of-code)和程式碼結構 Web 報告中。

編譯搭配 [/doc](doc-process-documentation-comments-c-cpp.md) 可處理檔案的文件註解。

## <a name="example"></a>範例

```
// xml_summary_tag.cpp
// compile with: /LD /clr /doc
// post-build command: xdcmake xml_summary_tag.dll

/// Text for class MyClass.
public ref class MyClass {
public:
   /// <summary>MyMethod is a method in the MyClass class.
   /// <para>Here's how you could make a second paragraph in a description. <see cref="System::Console::WriteLine"/> for information about output statements.</para>
   /// <seealso cref="MyClass::MyMethod2"/>
   /// </summary>
   void MyMethod(int Int1) {}

   /// text
   void MyMethod2() {}
};
```

## <a name="see-also"></a>另請參閱

[XML 文件](xml-documentation-visual-cpp.md)
