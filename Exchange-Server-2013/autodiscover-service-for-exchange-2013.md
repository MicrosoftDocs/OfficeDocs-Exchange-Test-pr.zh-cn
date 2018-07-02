---
title: '自动发现服务: Exchange 2013 Help'
TOCTitle: 自动发现服务
ms:assetid: b03c0f21-cbc2-4be8-ad03-73a7dac16ffc
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb124251(v=EXCHG.150)
ms:contentKeyID: 50556643
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 自动发现服务

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2016-12-09_

了解 Microsoft Exchange 2013 的 Exchange 自动发现服务。您将了解 Exchange 自动发现服务的功能、工作原理以及部署选项。

MicrosoftExchange 2013 包括一项名为自动发现服务的服务。本主题概括介绍该服务，说明其工作方式，其配置 Outlook 客户端的方式，以及有哪些选项可以在邮件环境中部署自动发现服务。

自动发现服务执行下列操作：

  - 自动为运行 MicrosoftOffice Outlook 2007、Outlook 2010 或 Outlook 2013 的客户端以及受支持的移动电话配置用户配置文件设置。支持运行 Windows Mobile 6.1 或更高版本的电话。如果您的电话不是 Windows 移动电话，请检查您的移动电话说明书以确定其是否受支持。

  - 可以访问连接到 Exchange 邮件环境的 Outlook 2007、Outlook 2010 或 Outlook 2013 客户端的 Exchange 功能。

  - 使用用户的电子邮件地址和密码为 Outlook 2007、Outlook 2010 或 Outlook 2013 客户端和受支持的移动电话提供配置文件设置。如果已将 Outlook 客户端加入域，则将使用用户的域帐户。

**目录**

自动发现服务概述

自动发现服务的工作方式

自动发现服务的部署选项

配置自动发现以实现跨林移动

## 自动发现服务概述

自动发现服务使配置 Outlook 2007、Outlook 2010 或 Outlook 2013 以及某些移动电话变得更加容易。自动发现服务不能与早于 Office Outlook 2007 版本的 Outlook 一起使用。在 Microsoft Exchange 的早期版本（Exchange 2003 SP2 或更早版本）和 Outlook 的早期版本（Outlook 2003 或更早版本）中，必须手动配置所有用户配置文件才能访问 Exchange。如果邮件环境发生改变，管理这些配置文件将需要额外工作。否则，Outlook 客户端将停止正常运行。

通过自动发现服务，Outlook 找到一个新的连接点，该连接点由用户的邮箱 GUID + @ + 用户主 SMTP 地址的域部分组成。自动发现服务向客户端返回以下信息：

  - 用户的显示名称

  - 内部和外部连接的单独连接设置

  - 用户邮箱服务器的位置

  - 各种 Outlook 功能的 URL，这些功能管理忙/闲信息、统一消息和脱机通讯簿等功能

  - Outlook Anywhere 服务器设置

当用户的 Exchange 信息更改时，Outlook 将使用自动发现服务自动重新配置用户的配置文件。例如，如果移动了用户邮箱，或者客户端无法连接到用户邮箱或可用的 Exchange 功能，Outlook 将联系自动发现服务并自动更新用户配置文件，使其包含连接到邮箱和 Exchange 功能所需的信息。

返回顶部

## 自动发现服务的工作方式

在 Exchange 2013 中安装客户端访问服务器角色时，将在 Internet 信息服务 (IIS) 中的默认网站下创建一个名为自动发现的默认虚拟目录。在下列情况下，此虚拟目录处理来自 Outlook 2007、Outlook 2010 或 Outlook 2013 客户端和支持的移动电话的自动发现服务请求：

  - 配置或更新用户帐户时

  - Outlook 客户端定期检查对 Exchange Web 服务 URL 的更改时

  - Exchange 邮件环境中发生了基本网络连接更改时

此外，将在安装客户端访问服务器的服务器上新建名为服务连接点 (SCP) 的 Active Directory 对象。

