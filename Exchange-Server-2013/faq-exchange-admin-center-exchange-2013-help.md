---
title: '常见问题：Exchange 管理中心: Exchange 2013 Help'
TOCTitle: 常见问题：Exchange 管理中心
ms:assetid: 3de0042f-74a6-458f-947c-3cd6eeacd6ab
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ552409(v=EXCHG.150)
ms:contentKeyID: 50490357
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 常见问题：Exchange 管理中心

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2015-03-09_

本主题提供了一系列有关 Microsoft Exchange Server 2013 中新的 Exchange 管理中心 (EAC) 的常见问题。还有其他此处未回答的关于 EAC 的问题？给我们发送电子邮件，地址是 [Ex2013HelpFeedback@microsoft.com](mailto:ex2013helpfeedback@microsoft.com)。

## EAC 是专为 Exchange Online 开发的吗？

EAC 可为 Exchange 2013 提供所有部署选项，包括希望进行内部部署、使用 Exchange Online 在云中部署或者混合部署的客户。

## 您是否曾因主要为中小客户构建接口而放弃 Exchange 管理控制台 (EMC)？

EAC 旨在为所有类型的客户提供单一、直观的管理体验，并且设计上有助于更加简单地执行最常见的管理任务。

我们创建的单一接口可提供一系列比 Exchange 管理控制台 (EMC) 和 Exchange 控制面板 (ECP) 更为丰富广泛的方案，并能为客户解决诸多关键性挑战和满足他们的各种方案需求。

另外，我们听取了各种规模客户的意见，发现他们主要有以下几点顾虑：

  - 为使管理工具正常运行而维护和下载修补程序对客户来说是一项运营开销，反过来会增加运营成本。

  - 随着 IT 工作人员变得越来越具有移动性，客户希望能够在任何地方管理他们的环境，而不只限于通过安装了管理工具的台式机和服务器。

  - 针对不同的部署选项使用多种工具会造成混淆并会增加培训和运营成本

## EAC 是否会恢复使用 PowerShell 日志记录和 cmdlet 曝光功能？

我们已经听取了早期客户关于这一问题的反馈，并计划在将来的更新中评估解决此问题的可能性。

## EMC 会再引入一个 Service Pack 吗？

否，我们全力支持 EAC 体验。

## 能否使用 Exchange 2010 的 EMC 来管理 Exchange 2013 对象？

不能。您不能使用 Exchange 2010 的 EMC 管理 Exchange 2013 的对象和服务器。当客户升级到 Exchange 2013 之后，我们鼓励客户使用 EAC 执行下列任务：

1.  管理 Exchange 2013 邮箱、服务器和对应的服务。

2.  查看并更新 Exchange 2010 邮箱和属性。

3.  查看并更新 Exchange 2007 邮箱和属性。

我们鼓励客户使用 Exchange 2010 EMC 来创建和管理 Exchange 2010 邮箱。

我们鼓励客户使用 Exchange 2007 EMC 来创建和管理 Exchange 2007 邮箱。

客户可继续使用 Exchange 命令行管理程序和脚本任务来执行管理任务。

## 为什么搜索框不始终保持可见状态？

这体现了我们设计 Exchange 2013 的一项原则：除非您真正需要使用它，否则希望您不受任何干扰。这一简洁性原则体现在包括 EAC 在内的所有产品的最终用户体验之中。当单击图标后，搜索框便会滑出。它不仅为用户在文本框内键入查询提供充足的空间，还提供会在出现实时查询匹配时显示的下拉提示菜单。这种改进使我们能够隐藏不必要的复杂性，同时不会减少管理体验。我们将继续根据大家的反馈意见提升所有用户体验。

## EAC 能否在平板电脑上正常运行？

EAC 目前尚不支持通过平板电脑和移动设备进行管理。

## 当我尝试访问 Exchange 2013 EAC 时，为什么会打开 Exchange 2010 ECP？

如果您的邮箱位于 Exchange 2010 邮箱服务器上，Exchange 2010 ECP 会在您的浏览器中自动加载。这是设计造成的。可以通过向 URL 添加 Exchange 版本的方式来访问 EAC。例如，如果要访问其虚拟目录托管在客户端访问服务器 CAS01-NA 上的 EAC，请使用下列 URL：`https://CAS01-NA/ecp?ExchClientVer=15`.

## 你们对 EAC 的使用地点有何限制？

为了限制 Internet 访问（而不是 Intranet 访问），Exchange 在 IIS 中提供了虚拟目录级别的分区。管理员可以显式地允许或拒绝由外部 Internet 客户端（例如未加入企业防火墙内的某个域的客户端）执行 IT 管理的方案。有关详细信息，请参阅[关闭对 Exchange 管理中心的访问](turn-off-access-to-the-exchange-admin-center-exchange-2013-help.md)。

## Exchange 2013 工具箱有哪些变化？

在 Exchange 2007 和 Exchange 2010 中，EMC 中包含的工具箱提供了各种用于管理 Exchange 组织的工具。Exchange 2013 的工具箱较以前的版本有较大幅度的缩减。在 Exchange 2013 工具箱中，仍然可以使用详细信息模板编辑器、远程连接分析器和队列查看器。剩余的工具或被用作其他用途，或被移到 EAC 中。

下表列出了对 Exchange 2013 工具箱所做的更改：


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>工具</th>
<th>当前状态</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange 最佳实践分析工具 (ExBPA)</p></td>
<td><p>ExBPA 已停用。准备情况检查已替代了 ExBPA，用于确保 Active Directory 林和 Exchange 服务器已准备好安装 Exchange 2013。各项准备情况检查主题均介绍了适当的做法来解决运行准备情况检查时发现的问题。如果安装过程中显示准备情况检查，那么您只能执行该准备情况检查主题中列出的步骤。</p></td>
</tr>
<tr class="even">
<td><p>邮件流故障排除程序</p></td>
<td><p>邮件流故障排除程序已停用。您现在可以使用 EAC 中的邮件跟踪功能。转到“邮件流”&gt;“传递报告”。</p></td>
</tr>
<tr class="odd">
<td><p>性能监视器</p></td>
<td><p>性能监视器已从工具箱中停用。您仍可以在 Windows Server 2008 和 Windows Server 2012 的“管理工具”下找到性能监视器。</p></td>
</tr>
<tr class="even">
<td><p>性能故障排除程序</p></td>
<td><p>性能故障排除程序已从工具箱中停用。</p></td>
</tr>
<tr class="odd">
<td><p>路由日志查看器</p></td>
<td><p>路由日志查看器已停用。</p></td>
</tr>
<tr class="even">
<td><p>公用文件夹管理控制台</p></td>
<td><p>现在从 EAC 内管理公用文件夹。在 EAC 中，转到“公用文件夹”。</p></td>
</tr>
<tr class="odd">
<td><p>基于角色的访问控制 (RBAC) 用户编辑器</p></td>
<td><p>现在从 EAC 内管理 RBAC。在 EAC 中，转到“权限”。</p></td>
</tr>
</tbody>
</table>

