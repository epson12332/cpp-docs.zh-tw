---
title: "recursive_timed_mutex 類別 | Microsoft Docs"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: cpp-standard-libraries
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- mutex/std::recursive_timed_mutex
- mutex/std::recursive_timed_mutex::recursive_timed_mutex
- mutex/std::recursive_timed_mutex::lock
- mutex/std::recursive_timed_mutex::try_lock
- mutex/std::recursive_timed_mutex::try_lock_for
- mutex/std::recursive_timed_mutex::try_lock_until
- mutex/std::recursive_timed_mutex::unlock
dev_langs: C++
ms.assetid: 59cc2d5c-ed80-45f3-a0a8-05652a8ead7e
caps.latest.revision: "9"
author: corob-msft
ms.author: corob
manager: ghogen
helpviewer_keywords:
- std::recursive_timed_mutex [C++]
- std::recursive_timed_mutex [C++], recursive_timed_mutex
- std::recursive_timed_mutex [C++], lock
- std::recursive_timed_mutex [C++], try_lock
- std::recursive_timed_mutex [C++], try_lock_for
- std::recursive_timed_mutex [C++], try_lock_until
- std::recursive_timed_mutex [C++], unlock
ms.workload: cplusplus
ms.openlocfilehash: 9ed5930eca492d6793ab08c39b6af8b45a9124c2
ms.sourcegitcommit: 8fa8fdf0fbb4f57950f1e8f4f9b81b4d39ec7d7a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="recursivetimedmutex-class"></a>recursive_timed_mutex 類別
代表計時的 mutex 類型。 藉由在程式內使用限時的封鎖，可以使用這個類型的物件來強制執行互斥。 不同於 [timed_mutex](../standard-library/timed-mutex-class.md) 類型的物件，已針對 `recursive_timed_mutex` 物件妥善定義呼叫鎖定方法的效果。  
  
## <a name="syntax"></a>語法  
  
```
class recursive_timed_mutex;
```  
  
## <a name="members"></a>成員  
  
### <a name="public-constructors"></a>公用建構函式  
  
|名稱|描述|  
|----------|-----------------|  
|[recursive_timed_mutex](#recursive_timed_mutex)|建構未鎖定的 `recursive_timed_mutex` 物件。|  
|[~recursive_timed_mutex 解構函式](#dtorrecursive_timed_mutex_destructor)|釋出 `recursive_timed_mutex` 物件所使用的任何資源。|  
  
### <a name="public-methods"></a>公用方法  
  
|名稱|描述|  
|----------|-----------------|  
|[lock](#lock)|封鎖呼叫的執行緒，直到執行緒取得 `mutex` 的擁有權。|  
|[try_lock](#try_lock)|嘗試在不造成封鎖的情況下，取得 `mutex` 的擁有權。|  
|[try_lock_for](#try_lock_for)|嘗試取得所指定時間間隔內 `mutex` 的所有權。|  
|[try_lock_until](#try_lock_until)|嘗試取得所指定時間間隔之前 `mutex` 的所有權。|  
|[unlock](#unlock)|釋放 `mutex` 的擁有權。|  
  
## <a name="requirements"></a>需求  
 **標頭：** \<mutex >  
  
 **命名空間：** std  
  
##  <a name="lock"></a>  lock  
 封鎖呼叫的執行緒，直到執行緒取得 `mutex` 的擁有權。  
  
```cpp  
void lock();
```  
  
### <a name="remarks"></a>備註  
 如果呼叫執行緒已經擁有 `mutex`，方法會立即傳回，而先前的鎖定仍持續有效。  
  
##  <a name="recursive_timed_mutex"></a>  recursive_timed_mutex 建構函式  
 建構未鎖定的 `recursive_timed_mutex` 物件。  
  
```cpp  
recursive_timed_mutex();
```  
  
##  <a name="dtorrecursive_timed_mutex_destructor"></a>  ~recursive_timed_mutex 解構函式  
 釋放 `recursive_timed_mutex` 物件使用的所有資源。  
  
```cpp  
~recursive_timed_mutex();
```  
  
### <a name="remarks"></a>備註  
 如果執行解構函式時物件已鎖定，則行為是未定義的。  
  
##  <a name="try_lock"></a>  try_lock  
 嘗試在不造成封鎖的情況下，取得 `mutex` 的擁有權。  
  
```cpp  
bool try_lock() noexcept;
```  
  
### <a name="return-value"></a>傳回值  
 如果方法成功取得 `mutex` 的擁有權，或是呼叫執行緒已經擁有 `mutex`，即為 `true`，否則為 `false`。  
  
### <a name="remarks"></a>備註  
 如果呼叫執行緒已經擁有 `mutex`，函式會立即傳回 `true`，而先前的鎖定仍持續有效。  
  
##  <a name="try_lock_for"></a>  try_lock_for  
 嘗試在不造成封鎖的情況下，取得 `mutex` 的擁有權。  
  
```cpp  
template <class Rep, class Period>
bool try_lock_for(const chrono::duration<Rep, Period>& Rel_time);
```  
  
### <a name="parameters"></a>參數  
 `Rel_time`  
 [chrono::duration](../standard-library/duration-class.md) 物件，此物件會指定方法嘗試取得 `mutex` 擁有權的時間上限。  
  
### <a name="return-value"></a>傳回值  
 如果方法成功取得 `mutex` 的擁有權，或是呼叫執行緒已經擁有 `mutex`，即為 `true`，否則為 `false`。  
  
### <a name="remarks"></a>備註  
 如果呼叫執行緒已經擁有 `mutex`，方法會立即傳回 `true`，而先前的鎖定仍持續有效。  
  
##  <a name="try_lock_until"></a>  try_lock_until  
 嘗試在不造成封鎖的情況下，取得 `mutex` 的擁有權。  
  
```cpp  
template <class Clock, class Duration>
bool try_lock_for(const chrono::time_point<Clock, Duration>& Abs_time);

bool try_lock_until(const xtime* Abs_time);
```  
  
### <a name="parameters"></a>參數  
 `Abs_time`  
 這個時間點所指定的臨界值一超過，方法就不再嘗試取得 `mutex` 的擁有權。  
  
### <a name="return-value"></a>傳回值  
 如果方法成功取得 `mutex` 的擁有權，或是呼叫執行緒已經擁有 `mutex`，即為 `true`，否則為 `false`。  
  
### <a name="remarks"></a>備註  
 如果呼叫執行緒已經擁有 `mutex`，方法會立即傳回 `true`，而先前的鎖定仍持續有效。  
  
##  <a name="unlock"></a>  unlock  
 釋放 `mutex` 的擁有權。  
  
```cpp  
void unlock();
```  
  
### <a name="remarks"></a>備註  
 這個方法只會在呼叫它的次數與在 `recursive_timed_mutex` 物件上成功呼叫 [lock](#lock)、[try_lock](#try_lock)、[try_lock_for](#try_lock_for) 及 [try_lock_until](#try_lock_until) 的次數一樣多之後，才會釋放 `mutex` 的擁有權。  
  
 如果呼叫的執行緒未擁有 `mutex`，則行為是未定義的。  
  
## <a name="see-also"></a>請參閱  
 [標頭檔參考](../standard-library/cpp-standard-library-header-files.md)   
 [\<mutex>](../standard-library/mutex.md)


