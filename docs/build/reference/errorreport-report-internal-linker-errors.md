---
title: /ERRORREPORT (回報內部連結器錯誤)
ms.date: 12/28/2017
f1_keywords:
- /ERRORREPORT
- VC.Project.VCLinkerTool.ErrorReporting
helpviewer_keywords:
- /ERRORREPORT linker option
- ERRORREPORT linker option
- -ERRORREPORT linker option
ms.assetid: f5fab595-a2f1-4eb0-ab5c-1c0fbd3d8c28
ms.openlocfilehash: 26cc157cb7247a3a2ea7c10b415df1160540c9ad
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62271725"
---
# <a name="errorreport-report-internal-linker-errors"></a>/ERRORREPORT (回報內部連結器錯誤)

> **/errorreport:**[**無** | **提示** | **佇列** | **傳送**]

## <a name="arguments"></a>引數

**none**<br/>
將不會收集有關內部編譯器錯誤的報告，也不會將報告傳送給 Microsoft。

**提示**<br/>
提示您在收到內部編譯器錯誤時傳送報告。 **提示字元**是在開發環境中編譯應用程式的預設值。

**queue**<br/>
佇列錯誤報告。 當您登入系統管理員權限時，以便您可以報告自上次登入的任何失敗，會顯示的視窗 （您將不會提示您傳送錯誤報告的頻率超過每隔三天一次）。 **佇列**是應用程式會在命令提示字元進行編譯時的預設值。

**傳送**<br/>
如果 Windows 錯誤報告服務的設定已啟用報告，自動傳送給 Microsoft 報告內部編譯器錯誤。

## <a name="remarks"></a>備註

**/ERRORREPORT**選項可讓您直接向 Microsoft 提供內部編譯器錯誤 (ICE) 資訊。

選項 **/errorreport: send**會自動將錯誤資訊傳送給 Microsoft，如果啟用 Windows 錯誤報告服務設定。

### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>在 Visual Studio 開發環境中設定這個編譯器選項

1. 開啟專案的 [ **屬性頁** ] 對話方塊。 如需詳細資訊，請參閱 <<c0> [ 設定C++Visual Studio 中的編譯器和組建屬性](../working-with-project-properties.md)。</c0>

1. 開啟**組態屬性** > **連結器** > **進階**屬性頁。

1. 修改**錯誤報告**屬性。

### <a name="to-set-this-compiler-option-programmatically"></a>若要以程式方式設定這個編譯器選項

- 請參閱 <xref:Microsoft.VisualStudio.VCProjectEngine.VCLinkerTool.ErrorReporting%2A>。

## <a name="see-also"></a>另請參閱

[/errorReport (回報編譯器內部錯誤)](errorreport-report-internal-compiler-errors.md)<br/>
[MSVC 連結器參考](linking.md)<br/>
[MSVC 連結器選項](linker-options.md)
