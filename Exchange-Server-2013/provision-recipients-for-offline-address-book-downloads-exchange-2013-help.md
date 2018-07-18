﻿---
title: 'Подготовка получателей для загрузки автономных адресных книг: Exchange 2013 Help'
TOCTitle: Подготовка получателей для загрузки автономных адресных книг
ms:assetid: 141751ac-16d3-4e3c-b70c-004aeedcb5a0
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/Aa996345(v=EXCHG.150)
ms:contentKeyID: 50487491
ms.date: 04/30/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Подготовка получателей для загрузки автономных адресных книг

 

_**Применимо к:** Exchange Online, Exchange Server 2013_

_**Последнее изменение раздела:** 2013-02-15_

При использовании нескольких автономных адресных книг в организации существует несколько способов настройки доступа различных получателей к загрузке автономных адресных книг.

  - **Для каждой базы данных почтовых ящиков** Можно использовать Центр администрирования Exchange или командную консоль, чтобы подготовить получателей для загрузок автономной адресной книги, связав базу данных почтовых ящиков с автономной адресной книгой по умолчанию для клиентов Office Outlook 2007, Outlook 2010 и Outlook 2013.

  - **Для каждого получателя**   Можно использовать командлет **Set-Mailbox** в командной консоли Exchange для указания автономной адресной книги, которую пользователи смогут загружать с помощью привязки автономной адресной книги непосредственно к почтовому ящику получателя.

  - **По нескольким получателям**   С помощью конвейерной команды в командной консоли Exchange можно указать автономную адресную книгу, которую могут загружать несколько получателей, на основе общих атрибутов.

  - **Для каждой политики адресной книги**   Можно назначить политику адресной книги для учетной записи пользователя почтового ящика, чтобы указать автономную адресную книгу, которая должна загружаться в почтовый ящик получателя. В случае назначения политики адресных книг учетной записи пользователя, которой уже назначена автономная адресная книга, такая автономная адресная книга, явным образом присвоенная почтовому ящику, имеет приоритет. Подробнее см. в разделе [Назначение политики адресной книги пользователям почты](assign-an-address-book-policy-to-mail-users-exchange-2013-help.md).

Дополнительные задачи управления, связанные с автономными адресными книгами (OAB), см. в разделе [Процедуры автономной адресной книги](offline-address-book-procedures-exchange-2013-help.md).

## Что нужно знать перед началом работы

  - Предполагаемое время для завершения каждой процедуры: 5 минут.

  - Для выполнения этих процедур нельзя использовать Центр администрирования Exchange. Необходимо использовать командную консоль.

  - Сочетания клавиш для процедур, описанных в этой статье, приведены в статье [Сочетания клавиш в Центре администрирования Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]  
> Возникли проблемы? Обратитесь за помощью к участникам форумов, посвященных Exchange. Посетите форумы по таким продуктам: <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> или <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Что необходимо сделать?

## Используйте командную консоль, чтобы подготовить получателей к загрузке автономной адресной книги, связав их базу данных почтовых ящиков с базой данных общедоступных папок или автономной адресной книгой по умолчанию.

Для выполнения этих процедур необходимы соответствующие разрешения. Сведения о необходимых разрешениях см. в статье Запись "Базы данных почтовых ящиков" в разделе [Разрешения получателей](recipients-permissions-exchange-2013-help.md).

В данном примере задается распространение через Интернет автономной адресной книги с именем "Моя автономная адресная книга" для базы данных почтовых ящиков по умолчанию.

    Set-MailboxDatabase -Identity "Mailbox Database" -OfflineAddressBook "My OAB"

Подробные сведения о синтаксисе и параметрах см. в разделе [Set-MailboxDatabase](https://technet.microsoft.com/ru-ru/library/bb123971\(v=exchg.150\)).

## Использование командной консоли Exchange для указания автономной адресной книги, которую пользователи смогут загружать с помощью привязки автономной адресной книги непосредственно к почтовому ящику получателя

Для выполнения этих процедур необходимы соответствующие разрешения. Сведения о необходимых разрешениях см. в статье Раздел "Разрешения подготовки получателей" в статье [Разрешения получателей](recipients-permissions-exchange-2013-help.md).

Чтобы указать автономную адресную книгу, которую пользователи смогут загружать с помощью привязки автономной адресной книги непосредственно к почтовому ящику получателя, введите команду в следующем формате.

    Set-Mailbox -Identity <MailboxIDParameter> -OfflineAddressBook <OfflineAddressBookIdParameter>

> [!NOTE]  
> Параметр <em>Identity</em> определяет почтовый ящик и может иметь следующие значения: идентификатор GUID, ADObjectID, различающееся имя (DN), <em>domain\account</em>, имя участника-пользователя (UPN), LegacyExchangeDN, SmtpAddress и псевдоним.


В этом примере показано, как разрешить пользователю Костерина загружать автономную адресную книгу с именем "Моя автономная адресная книга".

    Set-Mailbox -Identity Kim -OfflineAddressBook "My OAB"

Подробные сведения о синтаксисе и параметрах см. в разделе [Set-Mailbox](https://technet.microsoft.com/ru-ru/library/bb123981\(v=exchg.150\)).

## Использование командной консоли Exchange для указания автономной адресной книги, которую могут загружать несколько получателей

Для выполнения этих процедур необходимы соответствующие разрешения. Сведения о необходимых разрешениях см. в статье Тема «Разрешения подготовки получателей» в разделе [Разрешения получателей](recipients-permissions-exchange-2013-help.md).

В данном примере указано, что все почтовые ящики пользователей в США для компании Contoso загрузят автономную адресную книгу Contoso для США.

    Get-User -ResultSize Unlimited -Filter { Company -eq "Contoso" -and RecipientType -eq "UserMailbox" } | Where { $_.CountryOrRegion -eq "United States"} | Set-Mailbox -OfflineAddressBook "Contoso United States"

Дополнительные сведения о синтаксисе и параметрах см. в разделах [Get-User](https://technet.microsoft.com/ru-ru/library/aa996896\(v=exchg.150\)) и [Set-Mailbox](https://technet.microsoft.com/ru-ru/library/bb123981\(v=exchg.150\)).
