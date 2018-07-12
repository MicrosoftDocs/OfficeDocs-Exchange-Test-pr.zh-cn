---
title: '客户端和移动设备权限: Exchange 2013 Help'
TOCTitle: 客户端和移动设备权限
ms:assetid: 57eca42a-5a7f-4c65-89f0-7a84f2dbea19
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd638131(v=EXCHG.150)
ms:contentKeyID: 50490587
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 客户端和移动设备权限

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-11-10_

对客户端和移动设备执行任务所需的权限将视所执行的过程或要运行的 cmdlet 而定。有关客户端和移动设备功能的详细信息，请参阅[客户端和移动](clients-and-mobile-exchange-2013-help.md)。

若要了解执行过程或运行 cmdlet 所需的权限，请执行以下操作：

1.  在下表中查找与所要执行的过程或要运行的 cmdlet 最相关的功能。

2.  接下来，查看该功能所需的权限。您必须被分配到其中一个角色组、等效的自定义角色组或等效的管理角色。还可以单击角色组查看其管理角色。如果某个功能列出多个角色组，则您只需要被分配到其中一个角色组就可以使用此功能。有关角色组和管理角色的详细信息，请参阅[了解基于角色的访问控制](understanding-role-based-access-control-exchange-2013-help.md)。

3.  现在运行 **Get-ManagementRoleAssignment** cmdlet 以查看分配给您的角色组或管理角色，以便确定您是否具有管理该功能所需的权限。
    
    > [!NOTE]
    > 必须分配了 Role Management 管理角色才能运行 <strong>Get-ManagementRoleAssignment</strong> cmdlet。如果没有运行 <strong>Get-ManagementRoleAssignment</strong> cmdlet 的权限，则请求 Exchange 管理员检索分配给您的角色组或管理角色。


如果要将管理一项功能的权限委派给另一个用户，请参阅[委派角色分配](delegate-role-assignments-exchange-2013-help.md)。

> [!NOTE]
> 某些功能可能要求在要管理的服务器上拥有本地管理员权限。若要管理这些功能，必须是该服务器上 Local Administrators 组的成员。


## 客户端访问服务器权限

您可以为客户端访问服务器配置以下任何功能。

分配了仅限查看管理角色组的用户可以查看下表所示功能的配置。有关详细信息，请参阅[仅查看组织管理](view-only-organization-management-exchange-2013-help.md)。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>所需的权限</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>客户端访问服务器阵列设置</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="server-management-exchange-2013-help.md">服务器管理</a></p></td>
</tr>
<tr class="even">
<td><p>客户端访问服务器设置</p></td>
<td><p><a href="server-management-exchange-2013-help.md">服务器管理</a></p></td>
</tr>
<tr class="odd">
<td><p>客户端访问服务电子邮件通道设置</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="server-management-exchange-2013-help.md">服务器管理</a></p></td>
</tr>
<tr class="even">
<td><p>客户端访问用户设置</p></td>
<td><p><a href="server-management-exchange-2013-help.md">服务器管理</a></p></td>
</tr>
<tr class="odd">
<td><p>客户端访问虚拟目录设置</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="server-management-exchange-2013-help.md">服务器管理</a></p></td>
</tr>
<tr class="even">
<td><p>RPC 客户端访问设置</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="server-management-exchange-2013-help.md">服务器管理</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">仅查看组织管理</a></p></td>
</tr>
<tr class="odd">
<td><p>推送通知代理设置</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件人管理</a></p></td>
</tr>
<tr class="even">
<td><p>OAuth 身份验证重定向设置</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p></td>
</tr>
</tbody>
</table>


## Exchange ActiveSync 权限

您可以为 Exchange ActiveSync 进行以下任何配置。

