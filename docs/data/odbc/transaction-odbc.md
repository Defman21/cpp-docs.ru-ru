---
title: "Транзакция (ODBC) | Microsoft Docs"
ms.custom: ""
ms.date: "11/04/2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-cpp"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "C++"
helpviewer_keywords: 
  - "базы данных [C++], транзакции"
  - "ODBC [C++], транзакции"
  - "наборы записей ODBC [C++], транзакции"
  - "наборы записей ODBC [C++], обновление"
  - "наборы записей [C++], транзакции"
  - "наборы записей [C++], обновление"
  - "транзакции [C++], Классы MFC ODBC"
ms.assetid: a2ec0995-2029-45f2-8092-6efd6f2a77f4
caps.latest.revision: 8
author: "mikeblome"
ms.author: "mblome"
manager: "ghogen"
caps.handback.revision: 8
---
# Транзакция (ODBC)
[!INCLUDE[vs2017banner](../../assembler/inline/includes/vs2017banner.md)]

Данный раздел относится к классам ODBC библиотеки MFC.  
  
 Транзакция — это способ группировки, или создания пакета, последовательных обновлений [источника данных](../../data/odbc/data-source-odbc.md), которые завершаются одновременно или не завершаются при выполнении отката транзакции.  Если транзакция не используется, то изменения источника данных фиксируются автоматически, а не по требованию.  
  
> [!NOTE]
>  Не все драйверы базы данных ODBC поддерживают транзакции.  Для определения поддержки драйвером транзакции для определенной базы данных, необходимо вызвать функцию\-член `CanTransact` объекта класса [CDatabase](../../mfc/reference/cdatabase-class.md) или [CRecordset](../Topic/CRecordset%20Class.md).  Обратите внимание, что функция\-член `CanTransact` не предоставляет сведения о том, обеспечивает ли источник данных полную поддержку транзакции.  Кроме того, для проверки эффекта транзакции на открытом объекте `CRecordset` можно вызвать функции\-члены `CDatabase::GetCursorCommitBehavior` и `CDatabase::GetCursorRollbackBehavior` после вызова методов **CommitTrans** и **Rollback**.  
  
 Вызов функций\-членов `AddNew` и **Edit** объекта `CRecordset` немедленно отразиться на источнике данных при вызове метода **Update**.  При вызове метода **Delete** изменения вступают в силу немедленно.  Можно использовать транзакцию, состоящую из нескольких вызовов для `AddNew`, **Edit**, **Update** и **Delete**, которая будет выполнена, но не будет зафиксирована до тех пор, пока не будет явно вызван метод **CommitTrans**.  Устанавливая транзакцию, можно выполнить серию таких вызовов с сохранением возможности отката.  Если критический ресурс недоступен или какие\-то другие условия не позволяют зафиксировать всю транзакцию, то вместо фиксации транзакции ее можно откатить.  В результате отката ни одно изменение, принадлежащее транзакции, не повлияет на источник данных.  
  
> [!NOTE]
>  В настоящее время класс `CRecordset` не поддерживает обновления источника данных, если присутствует реализованная групповая выборка строк.  Это означает, что нельзя вызвать функции `AddNew`, **Edit**, **Delete** или **Update**.  Однако можно писать собственные функции для выполнения обновлений и последующего вызова данных функций в транзакции.  Дополнительные сведения о групповой выборке строк см. в разделе [Набор записей. Групповая выборка строк \(ODBC\)](../Topic/Recordset:%20Fetching%20Records%20in%20Bulk%20\(ODBC\).md).  
  
> [!NOTE]
>  Кроме того, изменяя набор записей, транзакции изменяют инструкции SQL, которые выполняются напрямую до тех пор, пока используется ODBC **HDBC**, связанный с объектом `CDatabase` или с ODBC **HSTMT**, основанном на **HDBC**.  
  
 Транзакции очень полезны, когда требуется одновременно обновить несколько записей.  В этом случае можно предотвратить частичное завершение транзакции, например, в случае возникновения исключения до выполнения последнего обновления.  Группировка обновлений в транзакцию позволяет восстановить \(откатить\) изменения и вернуть записи в состояние, в котором они находились до транзакции.  Например, если банк переводит деньги со счета А на счет В, то и операция отзыва денежных средств со счета А, и операция размещения их на счете B должны корректно обработать денежные средства, или вся транзакция должна закончиться откатом.  
  
 В классах баз данных транзакции реализуются с помощью объектов `CDatabase`.  Объект `CDatabase` представляет подключение к источнику данных, при котором один или более наборов записей сопоставляются с объектом `CDatabase`, работающим с таблицей базы данных через функции членов набора записей.  
  
> [!NOTE]
>  Поддерживается только один уровень транзакций.  Нельзя реализовать вложение транзакций и распространить транзакцию на несколько объектов базы данных.  
  
 В следующих разделах приведены дополнительные сведения о том, как осуществляется реализация транзакций.  
  
-   [Транзакции: выполнение транзакции в наборе записей \(ODBC\)](../../data/odbc/transaction-performing-a-transaction-in-a-recordset-odbc.md)  
  
-   [Транзакция. Влияние транзакций на обновления \(ODBC\)](../../data/odbc/transaction-how-transactions-affect-updates-odbc.md)  
  
## См. также  
 [Интерфейс ODBC \(ODBC\)](../Topic/Open%20Database%20Connectivity%20\(ODBC\).md)