---
title: '通讯簿策略: Exchange 2013 Help'
TOCTitle: 通讯簿策略
ms:assetid: d0a916a1-e3ed-49ae-b116-a559be0dcce6
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Hh529948(v=EXCHG.150)
ms:contentKeyID: 50491597
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 通讯簿策略

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2016-12-09_

了解如何将全局地址列表分段到特定的组，以便在 Outlook 和 Outlook Web App 中创建自定义 GAL。

全局地址列表 (GAL) 分段（也称为 *GAL 分段*）是管理员用于将用户划分到特定群体采用的流程，由此提供其组织的 GAL 的自定义视图。通讯簿策略 (ABP) 可让你将用户划分到特定组，从而提供你组织全球地址列表 (GAL) 的自定义视图。在创建 ABP 时，可以为策略指定一个 GAL、一个脱机通讯簿 (OAB)、一个房间列表以及一个或多个地址列表。然后，可以将 ABP 指定给邮箱用户，向他们提供对 Outlook 和 Outlook Web App 中的自定义 GAL 的访问权限。目的是提供一种更简单的机制为需要多个 GAL 的本地组织实现 GAL 分段。

> [!NOTE]
> ABP 用于优化每个用户组的 GAL 和地址列表，而不是让他们相互难以看到或与组织中的其他用户通信。ABP 仅从目录的角度创建虚拟的用户分割，而不是合法的分割。


**内容**

ABP 的工作方式

ABP 示例

Entourage、Outlook for Mac 和 ABP

## ABP 的工作方式

ABP 包含以下列表：

  - 一个 GAL

  - 一个 OAB

  - 一个房间列表（用于预定）

  - 一个或多个地址列表

在下图中，通讯簿策略 A 包含组织中存在的各种地址对象的一个子集（在图的下部显示）。ABP 的结果范围等于策略中包含的 GAL（在本例中为 GAL1）的范围。在创建了 ABP 并将其分配给用户之后，ABP 中的地址对象将成为用户可查看的对象的范围。

![通讯簿策略概述](images/Hh529948.68084064-7319-431b-be3b-0cce761258b1(EXCHG.150).gif "通讯簿策略概述")

可以使用以下方法将 ABP 分配给单个邮箱用户：


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>新建的还是现有的邮箱？</th>
<th>Shell</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>新建</p></td>
<td><p><a href="https://technet.microsoft.com/zh-cn/library/aa997663(v=exchg.150)">New-Mailbox</a> cmdlet 使用 <em>AddressBookPolicy</em> 参数</p></td>
</tr>
<tr class="even">
<td><p>现有</p></td>
<td><p><a href="https://technet.microsoft.com/zh-cn/library/bb123981(v=exchg.150)">Set-Mailbox</a> cmdlet 使用 <em>AddressBookPolicy</em> 参数</p>
<p></p></td>
</tr>
</tbody>
</table>


ABP 会在用户的客户端应用程序连接到 Exchange 2013 中的客户端访问服务器时生效。如果更改 ABP，则在用户重新启动或重新连接客户端之后，或在你于 Exchange 2013 邮箱服务器上重新启动 RPC 客户端访问服务器之后，更新后的 ABP 才会生效。

## 通讯簿策略路由代理

在不使用 ABP 的 Exchange 组织中，当在 Outlook 或 Outlook Web App 中创建邮件并发送到 Exchange 组织中的另一个收件人时，会出现下列情况：

1.  电子邮件地址解析。例如，如果在“**收件人**”字段中键入 **kweku@contoso.com**，SMTP 电子邮件地址会解析为用户的显示名称“**Kweku Ako-Adjei**”。

2.  你可以查看其他人的联系人卡片。名称解析后，你可以双击用户名并查看他们的联系信息，比如办公室和电话。

如果你正在使用 ABP，并且不希望各虚拟组织中的用户查看彼此潜在的私人信息，则可以开启通讯簿策略路由代理。ABP 路由代理是一个控制如何在组织中解析收件人的传输代理。在安装并配置 ABP 路由代理后，分配到不同 GAL 的用户会显示为外部收件人，因为他们无法对外部收件人的联系卡进行查看。

有关如何在 Exchange Online 中打开 ABP 路由代理的详细信息，请参阅[打开通讯簿策略路由](https://technet.microsoft.com/zh-cn/library/jj891095\(v=exchg.150\))。

有关如何在 Exchange Server 中打开 ABP 路由代理的详细信息，请参阅[安装并配置通讯簿策略路由代理](install-and-configure-the-address-book-policy-routing-agent-exchange-2013-help.md)

## ABP 示例

在下图中，Fabrikam 和 Tailspin Toys 共享同一个 Exchange 组织和同一个 CEO。CEO 是这两家公司的唯一共同员工。

![两个公司一个 CEO](images/Hh529948.c87a5654-d456-4688-acb2-0be15ba1cda6(EXCHG.150).gif "两个公司一个 CEO")

此配置包含三个 ABP：

  - 一个包含 Fabrikam 员工和 CEO

  - 一个包含 Tailspin Toys 员工和 CEO

  - 一个仅包含 CEO

ABP 遵循下列规则：

  - Tailspin Toys 中的用户在浏览 GAL 时只能看到 Tailspin Toys 员工和 CEO。

  - Fabrikam 中的用户在浏览 GAL 时只能看到 Fabrikam 员工和 CEO。

  - 在浏览 GAL 时，CEO 可看到所有 Fabrikam 和 Tailspin Toys 员工。

  - 查看 CEO 的组成员资格的用户只能看到其所在公司中的组。他们看不到存在于其他公司的组。

## Entourage、Outlook for Mac 和 ABP

ABP 不适用于连接到公司网络的 Entourage 用户或 Outlook for Mac 用户。在公司网络内部时，Entourage 和 Outlook for Mac 客户端会直接连接到全局目录服务器，并直接查询 Active Directory，而不使用客户端访问服务器。但是，通过 Internet 连接的 Outlook for Mac 2011 客户端可以使用 OAB 或 Exchange Web 服务 (EWS)。因此，这些客户端可以搜索基于分配的 ABP 的 GAL。有关 Outlook for Mac 2011 管理的详细信息，请参阅 [Outlook for Mac 2011 规划](https://go.microsoft.com/fwlink/p/?linkid=231878)

## 详细信息

[方案：部署通讯簿策略](scenario-deploying-address-book-policies-exchange-2013-help.md)

Exchange Online 中的[通讯簿策略程序](https://technet.microsoft.com/zh-cn/library/jj891096\(v=exchg.150\))

