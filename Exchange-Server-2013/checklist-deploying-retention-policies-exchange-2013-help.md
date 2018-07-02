---
title: '检查表：部署保留策略: Exchange 2013 Help'
TOCTitle: 检查表：部署保留策略
ms:assetid: 59e299fd-b6a8-48f5-88ae-dc20dbe32e90
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Ee364743(v=EXCHG.150)
ms:contentKeyID: 50490616
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 检查表：部署保留策略

 

_**适用于：**Exchange Online, Exchange Server 2013_

_**上一次修改主题：**2016-12-09_

使用此检查表可在 Microsoft Exchange Server 2013 组织中部署保留策略。在开始使用此检查表之前，请确保您熟悉以下主题中的概念：

  - [邮件记录管理](messaging-records-management-exchange-2013-help.md)

  - [保留标记和保留策略](retention-tags-and-retention-policies-exchange-2013-help.md)

## 用于部署保留策略的检查列表


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>完成？</th>
<th>任务</th>
<th>资源</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p> </p></td>
<td><p>评估不同用户组的邮件记录管理 (MRM) 要求。</p></td>
<td><p><a href="messaging-records-management-exchange-2013-help.md">邮件记录管理</a></p></td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>确定正在使用哪些 Microsoft Outlook 客户端版本。</p></td>
<td><p>解析 <code>%ExchangeInstallPath%Logging\RPC Client Access</code> 处的 RPC 客户端访问日志文件。</p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>创建保留标记。</p></td>
<td><p><a href="create-a-retention-policy-exchange-2013-help.md">创建保留策略</a></p></td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>创建保留策略。</p></td>
<td><p><a href="create-a-retention-policy-exchange-2013-help.md">创建保留策略</a></p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>将保留标记添加到保留策略。</p></td>
<td><p><a href="add-retention-tags-to-or-remove-retention-tags-from-a-retention-policy-exchange-2013-help.md">向保留策略添加保留标记或从中删除保留标记</a></p></td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>将邮箱置于保留挂起状态。</p></td>
<td><p><a href="place-a-mailbox-on-retention-hold-exchange-2013-help.md">放置的邮箱上保留挂起</a></p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>将保留策略应用于单个邮箱以进行测试。</p></td>
<td><p><a href="apply-a-retention-policy-to-mailboxes-exchange-2013-help.md">将保留策略应用于邮箱</a></p></td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>可选：实现客户端阻止功能以阻止旧版 Outlook 客户端。</p></td>
<td><p><a href="configure-outlook-client-blocking-exchange-2013-help.md">为邮件记录管理配置 Outlook 客户端阻止</a></p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>开始用户沟通和培训活动。包含处理保留策略以及移动或删除项目的截止时间。</p></td>
<td><p>不适用</p></td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>将保留策略应用于其他邮箱。</p></td>
<td><p><a href="apply-a-retention-policy-to-mailboxes-exchange-2013-help.md">将保留策略应用于邮箱</a></p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>提前几天提醒用户已临近截止日期。</p></td>
<td><p>不适用</p></td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>在截止日期，从邮箱删除保留挂起。</p></td>
<td><p><a href="place-a-mailbox-on-retention-hold-exchange-2013-help.md">放置的邮箱上保留挂起</a></p></td>
</tr>
</tbody>
</table>

