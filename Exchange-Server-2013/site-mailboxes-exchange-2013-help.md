---
title: '网站邮箱: Exchange 2013 Help'
TOCTitle: 网站邮箱
ms:assetid: 2c4393f4-d274-4e6c-bd09-9577e68c5a33
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ150499(v=EXCHG.150)
ms:contentKeyID: 50490246
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 网站邮箱

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2016-12-09_

电子邮件和文档传统上保存在两个唯一且单独的数据存储库中。大多数组织通过两个媒体进行协作。难题在于使用不同的客户端访问电子邮件和文档。这通常会导致用户工作效率降低和用户体验降级。

*网站邮箱*是 Microsoft Exchange 2013 中旨在解决此问题的一个新概念。网站邮箱通过允许用户使用相同的客户端接口同时访问 Microsoft SharePoint 2013 文档和 Exchange 电子邮件，从而改进协作和提高用户工作效率。网站邮箱在功能上由 SharePoint 2013 网站成员身份（所有者和成员）、通过用于电子邮件的 Exchange 2013 邮箱和用于文档的 SharePoint 2013 网站共享的存储，以及满足设置和生命周期需求的管理接口组成。

网站邮箱需要 Exchange 2013 和 SharePoint Server 2013 集成和配置。有关如何将 Exchange 2013 组织配置为与 SharePoint Server 2013 组织协作的详细信息，请参阅下列主题：

  - [在 SharePoint Server 2013 中配置网站邮箱](https://go.microsoft.com/fwlink/p/?linkid=258264)。

  - [与 SharePoint 和 Lync 的集成](integration-with-sharepoint-and-lync-exchange-2013-help.md)

有关 Exchange Server 2013 中的协作功能的详细信息，请参阅[协作](collaboration-exchange-2013-help.md)。

**目录**

网站邮箱的工作方式

网站邮箱设置策略

## 网站邮箱的工作方式

一个项目成员使用网站邮箱归档邮件或文档后，任何项目成员均可访问相应内容。用户可以使用 Outlook 2013 中的站点邮箱轻松访问他们所关心的项目的电子邮件和文档。此外，还可以从本身的 SharePoint 站点直接访问同一个内容集。使用网站邮箱时，内容保留在其所属的位置。Exchange 存储电子邮件，为用户提供与用户自己的邮箱日常所使用的邮件视图一样的电子邮件会话邮件视图。同时，SharePoint 存储文档，并将文档合著和版本控制合并到表格中。Exchange 从 SharePoint 中同步适量元数据用于创建 Outlook 中的文档视图（例如文档标题、上次修改日期、上次修改作者、大小）。

![网站邮箱存储和使用情况图](images/JJ150499.b98be571-d2e0-4ebd-9fe2-440a14e91e35(EXCHG.150).gif "网站邮箱存储和使用情况图")

## 网站邮箱设置策略

可通过使用 Exchange 命令行管理程序中的 **SiteMailboxProvisioningPolicy** cmdlet 设置网站邮箱配额。网站邮箱设置策略仅适用于发送到网站邮箱和从网站邮箱发送的电子邮件，以及 Exchange 服务器上网站邮箱的大小。在 SharePoint 中配置文档库设置。尽管您可以使用 **New-SiteMailboxProvisioningPolicy** cmdlet 创建多个网站邮箱设置策略，但只有默认设置策略才会应用到所有网站邮箱。您不能在组织内应用多个策略。通过设置策略，您可以设置以下配额：


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>配额</th>
<th>描述</th>
<th>默认设置</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>IssueWarningQuota</p></td>
<td><p><em>IssueWarningQuota</em> 参数指定触发网站邮箱警告消息的网站邮箱大小。</p></td>
<td><p>4.5 GB</p></td>
</tr>
<tr class="even">
<td><p>MaxReceiveSize</p></td>
<td><p><em>MaxReceiveSize</em> 参数指定站点邮箱可以接收的最大电子邮件大小。</p></td>
<td><p>36 MB</p></td>
</tr>
<tr class="odd">
<td><p>ProhibitSendReceiveQuota</p></td>
<td><p><em>ProhibitSendReceiveQuota</em> 参数指定站点邮箱无法再发送或接收邮件时的大小。</p></td>
<td><p>5 GB</p></td>
</tr>
</tbody>
</table>


有关如何配置网站邮箱设置策略的详细信息，请参阅[管理站点邮箱设置策略](manage-site-mailbox-provisioning-policies-exchange-2013-help.md)。

网站邮箱的工作方式

## 生命周期策略和保留

网站邮箱的生命周期是通过 SharePoint 进行管理。您应通过 SharePoint 执行所有的网站邮箱任务，例如，创建和删除网站邮箱。此外，您还可以创建 SharePoint 生命周期策略来管理网站邮箱的生命周期。例如，您可以在 SharePoint 中创建在 6 个月后自动关闭所有网站邮箱的生命周期策略。如果用户仍要求使用网站邮箱，则可以通过 SharePoint 重新激活相应的网站邮箱。我们建议您在场中使用生命周期应用程序。手动从 Exchange 中删除活动的网站邮箱将会孤立相应的网站邮箱。.

当 SharePoint 中的生命周期应用程序关闭某个网站邮箱时，该网站邮箱将按照生命周期策略中指示的时间段保留为关闭状态。然后，最终用户或管理员可以通过 SharePoint 重新激活该邮箱。保留期过后，邮箱数据库内部的 Exchange 网站邮箱的名称将预置有前缀“MDEL:”，以指示它具有删除标记。您将需要手动从邮箱数据库中删除这些网站邮箱，以便释放存储空间和别名。如果您未启用 SharePoint 生命周期策略，则无法确定哪些网站邮箱具有删除标记。在管理员删除网站邮箱之前，邮箱的内容仍可恢复。

可以使用以下命令来搜索并删除具有删除标记的网站邮箱。

```powershell
    Get-Mailbox MDEL:* | ?{$_.RecipientTypeDetails -eq "TeamMailbox"} | Remove-Mailbox -Confirm:$false
```

网站邮箱不支持项级别保留，但您可以在项目一级保留网站邮箱。因此当您删除整个网站邮箱时，保留的项也会删除。

## 合规性

使用 SharePoint 中的电子数据展示控制台时，网站邮箱会包括在就地电子数据展示范围内，因为您可以针对用户邮箱或网站邮箱执行关键字搜索。此外，您还可以将网站邮箱置于合法保留状态。有关详细信息，请参阅[就地电子数据展示](https://docs.microsoft.com/zh-cn/exchange/security-and-compliance/in-place-ediscovery/in-place-ediscovery)。

> [!NOTE]  
> 要在 Office 365 中将网站邮箱置于法定保留状态，必须向其分配 Exchange Online（计划 2）许可证。如果向网站邮箱分配的是 Exchange Online（计划 1）许可证，必须向其分配单独的 Exchange Online 存档许可证才能将其置于保留状态。


网站邮箱的工作方式

## 备份和还原

邮箱服务器内部的 Exchange 网站邮箱的备份和还原方法与其他所有 Exchange 邮箱相同。有关详细信息，请参阅[数据库可用性组 (DAG)](database-availability-groups-dags-exchange-2013-help.md)。

应将 SharePoint 文档备份和还原到相同的位置。如果将 SharePoint 内容还原到相同的 URL，那么网站邮箱将会继续工作，无需您进行其他任何配置。如果还原到不同的 URL，则需要运行 **Set-SiteMailbox** cmdlet 来更新 *SharePointURL* 属性。我们建议您不要将 SharePoint 内容还原到新林。

