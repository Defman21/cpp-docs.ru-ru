---
title: "omp_init_lock | Microsoft Docs"
ms.custom: ""
ms.date: "11/04/2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-cpp"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "omp_init_lock"
dev_langs: 
  - "C++"
helpviewer_keywords: 
  - "omp_init_lock OpenMP function"
ms.assetid: 7a65e3e2-2e31-4645-964c-c1e82e2a4d0e
caps.latest.revision: 15
author: "mikeblome"
ms.author: "mblome"
manager: "ghogen"
caps.handback.revision: 15
---
# omp_init_lock
[!INCLUDE[vs2017banner](../../../assembler/inline/includes/vs2017banner.md)]

Инициализирует простая блокировка.  
  
## Синтаксис  
  
```  
void omp_init_lock(  
   omp_lock_t *lock  
);  
```  
  
#### Параметры  
 `lock`  
 Переменная типа omp\_lock\_t.  
  
## Заметки  
 Дополнительные сведения см. в разделе [3.2.1 omp\_init\_lock and omp\_init\_nest\_lock Functions](../../../parallel/openmp/3-2-1-omp-init-lock-and-omp-init-nest-lock-functions.md).  
  
## Пример  
  
```  
// omp_init_lock.cpp  
// compile with: /openmp  
#include <stdio.h>  
#include <omp.h>  
  
omp_lock_t my_lock;  
  
int main() {  
   omp_init_lock(&my_lock);  
  
   #pragma omp parallel num_threads(4)  
   {  
      int tid = omp_get_thread_num( );  
      int i, j;  
  
      for (i = 0; i < 5; ++i) {  
         omp_set_lock(&my_lock);  
         printf_s("Thread %d - starting locked region\n", tid);  
         printf_s("Thread %d - ending locked region\n", tid);  
         omp_unset_lock(&my_lock);  
      }  
   }  
  
   omp_destroy_lock(&my_lock);  
}  
```  
  
  **0 \- Запуск блокированных поток области**  
**0 \- Область поток блокированных окончания**  
**0 \- Запуск блокированных поток области**  
**0 \- Область поток блокированных окончания**  
**0 \- Запуск блокированных поток области**  
**0 \- Область поток блокированных окончания**  
**0 \- Запуск блокированных поток области**  
**0 \- Область поток блокированных окончания**  
**0 \- Запуск блокированных поток области**  
**0 \- Область поток блокированных окончания**  
**1 \- Запуск блокированных поток области**  
**1 \- Область поток блокированных окончания**  
**1 \- Запуск блокированных поток области**  
**1 \- Область поток блокированных окончания**  
**1 \- Запуск блокированных поток области**  
**1 \- Область поток блокированных окончания**  
**1 \- Запуск блокированных поток области**  
**1 \- Область поток блокированных окончания**  
**1 \- Запуск блокированных поток области**  
**1 \- Область поток блокированных окончания**  
**2 \- Запуск блокированных поток области**  
**2 \- Область поток блокированных окончания**  
**2 \- Запуск блокированных поток области**  
**2 \- Область поток блокированных окончания**  
**2 \- Запуск блокированных поток области**  
**2 \- Область поток блокированных окончания**  
**2 \- Запуск блокированных поток области**  
**2 \- Область поток блокированных окончания**  
**2 \- Запуск блокированных поток области**  
**2 \- Область поток блокированных окончания**  
**3 \- Запуск блокированных поток области**  
**3 \- Область поток блокированных окончания**  
**3 \- Запуск блокированных поток области**  
**3 \- Область поток блокированных окончания**  
**3 \- Запуск блокированных поток области**  
**3 \- Область поток блокированных окончания**  
**3 \- Запуск блокированных поток области**  
**3 \- Область поток блокированных окончания**  
**3 \- Запуск блокированных поток области**  
**3 \- Область поток блокированных окончания**   
## См. также  
 [Functions](../../../parallel/openmp/reference/openmp-functions.md)