﻿---
title: 'Настройка режима запуска на сервере почтовых ящиков: Exchange 2013 Help'
TOCTitle: Настройка режима запуска на сервере почтовых ящиков
ms:assetid: 4457d6a0-52bd-4269-8cb5-d34d7fe9bfc3
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/Ee423544(v=EXCHG.150)
ms:contentKeyID: 50556398
ms.date: 04/30/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Настройка режима запуска на сервере почтовых ящиков

 

_**Применимо к:** Exchange Server 2013, Exchange Server 2016_

_**Последнее изменение раздела:** 2013-02-15_

Вы можете указать режим запуска службы единой системы обмена сообщениями Microsoft Exchange на сервере почтовых ящиков. По умолчанию сервер почтовых ящиков запускается в режиме TCP, но при использовании протокола TLS (Transport Layer Security) для шифрования трафика VoIP необходимо настроить сервер почтовых ящиков на использование TLS или двойного режима. Серверы почтовых ящиков рекомендуется настраивать на использование двойного режима запуска. Это связано с тем, что серверы клиентского доступа и серверы почтовых ящиков могут отвечать на все входящие вызовы для всех абонентских групп единой системы обмена сообщениями, но эти группы могут иметь разные настройки безопасности (незащищенный режим, режим с защитой SIP или защищенный режим). После изменения режима запуска службу единой системы обмена сообщениями Microsoft Exchange необходимо перезапустить, чтобы изменение вступило в силу.

> [!IMPORTANT]  
> По умолчанию серверы почтовых ящиков доступны для ответа на входящие вызовы. Для обработки вызовов единой системы обмена сообщениями сервер почтовых ящиков необходимо добавлять в абонентскую группу данной системы, только если выполняется интеграция единой системы обмена сообщениями с Microsoft Office Communications Server 2007 R2 или Microsoft Lync Server.


Сведения о дополнительных задачах управления, связанных с единой системой обмена сообщениями и серверами почтовых ящиков, см. в разделе [Процедуры служб единой системы обмена СООБЩЕНИЯМИ](um-services-procedures-exchange-2013-help.md).

## Что нужно знать перед началом работы

  - Предполагаемое время для завершения: менее 1 минуты.

  - Для выполнения этих процедур необходимы соответствующие разрешения. Сведения о необходимых разрешениях см. в статье запись "Сервер почтовых ящиков (служба единой системы обмена сообщениями)" в разделе [Разрешения единой системы обмена сообщениями](unified-messaging-permissions-exchange-2013-help.md).

  - Убедитесь, что сервер почтовых ящиков установлен либо на том же компьютере, что и сервер клиентского доступа, либо на отдельном компьютере.

  - Сочетания клавиш для процедур, описанных в этой статье, приведены в статье [Сочетания клавиш в Центре администрирования Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]  
> Возникли проблемы? Обратитесь за помощью к участникам форумов, посвященных Exchange. Посетите форумы по таким продуктам: <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> или <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Что необходимо сделать?

## Использование EAC для настройки режима запуска на сервере почтовых ящиков

1.  В Центре администрирования Exchange перейдите к разделу **Серверы** \> **Серверы**.

2.  Выберите из списка сервер Exchange, который необходимо изменить, и нажмите кнопку **Изменить**![Значок редактирования](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Значок редактирования").

3.  На странице **Exchange Server** нажмите кнопку **Единая система обмена сообщениями**.

4.  В разделе **Параметры службы единой системы обмена сообщениями** \> **Режим запуска единой системы обмена сообщениями** выберите следующее в раскрывающемся списке:
    
      - **TCP**   Выберите этот параметр, если вы не используете mTLS и применяете только незащищенные абонентские группы.
    
      - **TLS**   Выберите этот параметр, если вы используете mTLS и применяете только абонентские группы с безопасным режимом или безопасным режимом SIP.
    
      - **DUAL**   Выберите этот параметр, если вы используете mTLS и применяете незащищенные абонентские группы, абонентские группы с безопасным режимом или безопасным режимом SIP.

5.  Выбрав режим запуска нажмите кнопку **Сохранить**.

## Использование командной консоли для настройки режима запуска на сервере почтовых ящиков

В этом примере устанавливается двойной режим запуска для сервера почтовых ящиков с именем `MyUMServer1`.

    Set-UMService -Identity MyUMServer1 -UMStartUpMode Dual

В этом примере устанавливается режим TLS запуска для сервера почтовых ящиков с именем `MyUMServer1`.

    Set-UMService -Identity MyUMServer1 -UMStartUpMode TLS
