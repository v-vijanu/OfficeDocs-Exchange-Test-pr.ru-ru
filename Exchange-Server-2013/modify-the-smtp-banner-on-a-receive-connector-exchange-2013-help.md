﻿---
title: 'Изменение заголовка SMTP в соединителе получения: Exchange 2013 Help'
TOCTitle: Изменение заголовка SMTP в соединителе получения
ms:assetid: d667704e-fd69-4aca-9c35-eef7006944b2
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/Bb124740(v=EXCHG.150)
ms:contentKeyID: 52061269
ms.date: 04/30/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Изменение заголовка SMTP в соединителе получения

 

_**Применимо к:** Exchange Server 2013_

_**Последнее изменение раздела:** 2015-04-08_

*Заголовок SMTP* — это ответ на подключение SMTP, который получает удаленный SMTP-сервер обмена сообщениями после подключения к соединителю получения, настроенному на компьютере, на котором выполняется Microsoft Exchange Server 2013.

Ниже представлен ответ по умолчанию, полученный удаленным SMTP-сервером обмена сообщениями после подключения к соединителю получения.

    220 <Servername> Microsoft ESMTP MAIL service ready at <RegionalDay-Date-24HourTimeFormat> <RegionalTimeZoneOffset>

При указании пользовательского значения для заголовка SMTP на соединителе получения удаленный сервер обмена сообщениями SMTP, подключенный к этому соединителю, получит приведенный ниже ответ.

    220 <Banner Text>

Может потребоваться изменение заголовка SMTP для соединителей получения SMTP с выходом в Интернет во избежание раскрытия имение и программного обеспечения сервера обмена сообщениями в заголовке SMTP.

## Что нужно знать перед началом работы

  - Предполагаемое время для завершения: 5 минут.

  - Для выполнения этих процедур необходимы соответствующие разрешения. Сведения о необходимых разрешениях см. в статье Запись "Соединители получения" в разделе [Разрешения потока обработки почты](mail-flow-permissions-exchange-2013-help.md).

  - Для выполнения этой процедуры можно использовать только командную консоль.

  - Замещающая текстовая строка заголовка SMTP всегда должна начинаться с `220`. Как определено в RFC 2821, ответа SMTP "Служба готова" по умолчанию имеет код 220.

  - Сочетания клавиш для процедур, описанных в этой статье, приведены в статье [Сочетания клавиш в Центре администрирования Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]  
> Возникли проблемы? Обратитесь за помощью к участникам форумов, посвященных Exchange. Посетите форумы по таким продуктам: <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> или <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Использование командной консоли для изменения заголовка SMTP на соединителе получения

Выполните следующую команду:

    Set-ReceiveConnector <ConnectorIdentity> -Banner "220 <Banner Text>"

В этом примере выполняется изменение заголовка SMTP на существующем соединителе получения с именем "Из Интернета". В заголовке SMTP отображается `220 Contoso Corporation`.

    Set-ReceiveConnector "From the Internet" -Banner "220 Contoso Corporation"

В этом примере удаляется пользовательский заголовок SMTP на соединителе получения с именем "Из Интернета", который восстанавливает значение заголовка SMTP по умолчанию.

    Set-ReceiveConnector "From the Internet" -Banner $null

## Как проверить, что все получилось?

Чтобы убедиться в том, что вы успешно изменили заголовок SMTP на соединителе получения, выполните указанные ниже действия.

1.  Откройте клиент Telnet на компьютере, который может получить доступ к соединителю получения, и выполните следующую команду:
    
        open <Connector FQDN or IP address> <Port>

2.  Убедитесь, что ответ от соединителя получения содержит заданный заголовок SMTP.

Обратите внимание, что данная процедура работает только на соединителях получения, которые разрешают анонимную или обычную проверку подлинности. Подробнее см. в разделе [Тестирование связи по протоколу SMTP с помощью Telnet](use-telnet-to-test-smtp-communication-exchange-2013-help.md).

