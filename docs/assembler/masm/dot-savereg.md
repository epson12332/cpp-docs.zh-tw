---
title: .SAVEREG
ms.date: 08/30/2018
f1_keywords:
- .SAVEREG
helpviewer_keywords:
- .SAVEREG directive
ms.assetid: 1dbc2ef6-a197-40e7-9e55-fddcae8cef29
ms.openlocfilehash: cac7aa7f2bdbf6b60831d2beb062f86559ec0358
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62178159"
---
# <a name="savereg"></a>.SAVEREG

會產生其中一個`UWOP_SAVE_NONVOL`或是`UWOP_SAVE_NONVOL_FAR`回溯程式碼項目指定的暫存器 (`reg`) 和位移 (`offset`) 使用目前的序言位移。 MASM 會選擇最有效率的編碼方式。

## <a name="syntax"></a>語法

> .SAVEREG reg 位移

## <a name="remarks"></a>備註

.SAVEREG 允許 ml64.exe 使用者指定框架的函式的回溯時，而且只允許在序言，始[PROC](../../assembler/masm/proc.md)框架宣告[。ENDPROLOG](../../assembler/masm/dot-endprolog.md)指示詞。 這些指示詞不會產生程式碼路徑。它們只會產生`.xdata`和`.pdata`。 .SAVEREG 之前應該加實際實作要回溯動作的指示。 它是個不錯的做法，包裝的回溯程式指示詞和它們以確保協議要在巨集中的回溯程式碼。

如需詳細資訊，請參閱 < [MASM (ml64.exe) x64 的](../../assembler/masm/masm-for-x64-ml64-exe.md)。

## <a name="see-also"></a>另請參閱

[指示詞參考](../../assembler/masm/directives-reference.md)<br/>