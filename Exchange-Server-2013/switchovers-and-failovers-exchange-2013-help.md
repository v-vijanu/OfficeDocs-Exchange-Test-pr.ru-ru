﻿---
title: 'Переключения и отработки отказа: Exchange 2013 Help'
TOCTitle: Переключения и отработки отказа
ms:assetid: 75388645-cae1-402e-bf02-c4949d3e2c31
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/Dd298067(v=EXCHG.150)
ms:contentKeyID: 62523829
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Переключения и отработки отказа

 

_**Применимо к:** Exchange Server 2013 SP1_

_**Последнее изменение раздела:** 2015-12-02_

Переключения и отработки отказов — две формы отключений при сбоях в Microsoft Exchange Server 2013.

  - *Переключение* — это запланированное отключение базы данных или сервера, которое явным образом инициируется командлетом или управляемой системой доступности в Exchange 2013. Переключения обычно выполняются во время подготовки к обслуживанию. Переключения предполагают перемещение активной копии базы данных почтового ящика на другой сервер группы обеспечения доступности баз данных (DAG). Если при переключении не удается найти ни одной подходящей целевой базы данных, администратор получит уведомление об ошибке, а база данных почтового ящика не будет отключена.

  - *Отработка отказа* подразумевает неожиданные события, которые могут приводить к недоступности служб, данных или тех и других. Отработка отказа включает в себя автоматическое восстановление системы после сбоя путем активации пассивной копии базы данных почтового ящика и ее преобразования в активную. Если при отработке отказа не удается найти ни одной подходящей целевой базы данных, база данных почтового ящика будет отключена.

Exchange 2013 предназначен специально для обработки как переключений, так и отработок отказов.

Необходимы сведения о задачах управления, связанных с высоким уровнем доступности и устойчивостью сайтов к сбоям? См. раздел [Управление высокой доступностью и устойчивостью сайтов](managing-high-availability-and-site-resilience-exchange-2013-help.md).

## Переключения

В Exchange 2013 существует три типа переключений:

  - Переключения базы данных.

  - Переключения сервера.

  - Переключения центра данных.

## Переключения базы данных

*Переключение базы данных* — это процесс, в ходе которого одна активная база данных переключается на другую (пассивную) копию базы данных, которая затем становится новой активной копией базы данных. Переключения базы данных могут происходить как внутри центров данных, так и между ними. Переключение базы данных может выполняться с помощью Центра администрирования Exchange или командной консоли. Вне зависимости от используемого интерфейса, процесс переключения выполняется следующим образом.

1.  Администратор инициирует переключение базы данных, чтобы переместить текущую активную копию базы данных почтовых ящиков на другой сервер.

2.  Клиент, используемый при выполнении задачи, отправляет вызов RPC в службу репликации Microsoft Exchange участника группы доступности базы данных (DAG).

3.  Участник группы DAG может не выполнять обработку роли основного диспетчера Active Manager (PAM). В этом случае он переводит задачу на сервер, которому принадлежит роль PAM.

4.  В рамках этой задачи выполняется вызов RPC в службу репликации Microsoft Exchange сервера, которому принадлежит роль PAM.

5.  Диспетчер PAM считывает и обновляет сведения о местоположении базы данных, которые хранятся в базе данных кластера для группы доступности DAG.

6.  Диспетчер PAM подключается к службе репликации Microsoft Exchange участника группы DAG, пассивная копия которой активируется в качестве новой активной копии базы данных почтовых ящиков.

7.  Служба репликации Microsoft Exchange на целевом сервере отправляет запросы к службам репликации Microsoft Exchange всех участников группы DAG для определения наилучшего источника журнала копии базы данных.

8.  База данных отключается от текущего сервера, и служба репликации Microsoft Exchange на целевом сервере копирует оставшиеся журналы на целевой сервер.

9.  Служба репликации Microsoft Exchange на целевом сервере отправляет запросы о подключении базы данных.

10. Служба банка данных Microsoft Exchange на целевом сервере преобразует файлы журналов и подключает базу данных.

11. Коды ошибок возвращаются в службу репликации Microsoft Exchange на целевом сервере.

12. Диспетчер PAM обновляет сведения о состоянии копии базы данных в базе данных кластера для группы доступности DAG.

13. Служба репликации Microsoft Exchange на целевом сервере возвращает коды ошибок в службу репликации Microsoft Exchange диспетчера PAM.

14. Служба репликации Microsoft Exchange диспетчера PAM возвращает все ошибки на интерфейс администрирования, с которого выполнялся вызов задачи.

15. Приложение Remote PowerShell возвращает результаты операции на вызывающий интерфейс администрирования.

Дополнительные сведения о переключении базы данных см. в разделе [Активация копии базы данных почтовых ящиков](activate-a-mailbox-database-copy-exchange-2013-help.md).

