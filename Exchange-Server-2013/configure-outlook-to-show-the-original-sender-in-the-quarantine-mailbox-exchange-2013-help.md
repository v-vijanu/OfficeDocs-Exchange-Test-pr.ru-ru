﻿---
title: 'Настройка Outlook для отображения исходного отправителя в почтовом ящике карантина: Exchange 2013 Help'
TOCTitle: Настройка Outlook для отображения исходного отправителя в почтовом ящике карантина
ms:assetid: 9249425d-1b06-48a0-ad95-c4eefb641ff4
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/Ee861109(v=EXCHG.150)
ms:contentKeyID: 50488640
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Настройка Outlook для отображения исходного отправителя в почтовом ящике карантина

 

_**Применимо к:** Exchange Server 2013_

_**Последнее изменение раздела:** 2016-12-09_

Карантин нежелательной почты — функция агента фильтра содержимого, снижающая риск потери сообщений из надежных источников. Карантин нежелательной почты обеспечивает временное хранение сообщений, определенных как нежелательная почта, которые не следует доставлять в почтовый ящик пользователя в организации.

Когда сообщение достигает порога карантина для нежелательной почты, оно включается в отчет о недоставке (NDR) и доставляется на почтовый ящик карантина нежелательной почты. Поскольку сообщения, помещенные на карантин, хранятся в почтовом ящике карантина как отчеты о недоставке, адрес администратора почты в организации будет указываться в поле адреса "От:" для всех сообщений. Тем не менее, наличие исходного адреса отправителя, исходного адреса получателя, а также исходной вероятности нежелательной почты в списке полей упрощает поиск сообщения, которое нужно восстановить.

По умолчанию нельзя выбрать эти поля в Microsoft Outlook. Прежде чем добавлять эти поля при просмотре сообщения, необходимо сначала создать в Outlook форму, которая добавляет исходного отправителя, исходного получателя и исходную вероятность как поля, которые можно выбрать. Создав эту настраиваемую форму, можно настроить Outlook так, чтобы отобразить эти поля при просмотре сообщения.

