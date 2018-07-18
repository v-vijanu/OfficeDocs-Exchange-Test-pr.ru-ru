﻿---
title: 'Параметры преобразования TNEF: Exchange 2013 Help'
TOCTitle: Параметры преобразования TNEF
ms:assetid: 989a62fc-4bc1-448f-90c8-7c7b56fe1084
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/Bb310786(v=EXCHG.150)
ms:contentKeyID: 52059161
ms.date: 04/30/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Параметры преобразования TNEF

 

_**Применимо к:** Exchange Online, Exchange Server 2013_

_**Последнее изменение раздела:** 2015-03-09_

Можно указать, необходимо ли сохранять или удалять формат TNEF из сообщений, покидающих организацию Exchange. Формат TNEF, также известный как формат RTF Outlook или формат RTF Exchange, является специфическим форматом Майкрософт для инкапсулирования свойств сообщений MAPI. Все версии МайкрософтOutlook полностью поддерживают формат TNEF. Outlook Web App преобразует TNEF в формат MAPI и отображает отформатированные сообщения. Однако другие почтовые клиенты, которые не понимают формат TNEF, обычно отображают сообщения в формате TNEF как обычные текстовые сообщения с вложениями Winmail.dat или Win.dat.

**Содержание**

Параметры преобразования формата TNEF для удаленных доменов

Параметры преобразования TNEF для пользователей почты и почтовых контактов

Параметры преобразования TNEF в Outlook

Приоритеты параметров преобразования TNEF

## Параметры преобразования формата TNEF для удаленных доменов