## Переключения сервера

Переключение сервера — это процесс, в ходе которого все активные базы данных участника группы DAG активируются для одного или нескольких других участников этой группы. Как и переключения базы данных, переключение сервера выполняется внутри центров обработки данных и между ними, а также запускается с помощью консоли управления и Центра администрирования Exchange. Вне зависимости от используемого интерфейса, процесс переключения сервера выполняется следующим образом.

1.  Администратор инициирует переключение сервера, чтобы переместить все текущие активные копии базы данных почтовых ящиков на один или несколько других серверов.

2.  В рамках данной задачи для каждой активной базы данных на текущем сервере выполняются действия, описанные выше в этом разделе для переключений базы данных (шаги 2–4).

3.  Диспетчер PAM считывает и обновляет сведения о местоположении базы данных, которые хранятся в базе данных кластера для группы доступности DAG.

4.  Диспетчер PAM подключается к службе репликации Microsoft Exchange каждого участника группы DAG, для которого активируется пассивная копия.

5.  Служба репликации Microsoft Exchange на целевых серверах отправляет запросы к службам репликации Microsoft Exchange всех других участников группы DAG для определения наилучшего источника журнала копии базы данных.

6.  База данных отключается от текущего сервера, и служба репликации Microsoft Exchange на каждом целевом сервере копирует оставшиеся журналы.

7.  Служба репликации Microsoft Exchange на каждом целевом сервере отправляет запросы о подключении базы данных.

8.  Служба банка данных Microsoft Exchange на каждом целевом сервере преобразует файлы журналов и подключает базу данных.

9.  Коды ошибок возвращаются в службу репликации Microsoft Exchange на целевом сервере.

10. Диспетчер PAM обновляет сведения о состоянии копии базы данных в базе данных кластера для группы доступности DAG.

11. Служба репликации Microsoft Exchange на целевом сервере возвращает коды ошибок в службу репликации Microsoft Exchange диспетчера PAM.

12. Служба репликации Microsoft Exchange диспетчера PAM возвращает все ошибки на интерфейс администрирования, с которого выполнялся вызов задачи.

13. Приложение Remote PowerShell возвращает результаты операции на вызывающий интерфейс администрирования.

Дополнительные сведения о переключении сервера см. в разделе [Выполнение переключения сервера](perform-a-server-switchover-exchange-2013-help.md).

## Переключения центра данных

В конфигурации устойчивости сайта при возникновении сбоя в масштабе сайта может возникнуть автоматическое восстановление в группе обеспечения доступности баз данных (DAG). Это позволит системе обмена сообщениями сохранить работоспособное состояние. Для этой конфигурации требуется наличие как минимум трех расположений, поскольку она требует выполнить развертывание членов группы DAG в двух местах и следящего сервера DAG в третьем.

Если у вас нет трех расположений или, несмотря на их наличие, вы хотите управлять действиями по восстановлению на уровне центра обработки данных, можно настроить группу DAG для восстановления вручную в случае сбоя в масштабе сайта. В этом случае выполняется процесс под названием *переключение центра обработки данных*. Так же как и для многих сценариев аварийного восстановления, предварительное планирование и подготовка к переключению центра данных позволяют упростить процесс восстановления и сократить время отключения.

Из-за многочисленных изменений архитектуры в Exchange 2013, в том числе консолидации ролей сервера, переключение центра обработки данных в Exchange 2013 значительно проще, чем в Exchange 2010. Подробное описание действий по переключению центра обработки данных см. в разделе [Переключения центра обработки данных](datacenter-switchovers-exchange-2013-help.md).

## Отработки отказов

Отработка отказа — это процедура автоматической активации, которая может выполняться на уровне базы данных, сервера или центра обработки данных. Отработки отказов происходят в ответ на сбой, который оказал влияние на отдельную базу данных (например, потеря данных в изолированном хранилище), на весь сервер (например, сбой материнской платы или потеря питания) или на весь сайт (например, потеря всех членов группы DAG на сайте).