## Что нужно знать перед началом работы?

  - Предполагаемое время выполнения процедуры: 15 минут.

  - Для выполнения этих процедур необходимы соответствующие разрешения. Сведения о необходимых разрешениях см. в статье Запись "Доступ к почтовому ящику" в разделе [Разрешения потока обработки почты](mail-flow-permissions-exchange-2013-help.md).

  - Для этой процедуры необходимо настроить почтовый ящик карантина, который используется с целью защиты от нежелательной почты. Дополнительные сведения см. в разделе [Настройка почтового ящика карантина нежелательной почты](configure-a-spam-quarantine-mailbox-exchange-2013-help.md).

  - Для доступа к почтовый ящик карантина, необходимых для настройки профиля Outlook для этого почтового ящика и затем откройте почтовый ящик с помощью Outlook. Дополнительные сведения о настройке и использовании нескольких профилей Outlook [профилей электронной почты обзор Outlook](https://go.microsoft.com/fwlink/p/?linkid=178975)см.

  - Сочетания клавиш для процедур, описанных в этой статье, приведены в статье [Сочетания клавиш в Центре администрирования Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]  
> Возникли проблемы? Обратитесь за помощью к участникам форумов, посвященных Exchange. Посетите форумы по таким продуктам: <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> или <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Что необходимо сделать?

## Действие 1. Использование Блокнота для создания настраиваемой формы Outlook

1.  Откройте Блокнот и скопируйте следующий код в документ.
    
        [Description]
        MessageClass=IPM.Note
        CLSID={00020D31-0000-0000-C000-000000000046}
        DisplayName=Quarantine Extension Form
        Category=Standard
        Subcategory=Form
        Comment=This form allows the Original Sender (ReceivedRepresentingEmailAddress), Original Recipient (To), and Original SCL (OriginalScl) values to be viewed as columns.
        LargeIcon=IPML.ico
        SmallIcon=IPMS.ico
        Version=3.0
        Locale=enu
        Hidden=1
        Owner=Microsoft Corporation
        Contact=Your Name
        
        [Platforms]
        Platform1=Win16
        Platform2=NTx86
        Platform9=Win95
        
        [Platform.Win16]
        CPU=ix86
        OSVersion=Win3.1
        
        [Platform.NTx86]
        CPU=ix86
        OSVersion=WinNT3.5
        
        [Platform.Win95]
        CPU=ix86
        OSVersion=Win95
        
        [Properties]
        Property01=ReceivedRepresentingEmailAddress
        Property02=DisplayTo
        Property03=OriginalScl
        
        [Property.ReceivedRepresentingEmailAddress]
        Type=31
        NmidInteger=0x0078
        DisplayName=ReceivedRepresentingEmailAddress
        
        [Property.DisplayTo]
        Type=31
        NmidInteger=0x0E04
        DisplayName=DisplayTo
        
        [Property.OriginalScl]
        Type=3
        NmidPropset={41F28F13-83F4-4114-A584-EEDB5A6B0BFF}
        NmidString=OriginalScl
        DisplayName=OriginalScl
        
        [Verbs]
        Verb1=1
        
        [Verb.1]
        DisplayName=&Open
        Code=0
        Flags=0
        Attribs=2
        
        [Extensions]
        Extensions1=1
        
        [Extension.1]
        Type=31
        NmidPropset={00020D0C-0000-0000-C000-000000000046}
        NmidInteger=1
        Value=1000000000000000

2.  Сохраните файл в папке форм Office, используя следующие значения:
    
      - **Путь** *\<путь установки Office\>*\\\<*версия Office\>*\\Forms\\*\<LCID\>*
        
          - *\<Путь установки Office\>*   Для 32-разрядной версии Office в 32-разрядных версиях Microsoft Windows или 64-разрядной версии Office в 64-разрядных версиях Windows путь по умолчанию — `C:\Program Files\Microsoft Office`. Для 32-разрядной версии Office в 64-разрядных версиях Windows путь по умолчанию — `C:\Program Files (x86)\Microsoft Office`.
        
          - *\<Версия Office\>*   Для Outlook 2007 — `Office12`. Для Outlook 2010 значение равно `Office14`. Для Outlook 2013 значение равно `Office15`.
        
          - *\<LCID\>*   Это идентификатор языка и региональных параметров. Например, LCID для английского языка — 1033. Дополнительные сведения см. в статье [KB221435: Список поддерживаемых идентификаторов языков в Word](http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=221435).
    
      - **Имя**   В дальнейшем примем, что файл называется `QTNE.cfg`. Имя файла не важно, но не забудьте заключить его в кавычки, чтобы файл сохранялся как QTNE.cfg, а не как QTNE.cfg.txt.
    
    Например, в случае с 32-разрядной английской версией Outlook 2013, установленной в 64-разрядной версии Windows, сохраните файл как:
    
        "C:\Program Files (x86)\Microsoft Office\Office15\Forms\1033\QTNE.cfg"
    
    > [!NOTE]  
    > Если система управления доступом пользователей Windows (UAC) не позволяет сохранить файл в нужное место, сначала сохраните его во временной папке, а затем и скопируйте.


## Действие 2. Настройка Outlook для использования настраиваемой формы Outlook

Воспользуйтесь одним из приведенных ниже способов в зависимости от версии Outlook, установленной на компьютере.

## Настройка Outlook 2010 или Outlook 2013

1.  В Outlook 2010 или Outlook 2013 щелкните пункты меню **Файл** \> **Параметры** \> **Дополнительно**.

2.  В разделе **Разработка** нажмите **Настраиваемые формы**.

3.  В диалоговом окне **Параметры** нажмите кнопку **Управление формами**.

4.  В диалоговом окне **Диспетчер форм** нажмите кнопку **Установить**. Перейдите к расположению файла `QTNE.cfg`, выделите его и нажмите кнопку **Открыть**. Просмотрите сведения в диалоговом окне **Свойства формы** и нажмите кнопку **ОК**, чтобы установить форму расширения карантина в библиотеке личных форм.

5.  В диалоговом окне **Диспетчер форм** нажмите кнопку **Закрыть**. Щелкните **ОК** дважды, чтобы закрыть остальные диалоговые окна, и вернитесь в основное окно Outlook.

6.  На вкладке **Главная** в разделе **Почта** откройте папку "Входящие", щелкните правой кнопкой мыши строку заголовков столбцов (возможно, для просмотра столбцов потребуется увеличить ширину списка сообщений) и выберите пункт **Просмотр параметров**.

7.  В окне **Дополнительные параметры просмотра** выберите **Столбцы**.

8.  В диалоговом окне **Показать столбцы** в раскрывающемся списке **Выбрать столбцы из** прокрутите до конца списка и выберите **Формы**.

9.  В диалоговом окне **Выбор корпоративных форм для этой папки** в поле **Выбранные формы** выберите **Сообщение** и щелкните **Удалить**. В поле **Личные формы** выберите **Форма расширения карантина**, а затем нажмите **Добавить**. Завершив настройку, нажмите кнопку **Закрыть**.

10. В диалоговом окне **Показать столбцы** в разделе **Доступные столбцы** выберите одно или несколько из следующих полей и щелкните **Добавить** после каждого выбранного поля.
    
      - **ReceivedRepresentingEmailAddress**   Исходный отправитель
    
      - **DisplayTo**. Исходный получатель (обратите внимание, что после добавления элемент отображается как **To**).
    
      - **OriginalScl**   Исходное значение вероятности нежелательной почты
    
    Используйте кнопки **Вверх** или **Вниз** для расположения столбцов в представлении. Для достижения наилучших результатов поместите три новых поля после поля **Вложение** и до поля **От**. Закончив, нажмите кнопку **ОК** два раза, чтобы вернуться к главному окну Outlook.

## Настройка Outlook 2007

1.  В Outlook 2007 щелкните **Сервис** \> **Параметры**.

2.  В диалоговом окне **Параметры** выберите вкладку **Дополнительно**, затем в разделе **Общие** нажмите кнопку **Дополнительные параметры**.

3.  В диалоговом окне **Дополнительные параметры** нажмите кнопку **Настраиваемые формы**, затем в диалоговом окне **Настраиваемые формы** нажмите кнопку **Диспетчер форм**.

4.  В диалоговом окне **Диспетчер форм** нажмите кнопку **Установить**. Перейдите к расположению файла `QTNE.cfg`, выделите его и нажмите кнопку **Открыть**. Просмотрите сведения в диалоговом окне **Свойства формы** и нажмите кнопку **ОК**, чтобы установить форму расширения карантина в библиотеке личных форм.

5.  Закройте диалоговое окно **Диспетчер форм**, затем, нажимая кнопку **ОК**, закройте остальные диалоговые окна и вернитесь в основное окно Outlook 2007.

6.  В разделе **Почта** откройте папку "Входящие", щелкните правой кнопкой мыши строку заголовков столбцов (возможно, для просмотра столбцов потребуется увеличить ширину списка сообщений) и выберите пункт **Настроить текущее представление**.

7.  В диалоговом окне **Настройка представления: сообщения** щелкните **Показать поля**.

8.  В диалоговом окне **Показать поля** в раскрывающемся списке **Выбрать поля из** прокрутите до конца списка и выберите **Формы**.

9.  В диалоговом окне **Выбор корпоративных форм для этой папки** в поле **Выбранные формы** выберите **Сообщение** и щелкните **Удалить**. В поле **Личные формы** выберите **Форма расширения карантина**, а затем нажмите **Добавить**. Завершив настройку, нажмите кнопку **Закрыть**.

10. В диалоговом окне **Показать поля** в разделе **Доступные поля** выберите одно или несколько из следующих полей и щелкните **Добавить** после каждого выбранного поля.
    
      - **ReceivedRepresentingEmailAddress**   Исходный отправитель
    
      - **DisplayTo**. Исходный получатель (обратите внимание, что после добавления элемент отображается как **To**).
    
      - **OriginalScl**   Исходное значение вероятности нежелательной почты
    
    Используйте кнопки **Вверх** или **Вниз** для расположения столбцов в представлении. Для достижения наилучших результатов поместите три новых поля после поля **Вложение** и до поля **От**. Закончив, нажмите кнопку **ОК** два раза, чтобы вернуться к главному окну Outlook 2007.

## Как проверить, что все получилось?

Вы узнаете, сработала ли эта процедура, если исходный отправитель, исходный получатель или значение уровня вероятности нежелательной почты отображается для сообщений на карантине в почтовом ящике карантина нежелательной почты при просмотре через Outlook.
