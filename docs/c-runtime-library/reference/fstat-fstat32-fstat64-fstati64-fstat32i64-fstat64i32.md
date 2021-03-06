---
title: _fstat、_fstat32、_fstat64、_fstati64、_fstat32i64、_fstat64i32
ms.date: 11/04/2016
apiname:
- _fstat32
- _fstat64
- _fstati64
- _fstat
- _fstat64i32
- _fstat32i64
apilocation:
- msvcrt.dll
- msvcr80.dll
- msvcr90.dll
- msvcr100.dll
- msvcr100_clr0400.dll
- msvcr110.dll
- msvcr110_clr0400.dll
- msvcr120.dll
- msvcr120_clr0400.dll
- ucrtbase.dll
- api-ms-win-crt-filesystem-l1-1-0.dll
apitype: DLLExport
f1_keywords:
- _fstat32i64
- fstat
- fstat64i32
- _fstat64
- _fstati64
- fstat64
- _fstat32
- fstat32i64
- fstati64
- _fstat
- fstat32
- _fstat64i32
helpviewer_keywords:
- _fstat64 function
- fstati64 function
- _fstat64i32 function
- _fstat32i64 function
- _fstat32 function
- file information
- fstat64i32 function
- fstat32 function
- fstat function
- fstat64 function
- _fstat function
- _fstati64 function
- fstat32i64 function
ms.assetid: 088f5e7a-9636-4cf7-ab8e-e28d2aa4280a
ms.openlocfilehash: 36d8b0d6480266f86136119a470fb7af5859a5b8
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62332784"
---
# <a name="fstat-fstat32-fstat64-fstati64-fstat32i64-fstat64i32"></a>_fstat、_fstat32、_fstat64、_fstati64、_fstat32i64、_fstat64i32

取得開啟之檔案的相關資訊。

## <a name="syntax"></a>語法

```C
int _fstat(
   int fd,
   struct _stat *buffer
);
int _fstat32(
   int fd,
   struct __stat32 *buffer
);
int _fstat64(
   int fd,
   struct __stat64 *buffer
);
int _fstati64(
   int fd,
   struct _stati64 *buffer
);
int _fstat32i64(
   int fd,
   struct _stat32i64 *buffer
);
int _fstat64i32(
   int fd,
   struct _stat64i32 *buffer
);
```

### <a name="parameters"></a>參數

*fd*<br/>
已開啟之檔案的檔案描述項。

*buffer*<br/>
儲存結果的結構指標。

## <a name="return-value"></a>傳回值

如果取得檔案狀態資訊，則傳回 0。 傳回值為-1 表示錯誤。 如果檔案描述項無效，或*緩衝區*是**NULL**，無效參數處理常式會叫用，如中所述[Parameter Validation](../../c-runtime-library/parameter-validation.md)。 如果允許繼續，請執行**errno**設為**EBADF**、 在檔案描述項無效，或**EINVAL**的話*緩衝區*已**NULL**。

## <a name="remarks"></a>備註

**_Fstat**函式會取得開啟的檔案與相關聯的資訊*fd*並將它儲存在結構中所指*緩衝區*。 **_Stat** SYS\Stat.h 中定義的結構包含下列欄位。

|欄位|意義|
|-|-|
| **st_atime** | 最後存取檔案的時間。 |
| **st_ctime** | 建立檔案的時間。 |
| **st_dev** | 如果是裝置，請*fd*，否則為 0。 |
| **st_mode** | 檔案模式資訊的位元遮罩。 **_S_IFCHR**如果使用者設定位元*fd*指的是裝置。 **_S_IFREG**如果使用者設定位元*fd*指的是一般的檔案。 讀取/寫入位元會根據檔案的權限模式設定。 **_S_IFCHR**和其他常數於 SYS\Stat.h 中定義。 |
| **st_mtime** | 檔案的上次修改時間。 |
| **st_nlink** | 在非 NTFS 檔案系統上一律為 1。 |
| **st_rdev** | 如果是裝置，請*fd*，否則為 0。 |
| **st_size** | 檔案大小，以位元組為單位。 |

如果*fd*指的是裝置， **st_atime**， **st_ctime**， **st_mtime**，以及**st_size**欄位沒有意義。

因為 Stat.h 使用在 Types.h 中定義的 [_dev_t](../../c-runtime-library/standard-types.md) 類型，所以您必須在程式碼中的 Stat.h 之前包含 Types.h。