Группы доступности базы данных (DAG) и копии базы данных почтовых ящиков обеспечивают полную избыточность и быстрое восстановление как данных, так и служб, обеспечивающих доступ к этим данным. В следующей таблице указаны ожидаемые действия по восстановлению при различных сбоях. В одних случаях запустить процесс восстановления должен администратор, в других — ошибки автоматически обрабатываются системой.


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>Описание</th>
<th>Автоматическая активация</th>
<th>Автоматическое действие по восстановлению</th>
<th>Состояние при восстановлении: активная</th>
<th>Состояние при восстановлении: пассивная</th>
<th>Действия по восстановлению</th>
<th>Примечания</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>«Мягкий» сбой базы данных расширенного обработчика хранилищ (ESE): диски, на которых хранится база данных, возвращают ошибки при некоторых операциях чтения (например, ошибка -1018).</p></td>
<td><p>Возможное кратковременное отключение.</p>
<p>Возможная автоматическая отработка отказа.</p></td>
<td><p>Автоматическое исправление поврежденной страницы.</p></td>
<td><p>Ручное переключение, автоматическая отработка отказа или оперативное восстановление.</p></td>
<td><p>Сбой</p></td>
<td><p>Перестройка RAID, восстановление базы данных и копии базы данных, восстановление и запуск отладки, затем исправление страницы или исправление страницы на основе копии.</p></td>
<td><p>Могут возникать и другие &quot;мягкие&quot; ошибки базы данных.</p>
<p>Сюда не включены сбои блока файловой системы NTFS.</p>
<p>При переключении или отработке отказа выполняется обновление хост-сервера.</p></td>
</tr>
<tr class="even">
<td><p>&quot;<em>Полумягкий</em>&quot; сбой базы данных расширенного обработчика хранилищ (ESE): диски, на которых хранится база данных, возвращают ошибки при некоторых операциях записи.</p></td>
<td><p>Кратковременное отключение во время автоматической отработки отказа.</p></td>
<td><p>Автоматическое перестроение тома/диска после возможной замены диска.</p></td>
<td><p>Отключено, если отсутствует возможность восстановления.</p></td>
<td><p>Сбой</p></td>
<td><p>Перестроение с помощью RAID может решить проблему.</p>
<p>Копирование и исправление, восстановление и запуск отладки или перестроение тома/диска после возможной замены.</p></td>
<td><p>&quot;Полумягкая&quot; ошибка при операции записи обработчика ESE означает, что некоторые записи являются успешными.</p>
<p>Сюда не включен сбой блока файловой системы NTFS.</p></td>
</tr>
<tr class="odd">
<td><p>&quot;Полумягкий&quot; сбой журнала обработчика ESE: диски, на которых хранятся данные журнала, возвращают невосстановимые ошибки при некоторых операциях записи и чтения.</p></td>
<td><p>Кратковременное отключение во время автоматической отработки отказа.</p></td>
<td><p>Автоматическое перестроение тома/диска после возможной замены диска.</p></td>
<td><p>Отключено, если отсутствует возможность восстановления.</p></td>
<td><p>Сбой</p></td>
<td><p>Перестроение с помощью RAID может решить проблему.</p>
<p>Копирование и исправление, восстановление и запуск отладки или перестроение тома/диска после возможной замены.</p></td>
<td><p>&quot;Полумягкая&quot; ошибка чтения/записи обработчика ESE означает, что некоторые операции чтения/записи являются успешными.</p>
<p>При сбое базы данных автоматическое восстановление запускается до начала процесса восстановления данных журнала.</p></td>
</tr>
<tr class="even">
<td><p>Программная ошибка обработчика ESE или нехватка ресурсов: ошибка, при которой обработчик ESE завершает работу экземпляра (например, событие с идентификатором 1022, глубина контрольной точки слишком большая).</p></td>
<td><p>Кратковременное отключение во время автоматической отработки отказа.</p></td>
<td><p>Нет.</p></td>
<td><p>Отключено, если отсутствует возможность восстановления.</p></td>
<td><p>Сбой</p></td>
<td><p>Устранение ошибки базового ресурса.</p></td>
<td><p>Этот сбой может быть проявлением ошибок в других случаях.</p></td>
</tr>
<tr class="odd">
<td><p>Сбои блока NTFS: на дисках, содержащих базу данных или журналы, произошла ошибка операции чтения или записи в структуре управления NTFS.</p></td>
<td><p>Кратковременное отключение во время автоматической отработки отказа.</p></td>
<td><p>Полное перестроение тома после возможной замены диска.</p></td>
<td><p>Отключено, если отсутствует возможность восстановления.</p></td>
<td><p>Сбой</p></td>
<td><p>Перестроение с помощью RAID может решить проблему. Служебные программы NTFS могут решить проблемы в блоке NTFS. Возможно, потребуется восстановление Exchange.</p></td>
<td><p>Скорее всего, это может произойти, когда RAID не используется. Если это событие повлияет на активный том журнала, несколько последних файлов журнала будут утеряны.</p>
<p>Сюда не включены ошибки, автоматически исправленные системой NTFS либо ее базовым программным или аппаратным стеком.</p></td>
</tr>
<tr class="even">
<td><p>Сбой диска базы данных или журнала: на диске, содержащем базу данных или журналы, произошел полный отказ, и он недоступен.</p></td>
<td><p>Кратковременное отключение во время автоматической отработки отказа.</p></td>
<td><p>Диск переформатирован или заменен. Том полностью перестроен.</p></td>
<td><p>Отключено, если отсутствует возможность восстановления.</p></td>
<td><p>Сбой</p></td>
<td><p>Замена диска, возможно, с последующим перестроением RAID.</p>
<p>Замена диска с последующим полным перестроением тома.</p>
<p>Полное перестроение тома.</p></td>
<td><p>Неприменимо.</p></td>
</tr>
<tr class="odd">
<td><p>Сбой базы данных или тома журнала: произошел сбой тома из-за проблем в системе NTFS или на нижнем уровне тома.</p></td>
<td><p>Кратковременное отключение во время автоматической отработки отказа.</p></td>
<td><p>Диск переформатирован или заменен.</p></td>
<td><p>Отключено, если отсутствует возможность восстановления.</p></td>
<td><p>Сбой</p></td>
<td><p>Замена диска, возможно, с последующим перестроением RAID.</p>
<p>Замена диска с последующим полным перестроением тома.</p>
<p>Полное перестроение тома.</p></td>
<td><p>Неприменимо.</p></td>
</tr>
<tr class="even">
<td><p>Недостаточно места в базе данных или в томе журнала: недостаточно места в файловой системе NTFS, в которой находится база данных или файлы журнала.</p></td>
<td><p>Автоматическая обработка отказа, если другая копия находится в ином состоянии.</p></td>
<td><p>Нет.</p></td>
<td><p>Отключено.</p></td>
<td><p>Сбой</p></td>
<td><p>Запуск полной или добавочной архивации, удаление журнала вручную, ожидание завершения операции, возобновление копирования базы данных или восстановление поврежденной копии базы данных.</p></td>
<td><p>Неприменимо.</p></td>
</tr>
<tr class="odd">
<td><p>Администратор отключает неправильную базу данных.</p></td>
<td><p>Если автоматическая отработка отказа не заблокирована администратором, отключение будет кратковременным.</p>
<p>Если автоматическая отработка отказа запрещена, отключение будет продолжаться до тех пор, пока не будет подключена база данных.</p></td>
<td><p>Нет.</p></td>
<td><p>Отключено.</p></td>
<td><p>Неприменимо</p></td>
<td><p>Ошибку исправляет администратор.</p></td>
<td><p>Неприменимо.</p></td>
</tr>
<tr class="even">
<td><p>Администратор приостанавливает неправильную копию базы данных.</p></td>
<td><p>В зависимости от конфигурации и задействованной копии автоматическое восстановление может быть запрещено.</p></td>
<td><p>Нет.</p></td>
<td><p>Неприменимо.</p></td>
<td><p>Приостановка</p></td>
<td><p>Ошибку исправляет администратор.</p></td>
<td><p>Неприменимо.</p></td>
</tr>
<tr class="odd">
<td><p>Администратор отключает обслуживание базы данных хранилища, NTFS или тома.</p></td>
<td><p>Если автоматическая отработка отказа не заблокирована администратором, отключение будет кратковременным.</p>
<p>Если автоматическая отработка отказа заблокирована, отключение будет продолжаться до тех пор, пока администратор не завершит задачу.</p></td>
<td><p>Нет.</p></td>
<td><p>Отключено.</p></td>
<td><p>Неприменимо</p></td>
<td><p>Задачу завершает администратор.</p></td>
<td><p>Неприменимо.</p></td>
</tr>
<tr class="even">
<td><p>Администратор приостанавливает обслуживание копии базы данных хранилища, NTFS или тома.</p></td>
<td><p>В зависимости от конфигурации и задействованной копии автоматическое восстановление может быть запрещено.</p></td>
<td><p>Нет.</p></td>
<td><p>Неприменимо.</p></td>
<td><p>Приостановка</p></td>
<td><p>Действия завершает администратор.</p></td>
<td><p>Неприменимо.</p></td>
</tr>
<tr class="odd">
<td><p>Администратор отключает базу данных для обслуживания в автономном режиме.</p></td>
<td><p>Отключение до тех пор, пока не будет выполнено восстановление.</p></td>
<td><p>Нет.</p></td>
<td><p>Отключено.</p></td>
<td><p>Приостановка</p></td>
<td><p>Действия завершает администратор.</p></td>
<td><p>Активная и пассивная копии базы данных не совпадают.</p>
<p>Администратору необходимо приостановить копии.</p></td>
</tr>
<tr class="even">
<td><p>Сбой сети хранения данных (SAN), диска или контроллера хранилища.</p></td>
<td><p>Кратковременное отключение во время автоматической отработки отказа.</p></td>
<td><p>Нет.</p></td>
<td><p>Отключено.</p></td>
<td><p>Любое</p></td>
<td><p>Восстановление оборудования.</p></td>
<td><p>Пассивная копия базы данных будет находиться в состоянии, которое существовало во время сбоя системы.</p></td>
</tr>
<tr class="odd">
<td><p>Обслуживание оборудования сервера.</p></td>
<td><p>Кратковременное отключение во время автоматической отработки отказа (если не заблокировано администратором).</p></td>
<td><p>Нет.</p></td>
<td><p>Отключено.</p></td>
<td><p>Любое</p></td>
<td><p>Завершение действий.</p></td>
<td><p>Пассивная копия базы данных будет находиться в состоянии, которое существовало во время завершения работы системы.</p></td>
</tr>
<tr class="even">
<td><p>Обслуживание программного обеспечения сервера.</p></td>
<td><p>Кратковременное отключение во время автоматической отработки отказа (если не заблокировано администратором).</p></td>
<td><p>Нет.</p></td>
<td><p>Отключено.</p></td>
<td><p>Любое</p></td>
<td><p>Завершение действий.</p></td>
<td><p>Пассивная копия базы данных будет находиться в состоянии, которое существовало во время завершения работы системы.</p></td>
</tr>
<tr class="odd">
<td><p>Служба банка данных Microsoft Exchange остановлена или приостановлена администратором.</p></td>
<td><p>Кратковременное отключение во время автоматической отработки отказа.</p></td>
<td><p>Нет.</p></td>
<td><p>Отключено.</p></td>
<td><p>Любое</p></td>
<td><p>Перезапустите службу банка данных Microsoft Exchange.</p></td>
<td><p>Неприменимо.</p></td>
</tr>
<tr class="even">
<td><p>Сбой службы банка данных Microsoft Exchange. Операционная система по-прежнему работает.</p></td>
<td><p>Кратковременное отключение во время автоматической отработки отказа.</p></td>
<td><p>Диспетчер служб перезапускает службу банка данных Microsoft Exchange.</p></td>
<td><p>Отключено.</p></td>
<td><p>Любое</p></td>
<td><p>Перезапуск службы банка данных Microsoft Exchange вручную или автоматически.</p></td>
<td><p>Пассивная копия базы данных будет находиться в состоянии, которое существовало во время сбоя службы банка данных Microsoft Exchange.</p></td>
</tr>
<tr class="odd">
<td><p>Частичный отказ службы банка данных Microsoft Exchange. Часть хранилища Exchange прекращает функционировать, но это не считается полным отказом.</p></td>
<td><p>Возможное кратковременное отключение во время автоматической отработки отказа.</p></td>
<td><p>Нет.</p></td>
<td><p>Подключено и частично функционирует.</p></td>
<td><p>Любое, но, возможно, частично функционирующее</p></td>
<td><p>Перезагрузка сервера, перезапуск операционной системы или службы банка данных Microsoft Exchange.</p></td>
<td><p>Неприменимо.</p></td>
</tr>
<tr class="even">
<td><p>Сбой сервера. Сбой сервера по одной из следующих причин:</p>
<ul>
<li><p>Полный отказ питания</p></li>
<li><p>Невосстановимая поломка микросхемы процессора, материнской платы или объединительной платы</p></li>
<li><p>Ошибка остановки операционной системы</p></li>
<li><p>Операционная система не отвечает на запросы</p></li>
<li><p>Полный сбой связи</p></li>
</ul></td>
<td><p>Кратковременное отключение во время автоматической отработки отказа.</p></td>
<td><p>Перезагрузка компьютера.</p></td>
<td><p>Отключено.</p></td>
<td><p>Любое</p></td>
<td><p>Восстановление питания, изменение параметров операционной системы, изменение параметров оборудования, замена оборудования, перезапуск операционной системы, обслуживание операционной системы, обслуживание оборудования или устранение проблем связи.</p></td>
<td><p>Неприменимо.</p></td>
</tr>
<tr class="odd">
<td><p>Сбой кворума в группе доступности базы данных.</p></td>
<td><p>Отключение до тех пор, пока не будет выполнено восстановление.</p></td>
<td><p>Нет.</p></td>
<td><p>Отключено.</p></td>
<td><p>Любое</p></td>
<td><p>Восстановление неисправного кворума, назначение нового кворума или восстановление сети, ставшей причиной неисправности кворума.</p></td>
<td><p>Пассивная копия базы данных будет находиться в состоянии, которое существовало во время сбоя системы.</p></td>
</tr>
<tr class="even">
<td><p>Сбой связи в сети MAPI: сервер больше не доступен в сети MAPI.</p></td>
<td><p>Кратковременное отключение во время автоматической отработки отказа. Потерь данных быть не должно.</p></td>
<td><p>Нет. Попытки установки связи продолжают выполняться.</p></td>
<td><p>Отключено.</p></td>
<td><p>Любое</p></td>
<td><p>Устранение неполадки в оборудовании или программном обеспечении для решения проблемы связи.</p></td>
<td><p>Неприменимо.</p></td>
</tr>
<tr class="odd">
<td><p>Сбой связи в сети репликации: серверу не удается получить сигналы подтверждения, копии журнала или заполнение через поврежденную сеть репликации.</p></td>
<td><p>Возможно кратковременное отключение копирования или заполнения во время переключения нагрузки на другую сеть.</p></td>
<td><p>Нет. Попытки установки связи продолжают выполняться.</p></td>
<td><p>Нет.</p></td>
<td><p>Любое</p></td>
<td><p>Устранение неполадки в оборудовании или программном обеспечении для решения проблемы связи.</p></td>
<td><p>Сбой оказал влияние на устойчивость.</p></td>
</tr>
<tr class="even">
<td><p>Множественные ошибки сетевой связи: серверу не удается получить сигналы подтверждения, копии журнала или заполнение через несколько сетей.</p></td>
<td><p>Кратковременное отключение во время автоматической отработки отказа. Потерь данных быть не должно.</p></td>
<td><p>Нет. Попытки установки связи продолжают выполняться.</p></td>
<td><p>Отключено.</p></td>
<td><p>Любое</p></td>
<td><p>Устранение неполадки в оборудовании или программном обеспечении для решения проблемы связи.</p></td>
<td><p>По-прежнему работает по крайней мере дна сеть.</p></td>
</tr>
<tr class="odd">
<td><p>Частичный сбой одной или нескольких сетей: в сетях возникают ошибки с высокой скоростью.</p></td>
<td><p>Ошибка не обнаружена; никаких действий.</p></td>
<td><p>Нет.</p></td>
<td><p>Подключено, но возможны проблемы с производительностью.</p></td>
<td><p>Любое</p></td>
<td><p>Устранение неполадки в оборудовании или программном обеспечении для решения проблемы связи.</p></td>
<td><p>Скорости возникновения ошибок в сетях превышают обычные.</p></td>
</tr>
<tr class="even">
<td><p>Невыявленное зависание операционной системы: операционная система перестает отвечать на запросы, но это не выявлено системой мониторинга или кластеризации.</p></td>
<td><p>Нет.</p></td>
<td><p>Нет.</p></td>
<td><p>Любое.</p></td>
<td><p>Любое</p></td>
<td><p>Перезапуск или отключение неотвечающих ресурсов.</p></td>
<td><p>Зависание не выявлено, поэтому никакие действия не предпринимаются.</p>
<p>Возможно, некоторые функциональные возможности являются действующими.</p></td>
</tr>
<tr class="odd">
<td><p>Сбой диска с операционной системой.</p></td>
<td><p>Кратковременное отключение во время автоматической отработки отказа.</p></td>
<td><p>Нет.</p></td>
<td><p>Отключено.</p></td>
<td><p>Любое</p></td>
<td><p>Замена диска и перестроение сервера или перестроение тома с помощью RAID.</p></td>
<td><p>Неприменимо.</p></td>
</tr>
<tr class="even">
<td><p>Недостаточно места на диске с операционной системой.</p></td>
<td><p>Кратковременное отключение во время автоматической отработки отказа.</p></td>
<td><p>Нет.</p></td>
<td><p>Отключено.</p></td>
<td><p>Любое</p></td>
<td><p>Освобождение места в томе вручную.</p></td>
<td><p>Неприменимо.</p></td>
</tr>
<tr class="odd">
<td><p>На диске с двоичными файлами Exchange возникает сбой тома или диска.</p></td>
<td><p>Кратковременное отключение во время автоматической отработки отказа.</p></td>
<td><p>Нет.</p></td>
<td><p>Отключено.</p></td>
<td><p>Любое</p></td>
<td><p>Замена диска и переустановка приложения или перестроение тома с помощью RAID.</p></td>
<td><p>Неприменимо.</p></td>
</tr>
<tr class="even">
<td><p>Недостаточно места на диске с двоичными файлами Exchange.</p></td>
<td><p>Кратковременное отключение во время автоматической отработки отказа.</p></td>
<td><p>Нет.</p></td>
<td><p>Отключено.</p></td>
<td><p>Любое</p></td>
<td><p>Освобождение места в томе вручную.</p></td>
<td><p>Неприменимо.</p></td>
</tr>
<tr class="odd">
<td><p>Обнаружен недопустимый новый журнал: последовательность журнала прерывается существующим файлом.</p></td>
<td><p>Кратковременное отключение во время автоматической отработки отказа; возможно, с другими копиями не возникло такой проблемы.</p></td>
<td><p>Нет.</p></td>
<td><p>Отключено.</p></td>
<td><p>Сбой</p></td>
<td><p>Удаление аварийных журналов после определения источника.</p></td>
<td><p>Не следует реплицировать аварийные журналы.</p></td>
</tr>
<tr class="even">
<td><p>При непрерывной репликации обнаружен недопустимый журнал: при преобразовании обнаружен несоответствующий журнал во время операции копирования или преобразования.</p></td>
<td><p>Неприменимо.</p></td>
<td><p>Удаление журнала.</p></td>
<td><p>Неприменимо.</p></td>
<td><p>Сбой</p></td>
<td><p>Удаление недопустимого журнала; перемещение потока журналов, оказывающих негативное воздействие.</p></td>
<td><p>Неприменимо.</p></td>
</tr>
</tbody>
</table>


