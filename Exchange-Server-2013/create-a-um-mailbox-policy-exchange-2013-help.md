﻿---
title: 'Справка по Exchange 2013: создание политики почтовых ящиков UM'
TOCTitle: Создание политики почтовых ящиков единой системы обмена сообщениями
ms:assetid: 7f20874b-c46c-4505-9a78-f63eacb578ff
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/Bb123510(v=EXCHG.150)
ms:contentKeyID: 50556396
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Servers.UnifiedMessaging.CreateUMMailboxPolicyWizardForm.CreateUMMailboxPolicyWizardPage
ms.translationtype: MT
---

# Создание политики почтовых ящиков единой системы обмена сообщениями

 

_**Применимо к:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Последнее изменение раздела:** 2013-03-08_

Можно создать политику почтовых ящиков единой системы обмена сообщениями для применения общего набора параметров политики единой системы обмена сообщениями, таких как параметры политики ПИН или ограничения набора номеров, к коллекции почтовых ящиков с включенной функцией единой системы обмена сообщениями. Политики почтовых ящиков связывают пользователя единой системы обмена сообщениями с абонентской группой этой системы и обеспечивают применение общего набора политик или параметров безопасности к совокупности почтовых ящиков с включенной поддержкой единой системы обмена сообщениями. Эти политики полезны для применения и стандартизации параметров настройки единой системы обмена сообщениями для ее пользователей.

По умолчанию при создании абонентской группы также создается политика почтовых ящиков единой системы обмена сообщениями. Может потребоваться создать дополнительные или изменить существующие политики почтовых ящиков после развертывания единой системы обмена сообщениями в организации.

Дополнительные сведения об управленческих задачах, связанных с политиками почтовых ящиков единой системы обмена сообщениями, см. в разделе [Процедуры политики почтовых ящиков единой системы обмена СООБЩЕНИЯМИ](um-mailbox-policy-procedures-exchange-2013-help.md).

## Что нужно знать перед началом работы

  - Предполагаемое время для завершения: 3 минуты.

  - Для выполнения этих процедур необходимы соответствующие разрешения. Сведения о необходимых разрешениях см. в статье Запись «Политики почтовых ящиков единой системы обмена сообщениями» в разделе [Разрешения единой системы обмена сообщениями](unified-messaging-permissions-exchange-2013-help.md).

  - Перед выполнением этих процедур убедитесь, что абонентская группа единой системы обмена сообщениями создана. Дополнительные сведения см. в разделе [Создание абонентской группы единой системы обмена сообщениями](create-a-um-dial-plan-exchange-2013-help.md).

  - Сочетания клавиш для процедур, описанных в этой статье, приведены в статье [Сочетания клавиш в Центре администрирования Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]  
> Возникли проблемы? Обратитесь за помощью к участникам форумов, посвященных Exchange. Посетите форумы по таким продуктам: <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> или <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Что необходимо сделать?

## Использование EAC для создания политики почтовых ящиков единой системы обмена сообщениями

1.  
    
    В Центре администрирования Exchange последовательно выберите пункты **Единая система обмена сообщениями** \> **Абонентские группы единой системы обмена сообщениями**. Выберите из списка абонентскую группу единой системы обмена сообщениями, которую необходимо изменить, и нажмите кнопку **Правка**![Значок редактирования](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Значок редактирования").

2.  На странице **Абонентская группа единой системы обмена сообщениями** в разделе **Политики почтовых ящиков единой системы обмена сообщениями** щелкните **Создать**![Значок добавления](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Значок добавления").

3.  На странице **Создание политики почтовых ящиков единой системы обмена сообщениями** в поле **Имя** введите имя новой политики почтовых ящиков единой системы обмена сообщениями.
    
    В этом поле можно ввести уникальное имя политики почтовых ящиков единой системы обмена сообщениями. Это отображаемое имя, которое выводится в Центре администрирования Exchange. Если требуется изменить отображаемое имя политики почтовых ящиков единой системы обмена сообщениями после ее создания, необходимо сначала удалить существующую политику, а затем создать новую политику с нужным именем. Вы не сможете удалить политику почтовых ящиков единой системы обмена сообщениями, если с ней связаны пользователи с включенной поддержкой единой системы обмена сообщениями.
    
    Имя политики почтовых ящиков единой системы обмена сообщениями является обязательным, но используется только для отображения. Поскольку в организации может использоваться несколько политик почтовых ящиков единой системы обмена сообщениями, рекомендуется задавать осмысленные имена политик. Максимальная длина краткого имени политики почтовых ящиков единой системы обмена сообщениями составляет 64 символа. Имя может содержать пробелы. В имени не допускается использование следующих символов: " / \\ \[ \] : ; | = , + \* ? \< \>.

4.  Нажмите кнопку **Сохранить** для сохранения новой политики почтовых ящиков единой системы обмена сообщениями. При сохранении политики почтовых ящиков единой системы обмена сообщениями включаются все параметры по умолчанию, в том числе политики ПИН-кодов, функции голосовой почты и параметры защищенной голосовой почты. Если вы хотите настроить или изменить параметры по умолчанию для вновь созданной политики почтовых ящиков единой системы обмена сообщениями, используйте командлет **Set-UMMailbox**.

## Использование командной консоли для создания политики почтовых ящиков единой системы обмена сообщениями

В этом примере создается политика почтовых ящиков единой системы обмена сообщениями с именем `MyUMMailboxPolicy`, связанная с абонентской группой единой системы обмена сообщениями с именем `MyUMDialPlan`.

    New-UMMailboxPolicy -Name MyUMMailboxPolicy -UMDialPlan MyUMDialPlan