**_fstat64**，它會使用 **__stat64**結構，可讓檔案建立日期到 23:59:59，3000 年 12 月 31 日 UTC; 表示，而其他函式只能表示 23:59:59 年 1 月 18 日的日期2038 年 UTC。 1970 年 1 月 1 日午夜是所有這些函式的日期範圍下限。

這些函式的變化支援 32 位元或 64 位元時間類型，以及 32 位元或 64 位元檔案長度。 第一個數值尾碼 (**32**或**64**) 表示時間的大小類型使用，第二個尾碼為**i32**或是**i64**，表示檔案大小以 32 位元或 64 位元的整數。

**_fstat**相當於 **_fstat64i32**，以及**結構** **_stat**包含 64 位元時間。 這適用於除非 **_USE_32BIT_TIME_T**定義，在此情況下會採用舊版行為生效;**_fstat**使用 32 位元時間，以及**結構** **_stat**包含 32 位元時間。 這也適用於 **_fstati64**。

### <a name="time-type-and-file-length-type-variations-of-stat"></a>_stat 的時間類型和檔案長度類型版本

|函式|是否已定義 _USE_32BIT_TIME_T？|時間類型|檔案長度類型|
|---------------|------------------------------------|---------------|----------------------|
|**_fstat**|未定義|64 位元|32 位元|
|**_fstat**|已定義|32 位元|32 位元|
|**_fstat32**|不會受到巨集定義的影響|32 位元|32 位元|
|**_fstat64**|不會受到巨集定義的影響|64 位元|64 位元|
|**_fstati64**|未定義|64 位元|64 位元|
|**_fstati64**|已定義|32 位元|64 位元|
|**_fstat32i64**|不會受到巨集定義的影響|32 位元|64 位元|
|**_fstat64i32**|不會受到巨集定義的影響|64 位元|32 位元|

## <a name="requirements"></a>需求

|功能|必要的標頭|
|--------------|---------------------|
|**_fstat**|\<sys/stat.h> 和 \<sys/types.h>|
|**_fstat32**|\<sys/stat.h> 和 \<sys/types.h>|
|**_fstat64**|\<sys/stat.h> 和 \<sys/types.h>|
|**_fstati64**|\<sys/stat.h> 和 \<sys/types.h>|
|**_fstat32i64**|\<sys/stat.h> 和 \<sys/types.h>|
|**_fstat64i32**|\<sys/stat.h> 和 \<sys/types.h>|

如需相容性的詳細資訊，請參閱 [相容性](../../c-runtime-library/compatibility.md)。

## <a name="example"></a>範例

```C
// crt_fstat.c
// This program uses _fstat to report
// the size of a file named F_STAT.OUT.

#include <io.h>
#include <fcntl.h>
#include <time.h>
#include <sys/types.h>
#include <sys/stat.h>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <errno.h>
#include <share.h>

int main( void )
{
   struct _stat buf;
   int fd, result;
   char buffer[] = "A line to output";
   char timebuf[26];
   errno_t err;

   _sopen_s( &fd,
             "f_stat.out",
             _O_CREAT | _O_WRONLY | _O_TRUNC,
             _SH_DENYNO,
             _S_IREAD | _S_IWRITE );
   if( fd != -1 )
      _write( fd, buffer, strlen( buffer ) );

   // Get data associated with "fd":
   result = _fstat( fd, &buf );

   // Check if statistics are valid:
   if( result != 0 )
   {
      if (errno == EBADF)
        printf( "Bad file descriptor.\n" );
      else if (errno == EINVAL)
        printf( "Invalid argument to _fstat.\n" );
   }
   else
   {
      printf( "File size     : %ld\n", buf.st_size );
      err = ctime_s(timebuf, 26, &buf.st_mtime);
      if (err)
      {
         printf("Invalid argument to ctime_s.");
         exit(1);
      }
      printf( "Time modified : %s", timebuf );
   }
   _close( fd );
}
```

```Output
File size     : 16
Time modified : Wed May 07 15:25:11 2003
```

## <a name="see-also"></a>另請參閱

[檔案處理](../../c-runtime-library/file-handling.md)<br/>
[_access、_waccess](access-waccess.md)<br/>
[_chmod、_wchmod](chmod-wchmod.md)<br/>
[_filelength、_filelengthi64](filelength-filelengthi64.md)<br/>
[_stat、_wstat 函式](stat-functions.md)<br/>