## Отработки отказов в базах данных

Отработка отказа в базах данных происходит, когда активная копия базы данных больше не может оставаться активной. Как часть отработки отказа в базах данных выполняются следующие действия:

1.  Служба банка данных Microsoft Exchange обнаруживает сбой в базе данных.

2.  Служба банка данных Microsoft Exchange записывает сбои в журнал событий канала crimson.

3.  Диспетчер Active Manager на сервере, на котором находится неисправная база данных, обнаруживает события сбоя.

4.  Диспетчер Active Manager запрашивает сведения о состоянии копии базы данных у других серверов, на которых хранится копия базы данных.

5.  Другие серверы возвращают диспетчеру Active Manager запрошенные сведения о состоянии копии базы данных.

6.  PAM инициирует перемещение активной базы данных на другой сервер в группе DAG с использованием процесса выбора лучших копий.

7.  Диспетчер PAM обновляет местоположение подключения базы данных в базе данных кластера для обращения к выбранному серверу.

8.  Диспетчер PAM отправляет запрос диспетчеру Active Manager на выбранном сервере о его назначении главным сервером для этой базы данных.

9.  Диспетчер Active Manager на выбранном сервере отправляет запрос в службу репликации Microsoft Exchange на создание копии последних журналов с предыдущего сервера и устанавливает флажок подключения для этой базы данных.

