---
title: '激活邮箱数据库副本: Exchange 2013 Help'
TOCTitle: 激活邮箱数据库副本
ms:assetid: d948269b-c902-4d8d-8c2b-269473359baa
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Ee364750(v=EXCHG.150)
ms:contentKeyID: 50491759
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 激活邮箱数据库副本

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2012-11-01_

激活邮箱数据库副本是将特定被动副本指定为邮箱数据库的新主动副本的过程。我们将此过程称为\&quot;*数据库切换*\&quot;。数据库切换过程是指卸除当前的活动数据库，然后在指定的服务器上将相应的数据库副本作为新的活动邮箱数据库副本进行装载。成为活动邮箱数据库的数据库副本必须是能正常运行的最新副本。

若要了解与邮箱数据库副本相关的其他管理任务，请查看[管理邮箱数据库副本](managing-mailbox-database-copies-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成该任务的时间：1 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [高可用性和站点恢复权限](high-availability-and-site-resilience-permissions-exchange-2013-help.md)主题中的\&quot;邮箱数据库副本\&quot;条目。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 使用 EAC 移动活动邮箱数据库

1.  在 EAC 中，转到\&quot;服务器\&quot;\>\&quot;数据库\&quot;。

2.  选择要激活其副本的数据库。

3.  在细节窗格的\&quot;**数据库副本**\&quot;下，单击要激活的数据库副本下的\&quot;**激活**\&quot;。

4.  单击\&quot;**是**\&quot;，激活数据库副本。

## 使用命令行管理程序移动活动邮箱数据库

此示例激活 MBX3 上托管的数据库 DB4 的副本，并将其作为新的活动邮箱数据库进行装载。此命令将 DB4 设置为新的活动邮箱数据库，不会替代 MBX3 上的数据库装载拨号设置。

```powershell
Move-ActiveMailboxDatabase DB4 -ActivateOnServer MBX3 -MountDialOverride:None
```

此示例执行数据库 DB2 到邮箱服务器 MBX1 的切换操作。在此命令完成后，MBX1 会驻留 DB2 的主动副本。因为 *MountDialOverride* 参数设置为 `None`，所以 MBX1 会使用其自己定义的数据库自动装入拨号设置装入该数据库。

```powershell
Move-ActiveMailboxDatabase DB2 -ActivateOnServer MBX1 -MountDialOverride:None
```

此示例执行数据库 DB1 到邮箱服务器 MBX3 的切换操作。在此命令完成后，MBX3 会驻留 DB1 的主动副本。因为为 *MountDialOverride* 参数指定了值 `Good Availability`，所以 MBX3 会使用数据库自动装入拨号设置 *GoodAvailability* 装入数据库。

```powershell
Move-ActiveMailboxDatabase DB1 -ActivateOnServer MBX3 -MountDialOverride:GoodAvailability
```

此示例执行数据库 DB3 到邮箱服务器 MBX4 的切换操作。在此命令完成后，MBX4 会驻留 DB3 的主动副本。因为没有指定 *MountDialOverride* 参数，所以 MBX4 会使用数据库自动装入拨号设置 *Lossless* 装入数据库。

```powershell
Move-ActiveMailboxDatabase DB3 -ActivateOnServer MBX4
```

本示例将对邮箱服务器 MBX1 执行服务器切换。将利用 MBX1 上活动数据库的健全副本，在一台或多台其他邮箱服务器上激活 MBX1 上的所有活动邮箱数据库副本。

```powershell
Move-ActiveMailboxDatabase -Server MBX1
```

此示例将数据库 DB4 切换到邮箱服务器 MBX5 上。在此示例中，MBX5 上数据库副本的重播队列大于 6。因此，必须指定 *SkipLagChecks* 参数，才能激活 MBX5 上的数据库副本。

```powershell
Move-ActiveMailboxDatabase DB4 MBX5 -SkipLagChecks
```

此示例将数据库 DB5 切换到邮箱服务器 MBX6 上。在此示例中，MBX6 上数据库副本的 *ContentIndexState* 值为\&quot;Failed\&quot;。因此，必须指定 *SkipClientExperienceChecks* 参数，才能激活 MBX6 上的数据库副本。

```powershell
Move-ActiveMailboxDatabase DB5 MBX6 -SkipClientExperienceChecks
```

## 您如何知道这有效？

若要验证是否已成功激活邮箱数据库副本，请执行以下任意一项操作：

  - 在 EAC 中，导航至\&quot;服务器\&quot;\>\&quot;数据库\&quot;。选择相应数据库，然后在\&quot;详细信息\&quot;窗格中单击\&quot;查看详细信息\&quot;查看数据库备份属性。

  - 在命令行管理程序中，运行以下命令来显示数据库备份的状态信息。
    
    ```powershell
    Get-MailboxDatabaseCopyStatus <DatabaseCopyName> | Format-List
    ```

## 详细信息

[邮箱数据库副本](mailbox-database-copies-exchange-2013-help.md)

[配置邮箱数据库副本属性](configure-mailbox-database-copy-properties-exchange-2013-help.md)

