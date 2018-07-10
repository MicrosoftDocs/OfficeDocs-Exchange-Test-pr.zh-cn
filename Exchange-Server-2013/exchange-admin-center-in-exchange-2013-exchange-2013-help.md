---
title: 'Exchange 2013 中的 Exchange 管理中心: Exchange 2013 Help'
TOCTitle: Exchange 2013 中的 Exchange 管理中心
ms:assetid: a9aea11a-6ba3-4f4a-a76e-79072e7cfc7d
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ150562(v=EXCHG.150)
ms:contentKeyID: 50491279
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2013 中的 Exchange 管理中心

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-03-17_

Exchange 管理中心 (EAC) 是 Microsoft Exchange Server 2013 中提供的一个基于 Web 的管理控制台，该控制台针对 Exchange 内部部署、联机部署和混合部署进行了优化。EAC 替换了 Exchange 管理控制台 (EMC) 和 Exchange 控制面板 (ECP)，这是用于管理 Exchange Server 2010 的两个界面。

基于 Web 的 EAC 的一项优势是可以从 ECP IIS 虚拟目录内部对 Internet 和 Intranet 访问分区。利用此功能，可以控制是否允许用户从组织外部通过 Internet 访问 EAC，同时仍允许最终用户访问 Outlook Web App 选项。有关详细信息，请参阅[关闭对 Exchange 管理中心的访问](turn-off-access-to-the-exchange-admin-center-exchange-2013-help.md)。