При настройке параметров преобразования TNEF для удаленного домена эти параметры применяются ко всем сообщениям, отправленным в этот домен.

  - Для выделенной службы Exchange Online необходимо использовать Центр администрирования Exchange (EAC), чтобы задать параметры преобразования формата TNEF для удаленного домена в разделе **Поток почты** \> **Удаленные домены** \> **Изменить** (![Значок редактирования](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Значок редактирования")) \> **Использовать формат RTF Exchange**.

  - Для Exchange Online и Exchange 2013 используйте параметр *TnefEnabled* на командлете **Set-RemoteDomain**, чтобы настроить параметры преобразования формата TNEF для удаленного домена.

Для удаленных доменов в организации имеются следующие параметры конфигурации для преобразования TNEF.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Параметр</th>
<th>В Центре администрирования Exchange</th>
<th>В командной консоли</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Использовать формат TNEF для всех сообщений, отправляемых в удаленный домен.</p></td>
<td><p><strong>Постоянно</strong></p></td>
<td><p><code>$true</code></p></td>
</tr>
<tr class="even">
<td><p>Не использовать формат TNEF для всех сообщений, отправляемых в удаленный домен.</p></td>
<td><p><strong>Никогда</strong></p></td>
<td><p><code>$false</code></p></td>
</tr>
<tr class="odd">
<td><p>Сообщения TNEF для получателей в удаленном домене явно не разрешаются и явно не запрещаются. То, посылаются ли сообщения TNEF получателям в удаленном домене, зависит от определенной настройки почтового контакта или пользователя или от параметра, заданного отправителем в Outlook. Это значение по умолчанию.</p></td>
<td><p><strong>Использовать параметры пользователя</strong></p></td>
<td><p><code>$null</code> (пусто)</p></td>
</tr>
</tbody>
</table>


Дополнительные сведения об удаленных доменах см. в разделе [Удаленные домены](remote-domains-exchange-2013-help.md) или [Удаленные домены в Exchange Online](https://technet.microsoft.com/ru-ru/library/jj966211\(v=exchg.150\)).

В начало

## Параметры преобразования TNEF для пользователей почты и почтовых контактов

При настройке параметров преобразования TNEF для почтового контакта или почтового пользователя эти параметры применяются ко всем сообщениям, отправленным определенному получателю. Используйте параметр *UseMapiRichTextFormat* на командлетах **Set-MailUser** и **Set-MailContact**, чтобы настроить параметры преобразования TNEF для почтовых пользователей и почтовых контактов.

Для почтовых контактов и почтовых пользователей в организации имеются следующие параметры конфигурации для преобразования TNEF.

  - **Всегда**   TNEF используется для всех сообщений, отправленных получателю. Соответствующим значением для параметра *UseMapiRichTextFormat* является `Always`.

  - **Никогда**   TNEF никогда не используется для сообщений, отправленных получателю. Соответствующим значением для параметра *UseMapiRichTextFormat* является `Never`.

  - **Использовать параметры по умолчанию**   Сообщения TNEF для почтовых пользователей или почтовых контактов явно не разрешаются и не запрещаются. То, посылаются ли сообщения TNEF получателям в удаленном домене, зависит от соответствующего удаленного домена или от параметра, заданного отправителем в Outlook. Соответствующим значением для параметра *UseMapiRichTextFormat* является `UseDefaultSettings`. Это параметр по умолчанию.

В начало

## Параметры преобразования TNEF в Outlook

Отправители могут управлять параметрами преобразования сообщений в формате TNEF по умолчанию для сообщений TNEF, отправленных всем получателям за пределами организации Exchange. Такие параметры называются параметрами *формата сообщений Интернета*. Они применяются только к удаленным получателям, а не к получателям в организации Exchange.

> [!NOTE]  
> Следующие параметры определяют, как обрабатываются сообщения в формате Outlook RTF при отправке внешним получателям. Если используемым форматом сообщения является HTML или обычный текст, эти параметры не применяются.


В Outlook имеются следующие параметры преобразования TNEF.

  - **Преобразовать в формат HTML**.   Это значение используется по умолчанию. Все сообщения TNEF, отправляемые удаленным получателям, преобразуются в HTML. Форматирование сообщения должно быть аналогично форматированию исходного сообщения. Сообщения HTML с кодировкой MIME поддерживаются многими (но не всеми) клиентами электронной почты.

  - **Преобразовать в обычный текст**.   Все сообщения TNEF, отправляемые удаленным получателям, преобразуются в обычный текст. Форматирование сообщения теряется.

  - **Отправить, используя формат RTF**.   Все сообщения TNEF, отправляемые удаленным получателям, сохраняют формат TNEF.

В Outlook настройку этих параметров можно выполнить в следующих расположениях.

  - **Outlook 2010 или Outlook 2013** **Файл** \> **Параметры** \> **Почта** \> **Формат сообщений**.

  - **Outlook 2007** **Инструменты** \> **Параметры** \> **Формат почты** \> **Формат для Интернета**.

Отправители могут управлять параметрами преобразования сообщений в формате TNEF по умолчанию для сообщений TNEF, отправленных определенным получателям за пределами организации Exchange. Такие параметры называются параметрами *формата сообщений для получателей из Интернета*. Они применяются только к удаленным получателям, хранящимся в папке "Контакты", а не к получателям в организации Exchange. В папке "Контакты" для удаленных получателей имеются следующие параметры преобразования TNEF.

  - **Outlook выбирает наилучший формат отправки**.   Это значение используется по умолчанию. При выборе этого параметра Outlook использует параметр преобразования TNEF, заданный форматом для Интернета по умолчанию. Доступны следующие значения: **Преобразовать в формат HTML**, **Преобразовать в обычный текст** и **Отправить, используя формат RTF**. Таким образом, сообщение TNEF может сохранить этот формат либо быть преобразовано в HTML или обычный текст. Чтобы гарантировать сохранение формата сообщений TNEF для этого получателя, вместо параметра **Outlook выбирает наилучший формат отправки** следует выбрать **Отправить, используя формат RTF**.

  - **Отправка только обычным текстом**.   Все сообщения TNEF, отправляемые получателю, преобразуются в обычный текст. Форматирование сообщения теряется.

  - **Отправить, используя формат RTF**.   Все сообщения TNEF, отправляемые удаленным получателям, сохраняют формат TNEF.

В Outlook настройку этих параметров для контакта можно выполнить в следующих расположениях.

  - **Outlook 2010 или Outlook 2013**   Откройте карточку контакта, дважды щелкните адрес электронной почты, нажмите значок **Просмотр дополнительных параметров взаимодействия с данным пользователем** и выберите **Свойства Outlook**. В диалоговом окне **Свойства электронной почты** выберите **Формат для Интернета**.

  - **Outlook 2007**   Откройте карточку контакта, дважды щелкните поле **Электронная почта** и выберите **Формат для Интернета**.

В начало

## Приоритеты параметров преобразования TNEF

В следующем списке описаны приоритеты, которые используются Exchange для определения параметров преобразования TNEF исходящих сообщений, отправленных получателям за пределами организации Exchange.

1.  Параметры удаленных доменов;

2.  Параметры почтовых пользователей и почтовых контактов

3.  Настройки Outlook

Приоритеты в списке указаны в порядке убывания. Параметры TNEF на удаленном домене заменяют параметры TNEF пользователя электронной почты, контакта или Outlook. Допустим, вы отправляете сообщение в формате RTF в Outlook, но получатель находится на домене, параметры которого блокируют сообщения в формате TNEF. Получателю будет отправлено сообщение в формате обычного текста или HTML, но не TNEF.

Кроме того, Exchange никогда не отправляет сообщения STNEF внешним получателям. За пределы организации Exchange можно отправлять только сообщения в формате TNEF.

В начало
