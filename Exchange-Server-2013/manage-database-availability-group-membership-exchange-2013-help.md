---
title: '管理数据库可用性组成员身份: Exchange 2013 Help'
TOCTitle: 管理数据库可用性组成员身份
ms:assetid: fb2ea15e-96d5-4045-b75b-b0aa5fc60479
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd351278(v=EXCHG.150)
ms:contentKeyID: 50492031
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 管理数据库可用性组成员身份

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2014-08-13_

将服务器添加到数据库可用性组 (DAG) 后，此服务器与 DAG 中的其他服务器协同工作，提供从数据库、服务器或网络故障中自动执行数据库级恢复的功能。删除 DAG 中的某个服务器时，该服务器将不再自动受到防故障保护。

要查找与 DAG 相关的其他管理任务吗？请查看[管理数据库可用性组](managing-database-availability-groups-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：每个服务器 5 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [高可用性和站点恢复权限](high-availability-and-site-resilience-permissions-exchange-2013-help.md)主题中的\&quot;数据库可用性组\&quot;条目。

  - DAG 使用 Windows 故障转移群集 (WFC) 技术。作为 DAG 成员的每个邮箱服务器也是 DAG 使用的基础群集中的一个节点。因此，在任何特定时间，邮箱服务器都只能是一个 DAG 的成员。由于 DAG 使用 WFC 技术，所有添加到 DAG 的服务器必须运行相同的操作系统：Windows Server 2008 R2 Enterprise 或 Datacenter Edition，或者 Windows Server 2012 或 Windows Server 2012 R2 的 Standard 或 Datacenter Edition。

  - 在添加运行 Windows Server 2012 的邮箱服务器时，必须为 DAG 预留群集名称对象 (CNO)。如果您要添加运行 Windows Server 2012 R2 的邮箱服务器，并且 DAG 没有管理访问点，则您无需预暂存 CNO，因为没有管理访问点的 DAG 不含 CNO。有关详细步骤，请参阅[为数据库可用性组预留群集名称对象](pre-stage-the-cluster-name-object-for-a-database-availability-group-exchange-2013-help.md)。

  - 在添加成员到 DAG 之前，您必须首先创建 DAG。有关详细步骤，请参阅[创建数据库可用性组](create-a-database-availability-group-exchange-2013-help.md)。

  - 只有先将所有复制的数据库副本从服务器中删除，才能将服务器从 DAG 中删除。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!tip]
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 使用 EAC 管理数据库可用性组成员身份

1.  在 EAC 中，转到\&quot;服务器\&quot;\>\&quot;数据库可用性组\&quot;。

2.  选择要配置的 DAG，然后单击 ![管理 DAG 成员](images/Dd351278.d567ae56-d6cd-4edb-ab67-ad8f7c58f337(EXCHG.150).gif "管理 DAG 成员")。
    
      - 将一个或多个邮箱服务器添加至 DAG，单击 ![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")，从列表选择服务器，单击\&quot;添加\&quot;，然后单击\&quot;确定\&quot;。
    
      - 将一个或多个邮箱服务器从 DAG 删除，选择服务器，然后单击减号 (-) 图标。

3.  单击\&quot;保存\&quot;以保存更改。

4.  成功完成任务后，单击\&quot;关闭\&quot;。

## 使用命令行管理程序管理数据库可用性组成员身份

此示例向名为 DAG1 的 DAG 中添加邮箱服务器 MBX1。

    Add-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer MBX1

此示例从名为 DAG1 的 DAG 中删除邮箱服务器 MBX1。运行此命令之前，请确保邮箱服务器上不存在任何复制数据库。

    Remove-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer MBX1

此示例从名为 DAG2 的 DAG 中删除邮箱服务器 MBX4 的配置设置。MBX4 应当在较长时间内保持脱机状态，这样才能在它处于脱机时从 DAG 中删除其配置，以便用剩余的联机 DAG 成员建立仲裁。

    Remove-DatabaseAvailabilityGroupServer -Identity DAG2 -MailboxServer MBX4 -ConfigurationOnly

## 您如何知道这有效？

验证是否已成功管理 DAG 成员身份，请执行以下操作之一：

  - 在 EAC 中，导航到\&quot;服务器\&quot;\>\&quot;数据库可用性组\&quot;。当前 DAG 成员身份显示在\&quot;成员服务器\&quot;列。

  - 在 Shell 中，运行以下命令以显示 DAG 成员身份信息。
    
        Get-DatabaseAvailabilityGroup <DAGName> | Format-List Servers

## 详细信息

[Add-DatabaseAvailabilityGroupServer](https://technet.microsoft.com/zh-cn/library/dd298049\(v=exchg.150\))

[Remove-DatabaseAvailabilityGroupServer](https://technet.microsoft.com/zh-cn/library/dd297956\(v=exchg.150\))

