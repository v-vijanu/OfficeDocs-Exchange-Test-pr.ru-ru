﻿---
title: 'Включение или отключение управления правами на доступ к данным для внутренних сообщений: Exchange 2013 Help'
TOCTitle: Включение или отключение управления правами на доступ к данным для внутренних сообщений
ms:assetid: a6a17f57-5304-41f1-954d-7301857d54a1
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/Bb124077(v=EXCHG.150)
ms:contentKeyID: 50488806
ms.date: 04/30/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Включение или отключение управления правами на доступ к данным для внутренних сообщений

 

_**Применимо к:** Exchange Server 2013_

_**Последнее изменение раздела:** 2012-10-12_

В Microsoft Exchange Server 2013 система управления правами на доступ к данным (IRM) по умолчанию включена для внутренних сообщений. Это позволяет создавать правила защиты транспорта и правила защиты Microsoft Outlook для сообщений с защитой IRM на клиентах транспорта, клиентах Microsoft Outlook 2010 и более поздних версий. Активация управления правами на доступ к данным для внутренних сообщений является предварительным условием для работы всех прочих функций в Exchange Server 2013, например расшифровки транспорта, расшифровки правила журнала, управления правами на доступ к данным в Microsoft Office Outlook Web App и управления правами на доступ к данным в Microsoft Exchange ActiveSync.

> [!CAUTION]  
> Отключение управления правами на доступ к данным для внутренних сообщений приведет к отключению всех функций управления правами на доступ к данным в организации Exchange. Клиентские функции IRM в Outlook (например, возможность чтения, ответа, пересылки и создания сообщений с защитой IRM с помощью сервера служб управления правами Active Directory (AD RMS)) не затрагиваются


Дополнительные сведения об управленческих задачах, связанных с IRM, см. в разделе [Сведения о процедуры управления правами](information-rights-management-procedures-exchange-2013-help.md).

## Что нужно знать перед началом работы?

  - Осталось времени до завершения: 1 минута.

  - Для выполнения этих процедур необходимы соответствующие разрешения. Сведения о необходимых разрешениях см. в статье Запись "Защита прав" в разделе [Политика обмена сообщениями и разрешения для соответствия требованиям](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Центр администрирования Exchange (EAC) нельзя использовать для включения или отключения функций IRM для внутренних сообщений. Необходимо использовать командную консоль.

  - Сочетания клавиш для процедур, описанных в этой статье, приведены в статье [Сочетания клавиш в Центре администрирования Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]  
> Возникли проблемы? Обратитесь за помощью к участникам форумов, посвященных Exchange. Посетите форумы по таким продуктам: <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> или <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Использование командной строки для включения управления правами на доступ к данным для внутренних сообщений

В этом примере выполняется активация управления правами на доступ к данным для внутренних сообщений организации Exchange.

    Set-IRMConfiguration -InternalLicensingEnabled $true

Дополнительные сведения о синтаксисе и параметрах см. в разделе [Set-IRMConfiguration](https://technet.microsoft.com/ru-ru/library/dd979792\(v=exchg.150\)).

## Использование командной строки для отключения управления правами на доступ к данным для внутренних сообщений

В этом примере выполняется отключение управления правами на доступ к данным для внутренних сообщений в организации Exchange.

    Set-IRMConfiguration -InternalLicensingEnabled $false

Дополнительные сведения о синтаксисе и параметрах см. в разделе [Set-IRMConfiguration](https://technet.microsoft.com/ru-ru/library/dd979792\(v=exchg.150\)).

## Как проверить, что все получилось?

Чтобы убедиться, что функции IRM включены или отключены для внутренних сообщений, проверьте конфигурацию с помощью командлета [Get-IRMConfiguration](https://technet.microsoft.com/ru-ru/library/dd776120\(v=exchg.150\)).
