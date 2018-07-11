---
title: '使用 Windows 服务器备份来备份 Exchange: Exchange 2013 Help'
TOCTitle: 使用 Windows 服务器备份来备份 Exchange
ms:assetid: 188a8291-0a41-4ca2-b6d2-94242e2b1ffc
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd876854(v=EXCHG.150)
ms:contentKeyID: 50489968
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 使用 Windows 服务器备份来备份 Exchange

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2014-06-18_

您可以使用 Windows Server 备份来备份和还原 Exchange 数据库。Exchange 包括 Windows Server 备份的插件，可允许您创建 Exchange 数据的基于卷影复制服务 (VSS) 的备份。

## 在开始之前，您需要知道什么？

  - 估计完成时间：1 分钟，再加上备份数据所花费的时间

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [收件人权限](recipients-permissions-exchange-2013-help.md)主题中的\&quot;邮箱恢复\&quot;条目。

  - Windows 服务器备份功能必须安装在本地计算机上。

  - 在备份操作期间，运行 Exchange 数据文件的一致性检查，以确保文件的状态良好并可用于恢复。如果一致性检查成功，则 Exchange 数据可用于从该备份中恢复。如果一致性检查失败，则 Exchange 数据不可用于恢复。Windows Server Backup 会对为备份拍摄的快照运行一致性检查。因此，将文件从快照复制到备份媒体之前，显示备份的一致性并通知用户一致检查结果。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 使用 Windows 服务器备份来备份 Exchange

1.  启动 Windows Server 备份。

2.  选择\&quot;本地备份\&quot;。

3.  在\&quot;操作\&quot;窗格中，单击\&quot;一次性备份...\&quot;启动一次性备份向导。

4.  在\&quot;备份选项\&quot;页上，选择\&quot;不同选项\&quot;，然后单击\&quot;下一步\&quot;。

5.  在\&quot;选择备份配置\&quot;页上，选择\&quot;自定义\&quot;，然后单击\&quot;下一步\&quot;。

6.  在\&quot;选择备份项目\&quot;页上，单击\&quot;添加项目\&quot;以选择要备份的卷，然后单击\&quot;确定\&quot;。
    
    > [!NOTE]  
    > 选择卷，而非单独的文件夹。执行应用程序级别备份或恢复的唯一方法是选择整个卷。


7.  单击\&quot;高级设置\&quot;。在\&quot;排除\&quot;选项卡上，单击\&quot;添加排除\&quot;以添加任何你想在备份中排除的文件或文件类型。
    
    > [!NOTE]  
    > 默认情况下，含有操作系统组件或应用程序的卷将包含在备份中，并且不能排除。


8.  在\&quot;VSS 设置\&quot;选项卡上，选择\&quot;VSS 完全备份\&quot;，然后单击\&quot;确定\&quot;，再单击\&quot;下一步\&quot;。

9.  在\&quot;指定目标类型\&quot;页上，选择要存储备份的位置，然后单击\&quot;下一步\&quot;。
    
      - 如果您选择\&quot;本地驱动器\&quot;，会出现\&quot;选择备份目的地\&quot;页面。从\&quot;备份目的地\&quot;下拉列表中选择一个选项，然后单击\&quot;下一步\&quot;。
    
      - 如果您选择了\&quot;远程共享文件夹\&quot;，会出现\&quot;指定远程文件夹\&quot;页面。为备份文件指定 UNC 路径，并配置访问控制设置。如果您想使备份只能通过特定帐户访问，请选择\&quot;不继承\&quot;。为在承载远程文件夹的计算机上拥有写入权限的帐户提供用户名和密码，然后单击\&quot;确定\&quot;。或者，如果您想使备份可被所有有权访问该远程文件夹的用户访问，请选择\&quot;继承\&quot;。单击\&quot;下一步\&quot;。

10. 在\&quot;确认\&quot;页上检查备份设置，然后单击\&quot;备份\&quot;。

11. 在\&quot;备份进度\&quot;页上，您可以查看备份操作的状态和进度。

12. 单击\&quot;关闭\&quot;可随时退出\&quot;备份进度\&quot;页。正在进行的任何备份将继续在后台运行。

## 您如何知道这有效？

要验证是否已成功备份数据，请执行以下操作：

  - 在运行 Windows Server Backup 的服务器上，会显示上一次备份的状态，应该显示为\&quot;成功\&quot;。此外，您还可以通过查看 Windows Server Backup 日志验证备份已成功完成。

  - 打开\&quot;事件查看器\&quot;，并验证备份完成事件是否已记录在\&quot;应用程序\&quot;事件日志中。

  - 运行 Exchange Management Shell 中的以下命令以验证选定卷上的每一个数据库已成功备份：
    
        Get-MailboxDatabase -Server <ServerName> -Status | fl Name,*FullBackup
    
    数据库的 *SnapshotLastFullBackup* 和 *LastFullBackup* 属性表示上一次成功备份的时间以及该备份是否是 VSS 完全备份。

