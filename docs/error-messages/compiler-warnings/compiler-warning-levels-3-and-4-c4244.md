---
title: 編譯器警告 (層級 3 和 4) C4244
ms.date: 11/04/2016
ms.assetid: f116bb09-c479-4b4e-a647-fe629a1383f6
ms.openlocfilehash: af06dbf5bb4a1dd133c277d63c40da2a8a54770b
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62359926"
---
# <a name="compiler-warning-levels-3-and-4-c4244"></a>編譯器警告 (層級 3 和 4) C4244

'conversion'：將 'type1' 轉換為 'type2'，資料可能遺失

整數類型會轉換為較小的整數類型。 如果這是層級 4 警告*type1*是`int`並*type2*小於`int`。 否則，就是層級 3 (指派類型的值[__int64](../../cpp/int8-int16-int32-int64.md)類型的變數至`unsigned int`)。 資料可能會遺失。

如果出現 C4244，您應變更程式以使用相容的類型，或在您的程式碼中加入某些邏輯，以確保可能值的範圍一定會與您所使用的類型相容。

C4244 也可能引發層級 2;請參閱[編譯器警告 （層級 2） C4244](../../error-messages/compiler-warnings/compiler-warning-level-2-c4244.md)如需詳細資訊。

轉換可能會因為隱含轉換而發生問題。

下列範例會產生 C4244：

```
// C4244_level4.cpp
// compile with: /W4
int aa;
unsigned short bb;
int main() {
   int b = 0, c = 0;
   short a = b + c;   // C4244

   bb += c;   // C4244
   bb = bb + c;   // C4244
   bb += (unsigned short)aa;   // C4244
   bb = bb + (unsigned short)aa;   // OK
}
```

如需詳細資訊，請參閱 <<c0> [ 一般算術轉換](../../c-language/usual-arithmetic-conversions.md)。

```
// C4244_level3.cpp
// compile with: /W3
int main() {
   __int64 i = 8;
   unsigned int ii = i;   // C4244
}
```

為 64 位元目標建置程式碼時，可能會發生為 32 位元目標建置時不會產生的警告 C4244。 以指標之間的差異為例，32 位元平台上的是 32 位元數量，但 64 位元平台上的會是 64 位元數量。

下列範例會在進行 64 位元目標的編譯時產生 C4244：

```
// C4244_level3_b.cpp
// compile with: /W3
int main() {
   char* p1 = 0;
   char* p2 = 0;
   int x = p2 - p1;   // C4244
}
```