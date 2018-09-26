---
title: '挂起或恢复邮箱数据库副本: Exchange 2013 Help'
TOCTitle: 挂起或恢复邮箱数据库副本
ms:assetid: 96aa1b82-3e15-4215-843e-3d583af9504b
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd298159(v=EXCHG.150)
ms:contentKeyID: 50491202
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 挂起或恢复邮箱数据库副本

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2012-11-02_

由于各种原因，您可能需要挂起或恢复数据库副本，例如维护包含数据库副本的磁盘，或是为进行灾难恢复而暂停激活的单个数据库副本。

若要了解与邮箱数据库副本相关的其他管理任务，请查看[管理邮箱数据库副本](managing-mailbox-database-copies-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成该任务的时间：1 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [高可用性和站点恢复权限](high-availability-and-site-resilience-permissions-exchange-2013-help.md)主题中的\&quot;邮箱数据库副本\&quot;条目。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 使用 EAC 挂起邮箱数据库副本

1.  在 EAC 中，转到\&quot;服务器\&quot;\>\&quot;数据库\&quot;。

2.  选择要挂起其副本的数据库。

3.  在\&quot;详细信息\&quot;窗格的\&quot;数据库副本\&quot;下，在要挂起的数据库副本下单击\&quot;挂起\&quot;。

4.  在\&quot;注释\&quot;字段中，添加一条最多包含 512 个字符的可选注释，以便指定挂起原因。

5.  若要挂起数据库副本的自动激活，请选中\&quot;此副本只能通过手动干预激活\&quot;复选框。

6.  单击\&quot;保存\&quot;挂起数据库副本。

## 使用 EAC 恢复邮箱数据库副本

1.  在 EAC 中，转到\&quot;服务器\&quot;\>\&quot;数据库\&quot;。

2.  选择要恢复其副本的数据库。

3.  在\&quot;详细信息\&quot;窗格的\&quot;数据库副本\&quot;下，在要恢复的数据库副本下单击\&quot;恢复\&quot;。

4.  单击\&quot;是\&quot;恢复数据库副本。

## 使用命令行管理程序挂起邮箱数据库副本

此示例对服务器 MBX1 上托管的数据库 DB1 的副本暂停连续复制。此外，还指定了可选注释。

```powershell
Suspend-MailboxDatabaseCopy -Identity DB1\MBX1 -SuspendComment "Maintenance on MBX1" -Confirm:$False
```

此示例挂起了服务器 MBX2 上承载的数据库 DB2 的一个副本的激活。

```powershell
Suspend-MailboxDatabaseCopy -Identity DB2\MBX2 -ActivationOnly -Confirm:$False
```

## 使用命令行管理程序恢复邮箱数据库副本

此示例恢复了邮箱服务器 MBX1 上的数据库 DB1 的一个副本。

```powershell
Resume-MailboxDatabaseCopy -Identity DB1\MBX1
```

本示例恢复了服务器 MBX2 上数据库 DB2 的一个副本，仅用于复制。

```powershell
Resume-MailboxDatabaseCopy -Identity DB2\MBX2 -ReplicationOnly
```

## 您如何知道这有效？

若要验证是否已成功挂起或恢复邮箱数据库副本，请执行以下操作：

  - 在 EAC 中，导航至\&quot;服务器\&quot;\>\&quot;数据库\&quot;。选择相应数据库，然后在\&quot;详细信息\&quot;窗格中单击\&quot;查看详细信息\&quot;查看数据库备份属性。

  - 在命令行管理程序中，运行以下命令来显示数据库备份的状态信息。
    
    ```powershell
    Get-MailboxDatabaseCopyStatus <DatabaseCopyName> | Format-List
    ```