10. Служба репликации Microsoft Exchange копирует журналы с сервера, на котором ранее находилась активная копия базы данных.

11. Диспетчер Active Manager считывает номер последней версии журнала из базы данных кластера.

12. Служба банка данных Microsoft Exchange подключает новую активную копию базы данных.

## Отработки отказов на серверах

Отработка отказа на сервере происходит, если участник группы DAG больше не может обслуживать сеть MAPI или служба кластеров участника группы DAG больше не может поддерживать связь с оставшимися участниками этой группы. Как часть отработки отказа на сервере выполняются следующие действия.

1.  Служба кластеров диспетчера PAM отправляет уведомление этому диспетчеру в одном из двух случаев:
    
    1.  **Узел отключен**. Сервер доступен, но не может принимать участие в операциях группы DAG.
    
    2.  **Сеть MAPI отключена**. К серверу невозможно подключиться по сети MAPI, и поэтому сервер не может принимать участие в операциях группы DAG.

2.  Если сервер доступен, диспетчер PAM подключается к диспетчеру Active Manager на поврежденном сервере и запрашивает немедленное отключение всех баз данных.

3.  Для каждой поврежденной копии базы данных выполняется следующее:
    
    1.  Диспетчер PAM запрашивает сведения о состоянии копии базы данных у всех серверов в группе DAG.
    
    2.  Диспетчер PAM получает ответ от всех доступных и активных участников группы DAG.
    
    3.  Диспетчер PAM пытается определить наилучший источник журнала на всех отвечающих серверах, запрашивая у каждого номер последней версии журнала.
    
    4.  Каждый сервер сообщает в ответ номер версии журнала.

