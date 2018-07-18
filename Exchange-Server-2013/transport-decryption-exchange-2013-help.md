﻿---
title: 'Расшифровка транспорта: Exchange 2013 Help'
TOCTitle: Расшифровка транспорта
ms:assetid: 4267c46d-f488-404d-a5cb-51f9127461c0
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/Dd638122(v=EXCHG.150)
ms:contentKeyID: 50487901
ms.date: 04/30/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Расшифровка транспорта

 

_**Применимо к:** Exchange Server 2013_

_**Последнее изменение раздела:** 2015-04-07_

В Microsoft Exchange Server 2013, Microsoft Outlook 2010 и более поздних версиях, а также Microsoft Office Outlook Web App для защиты сообщений используется служба управления правами на доступ к данным (IRM). Можно создавать правила защиты Outlook, чтобы автоматически применять защиту службы управления правами на доступ к данным к сообщениям перед их отправкой из клиента Outlook 2010. Кроме того, можно создать правила защиты транспорта для применения защиты с использованием управления правами на доступ к данным к сообщениям в пути, которые соответствуют условиям правила. Расшифровка транспорта обеспечивает доступ к содержимому сообщений, защищенному службой IRM, для применения политик обмена сообщениями.

Для задач управления, связанных со службой управления правами на доступ к данным, см. раздел [Сведения о процедуры управления правами](information-rights-management-procedures-exchange-2013-help.md).

## Ограничения других решений шифрования

Если в организации необходимо обеспечить защиту конфиденциальных сведений, в том числе сведений о важных бизнес-задачах и персональных данных, используйте функцию шифрования сообщений и вложений электронной почты. Существуют различные решения шифрования электронной почты, например S/MIME. Подобные решения шифрования применяются в большей или меньшей степени в различных типах организаций. Однако такие решения представляют следующие проблемы.

  - **Невозможность применять политики обмена сообщениями**   В организациях действуют требования законодательства, согласно которым необходимо проверять содержимое сообщений на соответствие политикам обмена сообщениями. Тем не менее, шифрование сообщений с помощью большинства клиентских решений шифрования, в том числе S/MIME, не позволяет проверять содержимое сообщений на сервере. Без проверки содержимого в организации невозможно будет определить соответствие всех отправленных и полученных ее пользователями сообщений политикам обмена сообщениями. Например, в соответствии с требованием закона настроено правило транспорта, предписывающее определение персональных данных, например номера социального страхования, и автоматическое применение заявления об отказе к сообщению. Если сообщение зашифровано, агент правил транспорта в службе транспорта не сможет получить доступ к содержимому сообщения и применить заявление об отказе. Это приводит к нарушению политики.

  - **Уменьшение уровня защиты**   Антивирусное программное обеспечение не позволяет проверять содержимое зашифрованных сообщений, в результате чего организация становится более уязвимой для атак со стороны вредоносного ПО, например вирусов и червей. Обычно большинство пользователей доверяет содержимому зашифрованных сообщений, в результате чего повышается вероятность распространения вирусов в организации. Например, настроено правило защиты Outlook, предписывающее автоматическое применение защиты службы управления правами на доступ к данным ко всем сообщениям, отправляемым по списку рассылки "Все сотрудники" с шаблоном службы управления правами "Служебное, конфиденциальное". Рабочая станция пользователя заражена вирусом, который распространяется в результате автоматического использования параметра "Ответить всем" для ответа на сообщения. Если сообщение, содержащее вирус, зашифровано, антивирусная программа не сможет проверить это сообщение.

  - **Влияние на пользовательские агенты транспорта**   Организации обычно развертывают пользовательские агенты транспорта в различных целях, например для выполнения требований дополнительной обработки для обеспечения соответствия, безопасности или маршрутизации настраиваемых сообщений. Пользовательские агенты транспорта, развертываемые организациями для проверки или изменения сообщений, не позволяют обрабатывать зашифрованные сообщения. Если развернутые в организации пользовательские агенты транспорта не позволяют получать доступ к содержимому сообщения, шифрование сообщений может препятствовать достижению организацией целей, для которых эти пользовательские агенты развернуты.

## Использование средства расшифровки транспорта для зашифрованного содержимого

В Exchange 2013 служба управления правами на доступ к данным позволяет решить эти проблемы. Если сообщения защищены с помощью службы IRM, функция расшифровки транспорта позволяет расшифровывать их при передаче. Такие сообщения можно расшифровать с помощью агента расшифровки, который является агентом транспорта, ориентированным на проверку соответствия.

> [!NOTE]  
> Агент расшифровки встроен в Exchange 2013. Встроенные агенты не включаются в список агентов, возвращаемых командлетом <strong>Get-TransportAgent</strong>. Дополнительные сведения см. в разделе <a href="transport-agents-exchange-2013-help.md">Агенты транспорта</a>.


Агент расшифровки позволяет расшифровать следующие типы сообщений, защищенных с помощью службы управления правами на доступ к данным.

  - Сообщения, для которых пользователь Outlook Web App установил защиту с помощью службы управления правами на доступ к данным.

  - Сообщения, для которых пользователь Outlook 2010 установил защиту с помощью службы управления правами на доступ к данным.

  - Сообщения, для которых защита с помощью службы IRM автоматически установлена в Exchange 2013 и Outlook 2010 с помощью правил защиты Outlook.

> [!IMPORTANT]  
> Агент расшифровки позволяет расшифровывать только сообщения, для которых защита с помощью службы управления правами на доступ к данным установлена в организации сервером службы управления правами Active Directory (AD RMS).


