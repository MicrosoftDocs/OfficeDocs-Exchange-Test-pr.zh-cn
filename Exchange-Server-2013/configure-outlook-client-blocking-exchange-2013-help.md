---
title: '配置 Outlook 客户端阻止: Exchange 2013 Help'
TOCTitle: 配置 Outlook 客户端阻止
ms:assetid: 3a579c83-8bc7-4adc-a25c-8eb6eed7220c
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd335207(v=EXCHG.150)
ms:contentKeyID: 51408217
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 配置 Outlook 客户端阻止

 

_**适用于：** Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013_

_**上一次修改主题：** 2015-03-09_

在 Exchange Server 2013 中，可以使用保留策略或托管文件夹进行邮件记录管理 (MRM)。只有运行 Microsoft Outlook 2010 及更高版本的用户才能访问保留策略的所有客户端功能。但是，保留策略是通过托管文件夹助理应用于邮箱服务器，不管用户使用的 Outlook 客户端版本是什么。较旧的 Outlook 客户端不公开这些功能的 MRM 功能。例如，因为 Outlook 2007 不支持保留策略，所以用户无法将个人标记应用于项目或文件夹。

您可以阻止运行较旧版本 Outlook 的用户访问其 Exchange 邮箱。您可以基于每个邮箱或每个客户端服务器来阻止访问。

有关与 MRM 相关的其他管理任务，请参阅[邮件记录管理程序](messaging-records-management-procedures-exchange-2013-help.md)。

## 按客户端应用程序和版本列出 MRM 功能可用性

下表列出了在各种客户端应用程序和版本中可用的 MRM 功能。

### MRM 功能

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>客户端应用程序</th>
<th>可用 MRM 客户端功能</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook 2013 和Outlook 2010</p></td>
<td><p>所有</p></td>
</tr>
<tr class="even">
<td><p>Outlook 2007</p></td>
<td><p>托管文件夹</p></td>
</tr>
<tr class="odd">
<td><p>Outlook 2003 和较旧版本</p></td>
<td><p>不支持</p></td>
</tr>
<tr class="even">
<td><p>其他电子邮件客户端软件</p></td>
<td><p>无</p></td>
</tr>
</tbody>
</table>


下表显示了 Outlook 的版本号。

### Outlook 版本

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Outlook 版本</th>
<th>版本号</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook 2013</p></td>
<td><p>15</p></td>
</tr>
<tr class="even">
<td><p>Outlook 2010</p></td>
<td><p>14</p></td>
</tr>
<tr class="odd">
<td><p>Outlook 2007</p></td>
<td><p>12</p></td>
</tr>
<tr class="even">
<td><p>Outlook 2003</p></td>
<td><p>11</p></td>
</tr>
<tr class="odd">
<td><p>Outlook 2002</p></td>
<td><p>10</p></td>
</tr>
<tr class="even">
<td><p>Outlook 2000</p></td>
<td><p>9</p></td>
</tr>
<tr class="odd">
<td><p>Outlook 98</p></td>
<td><p>8.5</p></td>
</tr>
<tr class="even">
<td><p>Outlook 97</p></td>
<td><p>8</p></td>
</tr>
</tbody>
</table>


> [!NOTE]
> 进行任何更改之前，请注意修补程序和 Service Pack 版本可能会影响客户版本字符串。限制客户端访问时要小心谨慎，因为服务器端 Exchange 组件也必须使用 MAPI 进行登录。一些组件将其客户端版本报告为组件名称（如 SMTP 或 OLE DB），而其他组件报告 Exchange 内部版本号（如 6.0.4712.0）。因此，请避免限制版本号以 6.&lt;<em>x</em>.<em>x</em>.&gt; 开头的客户端。例如，若要完全阻止 MAPI 访问，请指定两个范围以便服务器组件可以登录，而不是指定 <strong>0.0.0-6.5535.65535.65535</strong>。例如，指定如下范围：<strong>0.0.0-5.9.9; 7.0.0-</strong>.


在执行这些步骤之后，请注意当阻止用户访问其邮箱时，他们会收到以下警告消息。


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Exchange Server 管理员已阻止您使用的 Outlook 版本。请与管理员联系以获取帮助。</p></td>
</tr>
</tbody>
</table>


若要绕过指示运行 Outlook 2010 之前的 Outlook 版本的电子邮件客户端不支持 MRM 功能的警告，可以在命令行管理程序中使用 **New-Mailbox**、**Enable-Mailbox** 和 **Set-Mailbox** cmdlet 的 *ManagedFolderMailboxPolicyAllowed* 参数。使用 *ManagedFolderMailboxPolicy* 参数为邮箱分配托管文件夹邮箱策略时，除非使用 *ManagedFolderMailboxPolicyAllowed* 参数，否则，默认情况下将出现警告。

## 在开始之前，您需要知道什么？

  - 估计完成时间：1 分钟。

  - 不能使用 Exchange 管理中心 (EAC) 执行这些过程。必须使用命令行管理程序。

  - 本主题中的过程需要特定权限。请参阅每个过程，以了解其权限信息。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

## 您想执行什么操作？

## 阻止基于每个邮箱的 Outlook 版本

您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [收件人权限](recipients-permissions-exchange-2013-help.md)主题中的\&quot;用户邮箱\&quot;条目。

此示例阻止了所有早于 11.8010.8036 的 Outlook 版本。

    Set-CASMailbox -Identity adam@contoso.com -MAPIBlockOutlookVersions "-11.8010.8036"

本示例还原对 Outlook 的一个版本阻止的邮箱的访问。

    Set-CASMailbox -Identity adam@contoso.com -MAPIBlockOutlookVersions $null

有关语法和参数的详细信息，请参阅 [Set-CASMailbox](https://technet.microsoft.com/zh-cn/library/bb125264\(v=exchg.150\))。

## 在客户端访问服务器上阻止 Outlook 版本

您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [客户端和移动设备权限](clients-and-mobile-devices-permissions-exchange-2013-help.md)主题中的\&quot;RPC 客户端访问设置\&quot;条目。

此示例阻止了版本 12.0.0 之前的 Outlook 客户端访问 Exchange 2010 或更高版本客户端访问服务器上的邮箱。

> [!important]
> 与 <em>BlockedClientVersions</em> 参数一起使用的值是示例值。您可以通过解析 <code>%ExchangeInstallPath%Logging\RPC Client Access</code> 处的 RPC 客户端访问日志文件，确定正确的客户端软件版本。


    Set-RpcClientAccess -Server CAS01 -BlockedClientVersions "0.0.0-5.65535.65535;7.0.0;8.02.4-11.65535.65535"

有关语法和参数的详细定义，请参阅 [Set-RpcClientAccess](https://technet.microsoft.com/zh-cn/library/dd351072\(v=exchg.150\))。

