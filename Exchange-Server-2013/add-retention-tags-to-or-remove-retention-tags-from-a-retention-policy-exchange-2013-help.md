---
title: '向保留策略添加保留标记或从中删除保留标记: Exchange Online Help'
TOCTitle: 向保留策略添加保留标记或从中删除保留标记
ms:assetid: 3a5196ce-2764-453d-9bc1-5ec22d06b40d
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd362328(v=EXCHG.150)
ms:contentKeyID: 50490345
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 向保留策略添加保留标记或从中删除保留标记

 

_**适用于：**Exchange Online, Exchange Server 2013_

_**上一次修改主题：**2015-03-02_

在创建策略时或之后的任何时候，都可以将保留标记添加到保留策略。有关如何创建保留策略（包括如何同时添加保留标记）的详细信息，请参阅[创建保留策略](create-a-retention-policy-exchange-2013-help.md)。

保留策略可以包含以下保留标记：

  - 支持的默认文件夹的一个或多个保留策略标记 (RPT)

  - 一个带有\&quot;移动到存档\&quot;操作的默认策略标记 (DPT)

  - 一个具有\&quot;删除但允许恢复\&quot;或\&quot;永久删除\&quot;操作的 DPT

  - 语音邮件的一个 DPT

  - 任意数量的个人标记

有关保留标记的详细信息，请参阅[保留标记和保留策略](retention-tags-and-retention-policies-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：10 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [收件人权限](recipients-permissions-exchange-2013-help.md)主题中的\&quot;邮件记录管理\&quot;条目。

  - 在保留标记链接到保留策略并且由托管文件夹助理处理某个邮箱之前，保留标记不会应用于该邮箱。若要启动托管文件夹助理处理邮箱，请参阅[配置托管文件夹助理](configure-the-managed-folder-assistant-exchange-2013-help.md)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。</td>
</tr>
</tbody>
</table>


## 您想执行什么操作？

## 使用 EAC 添加或删除保留标记

1.  转到\&quot;合规性管理\&quot;\>\&quot;保留策略\&quot;。

2.  在列表视图中，选择要添加保留标记的保留策略，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在\&quot;保留策略\&quot;中，使用下列设置：
    
      - **添加** ![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")   单击此按钮向策略中添加保留标记。
    
      - **删除** ![删除图标](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "删除图标")   从列表中选择一个标记，然后单击此按钮从策略中删除该标记。

## 使用命令行管理程序添加或删除保留标记

此示例将保留标记 VPs-Default、VPs-Inbox 和 VPs-DeletedItems 添加到保留策略 RetPolicy-VPs 中，该策略尚未链接保留标记。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876845.Caution(EXCHG.150).gif" title="小心" alt="小心" />小心：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果该策略已链接了保留标记，则此命令会替换现有标记。</td>
</tr>
</tbody>
</table>


    Set-RetentionPolicy -Identity "RetPolicy-VPs" -RetentionPolicyTagLinks "VPs-Default","VPs-Inbox","VPs-DeletedItems"

本示例将保留标记 VPs-DeletedItems 添加到保留策略 RetPolicy-VPs，该策略已经链接其他保留标记。

    $TagList = (Get-RetentionPolicy "RetPolicy-VPs").RetentionPolicyTagLinks
    $TagList.Add((Get-RetentionPolicyTag 'VPs-DeletedItems').DistinguishedName)
    Set-RetentionPolicy "RetPolicy-VPs" -RetentionPolicyTagLinks $TagList

此示例从保留策略 RetPolicy-VPs 中删除保留标记 VPs-Inbox。

    $TagList = (Get-RetentionPolicy "RetPolicy-VPs").RetentionPolicyTagLinks
    $TagList.Remove((Get-RetentionPolicyTag 'VPs-Inbox').DistinguishedName)
    Set-RetentionPolicy "RetPolicy-VPs" -RetentionPolicyTagLinks $TagList

有关语法和参数的详细信息，请参阅 [Set-RetentionPolicy](https://technet.microsoft.com/zh-cn/library/dd335196\(v=exchg.150\)) 和 [Get-RetentionPolicy](https://technet.microsoft.com/zh-cn/library/dd298086\(v=exchg.150\))。

## 您如何知道这有效？

要验证您是否已成功向保留策略中添加或从中删除了保留标记，请使用 [Get-RetentionPolicy](https://technet.microsoft.com/zh-cn/library/dd298086\(v=exchg.150\)) cmdlet 验证 *RetentionPolicyTagLinks* 属性。

本示例使用 **Get-RetentionPolicy** cmdlet 检索添加到\&quot;默认 MRM 策略\&quot;的保留标记，然后将这些标记传递给 **Format-Table** cmdlet，从而仅输出每个标记的名称属性。

    (Get-RetentionPolicy "Default MRM Policy").RetentionPolicyTagLinks | Format-Table name

