---
title: /ALLOWBIND
ms.date: 11/04/2016
f1_keywords:
- /allowbind
helpviewer_keywords:
- ALLOWBIND editbin option
- /ALLOWBIND editbin option
- -ALLOWBIND editbin option
ms.assetid: eaadbb8c-4339-4281-9a75-3a1ce2352ff8
ms.openlocfilehash: 4cb7e5a3627d865e2f2193dee096c72cced75f5f
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62273192"
---
# <a name="allowbind"></a>/ALLOWBIND

指定 DLL 是否可以繫結。

```

/ALLOWBIND[:NO]
```

## <a name="remarks"></a>備註

**/ALLOWBIND**向 Bind.exe 表示映像可繫結 DLL 的標頭中設定一個位元選項。 繫結可以允許更快速載入時，載入器不需要重訂基底，並為每個參考的 DLL 執行位址的修復映像。 您可能不想要繫結，如果已經過數位簽署的 DLL — 繫結失效的簽章。 如果在已使用位址空間配置隨機載入 (ASLR) 啟用映像，繫結會有任何作用 **/DYNAMICBASE**的支援 ASLR 的 Windows 版本上。

使用 **/allowbind: no**防止 Bind.exe 繫結 DLL。

如需詳細資訊，請參閱 < [/ALLOWBIND](allowbind-prevent-dll-binding.md)連結器選項。

## <a name="see-also"></a>另請參閱

[EDITBIN 選項](editbin-options.md)