4.  Диспетчер PAM извлекает текущее состояние каталога индекса поиска из базы данных кластера.

5.  На основе номера версии журнала и работоспособности каталога каждой копии базы данных диспетчер PAM выбирает лучшие копии для активации.

6.  Диспетчер PAM обновляет подключенное местоположение базы данных в базе данных кластера.

7.  Диспетчер PAM инициирует отработку отказа в базе данных, связываясь с диспетчером Active Manager на одном или нескольких серверах.

8.  Диспетчер Active Manager на выбранных серверах запрашивает службу репликации Microsoft Exchange на копирование последних журналов с предыдущего сервера и установку флажка подключения.

9.  Если база данных является подключаемой, диспетчер Active Manager на серверах подключает базы данных.

Дополнительные сведения о процессе выбора лучших копий диспетчером Active Manager см. в разделе [Активный диспетчер](active-manager-exchange-2013-help.md).

## Отработки отказа в центрах обработки данных

В Exchange 2013 внесены значительные изменения, призванные устранить проблемы, связанные с конфигурацией устойчивости сайтов Exchange 2010. Благодаря упрощению пространства имен, консолидации ролей сервера, разделению массива серверов клиентского доступа, восстановлению группы обеспечения доступности баз данных (в Exchange 2013 пространство имен не требуется перемещать вместе с DAG) и изменению подсистемы балансировки нагрузки Exchange 2013 предоставляет новые параметры устойчивости сайта, например возможность использования единого глобального пространства имен. Кроме того, при наличии более двух расположений для развертывания компонентов системы обмена сообщениями Exchange 2013 также предоставляет возможность настроить систему обмена сообщениями для автоматической отработки отказа в ответ на сбои, которые требовали ручного вмешательства в Exchange 2010.

