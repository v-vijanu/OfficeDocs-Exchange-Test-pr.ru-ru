﻿---
title: 'Фильтрация отправителей: Exchange 2013 Help'
TOCTitle: Фильтрация отправителей
ms:assetid: b833f864-ff10-46a0-a653-28fb9ba30896
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/Bb124354(v=EXCHG.150)
ms:contentKeyID: 50488988
ms.date: 04/30/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Фильтрация отправителей

 

_**Применимо к:** Exchange Server 2013_

_**Последнее изменение раздела:** 2012-10-12_

Фильтрация отправителей на основе заголовка MAIL FROM: SMTP-заголовок определяет, какое действие нужно выполнить (и нужно ли) в отношении входящего сообщения электронной почты. Фильтрация отправителей обеспечивается агентом фильтра отправителей.

Фильтр отправителя действует в отношении сообщений от определенных отправителей, поступающих извне организации. Администраторы поддерживают список отправителей, сообщения от которых блокируются. Администратор может блокировать отдельных отправителей (например, kim@contoso.com), целые домены (contoso.com) или домены вместе с дочерними доменами (\*.contoso.com). Доступна настройка параметров действий, которые агент фильтра отправителя должен предпринять, если выявлено сообщение от заблокированного отправителя. Доступны следующие действия:

  - Агент фильтра отправителей отклоняет SMTP-запрос с указанием ошибки сеанса SMTP `554 5.1.0 Sender Denied`, а затем разрывает подключение.

  - агента фильтра отправителей принимает сообщение и изменяет его, чтобы указать, что сообщение получено от заблокированного отправителя. Поскольку сообщение поступило от заблокированного отправителя и помечено соответствующим образом, эти данные будут учтены агентом фильтра содержимого при вычислении вероятности нежелательной почты (SCL).

Можно назначить блокированных отправителей и указать, как агент фильтра отправителей должен реагировать на сообщения от них. Дополнительные сведения о настройке агента фильтра отправителей см. в разделе [Управление фильтрацией отправителей](manage-sender-filtering-exchange-2013-help.md).

> [!IMPORTANT]  
> SMTP-заголовки «MAIL FROM:» могут быть подделаны. Поэтому не стоит полагаться только на агент фильтра отправителей. Используйте агент фильтра отправителя в сочетании с агентом кода отправителя. Агент кода отправителя использует исходный IP-адрес сервера отправителя, чтобы убедиться, что домен, указанный в SMTP-заголовке «MAIL FROM:», соответствует зарегистрированному домену. Дополнительные сведения о коде отправителя см. в разделе <a href="sender-id-exchange-2013-help.md">Код отправителя</a>.


## Использование агента фильтра отправителей для блокировки сообщений

Если на сервере Exchange включен агент фильтра отправителей, фильтрация отправителей блокирует входящие сообщения с Интернета, для которых не выполнена проверка подлинности. Такие сообщения обрабатываются как внешние сообщения. Можно отключить агент фильтра отправителей в конфигурациях отдельных компьютеров. Дополнительные сведения см. в разделе [Управление фильтрацией отправителей](manage-sender-filtering-exchange-2013-help.md).

Если на сервере Exchange включен агент фильтра отправителей, он фильтрует все сообщения, поступающие через все соединители приема на этом компьютере. Как было отмечено ранее в данном разделе, фильтр применяется только к сообщениям из внешних источников. *Внешними источниками* считаются источники, которые не прошли проверку подлинности. Такими источниками считаются анонимные интернет-источники.

Не рекомендуется применять фильтры к сообщениям электронной почты от доверенных партнеров или внутренних сообщений. При использовании фильтров нежелательной почты всегда существует вероятность ложного срабатывания фильтра. Следует настраивать агенты защиты от нежелательной почты только в отношении непроверенных и неизвестных источников. Это снижает вероятность ошибочного отклонения сообщений электронной почты. Можно включить агент фильтра отправителей для проверки сообщений из любого источника, а также отключить его. Дополнительные сведения см. в разделе [Управление фильтрацией отправителей](manage-sender-filtering-exchange-2013-help.md).

Можно настроить агент фильтра отправителей таким образом, чтобы блокировать входящие сообщения, в которых в SMTP-заголовке «MAIL FROM:» не указан отправитель и имя домена. Эту функцию можно использовать для предотвращения атак отчетов о недоставке на сервер Exchange. Большинство допустимых SMTP-сообщений приходит с SMTP-серверов, которые предоставляют сведения об отправителе и домене в команде SMTP «MAIL FROM:».

## Определение действия блокировки

После указания заблокированных отправителей и доменов необходимо определить, какие действия будет предпринимать агент фильтра отправителей в отношении сообщений от заблокированных отправителей и доменов. Такие сообщения рекомендуется отклонять. При использовании агента фильтра отправителя для блокировки адресов электронной почты и доменов, указанных администратором Exchange, вероятность ложных срабатываний по сравнению с использованием других агентов защиты от нежелательной почты относительно снижается. Например, в агенте фильтрации содержимого, который является агентом защиты от нежелательной почты, для отнесения сообщения к категории нежелательных используется много различных переменных.

Существует только два сценария, в которых допустимые сообщения могут быть отклонены агентом фильтра отправителей:

  - Если при вводе адреса электронной почты или имени домена допущена ошибка, может быть заблокирован не тот отправитель.

  - если в список блокируемых отправителей внесено имя домена, которое позже было перерегистрировано на другую компанию, могут непреднамеренно блокироваться ее допустимые сообщения.

В любом из этих случаев отклонение таких сообщений все же имеет смысл.
