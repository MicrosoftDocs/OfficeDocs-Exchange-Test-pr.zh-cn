---
title: '将保留策略应用于邮箱: Exchange Online Help'
TOCTitle: 将保留策略应用于邮箱
ms:assetid: 6ccc80db-d201-44f7-8d4b-473a89c14b2f
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd298052(v=EXCHG.150)
ms:contentKeyID: 50490883
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 将保留策略应用于邮箱

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2014-10-01_

使用保留策略可以对一个或多个保留标记进行分组，并将它们应用于邮箱以执行邮件保留设置。一个邮箱不能有多个保留策略。

> [!CAUTION]  
> 邮件将在链接到策略的保留标记中所定义的设置时间过期。这些设置包括将邮件移动到存档或将其永久删除等操作。将保留策略应用到一个或多个邮箱之前，我们建议您先对策略进行测试并检查每个与之相关联的保留标记。


有关与邮件记录管理 (IRM) 相关的其他管理任务，请参阅[邮件记录管理程序](messaging-records-management-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：5 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [邮件策略和遵从性权限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主题中的\&quot;应用保留策略\&quot;条目。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 您想执行什么操作？

## 使用 EAC 将保留策略应用于单个邮箱

1.  导航到\&quot;收件人\&quot;\>\&quot;邮箱\&quot;。

2.  在此列表视图中，选择您要应用保留策略的邮箱，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在\&quot;用户邮箱\&quot;中，单击\&quot;邮箱功能\&quot;。

4.  在\&quot;保留策略\&quot;列表中，选择要应用于邮箱的策略，然后单击\&quot;保存\&quot;。

## 使用 EAC 将保留策略应用于多个邮箱

1.  导航到\&quot;收件人\&quot;\>\&quot;邮箱\&quot;。

2.  在此列表视图中，使用 Shift 或 Ctrl 键选择多个邮箱。

3.  在详细信息窗格中，单击\&quot;更多选项\&quot;。

4.  在\&quot;保留策略\&quot;下，单击\&quot;更新\&quot;。

5.  在\&quot;批量分配保留策略\&quot;中，选择要应用于邮箱的保留策略，然后单击\&quot;保存\&quot;。

## 使用命令行管理程序将保留策略应用于单个邮箱

此示例将把保留策略 RP-Finance 应用于 Morris 的邮箱。

    Set-Mailbox "Morris" -RetentionPolicy "RP-Finance"

有关语法和参数的详细信息，请参阅 [Set-Mailbox](https://technet.microsoft.com/zh-cn/library/bb123981\(v=exchg.150\))。

## 使用命令行管理程序将保留策略应用于多个邮箱

本示例将新的保留策略 New-Retention-Policy 应用到所有包含旧策略 Old-Retention-Policy 的邮箱。

    $OldPolicy={Get-RetentionPolicy "Old-Retention-Policy"}.distinguishedName
    Get-Mailbox -Filter {RetentionPolicy -eq $OldPolicy} -Resultsize Unlimited | Set-Mailbox -RetentionPolicy "New-Retention-Policy"

此示例将保留策略 RetentionPolicy-Corp 应用于 Exchange 组织中的所有邮箱。

    Get-Mailbox -ResultSize unlimited | Set-Mailbox -RetentionPolicy "RetentionPolicy-Corp"

此示例将保留策略 RetentionPolicy-Finance 应用于 Finance 组织单位中的所有邮箱。

    Get-Mailbox -OrganizationalUnit "Finance" -ResultSize Unlimited | Set-Mailbox -RetentionPolicy "RetentionPolicy-Finance"

有关语法和参数的详细信息，请参阅 [Get-Mailbox](https://technet.microsoft.com/zh-cn/library/bb123685\(v=exchg.150\)) 和 [Set-Mailbox](https://technet.microsoft.com/zh-cn/library/bb123981\(v=exchg.150\))。

## 您如何知道这有效？

要验证您是否已应用保留策略，请运行 [Get-Mailbox](https://technet.microsoft.com/zh-cn/library/bb123685\(v=exchg.150\)) cmdlet 检索一个或多个邮箱的保留策略。

此示例检索 Morris 的邮箱的保留策略。

    Get-Mailbox Morris | Select RetentionPolicy

此命令检索应用了保留策略 RP-Finance 的所有邮箱。

    Get-Mailbox -ResultSize unlimited | Where-Object {$_.RetentionPolicy -eq "RP-Finance"} | Format-Table Name,RetentionPolicy -Auto