В Exchange 2013 была упрощена работа с устойчивостью сайта. Exchange использует отказоустойчивость, встроенную в пространство имен через несколько IP-адресов, распределения нагрузки (и в случае необходимости, возможность введения серверов в эксплуатацию и их выведения из эксплуатации). Одно из самых значительных изменений в Exchange 2013 — использование возможности клиентов производить кэширование нескольких IP-адресов, возвращенных из DNS-сервера, в ответ на запрос на разрешение имен. Если клиент имеет возможность кэшировать несколько IP-адресов (как почти все клиенты HTTP, но поскольку почти все протоколы клиентского доступа в Exchange 2013 основаны на HTTP (Outlook, мобильный Outlook, EAS, EWS, OWA, EAC, RPS и т. д.), во всех поддерживаемых клиентах HTTP есть возможность использовать различные IP-адреса), то отработка отказа возможна на стороне клиента. Можно настроить DNS на передачу клиенту нескольких IP-адресов во время разрешения имен. Например, клиент запрашивает адрес mail.contoso.com и получает два IP-адреса или четыре IP-адреса. Клиент будет использовать несколько полученных IP-адресов. Это упрощает работу клиента, поскольку если один из IP-адресов не работает, клиент имеет несколько других вариантов подключения. Если клиент пробует один адрес и тот не работает, клиент ждет 20 секунд, а затем пробует следующий адрес в списке. Таким образом, при потере подключения к основному массиву CAS и наличии второго опубликованного IP-адреса для второго массива CAS выполняется автоматическое восстановление клиентов (приблизительно через 21 секунду).

