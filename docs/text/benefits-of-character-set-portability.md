---
title: 字元集移植性的優點
ms.date: 11/04/2016
helpviewer_keywords:
- character sets [C++], benefits
- portability [C++], character sets
ms.assetid: bd60b925-1498-4e4f-897b-4c8ce66edcf7
ms.openlocfilehash: 0ca7e46cabb2d98a64a244863f8574a3e9e2a456
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62410770"
---
# <a name="benefits-of-character-set-portability"></a>字元集移植性的優點

您可以使用 MFC 和 C 執行階段可攜性功能，即使您目前不想要您的應用程式的國際化獲益：

- 可移植，可讓您的程式碼基底彈性。 您可以稍後再將它輕鬆地 Unicode 或 MBCS。

- 使用 Unicode，可讓您的應用程式的 Windows 更有效率。 因為 Windows 會使用 Unicode，非 Unicode 字串與作業系統之間來回必須轉譯，這會產生額外負荷。

## <a name="see-also"></a>另請參閱

[Unicode 和 MBCS](../text/unicode-and-mbcs.md)<br/>
[Unicode 的支援](../text/support-for-unicode.md)
