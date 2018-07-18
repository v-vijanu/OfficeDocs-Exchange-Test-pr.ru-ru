﻿---
title: 'Функции мобильных телефонов и планшетов: Exchange 2013 Help'
TOCTitle: Функции мобильных телефонов и планшетов
ms:assetid: ad54d9e6-7a1c-4fb0-b5a9-0b042b98ada3
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/Bb232162(v=EXCHG.150)
ms:contentKeyID: 50556429
ms.date: 04/30/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Функции мобильных телефонов и планшетов

 

_**Применимо к:** Exchange Server 2013_

_**Последнее изменение раздела:** 2015-03-09_

Пользователи могут пользоваться электронной почтой, календарем, контактами и задачами на мобильных телефонах, планшетах и других портативных устройствах через Microsoft Exchange ActiveSync. Кроме того, они могут настроить подпись и автоматические ответы. Широкий спектр мобильных телефонов и устройств позволяет работать с Exchange ActiveSync.

> [!NOTE]  
> Хотя мы постоянно ссылаемся на устройства, которые осуществляют доступ к серверу Exchange Server 2013, как на мобильные телефоны, существует множество устройств, которые могут получать доступ к Exchange 2013, но не имеют функциональных возможностей сотовых телефонов. Термин «мобильный телефон» в этой документации также относится и к этим устройствам.


## Устройства, совместимые с Exchange ActiveSync

Пользователи могут применять функции Exchange ActiveSync путем выбора мобильных телефонов, которые совместимы с Exchange ActiveSync. Эти мобильные телефоны выпускаются многими производителями и поддерживаются многими операторами. Дополнительные сведения см. в документации на конкретную модель телефона.

К мобильным телефонам, совместимым с Microsoft Exchange, относятся следующие:

  - **Apple**   Apple iPhone, iPod Touch и iPad — все устройства поддерживают службу Exchange ActiveSync.

  - **Windows Phone**   Windows Phone 8, Windows Phone 7, а также все предыдущие версии поддерживают работу с Exchange ActiveSync.

  - **Android**   Многие мобильные телефоны с операционной системой Android поддерживают службу Exchange ActiveSync. Однако такие мобильные устройства могут поддерживать не все доступные политики почтовых ящиков для мобильных устройств. Дополнительные сведения см. в разделе [Политики почтовых ящиков мобильных устройств](mobile-device-mailbox-policies-exchange-2013-help.md).

## Возможности программного обеспечения Windows Phone

Мобильные телефоны под управлением определенной версии программного обеспечения Windows Phone предлагают самый широкий набор функций для синхронизации с Exchange 2013. В следующей таблице перечислены политики почтовых ящиков для мобильных устройств Windows Phone 7 и Windows Phone 8.

### Функции Windows Phone 7 и 8

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Операционная система</th>
<th>Возможности</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Windows Phone 8</p></td>
<td><p>Windows Phone 8 поддерживает следующие политики почтовых ящиков мобильных устройств:</p>
<ul>
<li><p>Разрешить простой пароль устройства</p></li>
<li><p>Требовать ввода буквенно-цифрового пароля</p></li>
<li><p>Пароль устройства включен</p></li>
<li><p>Истечение срока действия пароля устройства</p></li>
<li><p>Служба IRM включена</p></li>
<li><p>Максимальное число неудачных попыток ввода пароля устройства</p></li>
<li><p>Максимальное время простоя устройства до блокировки</p></li>
<li><p>Минимальное количество сложных символов в пароле устройства</p></li>
<li><p>Минимальная длина пароля устройства</p></li>
<li><p>Требовать шифрование устройства</p></li>
<li><p>Удаленная очистка</p></li>
</ul>

> [!WARNING]  
> Если в организации используются другие параметры политики почтовых ящиков для мобильных устройств, необходимо включить политику <strong>Разрешить неинициализируемые устройства</strong>. Это может иметь последствия для безопасности организации, поскольку другие мобильные телефоны и устройства, которые удовлетворяют не всем требованиям параметров политики мобильного устройства, будет синхронизироваться. Дополнительные сведения см. в разделе <a href="mobile-device-mailbox-policies-exchange-2013-help.md">Политики почтовых ящиков мобильных устройств</a>.

</td>
</tr>
<tr class="even">
<td><p>Windows Phone 7</p></td>
<td><p>Мобильные телефоны Windows Phone 7 поддерживают только подмножество всех параметров политики почтовых ящиков Exchange ActiveSync.</p>
<ul>
<li><p>Необходимо ввести пароль</p></li>
<li><p>Минимальная длина пароля</p></li>
<li><p>Максимальное время простоя до блокировки</p></li>
<li><p>Максимальное число неудачных попыток ввода пароля устройства</p></li>
<li><p>Разрешить использовать простой пароль</p></li>
<li><p>Срок действия пароля</p></li>
<li><p>Журнал пароля</p></li>
<li><p>Отключить поддержку съемных носителей</p></li>
<li><p>Отключить IrDA</p></li>
<li><p>Отключить синхронизацию с настольным ПК</p></li>
<li><p>Блокировка удаленного рабочего стола</p></li>
<li><p>Отключить поддержку общего доступа к Интернету</p></li>
</ul></td>
</tr>
</tbody>
</table>