分配了仅限查看管理角色组的用户可以查看下表所示功能的配置。有关详细信息，请参阅[仅查看组织管理](view-only-organization-management-exchange-2013-help.md)。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>所需的权限</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange ActiveSync 自动阻止设置</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p></td>
</tr>
<tr class="even">
<td><p>Exchange ActiveSync 邮箱策略设置</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="server-management-exchange-2013-help.md">服务器管理</a></p></td>
</tr>
<tr class="odd">
<td><p>Exchange ActiveSync 服务器设置</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="server-management-exchange-2013-help.md">服务器管理</a></p></td>
</tr>
<tr class="even">
<td><p>Exchange ActiveSync 设置</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="server-management-exchange-2013-help.md">服务器管理</a></p></td>
</tr>
<tr class="odd">
<td><p>Exchange ActiveSync 用户设置</p></td>
<td><p><a href="recipient-management-exchange-2013-help.md">收件人管理</a></p></td>
</tr>
<tr class="even">
<td><p>Exchange ActiveSync 虚拟目录设置</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="server-management-exchange-2013-help.md">服务器管理</a></p></td>
</tr>
<tr class="odd">
<td><p>移动设备邮箱策略设置</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="server-management-exchange-2013-help.md">服务器管理</a></p></td>
</tr>
<tr class="even">
<td><p>移动设备用户设置</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="server-management-exchange-2013-help.md">服务器管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件人管理</a></p></td>
</tr>
</tbody>
</table>


## 自动发现权限

您可以为自动发现服务进行以下配置。

分配了仅限查看管理角色组的用户可以查看下表所示功能的配置。有关详细信息，请参阅[仅查看组织管理](view-only-organization-management-exchange-2013-help.md)。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>所需的权限</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>自动发现服务配置设置</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="server-management-exchange-2013-help.md">服务器管理</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">仅查看组织管理</a></p>
<p><a href="delegated-setup-exchange-2013-help.md">委派安装</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">清洁管理</a></p></td>
</tr>
<tr class="even">
<td><p>自动发现虚拟目录设置</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="server-management-exchange-2013-help.md">服务器管理</a></p></td>
</tr>
</tbody>
</table>


## 可用性服务权限

您可以为可用性服务进行以下配置。

分配了仅限查看管理角色组的用户可以查看下表所示功能的配置。有关详细信息，请参阅[仅查看组织管理](view-only-organization-management-exchange-2013-help.md)。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>所需的权限</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>可用性服务地址空间设置</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">仅查看组织管理</a></p></td>
</tr>
<tr class="even">
<td><p>可用性服务配置设置</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="server-management-exchange-2013-help.md">服务器管理</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">仅查看组织管理</a></p></td>
</tr>
</tbody>
</table>


## 客户端限制权限

您可以为客户端限制进行以下配置。

分配了仅限查看管理角色组的用户可以查看下表所示功能的配置。有关详细信息，请参阅[仅查看组织管理](view-only-organization-management-exchange-2013-help.md)。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>所需的权限</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>客户端限制设置</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">仅查看组织管理</a></p></td>
</tr>
</tbody>
</table>


## Exchange Web 服务权限

您可以为 Web 服务虚拟目录进行以下配置。

分配了仅限查看管理角色组的用户可以查看下表所示功能的配置。有关详细信息，请参阅[仅查看组织管理](view-only-organization-management-exchange-2013-help.md)。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>所需的权限</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange Web 服务虚拟目录设置</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="server-management-exchange-2013-help.md">服务器管理</a></p></td>
</tr>
<tr class="even">
<td><p>测试 Exchange Web 服务</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="server-management-exchange-2013-help.md">服务器管理</a></p></td>
</tr>
<tr class="odd">
<td><p>测试 Outlook Web 服务</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p></td>
</tr>
</tbody>
</table>


## Outlook 无处不在权限

您可以为 Outlook 无处不在 配置和管理以下设置。

分配了仅限查看管理角色组的用户可以查看下表所示功能的配置。有关详细信息，请参阅[仅查看组织管理](view-only-organization-management-exchange-2013-help.md)。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>所需的权限</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook 无处不在 配置（启用、禁用、更改、查看）</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="server-management-exchange-2013-help.md">服务器管理</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">仅查看组织管理</a></p>
<p><a href="delegated-setup-exchange-2013-help.md">委派安装</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">清洁管理</a></p></td>
</tr>
<tr class="even">
<td><p>RPC over HTTP Proxy 组件</p></td>
<td><p>本地服务器管理员</p></td>
</tr>
<tr class="odd">
<td><p>测试 Outlook 无处不在 连接</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">仅查看组织管理</a></p>
<p><a href="server-management-exchange-2013-help.md">服务器管理</a></p></td>
</tr>
</tbody>
</table>