> [!NOTE]  
> Агент расшифровки может сохранять сообщения, защищенные при передаче с помощью правил защиты транспорта, в зашифрованном виде. Агент расшифровки запускается для событий транспорта <strong>OnEndOfData</strong> и <strong>OnSubmit</strong>. Правила защиты транспорта применяются агентом правил транспорта, который запускается для события <strong>OnRoutedMessage</strong>, а защита с помощью службы управления правами на доступ к данным применяется агентом шифрования для события <strong>OnRoutedMessage</strong>. Дополнительные сведения об агентах транспорта и список событий SMTP, для которых они зарегистрированы, см. в разделе <a href="transport-agents-exchange-2013-help.md">Агенты транспорта</a>.


Расшифровка транспорта выполняется первой в лесу Active Directory службой транспорта Exchange 2013, обрабатывающей сообщение. Если сообщение пересылается в службу транспорта в другом лесу Active Directory, оно повторно расшифровывается. После расшифровки незашифрованное содержимое доступно другим агентам транспорта на этом сервере. Например, агент правил транспорта в службе транспорта может проверить содержимое сообщения и применить к нему правила транспорта. К незашифрованному сообщению можно применить любые действия, указанные в правиле, например применить заявление об отказе или изменить сообщение другим способом. Сторонние агенты транспорта, например антивирусные программы, могут проверять сообщение на наличие вирусов и вредоносного содержимого. После проверки сообщения другими агентами транспорта и возможного его изменения выполняется повторное шифрование этого сообщения с помощью тех прав пользователя, которые существовали до расшифровки сообщения агентом расшифровки. Это сообщение не расшифровывается повторно другими службами транспорта на серверах почтовых ящиков в организации.

Для отправки сообщений, расшифрованных агентом расшифровки, из службы транспорта необходимо их повторное шифрование. Если при расшифровке или шифровании сообщения возвращается сообщение о временной ошибке, служба транспорта повторно выполняет операцию. После третьего сбоя ошибка будет рассматриваться как постоянная. При возникновении постоянной ошибки, а также если временная ошибка становится постоянной после нескольких повторов, служба транспорта обрабатывает сообщения следующим образом.

  - Если постоянная ошибка происходит во время расшифровки, зашифрованное сообщение отправляется с отчетом о недоставке (отчет о недоставке отправляется, только если для расшифровки транспорта установлено значение `Mandatory`). Дополнительные сведения о параметрах конфигурации, доступных для расшифровки транспорта, см. в подразделе Настройка расшифровки транспорта далее в этом разделе.

  - Если постоянная ошибка происходит во время повторного шифрования, отчет о недоставке всегда отправляется без расшифрованного сообщения.

> [!IMPORTANT]  
> Все пользовательские или сторонние агенты, установленные в службе транспорта, получают доступ к расшифрованному сообщению. Необходимо учитывать поведение таких агентов транспорта. Рекомендуется проверить работу всех пользовательских и сторонних агентов транспорта перед их развертыванием в рабочей среде.<br />
Если после расшифровки сообщения агентом расшифровки агент транспорта создает новое сообщение и добавляет (прикрепляет) к нему исходное сообщение, защита будет применяться только к новому сообщению. Исходное сообщение, которое становится вложением в новое сообщении, повторно не шифруется. Получатель такого сообщения может открыть вложенное сообщение и выполнить по отношению к нему определенное действие, например переслать или ответить, независимо от наличия прав.


## Настройка расшифровки транспорта

Службу расшифровки транспорта можно настроить с помощью командлета [Set-IRMConfiguration](https://technet.microsoft.com/ru-ru/library/dd979792\(v=exchg.150\)) в командной консоли Exchange. Тем не менее, чтобы настроить расшифровку транспорта, необходимо предоставить серверам Exchange 2013 разрешение на расшифровку содержимого, защищенного сервером AD RMS организации. Для этого необходимо добавить федеративный почтовый ящик в группу суперпользователей, настроенную в кластере AD RMS организации.

> [!IMPORTANT]  
> В развертываниях перекрестного леса AD RMS, в которых кластер AD RMS развернут в каждом лесу, необходимо добавить федеративный почтовый ящик в группу суперпользователей в кластере AD RMS каждого леса, чтобы разрешить службе транспорта на сервере почтовых ящиков Exchange 2013 или транспортном сервере-концентраторе Exchange 2010 расшифровывать сообщения, защищенные в каждом кластере AD RMS.


Дополнительные сведения см. в разделе [Добавление федеративного почтового ящика в группу суперпользователей службы управления правами Active Directory](add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md).

В Exchange 2013 существует два параметра включения расшифровки транспорта.

  - **Mandatory**   Если для расшифровки транспорта установлен параметр `Mandatory`, агент расшифровки отклоняет сообщение и возвращает отправителю отчет о недоставке при возникновении постоянной ошибки во время расшифровки сообщения. Если в организации запрещается доставка сообщения при невозможности его успешной расшифровки, а также выполняется проверка антивирусными программами и применяются правила транспорта, необходимо выбрать этот параметр.

  - **Optional**   Если для расшифровки транспорта установлен параметр "Optional", агент расшифровки использует лучший метод расшифровки. Сообщения, которые можно расшифровать, расшифровываются, но сообщения, во время расшифровки которых произошла постоянная ошибка, также доставляются. Если в организации приоритет в определении правил доставки сообщений имеет политика обмена сообщениями, необходимо использовать этот параметр.

Дополнительные сведения о настройке расшифровки транспорта см. в разделе [Включение и отключение расшифровки транспорта](enable-or-disable-transport-decryption-exchange-2013-help.md).
