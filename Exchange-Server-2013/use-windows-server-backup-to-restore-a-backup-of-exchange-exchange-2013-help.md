---
title: '使用 Windows Server 备份还原 Exchange 的备份: Exchange 2013 Help'
TOCTitle: 使用 Windows Server 备份还原 Exchange 的备份
ms:assetid: 2d0f31dc-eb32-451a-8852-591269026506
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd876864(v=EXCHG.150)
ms:contentKeyID: 50490129
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 使用 Windows Server 备份还原 Exchange 的备份

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2014-06-18_

您可以使用 Windows Server 备份来备份和还原 Exchange 数据库。Exchange 包括 Windows Server 备份的插件，可允许您执行和还原 Exchange 数据的基于卷影复制服务 (VSS) 的备份。有关其他信息，请参阅[使用 Windows 服务器备份来备份和还原 Exchange 数据](using-windows-server-backup-to-back-up-and-restore-exchange-data-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：1 分钟，再加上还原数据所花费的时间

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [收件人权限](recipients-permissions-exchange-2013-help.md)主题中的\&quot;邮箱恢复\&quot;条目。

  - Windows 服务器备份功能必须安装在本地计算机上。

  - 在将数据库还原到其原始位置时，数据库可能保留异常关闭状态并且可由系统装入。当还原至备用位置时（例如，准备使用一个恢复数据库），必须通过使用 Exchange 数据库实用程序 (Eseutil.exe) 手动使数据库进入干净关闭状态。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 使用 Windows Server 备份还原 Exchange 的备份

1.  启动 Windows Server 备份。

2.  选择\&quot;本地备份\&quot;。

3.  在\&quot;操作\&quot;窗格中，单击\&quot;恢复...\&quot;启动恢复向导。

4.  在\&quot;入门\&quot;页上，执行下列操作之一：
    
      - 如果正在恢复的数据之前已在本地服务器上备份，选择\&quot;本服务器 (服务器名称)\&quot;，然后单击\&quot;下一步\&quot;。
    
      - 如果正在恢复的数据来自另一台服务器，或正在恢复的备份位于另一台计算机，选择\&quot;另一台服务器\&quot;，然后单击\&quot;下一步\&quot;。在\&quot;指定位置类型\&quot;页面上，选择\&quot;本地驱动器\&quot;或者\&quot;远程共享文件夹\&quot;，然后单击\&quot;下一步\&quot;。如果选择\&quot;本地驱动器\&quot;，则在\&quot;选择备份位置\&quot;页面上选择包含备份的驱动器，然后单击\&quot;下一步\&quot;。如果选择\&quot;远程共享文件夹\&quot;，则在\&quot;指定远程文件夹\&quot;页面上为备份的数据键入 UNC 路径，然后单击\&quot;下一步\&quot;。

5.  在\&quot;选择备份日期\&quot;页面上，选择要恢复的备份的日期和时间，然后单击\&quot;下一步\&quot;。

6.  在\&quot;选择恢复类型\&quot;页面上，选择\&quot;应用程序\&quot;，然后单击\&quot;下一步\&quot;。
    
    > [!NOTE]  
    > 如果&amp;quot;应用程序&amp;quot;在选项中不可用，则表示选择还原的备份是一个文件夹级的备份，而不是卷级备份。当通过 Windows 服务器备份对 Exchange 数据进行备份时，您必须执行卷级备份。


7.  在\&quot;选择应用程序\&quot;页面上，确认在\&quot;应用程序\&quot;字段中已选中 Exchange。单击\&quot;查看详细信息\&quot;以查看备份的应用程序组件。如果您要恢复的备份是最新的，将会显示**\&quot;不执行应用程序数据库前滚恢复\&quot;**复选框。如果要阻止 Windows Server 备份通过提交所有未提交的事务日志来前滚正在恢复的数据库，请选中此复选框。单击\&quot;下一步\&quot;。

8.  在\&quot;指定恢复选项\&quot;页面上，选择要恢复数据的位置，然后单击\&quot;下一步\&quot;：
    
      - 如果您想要将 Exchange 数据直接恢复到其原始位置，请选择\&quot;恢复到原始位置\&quot;。如果使用此选项，则不能选择还原的数据库；该卷上的所有备份数据库将还原到其原始位置。
    
      - 如果将单个数据库及其文件还原到一个指定位置，请选择\&quot;恢复到另一个位置\&quot;。单击\&quot;浏览\&quot;指定备用位置。如果您使用此选项，您就可以选择要还原的数据库。在还原后，数据文件可被移至恢复数据库，手动移回其原始位置或通过使用[数据库可移植性](database-portability-exchange-2013-help.md)将其安装在 Exchange 组织中的其他地方。在将数据库还原到备用位置时，还原的数据库将处于异常关闭状态。还原过程完成之后，您将需要使用 Eseutil.exe 手动使数据库进入干净关闭状态。

9.  在\&quot;确认\&quot;页面上，查看恢复设置，然后单击\&quot;恢复\&quot;。

10. 在\&quot;恢复进程\&quot;页面上，您可以查看恢复操作的状态和进程。

11. 恢复操作完成之后，单击\&quot;关闭\&quot;。

## 您如何知道这有效？

\&quot;恢复进程\&quot;页面会表明恢复进程是否成功完成。若要进一步验证是否已成功还原数据，请执行以下操作之一：

  - 检查备份的目标目录并验证还原数据是否存在。

  - 在运行 Windows Server Backup 的服务器上，通过查看备份日志验证作业是否已成功完成。

  - 打开事件查看器，并验证还原完成事件是否已记录在应用程序事件日志中。

