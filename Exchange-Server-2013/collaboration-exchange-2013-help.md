---
title: '协作: Exchange 2013 Help'
TOCTitle: 协作
ms:assetid: f45c1be1-2a66-4610-a28d-4adc6d212769
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ218725(v=EXCHG.150)
ms:contentKeyID: 50491984
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 协作

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2015-03-09_

Exchange 2013 提供了以下丰富的功能，可帮助最终用户在电子邮件中轻松地协作：

  - 站点邮箱

  - 公用文件夹

  - 共享邮箱

  - 通讯组

每个功能都有不同的用户体验和功能集，且应以用户所需功能以及组织能够提供的功能为基础使用。例如，站点邮箱提供出色的文档协作功能。但是，站点邮箱依赖 SharePoint Server 2013，因此，如果不打算部署 SharePoint，则应使用公用文件夹来共享文档。

该主题对比这些协作功能，帮助您确定向用户提供哪些功能。

## 站点邮箱

站点邮箱在功能上包含 SharePoint 2013 站点成员身份（所有者和成员）、通过 Exchange 2013 邮箱的电子邮件共享以及用于存储和共享的 SharePoint 2013 站点。实际上，站点邮箱汇集了 Exchange 电子邮件和 SharePoint 文档。对用户来说，站点邮箱可作为项目的中央筛选柜，为只能由站点会员访问和编辑的文件项目电子邮件和文档提供空间。此外，站点电子邮箱有指定的生命周期，并经过优化以用于具有设定的起始和结束日期的项目。若要完全实施站点邮箱，最终用户必须使用 Outlook 2013。

若要了解详细信息，请参阅 [网站邮箱](site-mailboxes-exchange-2013-help.md)。

## 公用文件夹

公用文件夹专为共享访问设计，为收集、组织信息及与您的工作组或组织中的其他人共享信息提供了一种轻松、有效的方式。

公用文件夹以易于浏览的深层次结构组织内容。通过浏览层次结构中与其相关的分支，用户可以找到感兴趣的相关内容。用户始终可以看到他们的 Outlook 文件夹视图中完整的层次结构。公用文件夹是一项实用的技术，它可用于分发组存档。公用文件夹可以是支持邮件的，并作为通讯组成员添加。发送给通讯组的电子邮件会自动添加至公用文件夹，用于日后参考。公用文件夹也提供简单的文档共享，并且不要求在您的组织中安装 SharePoint Server 2013。最后，最终用户可以将公用文件夹与以下支持的 Outlook 客户端配合使用：Outlook 2007、Outlook 2010 和 Outlook 2013。

若要了解详细信息，请参阅 [公用文件夹](public-folders-exchange-2013-help.md)。

## 共享邮箱

共享邮箱是是多个指定用户可以访问以读取和发送电子邮件以及共享公用日历的邮箱。共享邮箱可以提供通用电子邮件地址（如 info@contoso.com 或 sales@contoso.com），客户可以使用这些邮件地址来询问您的公司。如果共享邮箱在指定用户回复电子邮件时拥有“发送为”权限， 则显示为通过邮箱 （例如：sales@contoso.com）回复，而不是实际用户回复。

若要了解详细信息，请参阅 [共享邮箱](shared-mailboxes-exchange-2013-help.md)。

## 组

组（也称为“通讯组”）是将会出现在共享通讯簿中的两个或多个收件人的集合。将电子邮件发送到一个组时，该组的所有成员都会收到该电子邮件。通讯组可以按特定的讨论主题（例如“Dog Lovers”）组织，也可以按共享要求用户经常联络的公用工作结构的用户组织。

若要了解详细信息，请参阅 [收件人](recipients-exchange-2013-help.md)。

## 要使用哪一种？

通过下列表格，您可以快速浏览每个协作功能，帮助您决定使用哪一种。


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th></th>
<th>站点邮箱</th>
<th>公用文件夹</th>
<th>共享邮箱</th>
<th>组</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>组类型</strong></p></td>
<td><p>以团队形式共同处理具有特定起始和结束日期的特定项目的用户。</p></td>
<td><p>利用恰当的权限，组织中的每个人都可以访问和搜索公用文件夹。公用文件夹是维护历史记录或通讯组会话的理想选择。</p></td>
<td><p>代表虚拟标识工作的代理人，可与共享的邮箱标识回复电子邮件。示例：support@tailspintoys.com</p></td>
<td><p>需要向有共同兴趣或特征的收件人组发送电子邮件的用户。</p></td>
</tr>
<tr class="even">
<td><p><strong>理想组大小</strong></p></td>
<td><p>小</p></td>
<td><p>大型</p></td>
<td><p>小</p></td>
<td><p>大型</p></td>
</tr>
<tr class="odd">
<td><p><strong>访问</strong></p></td>
<td><p>站点邮箱所有者和成员。</p></td>
<td><p>组织中的任何人都可以访问。</p></td>
<td><p>用户可以被授予“完全访问”权限和/或“发送为”权限。如果被授予“完全访问”权限，则用户也必须添加共享邮箱至其 Outlook 配置文件以访问共享邮箱。</p></td>
<td><p>对于通讯组，必须手动添加成员。对于动态通讯组，成员添加基于筛选条件。</p></td>
</tr>
<tr class="even">
<td><p><strong>共享日历？</strong></p></td>
<td><p>否</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p><strong>电子邮件到达用户的个人收件箱？</strong></p></td>
<td><p>不到达。电子邮件到达站点邮箱。</p></td>
<td><p>不到达。电子邮件到达公用文件夹。</p></td>
<td><p>不到达。电子邮件到达共享邮箱的收件箱。</p></td>
<td><p>是。电子邮件到达通讯组成员的收件箱。</p></td>
</tr>
<tr class="even">
<td><p><strong>支持的客户端</strong></p></td>
<td><ul>
<li><p>Outlook 2013</p></li>
<li><p>SharePoint 2013</p></li>
</ul></td>
<td><ul>
<li><p>Outlook 2013</p></li>
<li><p>Outlook 2010</p></li>
<li><p>Outlook 2007</p></li>
</ul></td>
<td><ul>
<li><p>Outlook 2013</p></li>
<li><p>Outlook Web App</p></li>
<li><p>Outlook 2010</p></li>
<li><p>Outlook 2007</p></li>
</ul></td>
<td><ul>
<li><p>Outlook 2013</p></li>
<li><p>Outlook Web App</p></li>
<li><p>Outlook 2010</p></li>
<li><p>Outlook 2007</p></li>
</ul></td>
</tr>
</tbody>
</table>

