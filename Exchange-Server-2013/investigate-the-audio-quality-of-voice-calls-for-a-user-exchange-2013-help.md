﻿---
title: 'Оценка качества звука в голосовых вызовах для пользователя: Exchange 2013 Help'
TOCTitle: Оценка качества звука в голосовых вызовах для пользователя
ms:assetid: 0c945886-3cfa-423e-9b46-0d6b1584a145
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/JJ659059(v=EXCHG.150)
ms:contentKeyID: 50556333
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Оценка качества звука в голосовых вызовах для пользователя

 

_**Применимо к:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Последнее изменение раздела:** 2013-02-21_

Если пользователи сообщают о проблемах с качеством звука во время вызовов в единой системе обмена сообщениями, выявить причины проблем поможет отчет по журналам вызовов пользователей.

> [!NOTE]  
> Качество звука во время вызова зависит от факторов, не отражаемых в отчетах. Например, если на серверах Exchange не хватает памяти или ресурсов ЦП, пользователи могут жаловаться на снижение качества звука, хотя по отчетам оно будет высоким.


Сведения о дополнительных задачах, связанных с отчетами единой системы обмена сообщениями, см. в разделе [Процедуры отчеты единой системы обмена СООБЩЕНИЯМИ](um-reports-procedures-exchange-2013-help.md)

## Что нужно знать перед началом работы

  - Предполагаемое время для завершения: 5 минут.

  - Для выполнения этих процедур необходимы соответствующие разрешения. Сведения о необходимых разрешениях см. в статье запись "Командлеты отчетов со сводками и данными о вызовах единой системы обмена сообщениями" в разделе [Разрешения единой системы обмена сообщениями](unified-messaging-permissions-exchange-2013-help.md).

  - Сочетания клавиш для процедур, описанных в этой статье, приведены в статье [Сочетания клавиш в Центре администрирования Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]  
> Возникли проблемы? Обратитесь за помощью к участникам форумов, посвященных Exchange. Посетите форумы по таким продуктам: <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> или <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Использование Центра администрирования Exchange для получения журналов вызовов для пользователя с включенной поддержкой единой системы обмена сообщениями

1.  В Центре администрирования Exchange перейдите на страницу **Единая система обмена сообщениями** \> **Дополнительные параметры**![Значок дополнительных параметров](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Значок дополнительных параметров") \> **Журналы вызовов пользователей**.

2.  Нажмите кнопку **Выбрать пользователя** и выберите нужного пользователя.

3.  Чтобы получить дополнительные сведения о качестве звука по строке в отчете, выберите строку и нажмите кнопку **Сведения о качестве звука**. Доступны следующие данные:
    
      - **ДАТА И ВРЕМЯ** Дата и время вызова в часовом поясе, который выбранный пользователь установил в Outlook Web App.
    
      - **ПОЛЬЗОВАТЕЛЬ** Выбранный пользователь.
    
      - **АБОНЕНТСКАЯ ГРУППА ЕДИНОЙ СИСТЕМЫ ОБМЕНА СООБЩЕНИЯМИ** Абонентская группа вызова.
    
      - **ШЛЮЗ IP ЕДИНОЙ СИСТЕМЫ ОБМЕНА СООБЩЕНИЯМИ** Шлюз IP единой системы обмена сообщениями, использованный для вызова.
    
      - **АУДИОКОДЕК** Используемый во время вызова аудиокодек.
    
      - **NMOS**   Оценка NMOS (Network Mean Opinion Score) для вызова. Оценка NMOS указывает, насколько высоким было качество звука во время вызова по шкале от 1 до 5, где 5 соответствует превосходному качеству звука.
        
        > [!NOTE]  
        > Максимальная оценка NMOS, возможная для вызова, зависит от используемого аудиокодека. Оценка NMOS может быть недоступна для очень коротких вызовов продолжительностью до 10 секунд.
    
      - **Снижение качества NMOS** степень снижения качества звука по оценке NMOS по сравнению с максимально возможным значением для используемого аудиокодека. Например, если значение снижения оценки NMOS для вызова составило 1,2, а оценка NMOS составляла 3,3, то максимальная оценка NMOS для это вызова равна 4,5 (1,2 + 3,3).
    
      - **Дрожание**   Среднее отклонение в получении пакетов данных для вызова.
    
      - **Потеряно пакетов**   Средний процент потери пакетов данных для выбранного вызова. Потеря пакетов является показателем надежности соединения.
    
      - **Круговой путь**   Среднее время приема-передачи звука для выбранного звонка в миллисекундах. Значение приема-передачи позволяет определить задержку соединения.
    
      - **Продолжительность потери импульсов**   Средняя длительность потери пакетов во время пиков потерь для выбранного звонка.
