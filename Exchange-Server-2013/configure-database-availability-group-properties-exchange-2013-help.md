﻿---
title: 'Настройка свойств группы обеспечения доступности баз данных: Exchange 2013 Help'
TOCTitle: Настройка свойств группы обеспечения доступности баз данных
ms:assetid: 50daeac5-a16f-4362-a325-19e0fe25d59d
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/Dd297985(v=EXCHG.150)
ms:contentKeyID: 50488140
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Настройка свойств группы обеспечения доступности баз данных

 

_**Применимо к:** Exchange Server 2013_

_**Последнее изменение раздела:** 2014-06-24_

С помощью Центра администрирования Exchange или командной консоли вы можете настроить свойства группы обеспечения доступности баз данных, включая IP-адреса, настройки следящего сервера и следящего каталога, которые используются в этой группе. Командная консоль позволяет настроить свойства группы обеспечения доступности баз данных, недоступные в Центре администрирования Exchange, например сведения о дополнительном следящем сервере и альтернативном следящем каталоге, TCP-порт, который используется для репликации, и режим координации активации центра данных (DAC).

## Что нужно знать перед началом работы?

  - Предполагаемое время для завершения: 1 минута.

  - Для выполнения этих процедур необходимы соответствующие разрешения. Сведения о необходимых разрешениях см. в статье Запись "Группы обеспечения доступности баз данных" в разделе [Разрешения высокого уровня доступности и устойчивости сайта](high-availability-and-site-resilience-permissions-exchange-2013-help.md).

  - Значения свойств группы DAG хранятся в Active Directory и в базе данных кластера. Тем не менее некоторые свойства хранятся только в базе данных кластера. В результате базовый кластер для группы обеспечения доступности баз данных должен работать и иметь кворум, чтобы можно было задать следующие свойства:
    
      - ReplicationPort
    
      - NetworkCompression
    
      - NetworkEncryption
    
      - DiscoverNetworks

  - Сочетания клавиш для процедур, описанных в этой статье, приведены в статье [Сочетания клавиш в Центре администрирования Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]  
> Возникли проблемы? Обратитесь за помощью к участникам форумов, посвященных Exchange. Посетите форумы по таким продуктам: <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> или <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Что необходимо сделать?

## Использование EAC для настройки свойств группы обеспечения доступности базы данных

1.  В Центре администрирования Exchange последовательно выберите пункты **Серверы** \> **Группы обеспечения доступности баз данных**.

