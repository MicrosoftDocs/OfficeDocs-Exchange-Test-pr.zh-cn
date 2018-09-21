---
title: '配置邮箱的存储配额: Exchange 2013 Help'
TOCTitle: 配置邮箱的存储配额
ms:assetid: 5f5fe292-c80e-4a0b-b3e6-e193ea5171d0
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa998353(v=EXCHG.150)
ms:contentKeyID: 50556588
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 配置邮箱的存储配额

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-07-07_

**摘要：** 使用 EAC 或命令行管理程序设置特定邮箱的存储配额。

通过存储配额，可以控制邮箱大小，并能管理邮箱数据库的增长。当邮箱达到或超过指定的存储配额时，Exchange 会向邮箱所有者发送描述性通知。

> [!NOTE]  
> 存储配额针对的是运行 cmdlet <code>Get-MailboxStatistics</code> 时由属性 <code>TotalItemSize</code> 定义的给定邮箱大小。有关详细信息，请参阅 <a href="https://technet.microsoft.com/zh-cn/library/bb124612(v=exchg.150)">Get-MailboxStatistics</a>。


通常是按数据库配置存储配额。也就是说，为邮箱数据库配置的存储配额应用于该数据库中的所有邮箱。若要详细了解如何管理每个数据库邮箱的设置，请参阅[管理 Exchange 2013 中的邮箱数据库](manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md)。

本主题介绍了如何自定义特定邮箱的存储设置，而不是使用邮箱数据库中的存储设置。有关与用户邮箱相关的其他管理任务，请参阅[管理用户邮箱](https://docs.microsoft.com/zh-cn/exchange/recipients-in-exchange-online/manage-user-mailboxes/manage-user-mailboxes)。

## 开始前，需要知道什么？

  - 估计完成时间：2 分钟。

  - [收件人权限](recipients-permissions-exchange-2013-help.md)主题中的您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅“收件人预配权限”部分。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您要做什么？

## 使用 EAC 配置邮箱的存储配额

1.  在 EAC 中，依次转到“**收件人**”\>“**邮箱**”。

2.  在用户邮箱列表中，依次单击要更改其存储配额的邮箱和“**编辑**”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在“邮箱属性”页面上，依次单击“**邮箱使用情况**”和“**更多选项**”。

4.  单击“**为此邮箱自定义设置**”，然后配置以下框。任何存储配额设置的值范围介于 0 到 2047 GB 之间。
    
      - “**在达到该限度时发出警告(GB)**”   此框显示向用户发出警告的存储配额上限。如果邮箱大小达到或超过指定值，Exchange 会向用户发送警告消息。
        
        > [!IMPORTANT]  
        > 只有当此设置的值大于“<strong>禁止发送</strong>”配额中指定的值的一半时，与“<strong>发出警告</strong>”配额相关联的消息才会发送给用户。例如，如果将“<strong>禁止发送</strong>”配额设置为 8 MB，至少必须将“<strong>发出警告</strong>”配额设置为 4 MB。否则，不会发送与“<strong>发出警告</strong>”配额相关联的消息。
    
      - “**在达到该限度时禁止发送(GB)**”   此框显示邮箱的“*禁止发送*”限制。如果邮箱大小达到或超过指定的限制，Exchange 会阻止用户发送新邮件，并显示描述性错误消息。
    
      - “**在达到该限度时禁止发送和接收(GB)**”   此框显示邮箱的“*禁止发送和接收*”限制。如果邮箱大小达到或超过指定的限制，Exchange 会阻止邮箱用户发送新邮件，并且不会向邮箱发送任何新邮件。系统会将发送到邮箱的任何邮件都返回给收件人，并显示描述性错误消息。

5.  单击“**保存**”保存更改。

## 使用命令行管理程序配置邮箱的存储配额

此示例将 Joe Healy 的邮箱的“发出警告”、“禁止发送”、“禁止发送和接收”配额分别设置为 24.5 GB、24.75 GB 和 25 GB。

> [!NOTE]  
> 为了确保使用邮箱的自定义设置，而非邮箱数据库默认设置，必须将 <em>UseDatabaseQuotaDefaults</em> 参数设置为 <code>$false</code>。


    Set-Mailbox -Identity "Joe Healy" -IssueWarningQuota 24.5gb -ProhibitSendQuota 24.75gb -ProhibitSendReceiveQuota 25gb -UseDatabaseQuotaDefaults $false

此示例将 Ayla Kol 的邮箱的“发出警告”、“禁止发送”、“禁止发送和接收”配额分别设置为 900 MB、950 MB 和 1 GB，然后将邮箱配置为使用自定义设置。

    Set-Mailbox -Identity "Ayla Kol" -IssueWarningQuota 900mb -ProhibitSendQuota 950mb -ProhibitSendReceiveQuota 1gb -UseDatabaseQuotaDefaults $false

有关语法和参数的详细信息，请参阅 [Set-Mailbox](https://technet.microsoft.com/zh-cn/library/bb123981\(v=exchg.150\))。

## 如何判断是否生效？

若要验证是否已成功设置邮箱的存储配额，请执行下列操作之一：

1.  在 EAC 中，依次转到“**收件人**”\>“**邮箱**”。

2.  在用户邮箱列表中，依次单击要验证其存储配额的邮箱和“**编辑**”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在“邮箱属性”页面上，依次单击“**邮箱使用情况**”和“**更多选项**”。

4.  验证是否已选中“**为此邮箱自定义设置**”。

5.  验证存储配额设置。

或

在命令行管理程序中运行以下命令。

    Get-Mailbox <identity> | fl IssueWarningQuota,ProhibitSendQuota,ProhibitSendReceiveQuota,UseDatabaseQuotaDefaults

