---
title: '配置跨林拓扑的可用性服务: Exchange 2013 Help'
TOCTitle: 配置跨林拓扑的可用性服务
ms:assetid: f1e7d407-f0d3-47a7-8cc3-03c5980445d5
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb125182(v=EXCHG.150)
ms:contentKeyID: 52061565
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 配置跨林拓扑的可用性服务

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2014-10-22_

可用性服务可以改善信息工作人员的忙/闲数据，方法是为运行 MicrosoftOutlook 的客户端提供安全、一致并且最新的忙/闲信息。默认情况下，随 Exchange Server 2013 一起安装此服务。在所有连接客户端均运行 Outlook 的跨林拓扑中，可用性服务是检索忙/闲信息的唯一方法。可以使用命令行管理程序配置跨林拓扑的可用性服务。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>不能使用 EAC 配置跨林拓扑的可用性服务。</td>
</tr>
</tbody>
</table>


## 在受信任和不受信任的林中使用可用性服务

可以在跨受信任的或不受信任的林的跨林拓扑中使用可用性服务。可用的忙/闲信息类型取决于使用的林受信任与否。

**受信任的林**   在受信任的林中，您可以将可用性服务配置为基于每个用户检索忙/闲信息。将可用性服务配置为基于每个用户检索忙/闲信息时，该服务可以代表特定用户提出跨林请求。这样，远程林中的用户可以检索其他林中的用户的详细忙/闲信息。

**不受信任的林** 在不受信任的林中，您只能将可用性服务配置为基于组织范围检索忙/闲信息。当可用性服务提出组织级忙/闲跨林请求时，将返回组织中每个用户的忙/闲信息。在不受信任的林中，无法控制基于每个用户返回的忙/闲信息的级别。

## 为跨林拓扑配置 Windows

默认情况下，全局地址列表 (GAL) 包含来自单个林的邮件收件人。如果您有跨林环境，我们建议使用 Microsoft Identity Lifecycle Manager (ILM) 2007 Feature Pack 1 (FP1) 以确保任何给定林中的 GAL 都包含来自其他林的邮件收件人。ILM 2007 FP1 创建表示来自其他林的收件人的邮件用户，从而允许用户在 GAL 中查看它们并发送邮件。例如，林 A 中的用户在林 B 中显示为邮件用户，林 B 中的用户在林 A 中也显示为邮件用户。然后，目标林中的用户可以选择表示另一个林中的收件人的邮件用户对象，以发送邮件。

若要启用 GAL 同步，应创建管理代理，以便将已启用邮件的用户、联系人和组从指定的 Active Directory 服务导入到中心元目录。在元目录中，已启用邮件的对象表示为邮件用户。组表示为没有任何关联的成员身份的联系人。然后，管理代理将这些邮件用户导出到指定目标林中的组织单位。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤的时间：5 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[客户端和移动设备权限](clients-and-mobile-devices-permissions-exchange-2013-help.md)主题中的“可用性服务权限”条目。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.</td>
</tr>
</tbody>
</table>


## 您想执行什么操作？

## 使用命令行管理程序在受信任的跨林拓扑中配置每个用户的忙/闲信息

本示例将可用性服务配置为检索目标林中的邮箱服务器上每个用户的忙/闲信息。

    Get-MailboxServer | Add-ADPermission -Accessrights Extendedright -Extendedrights "ms-Exch-
    EPI-Token-Serialization" -User "<Remote Forest Domain>\Exchange servers"

本示例定义可用性服务在源林中的本地邮箱服务器上使用的忙/闲访问方法。将本地邮箱服务器配置为基于每个用户从林 ContosoForest.com 访问忙/闲信息。本示例使用服务帐户检索忙/闲信息。

    Add-AvailabilityAddressSpace -Forestname ContosoForest.com -AccessMethod PerUserFB -UseServiceAccount:$true

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>若要配置双向跨林可用性，请在目标林中重复这些步骤。</td>
</tr>
</tbody>
</table>


如果选择配置受信任的跨林可用性，并选择使用服务帐户（而不是指定组织范围或每个用户的凭据），则必须扩展权限，如“通过命令行管理程序使用服务帐户配置受信任的跨林可用性”部分中的示例所示。在目标林中执行该步骤可以授予源林中的邮箱服务器序列化原始用户上下文的权限。

## 使用命令行管理程序配置服务帐户的受信任的跨林可用性

本示例将配置服务帐户的受信任的跨林可用性。

    Get-MailboxServer | Add-ADPermission -Accessrights Extendedright -Extendedright "ms-Exch-EPI-Token-Serialization" -User "<Remote Forest Domain>\Exchange servers"

有关语法和参数的详细信息，请参阅以下主题：

  - [Get-MailboxServer](https://technet.microsoft.com/zh-cn/library/bb123539\(v=exchg.150\))

  - [Add-ADPermission](https://technet.microsoft.com/zh-cn/library/bb124403\(v=exchg.150\))

  - [Add-AvailabilityAddressSpace](https://technet.microsoft.com/zh-cn/library/bb124122\(v=exchg.150\))

  - [Set-AvailabilityConfig](https://technet.microsoft.com/zh-cn/library/bb124103\(v=exchg.150\))

## 使用命令行管理程序在不受信任的跨林拓扑中配置组织范围的忙/闲信息

本示例将在可用性配置对象上设置组织范围的帐户，以配置对目标林中的忙/闲信息的访问级别。

    Set-AvailabilityConfig -OrgWideAccount "Contoso.com\User"

本示例将为源林添加可用性地址空间配置对象。

    $a = Get-Credential (Enter the credentials for organization-wide user in Contoso.com domain)
    Add-AvailabilityAddressspace -Forestname Contoso.com -Accessmethod OrgWideFB -Credential:$a

