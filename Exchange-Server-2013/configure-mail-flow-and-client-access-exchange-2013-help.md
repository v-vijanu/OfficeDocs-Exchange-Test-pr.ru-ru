﻿---
title: 'Настройка потока обработки почты и клиентского доступа: Exchange 2013 Help'
TOCTitle: Настройка потока обработки почты и клиентского доступа
ms:assetid: 4acc7f2a-93ce-468c-9ace-d5f7eecbd8d4
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/JJ218640(v=EXCHG.150)
ms:contentKeyID: 50488009
ms.date: 04/30/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Настройка потока обработки почты и клиентского доступа

 

_**Применимо к:** Exchange Server 2013_

_**Последнее изменение раздела:** 2016-12-09_

Задачи, выполняемые после установки, для потока обработки почты и клиентского доступа в Exchange Server 2013, включая настройку SSL-сертификата.

После установки Microsoft Exchange Server 2013 в организации необходимо настроить Exchange Server 2013 для потока почты и клиентского доступа. Без этих шагов вы не сможете отправлять почту в Интернет, а внешние клиенты, такие как Microsoft Office Outlook и устройства с Exchange ActiveSync, не смогут подключаться к организации Exchange.

Действия, описанные в этом разделе, предполагают базовой развертывание Exchange с одним сайтом Active Directory и пространством имен SMTP.

> [!IMPORTANT]  
> В этом разделе используются примеры значений, например Ex2013CAS, contoso.com, mail.contoso.com и 172.16.10.11. Замените их значениями имен серверов, полных доменных имен и IP-адресов вашей организации.


Дополнительные сведения о задачах управления, связанные с потоком обработки почты, клиентами и устройствами, см. в разделах [Поток обработки почты](mail-flow-exchange-2013-help.md) и [Клиенты и мобильные устройства](clients-and-mobile-exchange-2013-help.md).

## Что нужно знать перед началом работы

  - Предполагаемое время выполнения задачи: 50 минут.

  - Для процедур в этом разделе требуются особые разрешения. См. информацию о разрешениях по каждой процедуре.

  - Вы можете получать предупреждения о сертификате при подключении к веб-сайту Центра администрирования Exchange, пока не настроите сертификат SSL на сервере клиентского доступа. Как это сделать, будет показано далее в этом разделе.

  - Сочетания клавиш для процедур, описанных в этой статье, приведены в статье [Сочетания клавиш в Центре администрирования Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!IMPORTANT]  
> Для каждой организации требуется как минимум один сервер клиентского доступа и один сервер почтовых ящиков в лесу Active Directory. Кроме того, каждый из узлов Active Directory, который содержит сервер почтовых ящиков, должен также содержать как минимум один сервер клиентского доступа. При разделении серверных ролей рекомендуем сначала установить роль сервера почтовых ящиков.


> [!TIP]  
> Возникли проблемы? Обратитесь за помощью к участникам форумов, посвященных Exchange. Посетите форумы по таким продуктам: <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> или <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Как это сделать

## Действие 1. Создание соединителя отправки.

Для выполнения этих процедур необходимы соответствующие разрешения. Сведения о необходимых разрешениях см. в статье запись "Соединители отправки" в статье [Разрешения потока обработки почты](mail-flow-permissions-exchange-2013-help.md).

Чтобы отправлять почту в Интернет, нужно создать соединитель отправки на сервере почтовых ящиков. Выполните следующие действия.

1.  Откройте Центр администрирования Exchange, перейдя к URL-адресу сервера клиентского доступа. Например, https://Ex2013CAS/ECP.

2.  Введите имя пользователя и пароль в соответствующих полях **Домен\\Имя пользователя** и **Пароль** и нажмите кнопку **Вход**.