是否要了解本主题的 Exchange Online 版本？请参阅[Exchange Online 中的 Exchange 管理中心](https://technet.microsoft.com/zh-cn/library/jj200743\(v=exchg.150\))。

是否要了解本主题的 Exchange Online Protection 版本？请参阅[Exchange Online Protection \[EOP\] 中的 Exchange 管理中心](https://technet.microsoft.com/zh-cn/library/jj723141\(v=exchg.150\))。

目录

访问 EAC

EAC 中常用的用户界面元素

支持的浏览器

## 访问 EAC

因为 EAC 现在是一个基于 Web 的管理控制台，因此需要使用 ECP 虚拟目录 URL 才能通过 Web 浏览器访问它。在大多数情况下，EAC 的 URL 将如下所示：

  - **内部 URL：`https://<CASServerName>/ecp`**   内部 URL 用于从组织的防火墙内部访问 EAC。

  - **外部 URL：`https://mail.contoso.com/ecp`**   外部 URL 用于从组织的防火墙外部访问 EAC。某些组织可能希望关闭对 EAC 的外部访问。有关详细信息，请参阅[关闭对 Exchange 管理中心的访问](turn-off-access-to-the-exchange-admin-center-exchange-2013-help.md)。

若要查找 EAC 的内部或外部 URL，可以使用 [Get-EcpVirtualDirectory](https://technet.microsoft.com/zh-cn/library/dd351058\(v=exchg.150\)) cmdlet。有关详细信息，请参阅[为 Exchange 管理中心找到内部和外部 URL](find-the-internal-and-external-urls-for-the-exchange-admin-center-exchange-2013-help.md)。

如果采用了共存方案，即在同一组织中运行了 Exchange Server 2010 和 Exchange Server 2013，而且邮箱仍位于 Exchange 2010 邮箱服务器上，则浏览器将默认为 Exchange Server 2010 ECP。可以通过向 URL 添加 Exchange 版本的方式来访问 EAC。例如，如果要访问其虚拟目录托管在客户端访问服务器 CAS15-NA 上的 EAC，请使用下列 URL：`https://CAS15-NA/ecp/?ExchClientVer=15`。相反，如果您要访问 Exchange 2010 ECP，同时您的邮箱驻留在 Exchange 2013 邮箱服务器上，请使用以下 URL：`https://CAS14-NA/ecp/?ExchClientVer=14`.

## EAC 中常用的用户界面元素

本部分将介绍 EAC 中常用的用户界面元素。

![Exchange 管理中心](images/JJ150562.cd617bc0-19ef-47d2-bba1-4e9546b12e0c(EXCHG.150).gif "Exchange 管理中心")

## 跨界导航

跨界导航运行您在 Exchange Online 和内部部署 Exchange 部署之间轻松切换。如果没有 Exchange Online 组织，此链接将指向 Office 365 注册页面。若要了解详细信息，请参阅[Exchange Server 混合部署](https://technet.microsoft.com/zh-cn/library/jj200581\(v=exchg.150\))。

## 功能窗格

这是您要在 EAC 中执行的大部分任务的第一级导航。此功能窗格与 Exchange 2010 中的 EMC 控制台树类似。但是，在 Exchange 2013 中，此功能窗格按功能区，而不是按服务器角色进行组织，并且只需单击数下便可找到您所需的内容。

  - **收件人**   可以通过收件人功能管理邮箱、群组、资源邮箱、联系人、共享邮箱以及邮箱迁移和移动。

  - **权限**   可以通过权限功能管理管理员角色、用户角色和 Outlook Web App 策略。

  - **合规性管理**   可以通过合规性管理功能管理就地电子数据展示、就地保留、审核、数据丢失预防 (DLP)、保留策略、保留标记和日记规则。

  - **组织**   可以通过组织功能管理与 Exchange 组织有关的任务，包括联合共享、Outlook Apps 和地址列表。

  - **保护**   可以通过保护功能管理组织的反恶意软件保护。

  - **邮件流**   可以通过邮件流功能管理规则、送达报告、接受域、电子邮件地址策略以及发送和接收连接器。

  - **移动**   可以通过移动功能管理允许连接到您的组织的移动设备。可以管理移动设备访问权限和移动设备邮箱策略。

  - **公用文件夹**   在 Exchange 2010 中，必须使用公用文件夹管理控制台管理公用文件夹；该文件夹位于 EMC 外部的“工具箱”中。在 Exchange 2013 中，可以从“公用文件夹”功能区内部管理公用文件夹。

  - **统一消息**   可以通过统一消息功能管理 UM 拨号计划和 UM IP 网关。

  - **服务器**   可以通过服务器功能管理邮箱和客户端访问服务器、数据库、数据库可用性组 (DAG)、虚拟目录以及证书。

  - **混合**   可以通过此功能设置和配置混合组织。

## 选项卡

选项卡是导航的第二级。每个功能区都包含各种选项卡，每种选项卡代表一项完整的功能。此规则的唯一例外是混合功能区。您必须先使用混合配置向导为混合部署启用您的组织。

## 工具栏

单击大多数选项卡时，将看到一个工具栏。工具栏包含执行特定操作的图标。下表介绍了最常用的图标及其操作。若要显示与图标关联的操作，只需将鼠标悬停到相应图标上。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>图标</th>
<th>名称</th>
<th>操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><img src="images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif" title="添加图标" alt="添加图标" /></p></td>
<td><p>添加、新建</p></td>
<td><p>使用此图标可新建对象。其中一些图标有关联的向下箭头，单击该箭头会显示可以创建的其他对象。例如，在“收件人”&gt;“邮箱”中，单击向下箭头可显示附加选项“用户邮箱”和“链接邮箱”。</p></td>
</tr>
<tr class="even">
<td><p><img src="images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif" title="编辑图标" alt="编辑图标" /></p></td>
<td><p>编辑</p></td>
<td><p>使用此图标可编辑对象。</p></td>
</tr>
<tr class="odd">
<td><p><img src="images/JJ657511.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif" title="删除图标" alt="删除图标" /></p></td>
<td><p>删除</p></td>
<td><p>使用此图标可删除对象。有些删除图标有一个向下箭头，单击该箭头可显示其他选项。</p></td>
</tr>
<tr class="even">
<td><p><img src="images/Dn750895.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif" title="搜索图标" alt="搜索图标" /></p></td>
<td><p>搜索</p></td>
<td><p>使用此图标可打开搜索框，并能在其中键入要查找的对象的搜索短语。请查看<a href="https://technet.microsoft.com/zh-cn/library/jj156853(v=exchg.150)">收件人 &gt; 高级搜索</a>，了解更多搜索选项。</p></td>
</tr>
<tr class="odd">
<td><p><img src="images/Dd353189.85f271ca-32a4-426c-842a-d2172567099d(EXCHG.150).gif" title="刷新图标" alt="刷新图标" /></p></td>
<td><p>刷新</p></td>
<td><p>使用此图标可刷新列表视图。</p></td>
</tr>
<tr class="even">
<td><p><img src="images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif" title="更多选项图标" alt="更多选项图标" /></p></td>
<td><p>更多选项</p></td>
<td><p>使用此图标可查看您能对相应选项卡的对象另外执行哪些操作。例如，在“收件人”&gt;“邮箱”中，单击此图标可显示以下选项：“禁用”、“添加/删除列”、“将数据导出到 CSV 文件”、“连接邮箱”和“高级搜索”。</p></td>
</tr>
<tr class="odd">
<td><p><img src="images/JJ150576.1732c727-328b-4a1a-b84d-6d7252c7dcab(EXCHG.150).gif" title="向上键图标" alt="向上键图标" />   <img src="images/JJ150576.ef5ca57d-a033-457b-bd92-6361877c33d0(EXCHG.150).gif" title="向下键图标" alt="向下键图标" /></p></td>
<td><p>向上箭头和向下箭头</p></td>
<td><p>使用这些图标可提升或降低对象的优先级。例如，在“邮件流”&gt;“电子邮件地址策略”中，单击向上箭头可以提升电子邮件地址策略的优先级。您还可以使用这些箭头导航公用文件夹层次结构，以及在列表视图中将规则上移或下移。</p></td>
</tr>
<tr class="even">
<td><p><img src="images/JJ657480.ed7f7abf-39d8-4f43-a918-ccb3bff87ef5(EXCHG.150).gif" title="复制图标" alt="复制图标" /></p></td>
<td><p>复制</p></td>
<td><p>使用此图标可复制对象，以便在不更改原始对象的情况下对其进行更改。例如，在“权限”&gt;“管理员角色”中，从列表视图中选择一个角色，然后单击此图标可以根据现有角色组新建一个角色组。</p></td>
</tr>
<tr class="odd">
<td><p><img src="images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif" title="删除图标" alt="删除图标" /></p></td>
<td><p>删除</p></td>
<td><p>使用此图标可从列表中删除项目。例如，在“公用文件夹权限”对话框中，通过选择用户并单击此图标，可将用户从允许访问公用文件夹的用户列表中删除。</p></td>
</tr>
</tbody>
</table>


## 列表视图

单击某个选项卡时，在大多数情况下，将会看到一个列表视图。EAC 中的列表视图设计可消除 ECP 中存在的限制。ECP 最多只能显示 500 个对象；如果要查看详细信息窗格中未列出的对象，需要使用搜索和筛选选项查找这些特定对象。在 Exchange 2013 中，可从 EAC 列表视图内部查看的限制大约为 20,000 个对象（针对内部部署），在 Exchange Online 中为 10,000 个。此外还包括了分页功能，因此可以对结果进行分页。在“收件人”列表视图中，还可以配置页面大小以及将数据导出到 CSV 文件。

## 详细信息窗格

从列表视图中选择对象时，有关该对象的信息将在详细信息窗格中显示。在有些情况下（例如，处理收件人对象），详细信息窗格包含快速管理任务。例如，如果导航到“收件人”\>“邮箱”并从列表视图中选择一个邮箱，则详细信息窗格将显示一个用于为该邮箱启用或禁用存档的选项。详细信息窗格还可用于批量编辑多个对象。只需按下 Ctrl 键，选择要进行批量编辑的对象，然后使用详细信息窗格中的选项。例如，通过选择多个邮箱，可以批量更新用户的联系人和组织信息、自定义属性、邮箱配额、Outlook Web App 设置等。

## 通知

EAC 中有一个通知查看器，可显示长时间运行的进程的状态，并在进程完成时提供通知。此外，尤其是对于长时间运行的进程（如移动请求），可以选择接收电子邮件通知。

## 自有图块和帮助

使用*自有图块*可以注销 EAC，然后以其他用户身份登录。从“帮助”![帮助图标](images/JJ150562.a32eac4e-345d-4236-a284-204390aff4ee(EXCHG.150).gif "帮助图标") 下拉菜单中，您可以执行下列操作：

  - **帮助**   单击 ![帮助图标](images/JJ150562.a32eac4e-345d-4236-a284-204390aff4ee(EXCHG.150).gif "帮助图标") 可查看联机帮助内容。

  - **禁用帮助气泡**   当您创建或编辑对象时，帮助泡气会显示字段的上下文相关帮助。您可以关闭“帮助”气泡，如果已被禁用，也可以打开它。

  - **版权和隐私**   单击隐私或版权链接可阅读 Exchange 2013 的版权和隐私信息。

## 支持的浏览器

为获得最佳 EAC 体验，使用标记为“最佳”的操作系统和浏览器组合之一。

> [!NOTE]
> 不支持上表中未列出的其他操作系统和浏览器组合（包括 touch）。


  - “**最佳**”：支持所有功能并经过完全测试。

  - “**支持**”：具有相同的最佳功能支持。然而，支持的浏览器将缺少浏览器和操作系统组合不支持的功能。

  - “**不支持**”：不支持或未经测试的浏览器和操作系统。


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Web 浏览器</p></td>
<td><p>Windows XP 和 Windows Server 2003</p></td>
<td><p>Windows Vista</p></td>
<td><p>Windows 7 和 Windows Server 2008</p></td>
<td><p>Windows 8 和 Windows Server 2012</p></td>
<td><p>Mac OSX</p></td>
<td><p>Linux</p></td>
</tr>
<tr class="even">
<td><p>Internet Explorer 8</p></td>
<td><p>支持</p></td>
<td><p>支持</p></td>
<td><p>高级</p></td>
<td><p>不支持</p></td>
<td><p>不支持</p></td>
<td><p>不支持</p></td>
</tr>
<tr class="odd">
<td><p>Internet Explorer 9</p></td>
<td><p>不支持</p></td>
<td><p>支持</p></td>
<td><p>高级</p></td>
<td><p>不支持</p></td>
<td><p>不支持</p></td>
<td><p>不支持</p></td>
</tr>
<tr class="even">
<td><p>Internet Explorer 10 或更高版本</p></td>
<td><p>不支持</p></td>
<td><p>支持</p></td>
<td><p>高级</p></td>
<td><p>高级</p></td>
<td><p>不支持</p></td>
<td><p>不支持</p></td>
</tr>
<tr class="odd">
<td><p>Firefox 11 或更高版本</p></td>
<td><p>支持</p></td>
<td><p>支持</p></td>
<td><p>高级</p></td>
<td><p>高级</p></td>
<td><p>高级</p></td>
<td><p>支持</p></td>
</tr>
<tr class="even">
<td><p>Safari 5.1 或更高版本</p></td>
<td><p>不支持</p></td>
<td><p>不支持</p></td>
<td><p>不支持</p></td>
<td><p>不支持</p></td>
<td><p>高级</p></td>
<td><p>不支持</p></td>
</tr>
<tr class="odd">
<td><p>Chrome 18 或更高版本</p></td>
<td><p>支持</p></td>
<td><p>支持</p></td>
<td><p>高级</p></td>
<td><p>高级</p></td>
<td><p>高级</p></td>
<td><p>不支持</p></td>
</tr>
</tbody>
</table>

