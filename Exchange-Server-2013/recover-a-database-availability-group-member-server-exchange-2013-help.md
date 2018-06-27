---
title: '恢复数据库可用性组成员服务器: Exchange 2013 Help'
TOCTitle: 恢复数据库可用性组成员服务器
ms:assetid: eccd8f61-9706-4bb7-a62a-ec7c166f8019
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd638206(v=EXCHG.150)
ms:contentKeyID: 50491889
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 恢复数据库可用性组成员服务器

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2016-12-09_

如果作为数据库可用性组 (DAG) 成员的邮箱服务器丢失，或发生故障且无法恢复并需要进行替换时，可执行服务器恢复操作。Microsoft Exchange Server 2013 安装程序包含可用于执行服务器恢复操作的开关 */m:RecoverServer*。运行带有 */m:RecoverServer* 开关的安装程序，会使安装程序从与运行安装程序的服务器同名的服务器 Active Directory 中读取该服务器的配置信息。从 Active Directory 中收集服务器配置信息后，会在该服务器上安装原来的 Exchange 文件和服务，并将存储在 Active Directory 中的角色和设置应用到该服务器。

要查找与 DAG 相关的其他管理任务吗？请查看[管理数据库可用性组](managing-database-availability-groups-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：30 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[高可用性和站点恢复权限](high-availability-and-site-resilience-permissions-exchange-2013-help.md)主题中的“邮箱数据库副本”条目。

  - 如果 Exchange 不是安装在默认位置，则必须使用 */TargetDir* 设置开关指定 Exchange 程序文件的位置。如果不使用 */TargetDir* 开关，则 Exchange 程序文件将安装在默认位置 (%programfiles%\\Microsoft\\Exchange Server\\V15) 中。
    
    若要确定安装位置，请执行下列步骤：
    
    1.  打开 ADSIEDIT.MSC 或 LDP.EXE。
    
    2.  导航到以下位置：**CN=ExServerName,CN=Servers,CN=First Administrative Group,CN=Administrative Groups,CN=ExOrg Name,CN=Microsoft Exchange,CN=Services,CN=Configuration,DC=DomainName,CN=Com**
    
    3.  右键单击 Exchange 服务器对象，然后单击“属性”。
    
    4.  找到 **msExchInstallPath** 属性。此属性存储当前安装路径。

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


## 使用安装程序 /m:RecoverServer 恢复服务器

1.  使用 [Get-MailboxDatabase](https://technet.microsoft.com/zh-cn/library/bb124924\(v=exchg.150\)) cmdlet 为要恢复的服务器上的任何邮箱数据库副本检索所有重播延迟和截断延迟设置：
    
        Get-MailboxDatabase DB1 | Format-List *lag*

2.  使用 [Remove-MailboxDatabaseCopy](https://technet.microsoft.com/zh-cn/library/dd335119\(v=exchg.150\)) cmdlet 删除要恢复的服务器上的所有邮箱数据库副本：
    
        Remove-MailboxDatabaseCopy DB1\MBX1

3.  使用 [Remove-DatabaseAvailabilityGroupServer](https://technet.microsoft.com/zh-cn/library/dd297956\(v=exchg.150\)) cmdlet 从 DAG 中删除故障服务器的配置：
    
        Remove-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer MBX1
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果要删除的 DAG 成员处于脱机状态，并且无法将其联机，则必须向上述命令中添加 <em>ConfigurationOnly</em> 参数。如果使用 <em>ConfigurationOnly</em> 开关，则必须从群集手动退出节点。</td>
    </tr>
    </tbody>
    </table>


4.  在 Active Directory 中重置服务器的计算机帐户。有关详细步骤，请参阅[重置计算机帐户](http://go.microsoft.com/fwlink/p/?linkid=167188)。

5.  打开命令提示符窗口。使用原始安装媒体运行以下命令：
    
        Setup /m:RecoverServer

6.  安装恢复过程完成后，使用 [Add-DatabaseAvailabilityGroupServer](https://technet.microsoft.com/zh-cn/library/dd298049\(v=exchg.150\)) cmdlet 将恢复后的服务器添加到 DAG 中：
    
        Add-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer MBX1

7.  将服务器添加回 DAG 后，可以使用 [Add-MailboxDatabaseCopy](https://technet.microsoft.com/zh-cn/library/dd298105\(v=exchg.150\)) cmdlet 重新配置邮箱数据库副本。如果以前添加的任何数据库副本的重播延迟或截断延迟时间大于 0，可以使用 [Add-MailboxDatabaseCopy](https://technet.microsoft.com/zh-cn/library/dd298105\(v=exchg.150\)) cmdlet 的 *ReplayLagTime* 和 *TruncationLagTime* 参数重新配置这些设置：
    
        Add-MailboxDatabaseCopy -Identity DB1 -MailboxServer MBX1
        Add-MailboxDatabaseCopy -Identity DB2 -MailboxServer MBX1 -ReplayLagTime 3.00:00:00
        Add-MailboxDatabaseCopy -Identity DB3 -MailboxServer MBX1 -ReplayLagTime 3.00:00:00 -TruncationLagTime 3.00:00:00

## 您如何知道这有效？

若要验证是否成功恢复了 DAG 成员，请执行以下操作：

  - 在命令行管理程序中，运行以下命令验证恢复后的 DAG 成员的运行状况和状态。
    
        Test-ReplicationHealth <ServerName>
    
        Get-MailboxDatabaseCopyStatus -Server <ServerName>
    
    所有复制运行状态测试都应成功通过，并且数据库及其内容索引的状态都应当正常。