3.  Перейдите в раздел **Поток почты** \> **Соединители отправки**. На странице **Соединители отправки** щелкните **Создать**![Значок добавления](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Значок добавления").

4.  В мастере **создания соединителя отправки** укажите имя соединителя отправки и выберите **Интернет**. Нажмите кнопку **Далее**.

5.  Убедитесь, что включен параметр **Запись MX, связанная с доменом получателя**. Нажмите кнопку **Далее**.

6.  В разделе **Адресное пространство** нажмите кнопку **Добавить**![Значок добавления](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Значок добавления"). В окне **Добавление домена** выберите **SMTP** в поле **Тип**. В поле **Полное доменное имя (FQDN)** введите **\***. Нажмите кнопку **Сохранить**.

7.  Убедитесь, что не включен параметр **Соединитель отправки с заданной областью**, и нажмите кнопку **Далее**.

8.  На вкладке **Исходный сервер** нажмите кнопку **Добавить**![Значок добавления](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Значок добавления"). В окне **Выбор сервера** выберите сервер почтовых ящиков. Выбрав сервер, щелкните **Добавить**, а затем — **ОК**.

9.  Нажмите кнопку **Готово**.

> [!NOTE]  
> При установке Exchange 2013 создается соединитель получения для входящих сообщений по умолчанию. Этот соединитель принимает анонимные подключения SMTP с внешних серверов. Вам'не требуется проводить какую-либо дополнительную настройку, если это вас устраивает. Если необходимо ограничить входящие подключения с внешних серверов, измените соединитель получения <strong>Интерфейс по умолчанию &lt;Сервер клиентского доступа&gt;</strong> на сервере клиентского доступа.


## Как проверить, что шаг выполнен?

Чтобы убедиться в том, что вы успешно создали исходящий соединитель отправки, выполните следующие действия:

1.  В EAC проверьте, что новый соединитель отправки отображается в разделе **Поток почты** \> **Соединители отправки**.

2.  Откройте Outlook Web App и отправьте сообщение электронной почты внешнему получателю. Если он получает это сообщение, то вы правильно настроили соединитель отправки.

## Действие 2. Добавление дополнительных обслуживаемых доменов

Для выполнения этих процедур необходимы соответствующие разрешения. Сведения о необходимых разрешениях см. в статье запись "Обслуживаемые домены" в разделе [Разрешения потока обработки почты](mail-flow-permissions-exchange-2013-help.md).

По умолчанию при развертывании новой организации Exchange 2013 в лесу Active Directory Exchange использует имя домена Active Directory, в котором была выполнена команда Setup /PrepareAD. Если необходимо, чтобы получатели получали и отправляли сообщения пользователям в другом домене, необходимо добавить его в качестве обслуживаемого. Этот домен также добавляется в качестве основного SMTP-адреса электронной почты по умолчанию политики адресов в следующем действии.

> [!IMPORTANT]  
> Для каждого домена SMTP, для которого необходимо принимать электронную почту из Интернета, требуется общедоступная запись ресурса MX службы доменных имен (DNS). Каждая запись MX должна разрешаться в сервер с выходом в Интернет, который получает электронную почту для организации.


1.  Откройте Центр администрирования Exchange, перейдя к URL-адресу сервера клиентского доступа. Например, https://Ex2013CAS/ECP.

2.  Введите имя пользователя и пароль в соответствующих полях **Домен\\Имя пользователя** и **Пароль** и нажмите кнопку **Вход**.

3.  Перейдите в раздел **Поток почты** \> **Обслуживаемые домены**. На странице **Обслуживаемые домены** щелкните **Создать**![Значок добавления](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Значок добавления").

4.  В мастере **создания обслуживаемых доменов** укажите имя обслуживаемого домена.

5.  В поле **Обслуживаемый домен** укажите домен получателя SMTP, который необходимо добавить, например contoso.com.

6.  Выберите пункт **Заслуживающий доверия домен** и нажмите кнопку **Сохранить**.

## Как проверить, что шаг выполнен?

Чтобы убедиться в том, что вы успешно создали обслуживаемый домен, выполните следующие действия:

  - В EAC проверьте, что новый домен отображается в разделе **Поток почты** \> **Обслуживаемые домены**.

## Действие 3. Настройка политики адресов электронной почты по умолчанию

Для выполнения этих процедур необходимы соответствующие разрешения. Сведения о необходимых разрешениях см. в статье запись "Политики адресов электронной почты" в статье [Разрешения для электронных адресов и адресных книг](email-address-and-address-book-permissions-exchange-2013-help.md).

Если вы добавили обслуживаемый домен на предыдущем шаге и хотите, чтобы он добавился для каждого получателя в организации, необходимо обновить политику адресов электронной почты по умолчанию.

1.  Откройте Центр администрирования Exchange, перейдя к URL-адресу сервера клиентского доступа. Например, https://Ex2013CAS/ECP.

2.  Введите имя пользователя и пароль в соответствующих полях **Домен\\Имя пользователя** и **Пароль** и нажмите кнопку **Вход**.

3.  Откройте раздел **Поток обработки почты** \> **Политики адресов электронной почты**. На странице **Политики адресов электронной почты** выберите **Политика по умолчанию**, а затем щелкните **Правка**![Значок редактирования](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Значок редактирования").

4.  На странице **Политика адресов электронной почты по умолчанию** щелкните **Формат адреса электронной почты**.

5.  В разделе **Формат электронной почты**, щелкните SMTP-адрес, который требуется изменить, а затем выберите пункт **Правка**![Значок редактирования](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Значок редактирования").

6.  На странице **Формат электронной почты** в поле **Параметры адреса электронной почты** укажите домен получателя SMTP, который необходимо применять ко всем получателям в организации Exchange. Этот домен должен соответствовать обслуживаемому домену, добавленному в предыдущем действии. Например, contoso.com. Щелкните **Сохранить**.

7.  Нажмите кнопку **Сохранить**.

8.  В области сведений **Политика по умолчанию** щелкните **Применить**.

> [!NOTE]  
> Рекомендуется настроить имя участника-пользователя, которое совпадает с основным адресом электронной почты каждого пользователя. Если не указать имя участника-пользователя, совпадающее с адресом электронной почты пользователя, пользователь будет вынужден вручную указать домен и имя пользователя или имя участника-пользователя в дополнение к адресу электронной почты. Если его UPN соответствует адресу электронной почты, Outlook Web App, ActiveSync и Outlook автоматически сопоставят адрес электронной почты и UPN.


## Как проверить, что шаг выполнен?

Чтобы убедиться, что вы успешно настроили политики адресов электронной почты по умолчанию, выполните следующие действия:

1.  В центре администрирования Exchange перейдите к разделу **Получатели** \> **Почтовые ящики**.

2.  Выберите почтовый ящик, а затем в области сведений о получателе убедитесь, что **Почтовый ящик пользователя** задан как *\<alias\>*@*\<new accepted domain\>*. Например, david@contoso.com.

3.  При необходимости создайте новый почтовый ящик и убедитесь, что его адрес электронной почты содержит новый обслуживаемый домен, выполнив следующие действия:
    
    1.  Перейдите в раздел **Получатели** \> **Почтовые ящики**, нажмите кнопку **Создать**![Значок добавления](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Значок добавления"), а затем выберите пункт **Почтовый ящик пользователя**.
    
    2.  На странице "Новый почтовый ящик пользователя" введите необходимые данные, чтобы создать новый почтовый ящик. Нажмите кнопку **Сохранить**.
    
    3.  Выберите почтовый ящик, а затем в области сведений о получателе убедитесь, что **Почтовый ящик пользователя** задан как *\<alias\>*@*\<new accepted domain\>*. Например, david@contoso.com.

## Действие 4. Настройка внешних URL-адресов

Для выполнения этих процедур необходимы соответствующие разрешения. Сведения о необходимых разрешениях см. в статье Раздел "Настройки виртуального каталога *\<Service\>*" в статье [Разрешения клиентов и мобильных устройств](clients-and-mobile-devices-permissions-exchange-2013-help.md).

Прежде чем клиенты смогут подключаться к новому серверу из Интернета, необходимо настроить внешние домены или URL-адреса в виртуальных каталогах сервера клиентского доступа, а затем настроить общедоступные записи службы доменных имен (DNS). Указанные ниже действия настраивают один и тот же внешний домен для внешних URL-адресов каждого виртуального каталога. Если вы хотите настроить другие внешние домены для внешних URL-адресов виртуального каталога, необходимо настроить внешние URL-адреса вручную. Подробнее см. в разделе [Управление виртуальным каталогом](virtual-directory-management-exchange-2013-help.md).

1.  Откройте Центр администрирования Exchange, перейдя к URL-адресу сервера клиентского доступа. Например, https://Ex2013CAS/ECP.

2.  Введите имя пользователя и пароль в соответствующих полях **Домен\\Имя пользователя** и **Пароль** и нажмите кнопку **Вход**.

3.  Откройте раздел **Серверы** \> **Серверы**, выберите имя сервера клиентского доступа, доступного из Интернета, а затем нажмите **Правка**![Значок редактирования](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Значок редактирования").

4.  Щелкните **Мобильный Outlook**.

5.  В поле **Укажите внешнее имя узла** укажите доступное извне полное доменное имя сервера клиентского доступа. Например, mail.contoso.com.

6.  Пользуясь случаем, можно также установить внутренне доступное полное доменное имя сервера клиентского доступа. В поле **Укажите внутреннее имя узла** вставьте полное доменное имя, которое использовалось в предыдущем шаге. Например, mail.contoso.com.

7.  Нажмите кнопку **Сохранить**.

8.  Перейдите к разделу **Серверы** \> **Виртуальные каталоги**, затем щелкните **Настроить домен внешнего доступа**![Значок конфигурации](images/JJ218640.a9c33f23-3d44-44e7-a5d0-8446200c746e(EXCHG.150).gif "Значок конфигурации").

9.  В разделе **Выберите серверы клиентского доступа для использования с внешним URL-адресом** щелкните **Добавить**![Значок добавления](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Значок добавления")

10. Выберите серверы клиентского доступа, которые требуется настроить, и щелкните **Добавить**. Добавив все серверы клиентского доступа, которые нужно настроить, щелкните **ОК**.

11. В поле **Введите имя домена, которое будет использоваться для внешних серверов клиентского доступа** введите внешний домен, который необходимо применить. Например, mail.contoso.com. Нажмите кнопку **Сохранить**.
    
    > [!NOTE]  
    > Некоторые организации делают полное доменное имя Outlook Web App уникальным, чтобы защитить пользователей от изменений, вызванных изменениями в полном доменном имени базового сервера. Много организаций используют в качестве полного доменного имени Outlook Web App owa.contoso.com вместо mail.contoso.com. Если вы хотите настроить уникальное полное доменное имя Outlook Web App, выполните следующие действия после завершения предыдущего шага. Этот контрольный список предполагает, что вы настроили уникальное полное доменное имя Outlook Web App.
    <ol>
    <li><p>Выберите <strong>owa (веб-сайт по умолчанию)</strong> и щелкните <strong>Редактировать</strong> <img src="images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif" title="Значок редактирования" alt="Значок редактирования" />.</p></li>
    <li><p>В поле <strong>Внешний URL-адрес</strong> введите <strong>https://</strong>, затем уникальное полное доменное имя Outlook Web App, которое будет использоваться, после чего добавьте <strong>/owa</strong>. Например, https://owa.contoso.com/owa.</p></li>
    <li><p>Нажмите кнопку <strong>Сохранить</strong>.</p></li>
    <li><p>Выберите <strong>ecp (веб-сайт по умолчанию)</strong> и щелкните <strong>Редактировать</strong> <img src="images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif" title="Значок редактирования" alt="Значок редактирования" />.</p></li>
    <li><p>В поле <strong>Внешний URL-адрес</strong> введите <strong>https://</strong>, затем такое же полное доменное имя Outlook Web App, которое было указано в предыдущем шаге, после чего добавьте <strong>/ecp</strong>. Например, https://owa.contoso.com/ecp.</p></li>
    <li><p>Нажмите кнопку <strong>Сохранить</strong>.</p></li>
    </ol>


Настроив внешний URL-адрес в виртуальных каталогах сервера клиентского доступа, необходимо настроить общедоступные DNS-записи для автообнаружения, Outlook Web App и потока обработки почты. Общедоступные DNS-записи должны указывать на внешний IP-адрес или полное доменное имя сервера клиентского доступа, доступного из Интернета, и использовать доступные извне полные доменные имена, настроенные на сервере клиентского доступа. Ниже приведены примеры рекомендуемых записей DNS, которые необходимо создать для обеспечения потока почты и подключения внешних клиентов.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Полное доменное имя</th>
<th>Тип записи DNS</th>
<th>Значение</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Contoso.com</p></td>
<td><p>MX</p></td>
<td><p>Mail.contoso.com</p></td>
</tr>
<tr class="even">
<td><p>Mail.contoso.com</p></td>
<td><p>A</p></td>
<td><p>172.16.10.11</p></td>
</tr>
<tr class="odd">
<td><p>Owa.contoso.com</p></td>
<td><p>CNAME</p></td>
<td><p>Mail.contoso.com</p></td>
</tr>
<tr class="even">
<td><p>Autodiscover.contoso.com</p></td>
<td><p>CNAME</p></td>
<td><p>Mail.contoso.com</p></td>
</tr>
</tbody>
</table>


## Как проверить, что шаг выполнен?

Чтобы убедиться, что вы успешно настроили внешний URL-адрес в виртуальных каталогах сервера клиентского доступа, выполните следующие действия.

1.  В Центре администрирования Exchange последовательно выберите пункты **Серверы** \> **Виртуальные каталоги**.

2.  В поле **Выберите сервер** выберите сервер клиентского доступа с выходом в Интернет.

3.  Выберите виртуальный каталог, а затем в области сведений, убедитесь, что поле **Внешний URL-адрес** содержит правильное полное доменное имя, как показано ниже:
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Виртуальный каталог</th>
    <th>Значение внешнего URL-адреса</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><strong>Автообнаружение</strong></p></td>
    <td><p>Внешний URL-адрес не отображается</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>ECP</strong></p></td>
    <td><p>https://owa.contoso.com/ecp</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>EWS</strong></p></td>
    <td><p>https://mail.contoso.com/EWS/Exchange.asmx</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>Microsoft-Server-ActiveSync</strong></p></td>
    <td><p>https://mail.contoso.com/Microsoft-Server-ActiveSync</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>OAB</strong></p></td>
    <td><p>https://mail.contoso.com/OAB</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>OWA</strong></p></td>
    <td><p>https://owa.contoso.com/owa</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>PowerShell</strong></p></td>
    <td><p>http://mail.contoso.com/PowerShell</p></td>
    </tr>
    </tbody>
    </table>


Чтобы убедиться, что общедоступные DNS-записи успешно настроены, выполните следующие действия.

1.  Откройте командную строку и выполните `nslookup.exe`.

2.  Измените значение на DNS-сервер, который может обращаться с запросами к общедоступной зоне DNS.

3.  В `nslookup` найдите запись для всех созданных полных доменных имен. Убедитесь, что для каждого полного доменного имени возвращается правильное значение.

4.  В `nslookup` введите `set type=mx`, а затем найдите обслуживаемый домен, добавленный на шаге 1. Убедитесь, что возвращенное значение соответствует полному доменному имени сервера клиентского доступа.

## Действие 5. Настройка внутренних URL-адресов

Для выполнения этих процедур необходимы соответствующие разрешения. Сведения о необходимых разрешениях см. в статье Раздел "Настройки виртуального каталога *\<Service\>*" в статье [Разрешения клиентов и мобильных устройств](clients-and-mobile-devices-permissions-exchange-2013-help.md).

Прежде чем клиенты смогут подключаться к новому серверу из вашей интрасети, необходимо настроить внутренние домены или URL-адреса в виртуальных каталогах сервера клиентского доступа, а затем настроить частные записи службы доменных имен (DNS).

Выполнив описанные ниже действия, вы сможете выбрать, нужно ли пользователям использовать одинаковый URL-адрес для доступа к серверу Exchange в интрасети и Интернете либо следует ли им использовать разные URL-адреса. Это решение зависит от существующей схемы адресации или от схемы, которую вы хотите внедрить. Если внедряется новая схема адресации, мы советуем использовать одинаковый URL-адрес для внутренних и внешних URL-адресов. Использование одинаковых URL-адресов упрощает пользователям доступ к серверу Exchange, поскольку им необходимо будет запомнить только один адрес. Независимо от вашего решения необходимо настроить частную зону DNS для настраиваемого адресного пространства. Дополнительные сведения об администрировании зон DNS см. в разделе [Администрирование DNS-сервера](http://go.microsoft.com/fwlink/p/?linkid=190631).

Дополнительные сведения о внутренних и внешних URL-адресах в виртуальных каталогах см. в разделе [Управление виртуальным каталогом](virtual-directory-management-exchange-2013-help.md).

## Настройка одинаковых внутреннего и внешнего URL-адресов

1.  Откройте консоль управления Exchange на сервере клиентского доступа.

2.  Сохраните имя узла сервера клиентского доступа в переменной, которая будет использоваться в следующем шаге. Например, Ex2013CAS.
    
        $HostName = "Ex2013CAS"

3.  Выполните следующие команды в консоли для настройки внутренних URL-адресов таким образом, чтобы они совпадали с внешним URL-адресом виртуального каталога.
    
        Set-EcpVirtualDirectory "$HostName\ECP (Default Web Site)" -InternalUrl ((Get-EcpVirtualDirectory "$HostName\ECP (Default Web Site)").ExternalUrl)
        
        Set-WebServicesVirtualDirectory "$HostName\EWS (Default Web Site)" -InternalUrl ((get-WebServicesVirtualDirectory "$HostName\EWS (Default Web Site)").ExternalUrl)
        
        Set-ActiveSyncVirtualDirectory "$HostName\Microsoft-Server-ActiveSync (Default Web Site)" -InternalUrl ((Get-ActiveSyncVirtualDirectory "$HostName\Microsoft-Server-ActiveSync (Default Web Site)").ExternalUrl)
        
        Set-OabVirtualDirectory "$HostName\OAB (Default Web Site)" -InternalUrl ((Get-OabVirtualDirectory "$HostName\OAB (Default Web Site)").ExternalUrl)
        
        Set-OwaVirtualDirectory "$HostName\OWA (Default Web Site)" -InternalUrl ((Get-OwaVirtualDirectory "$HostName\OWA (Default Web Site)").ExternalUrl)
        
        Set-PowerShellVirtualDirectory "$HostName\PowerShell (Default Web Site)" -InternalUrl ((Get-PowerShellVirtualDirectory "$HostName\PowerShell (Default Web Site)").ExternalUrl)

4.  Не выходите из командной консоли. Настройте там автономную адресную книгу так, чтобы служба автообнаружения могла выбрать нужный виртуальный каталог для ее распространения. Для этого выполните приведенные ниже команды.
    
        Get-OfflineAddressBook | Set-OfflineAddressBook -GlobalWebDistributionEnabled $True -VirtualDirectories $Null

После настройки внутреннего URL-адреса в виртуальных каталогах сервера клиентского доступа необходимо настроить частные записи DNS для Outlook Web App и других возможностей подключения. В зависимости от конфигурации нужно будет настроить частные DNS-записи так, чтобы они указывали на внутренний или внешний IP-адрес либо полное доменное имя сервера клиентского доступа. Ниже приведены примеры рекомендуемых DNS-записей, которые необходимо создать для подключения внутренних клиентов.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>FQDN</th>
<th>Тип записи DNS</th>
<th>Значение</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Mail.contoso.com</p></td>
<td><p>CNAME</p></td>
<td><p>Ex2013CAS.corp.contoso.com</p></td>
</tr>
<tr class="even">
<td><p>Owa.contoso.com</p></td>
<td><p>CNAME</p></td>
<td><p>Ex2013CAS.corp.contoso.com</p></td>
</tr>
</tbody>
</table>


## Как проверить, что шаг выполнен?

Чтобы убедиться, что вы успешно настроили внутренний URL-адрес в виртуальных каталогах сервера клиентского доступа, выполните следующие действия.

1.  В центре администрирования Exchange последовательно выберите пункты **Серверы** \> **Виртуальные каталоги**.

2.  В поле **Выберите сервер** выберите сервер клиентского доступа с выходом в Интернет.

3.  Выберите виртуальный каталог и щелкните **Редактировать** ![Значок редактирования](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Значок редактирования").

4.  Проверьте, чтобы в поле **Внутренний URL-адрес** было указано правильное полное доменное имя и служба, как показано ниже:
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Виртуальный каталог</th>
    <th>Значение внутреннего URL-адреса</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><strong>Автообнаружение</strong></p></td>
    <td><p>Внутренний URL-адрес не отображается</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>ECP</strong></p></td>
    <td><p>https://owa.contoso.com/ecp</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>EWS</strong></p></td>
    <td><p>https://mail.contoso.com/EWS/Exchange.asmx</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>Microsoft-Server-ActiveSync</strong></p></td>
    <td><p>https://mail.contoso.com/Microsoft-Server-ActiveSync</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>OAB</strong></p></td>
    <td><p>https://mail.contoso.com/OAB</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>OWA</strong></p></td>
    <td><p>https://owa.contoso.com/owa</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>PowerShell</strong></p></td>
    <td><p>http://mail.contoso.com/PowerShell</p></td>
    </tr>
    </tbody>
    </table>


Чтобы убедиться, что частные DNS-записи успешно настроены, выполните следующие действия.

1.  Откройте командную строку и выполните `nslookup.exe`.

2.  Измените значение на DNS-сервер, который может обращаться с запросами к частной зоне DNS.

3.  В `nslookup` найдите запись для всех созданных полных доменных имен. Убедитесь, что для каждого полного доменного имени возвращается правильное значение.

## Настройка различных внутренних и внешних URL-адресов

1.  Откройте центр администрирования Exchange, перейдя к URL-адресу сервера клиентского доступа. Например, https://Ex2013CAS/ECP.

2.  Перейдите к пунктам **Серверы** \> **Виртуальные каталоги**.

3.  В поле **Выберите сервер** выберите сервер клиентского доступа с выходом в Интернет.

4.  Выберите виртуальный каталог, который нужно изменить, и щелкните **Редактировать**![Значок редактирования](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Значок редактирования").

5.  В поле **Внутренний URL-адрес** замените имя узла между **https://** и первой косой чертой (**/** ) на новое полное доменное имя, которое будет использоваться. Например, если нужно изменить полное доменное имя виртуального каталога EWS с Ex2013CAS.corp.contoso.com на internal.contoso.com, измените внутренний URL-адрес с https://Ex2013CAS.corp.contoso.com/ews/exchange.asmx на https://internal.contoso.com/ews/exchange.asmx.

6.  Нажмите кнопку **Сохранить**.

7.  Повторите шаги 5 и 6 для каждого виртуального каталога, который необходимо изменить.
    
    > [!NOTE]  
    > Внутренние URL-адреса виртуальных каталогов ECP и OWA должны быть одинаковыми.<br />
    Невозможно установить внутренний URL-адрес в виртуальном каталоге автообнаружения.


8.  И, наконец, нам необходимо открыть командную консоль и настроить автономную адресную книгу, чтобы разрешить автообнаружению выбирать правильный виртуальный каталог для распространения автономной адресной книги. Чтобы сделать это, выполните указанные ниже команды.
    
        Get-OfflineAddressBook | Set-OfflineAddressBook -GlobalWebDistributionEnabled $True -VirtualDirectories $Null

После настройки внутреннего URL-адреса в виртуальных каталогах сервера клиентского доступа необходимо настроить частные записи DNS для Outlook Web App и других возможностей подключения. В зависимости от конфигурации нужно будет настроить частные DNS-записи так, чтобы они указывали на внутренний или внешний IP-адрес либо полное доменное имя сервера клиентского доступа. Ниже приведен пример рекомендуемой DNS-записи, которую следует создать для подключения внутренних клиентов, если внутренние URL-адреса виртуального каталога настроены для использования internal.contoso.com.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>FQDN</th>
<th>Тип записи DNS</th>
<th>Значение</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>internal.contoso.com</p></td>
<td><p>CNAME</p></td>
<td><p>Ex2013CAS.corp.contoso.com</p></td>
</tr>
</tbody>
</table>


## Как проверить, что шаг выполнен?

Чтобы убедиться, что вы успешно настроили внутренний URL-адрес в виртуальных каталогах сервера клиентского доступа, выполните следующие действия.

1.  В центре администрирования Exchange последовательно выберите пункты **Серверы** \> **Виртуальные каталоги**.

2.  В поле **Выберите сервер** выберите сервер клиентского доступа с выходом в Интернет.

3.  Выберите виртуальный каталог и щелкните **Редактировать** ![Значок редактирования](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Значок редактирования").

4.  Проверьте, чтобы в поле **Внутренний URL-адрес** было указано правильное полное доменное имя. Например, вы настроили внутренние URL-адреса для использования internal.contoso.com.
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Виртуальный каталог</th>
    <th>Значение внутреннего URL-адреса</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><strong>Автообнаружение</strong></p></td>
    <td><p>Внутренний URL-адрес не отображается</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>ECP</strong></p></td>
    <td><p>https://internal.contoso.com/ecp</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>EWS</strong></p></td>
    <td><p>https://internal.contoso.com/EWS/Exchange.asmx</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>Microsoft-Server-ActiveSync</strong></p></td>
    <td><p>https://internal.contoso.com/Microsoft-Server-ActiveSync</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>OAB</strong></p></td>
    <td><p>https://internal.contoso.com/OAB</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>OWA</strong></p></td>
    <td><p>https://internal.contoso.com/owa</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>PowerShell</strong></p></td>
    <td><p>http://internal.contoso.com/PowerShell</p></td>
    </tr>
    </tbody>
    </table>


Чтобы убедиться, что частные DNS-записи успешно настроены, выполните следующие действия.

1.  Откройте командную строку и выполните `nslookup.exe`.

2.  Измените значение на DNS-сервер, который может обращаться с запросами к частной зоне DNS.

3.  В `nslookup` найдите запись для всех созданных полных доменных имен. Убедитесь, что для каждого полного доменного имени возвращается правильное значение.

## Действие 6. Настройка SSL-сертификата

Для выполнения этих процедур необходимы соответствующие разрешения. Сведения о необходимых разрешениях см. в статье запись "Управление сертификатами" в статье [Разрешения потока обработки почты](mail-flow-permissions-exchange-2013-help.md).

Некоторые службы, такие как мобильный Outlook и Exchange ActiveSync, требуют настройки сертификатов на сервере Exchange 2013. Следующие шаги описывают, как настроить SSL-сертификат от стороннего центра сертификации (ЦС):

1.  Откройте Центр администрирования Exchange, перейдя к URL-адресу сервера клиентского доступа. Например, https://Ex2013CAS/ECP.

2.  Введите имя пользователя и пароль в соответствующих полях **Домен\\Имя пользователя** и **Пароль** и нажмите кнопку **Вход**.

3.  Откройте раздел **Серверы** \> **Сертификаты**. На странице **Сертификаты** убедитесь, что ваш сервер клиентского доступа выбран в поле **Выберите сервер**, а затем щелкните **Создать**![Значок добавления](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Значок добавления").

4.  В мастере **создания сертификата Exchange** выберите параметр **Создать запрос на сертификат из центра сертификации** и нажмите **Далее**.

5.  Укажите имя для этого сертификата, а затем щелкните **Далее**.

6.  Чтобы запросить сертификат с подстановочным знаком, выберите **Запросить сертификат с подстановочным знаком**, а затем укажите корневой домен всех поддоменов в поле **Корневой домен**. Если не требуется запрашивать сертификат с подстановочным знаком, а вместо этого необходимо указать каждый домен, который нужно добавить к сертификату, оставьте эту страницу незаполненной. Нажмите кнопку **"Далее"**.

7.  Щелкните **Обзор** и укажите сервер Exchange Server для хранения сертификата. Это должен быть сервер клиентского доступа с выходом в Интернет. Нажмите кнопку **"Далее"**.

8.  Для каждой службы в списке проверьте правильность внешних или внутренних имен сервера, которые будут использоваться пользователями для подключения к серверу Exchange. Например:
    
      - Если внутренний и внешний URL-адреса совпадают, в **Outlook Web App (при доступе через Интернет)** и **Outlook Web App (при доступе через интрасеть)** будет показан адрес owa.contoso.com. В **автономной адресной книге (при доступе через Интернет)** и **автономной адресной книге (при доступе через интрасеть)** будет показан адрес mail.contoso.com.
    
      - Если заданы внутренние URL-адреса формата internal.contoso.com, в **Outlook Web App (при доступе через Интернет)** будет показан адрес owa.contoso.com, а в **Outlook Web App (при доступе через интрасеть)** — адрес internal.contoso.com.
    
    Эти домены будут использоваться при создании запроса SSL-сертификата. Нажмите кнопку **"Далее"**.

9.  Добавьте все дополнительные домены, которые необходимо включить в SSL-сертификат.

10. Выберите домен, который будет общим именем для сертификата, а затем щелкните **Установить как общее имя**. Например, contoso.com. Щелкните **Далее**.

11. Предоставьте информацию о вашей организации. Эта информация будет включена в SSL-сертификат. Нажмите кнопку **Далее**.

12. Укажите сетевое расположение, где будет сохранен этот запрос сертификата. Нажмите кнопку **Готово**.

После сохранения запроса сертификата отправьте запрос в центр сертификации. Это может быть внутренний центр сертификации или сторонний центр сертификации в зависимости от политики организации. Клиенты, подключающиеся к серверу клиентского доступа, должны доверять центру, который вы используете. После получения сертификата из центра сертификации выполните следующие действия:

1.  На странице **Сервер** \> **Сертификаты** в EAC выберите запрос сертификата, созданный на предыдущих шагах.

2.  В области сведений о запросе сертификата щелкните **Завершено** в разделе **Состояние**.

3.  На странице выполнения ожидающего запроса укажите путь к файлу SSL-сертификата и нажмите **ОК**.

4.  Выберите новый сертификат, который вы только что добавили, а затем щелкните **Правка**![Значок редактирования](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Значок редактирования").

5.  На странице сертификата щелкните **Службы**.

6.  Выберите службы, которые необходимо назначить данному сертификату. Как минимум необходимо выбрать **SMTP** и **IIS**. Нажмите кнопку **Сохранить**.

7.  Если возникает предупреждение **Перезаписать существующий сертификат SMTP по умолчанию?**, щелкните **Да**.

## Как проверить, что шаг выполнен?

Чтобы убедиться в том, что вы успешно добавили новый сертификат, выполните следующие действия:

1.  В центре администрирования Exchange последовательно выберите пункты **Серверы** \> **Сертификаты**.

2.  Выберите новый сертификат и затем в области сведений убедитесь, что выполнены следующие условия:
    
      - значение параметра **Состояние** равно **Действительный**;
    
      - в поле **Назначен службам** указаны как минимум **IIS** и **SMTP**.

## Как проверить, что это работает?

Чтобы убедиться, что вы настроили поток почты и внешний клиентский доступ, выполните следующие действия:

1.  Создайте новый профиль в приложении Outlook и/или на устройстве ActiveSync. Убедитесь, что новый профиль успешно создается в Outlook или на мобильном устройстве.

2.  В Outlook или на мобильном устройстве отправьте новое сообщение внешнему получателю. Убедитесь, что внешний получатель получил сообщение.

3.  В почтовом ящике внешнего получателя ответьте на сообщение, отправленное из почтового ящика Exchange. Убедитесь, что сообщение успешно доставлено в почтовый ящик Exchange.

4.  Перейдите по адресу https://owa.contoso.com/owa, чтобы убедиться в отсутствии предупреждений сертификата.
