---
title: '电子邮件地址和通讯簿: Exchange 2013 Help'
TOCTitle: 电子邮件地址和通讯簿
ms:assetid: b97d0f68-691a-42af-9a6c-4dcc37b28a42
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ657488(v=EXCHG.150)
ms:contentKeyID: 50491420
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 电子邮件地址和通讯簿

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-03-09_

收件人（包括用户、资源、联系人和组）是 Active Directory 中任何已启用邮件功能的对象，Microsoft Exchange 可以向其传递或路由邮件。为了使收件人可以发送或接收电子邮件，收件人必须有电子邮件地址。通讯簿是用户之间相互查找以便发送电子邮件的一种方法。组织通讯簿有很多不同的方法。请参阅关键术语获取有关 Exchange Server 2013 中通讯簿功能的详细描述。

## 关键术语

以下术语定义了与 Exchange 2013 中的电子邮件地址和通讯簿关联的各个核心组件。

  - **通讯簿策略**  
    通过通讯簿策略 (ABP)，可以将用户分割成特定的组，以提供组织全局通讯簿 (GAL) 的自定义视图。在创建 ABP 时，可以为策略指定一个 GAL、一个脱机通讯簿 (OAB)、一个房间列表以及一个或多个地址列表。然后，可以将 ABP 指定给邮箱用户，向他们提供对 Outlook 和 Outlook Web App 中的自定义 GAL 的访问权限。目的是提供一种更简单的机制为需要多个 GAL 的内部部署组织实现 GAL 分段。

<!-- end list -->

  - **地址列表**  
    地址列表是 GAL 的子集。每个地址列表是由一个或多个类型的已启用邮件功能的收件人组成的集合（例如，用户、联系人、组、公用文件夹、会议，以及其他资源）。您可以使用地址列表对收件人和资源进行组织，使用户更轻松地查找所需的收件人和资源。地址列表是动态更新的。因此，当新收件人添加到组织中时，他们会自动添加到相应的地址列表中。

<!-- end list -->

  - **电子邮件地址策略**  
    电子邮件地址策略为收件人生成主电子邮件地址和辅电子邮件地址，以便其可以接收和发送电子邮件。默认情况下，Exchange 包含适用于所有已启用邮件功能的用户的电子邮件地址策略。

<!-- end list -->

  - **分层通讯簿**  
    分层通讯簿 (HAB) 允许最终用户使用组织层次结构（例如资历或管理结构）在通讯簿中查找收件人。通常，用户仅限于默认 GAL 及其相关收件人属性，GAL 的结构通常不会准确反映组织中收件人的管理或资历关系。能够自定义 HAB 以反映您的组织独特的业务结构，这可以为您的用户提供查找内部收件人的高效方法。

<!-- end list -->

  - **脱机通讯簿**  
    脱机通讯簿 (OAB) 是已下载的地址列表集合的副本，通过此通讯簿，Microsoft Outlook 用户可以在与服务器断开连接的情况下访问它所包含的信息。

## 电子邮件地址和通讯簿文档

以下表格中包含一些主题的链接，这些主题可以帮助您了解并管理 Exchange 2013 中的电子邮件地址和通讯簿。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>主题</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="address-lists-exchange-2013-help.md">地址列表</a></p></td>
<td><p>了解更多有关用于组织您的收件人以便最终用户轻松访问的方法的地址列表和 GAL 的信息。</p></td>
</tr>
<tr class="even">
<td><p><a href="address-book-policies-exchange-2013-help.md">通讯簿策略</a></p></td>
<td><p>了解更多有关如何将您的地址列表和 GAL 分开放入不同虚拟组织的信息。</p></td>
</tr>
<tr class="odd">
<td><p><a href="details-templates-exchange-2013-help.md">详细信息模板</a></p></td>
<td><p>了解更多有关在 Outlook 中自定义地址卡的信息。</p></td>
</tr>
<tr class="even">
<td><p><a href="email-address-policies-exchange-2013-help.md">电子邮件地址策略</a></p></td>
<td><p>了解更多有关代理电子邮件地址（通过此地址可以更轻松地找到收件人）的信息。</p></td>
</tr>
<tr class="odd">
<td><p><a href="hierarchical-address-books-exchange-2013-help.md">分层通讯簿</a></p></td>
<td><p>了解更多有关如何自定义 GAL 和地址列表以满足您组织独有的业务结构要求的信息。</p></td>
</tr>
<tr class="even">
<td><p><a href="offline-address-books-exchange-2013-help.md">脱机通讯簿</a></p></td>
<td><p>了解更多有关为用户提供在脱机情况下访问您组织地址列表的权限的信息。</p></td>
</tr>
</tbody>
</table>

