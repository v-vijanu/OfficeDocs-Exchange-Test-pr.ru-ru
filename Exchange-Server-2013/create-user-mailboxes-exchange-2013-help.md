﻿---
title: 'Создание почтовых ящиков пользователя: Exchange 2013 Help'
TOCTitle: Создание почтовых ящиков пользователя
ms:assetid: 51a8b4c6-a53e-41c5-8bb1-ea4c0eaa0174
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/JJ991919(v=EXCHG.150)
ms:contentKeyID: 52061230
ms.date: 04/30/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Создание почтовых ящиков пользователя

 

_**Применимо к:** Exchange Online, Exchange Server 2013_

_**Последнее изменение раздела:** 2013-04-12_

Почтовые ящики — это наиболее распространенный тип получателей, используемый сотрудниками в организации Exchange. Каждый почтовый ящик связан с учетной записью пользователя Active Directory. Пользователь может использовать почтовый ящик для отправки и получения сообщений, а также для хранения сообщений, встреч, задач, заметок и документов. Для создания почтовых ящиков пользователя используйте Центр администрирования Exchange или командную консоль.

Вы также можете создавать почтовые ящики для существующих пользователей, у которых есть учетная запись Active Directory, но нет соответствующего почтового ящика. Этот процесс известен как *включение почтовых ящиков* для существующих пользователей.