SCP 对象包含林的自动发现服务 URL 的权威列表。可使用 **Set-ClientAccessServer** cmdlet 更新 SCP 对象。有关详细信息，请参阅[Set-ClientAccessServer](https://technet.microsoft.com/zh-cn/library/bb125157\(v=exchg.150\))。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在运行 <strong>Set-ClientAccessServer</strong> cmdlet 之前，请确保客户端访问服务器上通过身份验证的用户帐户对 SCP 对象具有读取权限。如果用户没有正确的权限，他们将无法搜索和读取项目。</td>
</tr>
</tbody>
</table>


有关 SCP 对象的详细信息，请参阅[发布服务连接点](https://go.microsoft.com/fwlink/p/?linkid=72744)。

对于外部访问，或在使用 DNS 时，客户端通过使用用户电子邮件地址中的主 SMTP 域地址找到 Internet 上的自动发现服务。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>必须在 Outlook 客户端的 DNS 中提供托管服务 (SRV) 资源记录，才能使用 DNS 发现自动发现服务。有关详细信息，请参阅有关配置 DNS 的 Windows 文档，还可以参阅<a href="https://go.microsoft.com/fwlink/p/?linkid=85214">白皮书：Exchange 2007 自动发现服务</a>。</td>
</tr>
</tbody>
</table>


根据是否已在独立站点上配置自动发现服务，自动发现服务的 URL 将是 https://\<*smtp-address-domain*\>/autodiscover/autodiscover.xml 或 https://autodiscover\<*smtp-address-domain*\>/autodiscover/autodiscover.xml，其中 ://\<*smtp-address-domain*\> 是主 SMTP 域地址。例如，如果用户的电子邮件地址是 tony@contoso.com，则主 SMTP 域地址是 contoso.com。当客户端连接到 Active Directory 时，客户端将查找在安装期间创建的 SCP 对象。在包括多个客户端访问服务器的部署中，将为每个客户端访问服务器创建一个自动发现 SCP 对象。SCP 对象包含 *ServiceBindingInfo* 属性，该属性具有客户端访问服务器的完全限定的域名 (FQDN)，格式为 https://CAS01/autodiscover/autodiscover.xml，其中 CAS01 是客户端访问服务器的 FQDN。Outlook 2007、Outlook 2010 或 Outlook 2013 客户端使用用户凭据对 Active Directory 进行身份验证，并搜索自动发现 SCP 对象。在客户端获取并枚举自动发现服务的实例后，客户端将连接到枚举列表中的第一个客户端访问服务器，并将获取连接到用户邮箱和可用 Exchange 功能所需的 XML 数据形式的配置文件信息。

返回顶部

## 自动发现服务的部署选项

必须正确部署和配置自动发现服务以便 Outlook 2007、Outlook 2010 和 Outlook 2013 客户端能自动连接到 Exchange 功能，例如脱机通讯簿、可用性服务和统一消息 (UM)。部署自动发现服务仅是确保 Outlook 2007、Outlook 2010 或 Outlook 2013 客户端可以访问 Exchange 服务（例如可用性服务）的一个步骤。

## 配置自动发现以实现跨林移动

自动发现服务可以提供用户配置文件信息，用于连接其邮箱已从一个 Outlook 林移动到另一个此类林的 Exchange 客户端。为确保执行此操作，必须使用 **New-MailUser** cmdlet 同时在用户的邮箱驻留的原始林和目标林中配置启用邮件的用户。在源林中，应该使用该 cmdlet 中的 *ExternalEmailAddress* 参数在目标林中指定邮箱的新电子邮件地址。有关详细信息，请参阅[New-MailUser](https://technet.microsoft.com/zh-cn/library/aa996335\(v=exchg.150\))。

在配置启用邮件的用户后，原始林中的自动发现服务会将通过身份验证的用户重定向到目标林中的新电子邮件地址。接着会将正在连接的 Outlook 客户端重定向到其中的邮箱已移动的目标林中的客户端访问服务器。

返回顶部