Современные клиенты HTTP (операционные системы и веб-браузеры возрастом не более десяти лет) используют такую избыточность автоматически. Стек HTTP может принимать несколько IP-адресов для полного доменного имени, и если невозможно подключиться с помощью первого IP-адреса, система использует следующий IP-адрес в списке. При мягком отказе (потере соединения после установки сеанса, возможно, вследствие прерывистого сбоя службы, например если устройство сбрасывает пакеты и нуждается в снятии с эксплуатации) может понадобиться обновить браузер.

При правильной конфигурации отработка отказа происходит на уровне клиента, и клиенты автоматически перенаправляются на второй центр обработки данных, где есть рабочие серверы клиентского доступа, а они перенаправляют связь обратно на сервер почтовых ящиков пользователя, который остается нетронутым сбоем (потому что переключение не производится). Вместо того чтобы восстанавливать службу вручную, она восстанавливается сама, а вы можете сосредоточиться на решении основной проблемы (например, на замене вышедшей из строя подсистемы балансировки нагрузки).

Благодаря быстрой отработке отказа пространства имен между центрами обработки данных все, что требуется для отработки отказа центра обработки данных, — механизм отработки отказа роли сервера почтовых ящиков в центрах обработки данных. Для автоматической отработки отказа для группы DAG необходимо просто разработать решение, при котором группа равномерно распределяется между двумя центрами обработки данных, а затем разместить следящий сервер в третьем расположении для его арбитража членами группы DAG в каждом центре обработки данных (вне зависимости от состояния сети между центрами обработки данных с членами этой группы). Очень важно то, что третье расположение изолированно от сетевых сбоев, влияющих на расположения с членами группы DAG.

Если у вас всего два центра обработки данных и вы хотите настроить автоматический отработку отказа, можно использовать Microsoft Azure в качестве третьего расположения. Вам потребуется создать виртуальную сеть Azure и подключить ее к двум центрам обработки данных с помощью виртуальной частной сети из нескольких точек. Затем вы сможете разместить следящий сервер на виртуальной машине Microsoft Azure. Дополнительные сведения см. в статье [Использование виртуальной машины Microsoft Azure в качестве следящего сервера DAG](using-a-microsoft-azure-vm-as-a-dag-witness-server-exchange-2013-help.md).
