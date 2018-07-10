---
title: '公用文件夹的限制: Exchange 2013 Help'
TOCTitle: 公用文件夹的限制
ms:assetid: 709b075e-9584-484b-bcaa-e781c26497b4
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dn594582(v=EXCHG.150)
ms:contentKeyID: 61170967
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 公用文件夹的限制

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2016-12-09_

在 Exchange Server 2013 中，我们已将公用文件夹从传统数据库体系结构移至邮箱体系结构中。这一转变让公用文件夹能够从数据库可用性组 (DAG) 的弹性机制及其他历时多年创建的邮箱增强功能等事项中获益。但是，有新的限制和性能注意事项应该予以考虑。在本文档中，针对您所拥有的可能会影响公用文件夹性能和连接的配置选项，我们提供了一些高级别指南。

## 限制

下表列出了本地 Exchange Server 2013 中公用文件夹的限制。除非特别指出限制是推荐值，否则此表列出的值就是公用文件夹的支持限制。

> [!important]
> 若要了解针对 Office 365 的 Exchange Online 限制，请参阅 <a href="https://go.microsoft.com/fwlink/?linkid=391188">Exchange Online 限制</a>。



<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>项目</th>
<th>限制</th>
<th>注释</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>公用文件夹邮箱总数</p></td>
<td><p>100</p></td>
<td><p>尽管您可以创建超过 100 个公用文件夹邮箱，但不受支持。<a href="create-a-public-folder-mailbox-exchange-2013-help.md">创建公用文件夹邮箱</a></p></td>
</tr>
<tr class="even">
<td><p>层次结构中的公用文件夹总数</p></td>
<td><p>1,000,000</p></td>
<td><p>尽管您可以创建超过 1,000,000 个公用文件夹，但这并不受支持。对于不少于 100,000 个公用文件夹的任何部署，我们建议您阅读<a href="considerations-when-deploying-public-folders-exchange-2013-help.md">部署公用文件夹时的注意事项</a>。</p></td>
</tr>
<tr class="odd">
<td><p>父文件夹下的子文件夹数</p></td>
<td><p>10,000</p></td>
<td><p>尽管您可以在父文件夹下创建超过 1000 个子文件夹，但建议您不要这样做。</p>
<p><a href="https://technet.microsoft.com/zh-cn/library/bb123981(v=exchg.150)">Set-Mailbox</a> cmdlet 中的 <em>FolderHierarchyChildrenCountReceiveQuota</em> 参数。</p></td>
</tr>
<tr class="even">
<td><p>文件夹深度</p></td>
<td><p>300</p></td>
<td><p>文件夹深度是指在公用文件夹树的一个分支中可以存在的嵌套文件夹数量级。<a href="https://technet.microsoft.com/zh-cn/library/bb123981(v=exchg.150)">Set-Mailbox</a> cmdlet 中的 <em>FolderHierarchyDepthRecieveQuota</em> 参数。</p></td>
</tr>
<tr class="odd">
<td><p>每个公用文件夹的最大邮件数</p></td>
<td><p>1 百万</p></td>
<td><p><a href="https://technet.microsoft.com/zh-cn/library/bb123981(v=exchg.150)">Set-Mailbox</a> cmdlet 中的 <em>MailboxMessagesPerFolderCountRecieveQuota</em> 参数。</p></td>
</tr>
<tr class="even">
<td><p>单个公用文件夹的最大大小</p></td>
<td><p>10 GB</p></td>
<td><p>此限制不包括单个文件夹下的子文件夹。</p>
<p><a href="configure-storage-quotas-for-a-mailbox-exchange-2013-help.md">配置邮箱的存储配额</a></p></td>
</tr>
<tr class="odd">
<td><p>公用文件夹的邮箱大小</p></td>
<td><p>100 GB</p></td>
<td><p><a href="configure-storage-quotas-for-a-mailbox-exchange-2013-help.md">配置邮箱的存储配额</a></p></td>
</tr>
<tr class="even">
<td><p>每个公用文件夹邮箱的用户登录数</p></td>
<td><p>2,000 个并发用户登录</p></td>
<td><p>我们建议您配置层次结构，以便使每个公用文件夹邮箱的用户数不超过 2,000 个。例如，如果您有 20,000 个用户，则应有 10 个公用文件夹邮箱。</p></td>
</tr>
<tr class="odd">
<td><p>已移动项目的保留时间</p></td>
<td><p>推荐为 14 天</p></td>
<td><p>使用 <strong>Set-OrganizationConfig</strong> cmdlet 中的 <em>DefaultPublicFolderMovedItemRetention</em> 参数。</p></td>
</tr>
<tr class="even">
<td><p>期限限制</p></td>
<td><p>我们建议您按照用于常规邮箱的默认设置对此进行相同设置。</p></td>
<td><p>这些设置可以在以下级别设置：</p>
<ul>
<li><p><strong>组织级别：</strong> <strong>Set-OrganizationConfig</strong> cmdlet 中的 <em>DefaultPublicFolderAgeLimit</em> 参数。</p></li>
<li><p><strong>邮箱级别：</strong> <strong>Set-Mailbox</strong> cmdlet 中的 <em>AgeLimit</em> 参数。</p></li>
<li><p><strong>文件夹级别：</strong> <strong>Set-PublicFolder</strong> cmdlet 中的 <em>AgeLimit</em> 参数。</p></li>
</ul>
<p></p></td>
</tr>
<tr class="odd">
<td><p>已删除项目的保留时间</p></td>
<td><p>我们建议您按照用于常规邮箱的默认设置对此进行相同设置。</p></td>
<td><p>这些设置可以在以下级别设置：</p>
<ul>
<li><p><strong>组织级别：Set-OrganizationConfig cmdlet 中的</strong> <em>DefaultPublicFolderMovedItemRetention</em> 参数。</p></li>
<li><p><strong>邮箱级别：</strong> <strong>Set-Mailbox</strong> cmdlet 中的 <em>RetainDeletedItemsFor</em>。</p></li>
<li><p><strong>文件夹级别：</strong> <strong>Set-PublicFolder</strong> cmdlet 中的 <em>RetainDeleteItemsFor</em> 参数。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>可以迁移到 Exchange 2013 的公用文件夹的数量上限。</p></td>
<td><p>500,000</p></td>
<td><p>这是指在一次迁移中可从旧版 Exchange 移到 Exchange 2013 的公用文件夹的数量上限。若要详细了解如何迁移公用文件夹，请参阅<a href="use-batch-migration-to-migrate-public-folders-to-exchange-2013-from-previous-versions-exchange-2013-help.md">使用批处理迁移将公用文件夹从以前版本迁移到 Exchange 2013</a></p></td>
</tr>
</tbody>
</table>