## Outlook Web App 权限

您可以使用以下功能查看 Outlook Web App 设置，控制安全性和用户对 Outlook Web App 的访问，并测试 Outlook Web App 连接。

分配了仅限查看管理角色组的用户可以查看下表所示功能的配置。有关详细信息，请参阅[仅查看组织管理](view-only-organization-management-exchange-2013-help.md)。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>所需的权限</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>图形编辑器</p></td>
<td><p>本地服务器管理员</p></td>
</tr>
<tr class="even">
<td><p>IIS 管理器</p></td>
<td><p>本地服务器管理员</p></td>
</tr>
<tr class="odd">
<td><p>ISA Server 2006</p></td>
<td><p>ISA Server 企业管理员</p></td>
</tr>
<tr class="even">
<td><p>Outlook Web App 邮箱策略</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件人管理</a></p></td>
</tr>
<tr class="odd">
<td><p>Outlook Web App 虚拟目录</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="server-management-exchange-2013-help.md">服务器管理</a></p></td>
</tr>
<tr class="even">
<td><p>注册表编辑器</p></td>
<td><p>本地服务器管理员</p></td>
</tr>
<tr class="odd">
<td><p>S/MIME 配置</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p></td>
</tr>
<tr class="even">
<td><p>文本编辑器</p></td>
<td><p>本地服务器管理员</p></td>
</tr>
<tr class="odd">
<td><p>查看 Outlook Web App 邮箱策略</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件人管理</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">仅查看组织管理</a></p>
<p><a href="delegated-setup-exchange-2013-help.md">委派安装</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">清洁管理</a></p></td>
</tr>
</tbody>
</table>


## POP3 和 IMAP4 权限

您可以为 POP3 和 IMAP4 进行以下配置。

分配了仅限查看管理角色组的用户可以查看下表所示功能的配置。有关详细信息，请参阅[仅查看组织管理](view-only-organization-management-exchange-2013-help.md)。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>所需的权限</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>IMAP4 设置</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="server-management-exchange-2013-help.md">服务器管理</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">仅查看组织管理</a></p></td>
</tr>
<tr class="even">
<td><p>POP3 设置</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="server-management-exchange-2013-help.md">服务器管理</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">仅查看组织管理</a></p></td>
</tr>
<tr class="odd">
<td><p>测试 IMAP4 设置</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="server-management-exchange-2013-help.md">服务器管理</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">仅查看组织管理</a></p></td>
</tr>
<tr class="even">
<td><p>测试 POP3 设置</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="server-management-exchange-2013-help.md">服务器管理</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">仅查看组织管理</a></p></td>
</tr>
</tbody>
</table>


## Windows PowerShell 虚拟目录权限

您可以为 Windows PowerShell 进行以下配置。

分配了仅限查看管理角色组的用户可以查看下表所示功能的配置。有关详细信息，请参阅[仅查看组织管理](view-only-organization-management-exchange-2013-help.md)。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>所需的权限</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>测试 Windows PowerShell</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p></td>
</tr>
<tr class="even">
<td><p>Windows PowerShell 设置</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p></td>
</tr>
</tbody>
</table>


## 短信权限

您可以为短信进行以下配置。

分配了仅限查看管理角色组的用户可以查看下表所示功能的配置。有关详细信息，请参阅[仅查看组织管理](view-only-organization-management-exchange-2013-help.md)。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>所需的权限</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>文本消息通知设置</p></td>
<td><p><a href="recipient-management-exchange-2013-help.md">收件人管理</a></p></td>
</tr>
<tr class="even">
<td><p>文本消息设置</p></td>
<td><p><a href="recipient-management-exchange-2013-help.md">收件人管理</a></p></td>
</tr>
<tr class="odd">
<td><p>文本消息用户设置</p></td>
<td><p><a href="mytextmessaging-role-exchange-2013-help.md">MyTextMessaging 角色</a></p>
<p>用户可以在自己的邮箱中配置短信设置。管理员不能在另一用户的邮箱中配置短信设置。</p></td>
</tr>
</tbody>
</table>

