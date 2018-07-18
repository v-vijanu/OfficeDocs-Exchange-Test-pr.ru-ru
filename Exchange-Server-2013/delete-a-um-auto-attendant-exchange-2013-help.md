﻿---
title: 'Удаление автосекретаря единой системы обмена СООБЩЕНИЯМИ: Exchange 2013 Help'
TOCTitle: Удаление автосекретаря единой системы обмена СООБЩЕНИЯМИ
ms:assetid: 92846bbc-e6b9-45fc-8702-ef5c92eeb08f
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/Bb123780(v=EXCHG.150)
ms:contentKeyID: 50488642
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Удаление автосекретаря единой системы обмена СООБЩЕНИЯМИ

 

_**Применимо к:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Последнее изменение раздела:** 2012-11-30_

После удаления существующего автосекретаря единой системы обмена сообщениями на входящие вызовы, которые ранее обслуживались автоматическим секретарем единой системы обмена сообщениями, должен отвечать оператор-человек. Автоматического секретаря единой системы обмена сообщениями, связанного с абонентской группой единой системы обмена сообщениями в качестве автосекретаря единой системы обмена сообщениями по умолчанию, удалить невозможно.

Дополнительные задачи управления, связанные с автосекретарями единой системы обмена сообщениями, см. в разделе [Процедуры автосекретаря единой системы обмена сообщениями](um-auto-attendant-procedures-exchange-2013-help.md).

## Что нужно знать перед началом работы

  - Предполагаемое время для завершения: менее 1 минуты.

  - Для выполнения этих процедур необходимы соответствующие разрешения. Сведения о необходимых разрешениях см. в статье Запись «Автосекретари единой системы обмена сообщениями» в разделе [Разрешения единой системы обмена сообщениями](unified-messaging-permissions-exchange-2013-help.md).

  - Перед выполнением этих процедур убедитесь, что абонентская группа единой системы обмена сообщениями создана. Дополнительные сведения см. в разделе [Создание абонентской группы единой системы обмена сообщениями](create-a-um-dial-plan-exchange-2013-help.md).

  - Перед выполнением этих процедур убедитесь, что автосекретарь единой системы обмена сообщениями создан. Дополнительные сведения см. в разделе [Создание автосекретаря единой системы обмена сообщениями](create-a-um-auto-attendant-exchange-2013-help.md).

  - Сочетания клавиш для процедур, описанных в этой статье, приведены в статье [Сочетания клавиш в Центре администрирования Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]  
> Возникли проблемы? Обратитесь за помощью к участникам форумов, посвященных Exchange. Посетите форумы по таким продуктам: <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> или <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Что необходимо сделать?

## Использование EAC для удаления автосекретаря единой системы обмена сообщениями

1.  В Центре администрирования Exchange последовательно выберите пункты **Единая система обмена сообщениями** \> **Абонентские группы единой системы обмена сообщениями**. Выберите в списке абонентскую группу единой системы обмена сообщениями, которую необходимо изменить, и нажмите кнопку **Правка**![Значок редактирования](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Значок редактирования").

2.  На странице **Абонентская группа единой системы обмена сообщениями** в разделе **Автосекретари единой системы обмена сообщениями** выберите автосекретарь единой системы обмена сообщениями, который требуется удалить. На панели инструментов нажмите кнопку **Удалить**![Значок удаления](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Значок удаления"). На странице **Предупреждение** нажмите кнопку **Да**.

## Использование командной консоли для удаления автосекретаря единой системы обмена сообщениями

В этом примере показано удаление автосекретаря единой системы обмена сообщениями с именем `MyUMAutoAttendant`.

    Remove-UMAutoAttendant -Identity MyUMAutoAttendant
