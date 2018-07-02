---
title: '添加邮箱数据库副本: Exchange 2013 Help'
TOCTitle: 添加邮箱数据库副本
ms:assetid: 784bf48f-8af5-422c-a63f-2f01fc0cf151
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd298080(v=EXCHG.150)
ms:contentKeyID: 50490952
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 添加邮箱数据库副本

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2012-10-30_

添加邮箱数据库的副本会自动在现有数据库和数据库副本之间启用连续复制。数据库副本自动分配有格式为 \<*DatabaseName*\>\\\<*HostMailboxServerName*\> 的标识。例如，在服务器 MBX3 上托管的数据库 DB1 的副本会自动分配有标识 DB1\\MBX3。

若要了解与邮箱数据库副本相关的其他管理任务，请查看[管理邮箱数据库副本](managing-mailbox-database-copies-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 该任务的估计完成时间：2 分钟，外加数据库副本的种子设定时间，时间长短取决于各种因素，如数据库大小、速度、可用带宽和网络延迟以及存储速度。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [高可用性和站点恢复权限](high-availability-and-site-resilience-permissions-exchange-2013-help.md)主题中的\&quot;邮箱数据库副本\&quot;条目。

  - 必须装入数据库的主动副本。

  - 指定的邮箱服务器不得托管数据库的副本。

  - 数据库副本及其日志文件的路径必须在选定邮箱服务器上可用。

  - 托管主动副本和被动副本的服务器必须位于同一数据库可用性组 (DAG) 中。DAG 还必须有仲裁，且能够正常运行。

  - 如果要添加数据库的第二个副本（例如，创建数据库的第一个被动副本），不得为指定邮箱数据库启用循环日志记录。如果已启用循环日志记录，则必须先禁用它。在添加邮箱数据库副本之后，才可以启用循环日志记录。在为已复制的邮箱数据库启用循环日志记录之后，使用的是连续复制循环日志记录 (CRCL)，而不是 JET 循环日志记录。如果要添加数据库的第三个或后续副本，可以继续启用 CRCL。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.</td>
</tr>
</tbody>
</table>


## 您想执行什么操作？

## 使用 EAC 添加邮箱数据库副本

1.  
    
    在 EAC 中，转到\&quot;服务器\&quot;\>\&quot;数据库\&quot;。

2.  选择要复制的数据库，然后单击 ![添加数据库副本](images/Dd298080.435c15ff-abf2-4de8-b280-f053db1afa13(EXCHG.150).gif "添加数据库副本")。

3.  
    
    在\&quot;添加邮箱数据库副本\&quot;页上，单击\&quot;浏览...\&quot;，选择托管数据库副本的邮箱服务器，然后单击\&quot;确定\&quot;。

4.  可以选择为数据库副本配置\&quot;激活首选项编号\&quot;。

5.  单击\&quot;更多选项...\&quot;通过配置重播延迟时间将数据库副本指定为滞后数据库副本或推迟数据库副本的自动种子设定。

6.  单击\&quot;保存\&quot;可保存配置更改并添加邮箱数据库副本。

7.  单击\&quot;确定\&quot;确认出现的任何消息。

## 使用命令行管理程序添加邮箱数据库副本

此示例向邮箱服务器 MBX3 添加邮箱数据库 DB1 的副本。重播延隔时间和截断延隔时间保留默认值 0，激活首选项的值配置为 2。

    Add-MailboxDatabaseCopy -Identity DB1 -MailboxServer MBX3 -ActivationPreference 2

此示例向邮箱服务器 MBX4 添加邮箱数据库 DB2 的副本。重播延隔时间和截断延隔时间保留默认值 0，激活首选项的值配置为 `5`。另外，还推迟了对此副本进行种子设定，以便可以使用本地源服务器（而不是当前处于活动状态且距离 MBX4 很远的数据库副本）对此副本进行种子设定。

    Add-MailboxDatabaseCopy -Identity DB2 -MailboxServer MBX4 -ActivationPreference 5 -SeedingPostponed

此示例向邮箱服务器 MBX5 添加邮箱数据库 DB3 的副本。重播延隔时间设置为 3 天，截断延隔时间保留默认值 0，激活首选项的值配置为 `4`。

    Add-MailboxDatabaseCopy -Identity DB3 -MailboxServer MBX5 -ReplayLagTime 3.00:00:00 -ActivationPreference 4

## 您如何知道这有效？

要验证您是否已成功创建了邮箱数据库副本，请执行以下操作之一：

  - 在 EAC 中，依次转到\&quot;**服务器**\&quot;\>\&quot;**数据库**\&quot;。选择已复制的数据库。此时，细节窗格中会显示数据库副本的状态及其内容索引，以及当前的复制队列长度。

  - 在命令行管理程序中，运行以下命令检查是否已创建邮箱数据库副本以及它是否处于健康状态。
    
        Get-MailboxDatabaseCopyStatus <DatabaseCopyName>
    
    状态和内容索引状态应该为健康。

## 详细信息

[邮箱数据库副本](mailbox-database-copies-exchange-2013-help.md)

[管理邮箱数据库副本](managing-mailbox-database-copies-exchange-2013-help.md)

