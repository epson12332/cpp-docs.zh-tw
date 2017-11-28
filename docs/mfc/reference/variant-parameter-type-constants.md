---
title: "變異參數類型常數 |Microsoft 文件"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- cpp-windows
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- VTS_YPOS_HIMETRIC
- VTS_PICTURE
- VTS_FONT
- VTS_XPOS_HIMETRIC
- VTS_XPOS_PIXELS
- VTS_XSIZE_HIMETRIC
- VTS_YPOS_PIXELS
- VTS_TRISTATE
- VTS_HANDLE
- VTS_YSIZE_HIMETRIC
- VTS_COLOR
- VTS_OPTEXCLUSIVE
- VTS_YSIZE_PIXELS
- VTS_XSIZE_PIXELS
dev_langs:
- C++
helpviewer_keywords:
- VTS_XPOS_HIMETRIC constant [MFC]
- VTS_FONT constant [MFC]
- VTS_XPOS_PIXELS constant [MFC]
- VTS_COLOR constant [MFC]
- Variants [MFC]
- VTS_YPOS_PIXELS constant [MFC]
- VTS_YSIZE_HIMETRIC constant [MFC]
- VTS_YPOS_HIMETRIC constant [MFC]
- Variants, parameter type constants
- Variant data constants [MFC]
- VTS_PICTURE constant [MFC]
- VTS_TRISTATE constant [MFC]
- VTS_XSIZE_HIMETRIC constant [MFC]
- VTS_HANDLE constant [MFC]
- VTS_XSIZE_PIXELS constant [MFC]
- VTS_OPTEXCLUSIVE constant [MFC]
- VTS_YSIZE_PIXELS constant [MFC]
ms.assetid: de99c7a9-7aae-4dc4-b723-40c6380543ab
caps.latest.revision: 14
author: mikeblome
ms.author: mblome
manager: ghogen
ms.translationtype: MT
ms.sourcegitcommit: 4a770b6508067913aec51b8b3878f33e30eed4bb
ms.openlocfilehash: cc8daf0853a97e8903b47d29f70e190430931fd5
ms.contentlocale: zh-tw
ms.lasthandoff: 10/09/2017

---
# <a name="variant-parameter-type-constants"></a>變異參數類型常數
本主題會列出新的常數，以指出變異參數類型設計為使用 Microsoft Foundation 類別庫的 OLE 控制項類別。  
  
 下列是一份類別常數：  
  
##  <a name="_mfc_variant_data_constants"></a>變異資料常數  
  
-   **VTS_COLOR**用來代表 RGB 色彩值的 32 位元整數。  
  
-   **VTS_FONT**指標**IFontDisp** OLE 字型物件介面。  
  
-   **VTS_HANDLE** Windows 控制代碼值。  
  
-   **VTS_PICTURE**指標`IPictureDisp`OLE 圖片物件的介面。  
  
-   **VTS_OPTEXCLUSIVE**適用於群組中的控制項，例如選項按鈕控制項所使用的 16 位元值。 此類型告知容器是否其中一個控制項中的群組有**TRUE**值，其他所有項目必須是**FALSE**。  
  
-   **VTS_TRISTATE** 16 位元帶正負號的整數用於屬性可以具有一個的三個可能的值 （選取、 清除、 無法使用），例如，核取方塊。  
  
-   **VTS_XPOS_HIMETRIC**的 32 位元不帶正負號的整數，用來表示沿著 x 軸的位置**HIMETRIC**單位。  
  
-   **VTS_YPOS_HIMETRIC**的 32 位元不帶正負號的整數，用來表示沿著 y 軸中的位置**HIMETRIC**單位。  
  
-   **VTS_XPOS_PIXELS**的 32 位元不帶正負號的整數，用來代表沿著 x 軸單位為像素的位置。  
  
-   **VTS_YPOS_PIXELS**的 32 位元不帶正負號的整數，用來代表沿著 y 軸的位置，像素為單位。  
  
-   **VTS_XSIZE_PIXELS**的 32 位元不帶正負號的整數，用來表示螢幕物件像素為單位的寬度。  
  
-   **VTS_YSIZE_PIXELS**的 32 位元不帶正負號的整數，用來表示螢幕物件像素為單位的高度。  
  
-   **VTS_XSIZE_HIMETRIC**的 32 位元不帶正負號的整數，用來表示螢幕中物件的寬度**HIMETRIC**單位。  
  
-   **VTS_YSIZE_HIMETRIC**的 32 位元不帶正負號的整數，用來代表在螢幕物件的高度**HIMETRIC**單位。  
  
    > [!NOTE]
    >  所有的 variant 類型已定義其他的 variant 常數例外**VTS_FONT**和**VTS_PICTURE**，可提供 variant 資料共同的指標nstant。 這些常數會使用名為**VTS_P** `constantname`慣例。 例如， **VTS_PCOLOR**是指向**VTS_COLOR**常數。  
  
## <a name="requirements"></a>需求  
 **標頭：** afxdisp.h  
  
## <a name="see-also"></a>另請參閱  
 [巨集和全域變數](../../mfc/reference/mfc-macros-and-globals.md)