2.  Выберите группу DAG, которую необходимо настроить, и выберите команду ![Значок редактирования](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Значок редактирования").

3.      
    Страница **Общие** используется для просмотра членства в группе DAG и ее состояния, настройки следящего сервера и следящего каталога, а также автоматической настройки сети:
    
      - **Следящий сервер** Имя узла или полное доменное имя следящего сервера для группы обеспечения доступности баз данных. Хотя это обязательное свойство для всех групп обеспечения доступности баз данных, следящий сервер используется, когда имеется четное количество членов этой группы, а кластером применяется модель кворума "Большинство узлов и общих файловых ресурсов".
    
      - **Следящий каталог**   Полный путь к каталогу, который используется для хранения файла witness.log на следящем сервере. Хотя это обязательное свойство для всех групп обеспечения доступности баз данных, следящий каталог используется только в случае применения следящего сервера группы обеспечения доступности баз данных.
    
      - **Серверы в рабочем состоянии** Поле только для чтения, в котором отображается список членов группы обеспечения доступности баз данных и их текущее рабочее состояние.
    
      - **Настраивать сеть группы базы данных вручную** Установите этот флажок, чтобы настраивать все сети групп обеспечения доступности баз данных вручную. Если не установить этот флажок, сети групп обеспечения доступности баз данных будут настраиваться автоматически с учетом конфигурации сетевого интерфейса. Если этот флажок снят, командлеты **Set-DatabaseAvailabilityGroupNetwork** и **New-DatabaseAvailabilityGroupNetwork** отключены для административного использования для группы обеспечения доступности баз данных.

4.      
    Страница **IP-адреса** служит для просмотра и изменения IP-адресов, назначенных группе обеспечения доступности баз данных.
    
      - Выберите существующий IP-адрес и нажмите ![Значок редактирования](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Значок редактирования"), чтобы изменить его.
    
      - Выберите существующий IP-адрес и нажмите кнопку со знаком минус (удаление), чтобы удалить его.
    
      - Введите IP-адрес и щелкните ![Значок добавления](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Значок добавления"), чтобы добавить его к DAG.

5.  
    
    Щелкните **Сохранить**, чтобы сохранить все изменения.

## Использование командной консоли Exchange для настройки свойств группы доступности базы данных

В этом примере показано, как установить следящий каталог C:\\DAG1DIR для группы обеспечения доступности баз данных с именем DAG1.

    Set-DatabaseAvailabilityGroup -Identity DAG1 -WitnessDirectory C:\DAG1DIR

В этом примере показано, как предварительно настроить альтернативный следящий сервер CAS3 и альтернативный следящий каталог C:\\DAGFileShareWitnesses\\DAG1.contoso.com для группы обеспечения доступности баз данных с именем DAG1.

    Set-DatabaseAvailabilityGroup -Identity DAG1 -AlternateWitnessDirectory C:\DAGFileShareWitnesses\DAG1.contoso.com -AlternateWitnessServer CAS3

В этом примере показано, как настроить использование протокола DHCP для получения IP-адреса в группе обеспечения доступности баз данных с именем DAG1.

    Set-DatabaseAvailabilityGroup -Identity DAG1 -DatabaseAvailabilityGroupIPAddresses 0.0.0.0

В этом примере показано, как настроить использование статического IP-адреса 10.0.0.8 в группе обеспечения доступности баз данных с именем DAG1.

    Set-DatabaseAvailabilityGroup -Identity DAG1 -DatabaseAvailabilityGroupIPAddresses 10.0.0.8

В этом примере показано, как настроить группу обеспечения доступности баз данных DAG1 в нескольких подсетях с использованием нескольких статических IP-адресов.

    Set-DatabaseAvailabilityGroup -Identity DAG1 -DatabaseAvailabilityGroupIPAddresses 10.0.0.8,10.0.1.8

В этом примере показано, как настроить режим активации центра обработки данных для группы обеспечения доступности баз данных DAG1.

    Set-DatabaseAvailabilityGroup -Identity DAG1 -DatacenterActivationMode DagOnly

В этом примере показано, как настроить порт репликации 63132 для группы обеспечения доступности баз данных DAG1.

    Set-DatabaseAvailabilityGroup -Identity DAG1 -ReplicationPort 63132

> [!NOTE]  
> После изменения порта репликации по умолчанию для группы доступности базы данных необходимо вручную изменить исключения брандмауэра Windows для каждого участника группы DAG, чтобы разрешить подключение через указанный порт.


## Как проверить, что все получилось?

Чтобы убедиться, что группа обеспечения доступности баз данных успешно настроена:

  - В командной консоли выполните следующую команду, чтобы отобразить параметры конфигурации группы обеспечения доступности баз данных и проверить, настроена ли эта группа успешно.
    
        Get-DatabaseAvailabilityGroup <DAGName> | Format-List

## Дополнительные сведения

[Создание группы обеспечения доступности баз данных](create-a-database-availability-group-exchange-2013-help.md)

[Удаление группы обеспечения доступности баз данных](remove-a-database-availability-group-exchange-2013-help.md)

[Создание сети группы доступности базы данных](create-a-database-availability-group-network-exchange-2013-help.md)

[Управление членством в группе обеспечения доступности баз данных](manage-database-availability-group-membership-exchange-2013-help.md)

[Get-DatabaseAvailabilityGroup](https://technet.microsoft.com/ru-ru/library/dd351226\(v=exchg.150\))

[Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/ru-ru/library/dd297934\(v=exchg.150\))
