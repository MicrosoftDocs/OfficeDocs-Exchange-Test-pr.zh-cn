---
title: '为 Exchange 2010 准备 Active Directory 后，无法安装 Exchange 2007 角色'
TOCTitle: 为 Exchange 2010 准备 Active Directory 后，无法安装 Exchange 2007 角色 (_NoE12ServerWarning)
ms:assetid: 4e579f69-0de9-421c-ba31-4e63a25e6a45
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/ms.exch.setupreadiness.noe12serverwarning(v=EXCHG.150)
ms:contentKeyID: 50490530
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 为 Exchange 2010 准备 Active Directory 后，无法安装 Exchange 2007 角色 (\_NoE12ServerWarning)

 

_**适用于：** Exchange Server_

_**上一次修改主题：** 2016-12-09_

此主题中的内容尚未针对 Microsoft Exchange Server 2013 进行更新。虽然尚未更新，但仍可能适用于 Exchange 2013。如果您仍需要帮助，请查看下面的社区资源。

遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

运行 Microsoft Exchange Server 2010**Setup /PrepareAD** 时，Microsoft Exchange Server 分析工具会查询现有的 Active Directory 拓扑，以确定是否存在任何 Microsoft Exchange Server 2007 服务器角色。如果没有检测到 Exchange 2007 服务器角色，则会收到以下警告消息：


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>安装程序将通过“Setup /PrepareAD”为组织准备 Exchange Server 2010，但是在该拓扑中没有检测到 Exchange Server 2007 角色。在此操作后，将无法安装任何 Exchange Server 2007 角色。</p></td>
</tr>
</tbody>
</table>


在部署 Exchange Server 2010 之前，考虑以下因素，这可能需要您在部署 Exchange 2007 之前，使用所有已安装的服务器角色部署 Exchange 2007 服务器：

  - **第三方或内部已开发应用程序**   为 Exchange 2003 开发的应用程序可能与 Exchange 2010 不兼容，因此需要升级或更换。您可以维持 Exchange 2003 上的这些应用程序和关联用户总数；移动到 Exchange 2007；或使用 Exchange 2010 的兼容版本更换软件。

  - **共存或迁移要求**   如果您计划将邮箱迁移到您的组织，您可以部署 Exchange 2007，并使用 Microsoft Transporter 套件，或可以使用第三方共存或迁移解决方案。要下载 Microsoft Transporter Suite，请转到 Microsoft 下载中心的 [Microsoft Transporter Suite](http://go.microsoft.com/fwlink/?linkid=82688)。

此外，在为您的组织评估选项时，请务必考虑以下问题：

  - 是否制定了策略在 Exchange 2003 退役前将从属的应用程序移到 Exchange 2010 中？有关详细信息，请访问 Microsoft 支持生命周期 Web 页 ([https://go.microsoft.com/fwlink/?LinkID=55839](https://go.microsoft.com/fwlink/?linkid=55839))。

  - 您的策略是否需要 WebDAV 和 Web 服务共存 (Exchange 2007)?

  - 您是否考虑过支持 Exchange 的第三方产品或其他允许您满足共存或迁移要求的 Microsoft 技术？

  - 您的硬件生命周期方法是什么（继续尽可能使用现有 32 位服务器对购买新的 64 位服务器）？

  - 您的迁移计划是什么（尽快迁移所有服务器还是阶段性迁移策略）？同样，您的不同 Exchange 版本的共存时间线是什么？

如果您决定在部署 Exchange 2010 之前需要部署 Exchange 2007，部署单个带所有服务器角色的 Exchange 2007 足以允许在组织中部署未来 Exchange 2007。要将 Exchange 2007 服务器部署到您的 Exchange 2003 组织，请执行下列步骤：

1.  运行 Exchange 2007**Setup /PrepareSchema**。

2.  运行 Exchange 2007**Setup /PrepareAD**。

3.  在所有包含 Exchange 服务器可使用的收件人、Exchange 2003 服务器或全局编录的域上运行 Exchange 2007**Setup /PrepareDomain**。

4.  安装带所有四个服务器角色（集线器传输、客户端访问、邮箱和统一消息）的 Exchange 2007 服务器。