## Что нужно знать перед началом работы

  - Предполагаемое время выполнения каждой задачи для почтового ящика пользователя: от 2 до 5 минут.

  - При создании нового почтового ящика пользователя в псевдониме или имени входа пользователя не допускаются апостроф (') или кавычки ("), так как эти знаки не поддерживаются. Если при создании нового почтового ящика использовать неподдерживаемые знаки, сообщение об ошибке может и не появиться, но эти знаки могут впоследствии стать причиной проблем. Например, пользователи, которым были предоставлены разрешения на доступ к почтовому ящику, созданному с использованием неподдерживаемых знаков, могут столкнуться с проблемами или непредсказуемым поведением почтового ящика.

  - Для выполнения этих процедур необходимы соответствующие разрешения. Сведения о необходимых разрешениях см. в статье Тема «Разрешения подготовки получателей» в разделе [Разрешения получателей](recipients-permissions-exchange-2013-help.md).

  - Сочетания клавиш для процедур, описанных в этой статье, приведены в статье [Сочетания клавиш в Центре администрирования Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]  
> Возникли проблемы? Обратитесь за помощью к участникам форумов, посвященных Exchange. Посетите форумы по таким продуктам: <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> или <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Что необходимо сделать?

## Создание почтового ящика пользователя

## Использование EAC для создания почтового ящика пользователя

1.  В Центре администрирования Exchange перейдите к разделу **Получатели** \> **Почтовые ящики**.

2.  Нажмите кнопку **Создать** \> **Почтовый ящик пользователя**.

3.  На странице **Новый почтовый ящик пользователя** в поле **Псевдоним** введите псевдоним пользователя, который будет являться псевдонимом электронной почты для пользователя. Псевдоним пользователя — это часть адреса электронной почты слева от символа (@). Псевдоним должен быть уникальным в пределах леса.
    
    > [!NOTE]  
    > Если вы оставите это поле пустым, для псевдонима электронной почты будет использовано значение из области имени пользователя поля <strong>Имя входа пользователя</strong>.


4.  Для этого выберите один из приведенных ниже вариантов.
    
      - **Существующий пользователь**   Выберите, чтобы включить поддержку почты и создать почтовый ящик для существующего пользователя.
        
        Нажмите кнопку **Обзор**, чтобы открыть диалоговое окно **Выбор пользователя — весь лес**. В данном диалоговом окне отображается список учетных записей тех пользователей Active Directory в данном лесу, для которых не была включена поддержка почты или которые не имеют почтовых ящиков Exchange. Выберите учетную запись пользователя, для которой необходимо включить поддержку почты, а затем нажмите кнопку **ОК**. При выборе этой опции не требуется указывать данные учетной записи пользователя, потому что они уже присутствуют в Active Directory.
    
      - **Новый пользователь**   Выберите, чтобы создать новую учетную запись пользователя в Active Directory и создать для этого пользователя почтовый ящик. В случае выбора этой опции необходимо указать необходимые данные учетной записи пользователя.
    
    > [!NOTE]  
    > Учетная запись Active Directory, связанная с почтовыми ящиками пользователя, должна находиться в том же лесу, что и сервер Exchange. Чтобы создать почтовый ящик для учетной записи пользователя, хранящейся в доверенном лесу, необходимо создать связанный почтовый ящик. См. раздел <a href="manage-linked-mailboxes-exchange-2013-help.md">Управление связанными почтовыми ящиками</a>.


5.  Если на шаге 4 выбран пункт **Новый пользователь**, на странице **Новый почтовый ящик пользователя** необходимо заполнить следующие поля. В противном случае перейдите к шагу 7.
    
      - **Имя**   В этом текстовом поле можно ввести имя пользователя.
    
      - **Инициалы**   В этом текстовом поле можно ввести инициалы пользователя.
    
      - **Фамилия**   В этом текстовом поле можно ввести фамилию пользователя.
    
      - \* **Отображаемое имя**   Поле для ввода отображаемого имени пользователя. Это имя указывается в списке почтовых ящиков в Центре администрирования Exchange и в общей адресной книге. По умолчанию в это поле добавляются имена, введенные в полях **Имя**, **Инициалы** и **Фамилия**. Если эти поля не используются, все равно необходимо ввести имя в это поле, поскольку оно является обязательным для заполнения. Длина имени не может превышать 64 символов.
    
      - \* **Имя**   Поле для ввода имени пользователя. Это имя, которое содержится в списке Active Directory. В это поле также добавляются имена, введенные в поля **Имя**, **Отчество** и **Фамилия**. Если эти поля не используются, все равно необходимо ввести имя в это поле, поскольку оно является обязательным для заполнения. Кроме того, длина имени не может превышать 64 символа.
    
      - **Подразделение**   Можно выбрать другое подразделение, кроме указанного по умолчанию (которое расположено в области получателя). Если область получателей установлена на уровне леса, будет установлено значение по умолчанию для контейнера "Пользователи" домена Active Directory, в котором находится компьютер с запущенным Центром администрирования Exchange. Если область получателей настроена на определенный домен, то контейнер пользователей в этом домене выбирается по умолчанию. Если в качестве области получателей задано определенное подразделение организации, то оно выбирается по умолчанию.
        
        Нажмите кнопку **Обзор**, чтобы выбрать другое подразделение. В этом диалоговом окне отображаются все подразделения в лесу, которые находятся внутри определенной области. Выберите необходимое подразделение и нажмите кнопку **ОК**.
    
      - \* **Имя входа пользователя**   В этом поле введите имя, которое пользователь будет использовать для входа в почтовый ящик и домен. Имя для входа у пользователя состоит из псевдонима пользователя, который находится слева от знака @, и суффикса справа от этого знака. Обычно в качестве суффикса выступает имя домена, в котором размещается учетная запись пользователя. Обратите внимание, что в имени входа пользователя не допускаются апостроф (') или кавычки ("), потому что эти знаки не поддерживаются.
        
        > [!NOTE]  
        > Если значение имени пользователя отличается от значения в поле <strong>Псевдоним</strong>, адрес электронной почты пользователя и имя входа пользователя будут отличаться.
    
      - \* **Новый пароль**   В это поле необходимо ввести пароль, с помощью которого пользователь входит в свой почтовый ящик.
        
        > [!NOTE]  
        > Убедитесь, что введенный пароль соответствует требованиям к длине, сложности и истории паролей, предъявляемым для домена, в котором создается учетная запись пользователя.
    
      - \* **Подтверждение пароля**   В этом поле нужно подтвердить пароль, введенный в поле **Пароль**.
    
      - **Потребовать смены пароля при следующем входе в систему**   Установите этот флажок, если необходимо, чтобы пользователь сменил пароль при первом входе в почтовый ящик.
        
        Если этот флажок установлен, при первом входе нового пользователя в систему будет отображено диалоговое окно, в котором можно изменить пароль. Пользователю не будет разрешено выполнять какие-либо задачи до тех пор, пока пароль не будет успешно изменен.

6.  Чтобы настроить следующие поля, нажмите кнопку **Дополнительные параметры**. В противном случае перейдите к шагу 7, чтобы сохранить новый почтовый ящик пользователя.
    
      - **Указание базы данных почтовых ящиков**   С помощью этой опции можно самостоятельно указать базу данных почтовых ящиков, а не оставлять выбор базы данных для вас серверу Exchange. Нажмите кнопку **Обзор**, чтобы открыть диалоговое окно **Выбор базы данных почтовых ящиков**. Это диалоговое окно содержит список всех баз данных почтовых ящиков в организации Exchange. По умолчанию базы данных почтовых ящиков отсортированы по имени. Чтобы отсортировать список баз данных по имени или версии сервера, щелкните заголовок соответствующего столбца. Выберите необходимую базу данных почтовых ящиков и нажмите кнопку **ОК**.
    
      - **Создание локального архивного хранилища для этого пользователя**   Установите этот флажок, чтобы создать для почтового ящика архивный почтовый ящик. При создании архивного почтового ящика элементы автоматически перемещаются из основного почтового ящика в архивный на основе параметров политики хранения по умолчанию или на основе параметров, указанных пользователем.
        
        Нажмите кнопку **Обзор**, чтобы выбрать базу данных, расположенную в локальном лесу, для хранения архивного почтового ящика.
        
        Дополнительные сведения см. в разделе [Архивация на месте в Exchange 2013](in-place-archiving-in-exchange-2013-exchange-2013-help.md).
    
      - **Политика адресных книг**   Используйте эту опцию, чтобы указать политику адресных книг для почтового ящика. Политики адресных книг содержат глобальный список адресов, автономную адресную книгу, список помещений и набор списков адресов. Политика адресных книг предоставляет пользователям почтовых ящиков, которым она назначается, доступ к настраиваемому глобальному списку адресов в Outlook и Outlook Web App. Дополнительные сведения см. в разделе [Политики адресных книг](address-book-policies-exchange-2013-help.md).
        
        Из раскрывающегося списка выберите политику, которую нужно сопоставить с этим почтовым ящиком.

7.  По завершении нажмите кнопку **Сохранить**, чтобы создать почтовый ящик.

## Использование консоли для создания почтового ящика пользователя

В этом примере создается новая учетная запись и почтовый ящик для пользователя Pilar Pinilla со следующими сведениями:

  - Псевдоним — pilarp

  - Имя — Pilar, фамилия — Pinilla

  - Имя и отображаемое имя — Pilar Pinilla

  - Имя входа пользователя — pilarp@contoso.com

  - Пароль— Pa$$word1

  - Почтовый ящик будет создан в подразделении по умолчанию. Чтобы указать другое подразделение, используйте параметр *OrganizationalUnit*.

<!-- end list -->

    New-Mailbox -Alias pilarp -Name "Pilar Pinilla" -FirstName Pilar -LastName Pinilla -DisplayName "Pilar Pinilla" -UserPrincipalName pilarp@contoso.com -Password (ConvertTo-SecureString -String 'Pa$$word1' -AsPlainText -Force)

Дополнительные сведения о синтаксисе и параметрах см. в разделе [New-Mailbox](https://technet.microsoft.com/ru-ru/library/aa997663\(v=exchg.150\)).

## Как проверить, что все получилось?

Чтобы проверить, успешно ли создан почтовый ящик пользователя, выполните одно из следующих действий.

  - В Центре администрирования Exchange перейдите к разделу **Получатели** \> **Почтовые ящики**. Новый почтовый ящик пользователя отображается в списке почтовых ящиков. В разделе **Тип почтового ящика** указан тип **Пользователь**.

  - В командной консоли Exchange выполните следующую команду для вывода информации о новом почтовом ящике пользователя.
    
        Get-Mailbox <Name> | FL Name,RecipientTypeDetails,PrimarySmtpAddress

## Создание почтового ящика для существующего пользователя

Вы также можете создавать почтовые ящики для существующих пользователей, у которых есть учетная запись Active Directory, но нет соответствующего почтового ящика. Этот процесс известен как *включение почтовых ящиков* для существующих пользователей. После включения поддержки почтового ящика для пользователя этот пользователь может отправлять и получать сообщения электронной почты.

## Использование EAC для создания почтового ящика для существующего пользователя

1.  В Центре администрирования Exchange перейдите к разделу **Получатели** \> **Почтовые ящики**.

2.  Нажмите кнопку **Создать** \> **Почтовый ящик пользователя**.

3.  На странице **Новый почтовый ящик пользователя** в поле **Псевдоним** введите псевдоним пользователя, который будет являться псевдонимом электронной почты для пользователя. Псевдоним пользователя — это часть адреса электронной почты слева от символа (@). Псевдоним должен быть уникальным в пределах леса.
    
    > [!NOTE]  
    > Если вы оставите это поле пустым, для псевдонима электронной почты будет использовано значение из области имени пользователя поля <strong>Имя входа пользователя</strong>.


4.  Нажмите кнопку **Существующий пользователь**.

5.  Нажмите кнопку **Обзор**, чтобы открыть диалоговое окно **Выбор пользователя — весь лес**. В данном диалоговом окне отображается список учетных записей тех пользователей Active Directory в данном лесу, для которых не была включена поддержка почты или которые не имеют почтовых ящиков Exchange. Выберите учетную запись пользователя, для которой необходимо включить поддержку почты, а затем нажмите кнопку **ОК**.
    
    При создании почтового ящика для существующего пользователя нет необходимости указывать данные учетной записи, так как эта информация уже существует в Active Directory.
    
    > [!NOTE]  
    > Учетная запись Active Directory, связанная с почтовыми ящиками пользователя, должна находиться в том же лесу, что и сервер Exchange. Чтобы создать почтовый ящик для учетной записи пользователя, хранящейся в доверенном лесу, необходимо создать связанный почтовый ящик. См. раздел <a href="manage-linked-mailboxes-exchange-2013-help.md">Управление связанными почтовыми ящиками</a>.


6.  Чтобы настроить следующие поля, нажмите кнопку **Дополнительные параметры**. В противном случае перейдите к шагу 7, чтобы сохранить новый почтовый ящик пользователя.
    
      - **Указание базы данных почтовых ящиков**   С помощью этой опции можно самостоятельно указать базу данных почтовых ящиков, а не оставлять выбор базы данных для вас серверу Exchange. Нажмите кнопку **Обзор**, чтобы открыть диалоговое окно **Выбор базы данных почтовых ящиков**. Это диалоговое окно содержит список всех баз данных почтовых ящиков в организации Exchange. По умолчанию базы данных почтовых ящиков отсортированы по имени. Чтобы отсортировать список баз данных по имени или версии сервера, щелкните заголовок соответствующего столбца. Выберите необходимую базу данных почтовых ящиков и нажмите кнопку **ОК**.
    
      - **Создание локального архивного хранилища для этого пользователя**   Установите этот флажок, чтобы создать для почтового ящика архивный почтовый ящик. При создании архивного почтового ящика элементы автоматически перемещаются из основного почтового ящика в архивный на основе параметров политики хранения по умолчанию или на основе параметров, указанных пользователем.
        
        Нажмите кнопку **Обзор**, чтобы выбрать базу данных, расположенную в локальном лесу, для хранения архивного почтового ящика.
        
        Дополнительные сведения см. в разделе [Архивация на месте в Exchange 2013](in-place-archiving-in-exchange-2013-exchange-2013-help.md).
    
      - **Политика адресных книг**   Используйте эту опцию, чтобы указать политику адресных книг для почтового ящика. Политики адресных книг содержат глобальный список адресов, автономную адресную книгу, список помещений и набор списков адресов. Политика адресных книг предоставляет пользователям почтовых ящиков, которым она назначается, доступ к настраиваемому глобальному списку адресов в Outlook и Outlook Web App. Дополнительные сведения см. в разделе [Политики адресных книг](address-book-policies-exchange-2013-help.md).
        
        Из раскрывающегося списка выберите политику, которую нужно сопоставить с этим почтовым ящиком.

7.  По завершении нажмите кнопку **Сохранить**, чтобы создать почтовый ящик.

## Использование командной консоли для создания почтового ящика существующего пользователя

В этом примере создается почтовый ящик для существующего пользователя в базе данных Exchange UsersMailboxDatabase с именем estherv@contoso.com.

    Enable-Mailbox estherv@contoso.com -Database UsersMailboxDatabase

Также командлет **Enable-Mailbox** используется для включения поддержки почты для нескольких пользователей. Это делается путем передачи по конвейеру результатов командлета **Get-User** в командлет **Enable-Mailbox**. При выполнении командлета **Get-User** необходимо возвращать только тех пользователей, для которых еще не включена поддержка почты. Для этого необходимо указать значение User с параметром *RecipientTypeDetails*. Также можно ограничить результаты, возвращаемые с помощью параметра *Filter*, чтобы запросить только тех пользователей, которые соответствуют указанным критериям. Затем результаты необходимо передать по конвейеру в командлет **Enable-Mailbox**.

Например, следующая команда включает поддержку почтовых ящиков для пользователей с выключенной поддержкой почты и заданным значением свойства **UserPrincipalName** — это позволяет гарантировать, что системные учетные записи не будут случайно преобразованы в почтовые ящики.

    Get-User -RecipientTypeDetails User -Filter { UserPrincipalName -ne $Null } | Enable-Mailbox

Сведения о синтаксисе и параметрах см. в разделах [Enable-Mailbox](https://technet.microsoft.com/ru-ru/library/aa998251\(v=exchg.150\)) и [Get-User](https://technet.microsoft.com/ru-ru/library/aa996896\(v=exchg.150\)).

Дополнительные сведения о конвейеризации см. в разделе [Конвейеризация](https://technet.microsoft.com/ru-ru/library/aa998260\(v=exchg.150\)).

## Как проверить, что все получилось?

Чтобы убедиться в том, что почтовый ящик для существующего пользователя успешно создан, выполните одно из следующих действий:

  - В Центре администрирования Exchange перейдите к разделу **Получатели** \> **Почтовые ящики**. Новый почтовый ящик пользователя отображается в списке почтовых ящиков. В разделе **Тип почтового ящика** указан тип **Пользователь**.

  - В командной консоли Exchange выполните следующую команду, чтобы отобразить данные о новом почтовом ящике.
    
        Get-Mailbox <Name> | FL Name,RecipientTypeDetails,PrimarySmtpAddress
    
    Обратите внимание, что значение свойства *RecipientTypeDetails* — `UserMailbox`.
