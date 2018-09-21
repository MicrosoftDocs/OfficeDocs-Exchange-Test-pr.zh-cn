---
title: '将 Exchange 2010 系统邮箱移到 Exchange 2013 中: Exchange 2013 Help'
TOCTitle: 将 Exchange 2010 系统邮箱移到 Exchange 2013 中
ms:assetid: a3b03c4e-0bc7-41a2-885c-e9cac37566c8
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dn249849(v=EXCHG.150)
ms:contentKeyID: 54913711
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 将 Exchange 2010 系统邮箱移到 Exchange 2013 中

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-04-07_

在 Exchange 2010 中，Microsoft Exchange 系统邮箱是仲裁邮箱，用于存储全组织范围内的数据（如管理员审核日志）、电子数据展示搜索元数据和统一消息数据（如菜单、拨号计划和自定义问候语）。Microsoft Exchange 系统邮箱名为“SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9}”；显示名称是“Microsoft Exchange”。

当您将现有的 Exchange 2010 组织升级到 Exchange 2013 时，您需要将 Microsoft Exchange 系统邮箱移到 Exchange 2013 邮箱服务器上的邮箱数据库中。您应先安装并验证 Exchange 2013，然后再移动此邮箱。如果您没有将此系统邮箱移到 Exchange 2013 中，当 Exchange 2010 和 Exchange 2013 共存于您的 Exchange 组织中时，会出现以下问题：

  - 无法将 Exchange 2013 任务保存到管理员审核日志。运行 **Search-AdminAuditLog** cmdlet 或尝试在 EAC 中导出管理员审核日志时，您会收到一个错误，指出无法创建管理员审核日志搜索，因为系统邮箱 (SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9}) 位于未运行 Exchange 2013 的服务器上。每次运行命令时，Windows 应用程序日志中还会记录事件 ID 为 5000 的 Microsoft Exchange 错误。

  - 您不能使用 EAC 或 Exchange 2013 中的命令行管理程序运行电子数据展示搜索。可能会创建邮箱搜索，并将其排入队列，但无法将其启动。MsExchange 管理日志中会记录事件 ID 为 6 的错误，指出 **Start-MailboxSearch** cmdlet 失败。不过，您可以使用命令行管理程序和 Exchange 2010 中的 Exchange 控制面板 (ECP) 搜索邮箱。

在将 Exchange 2010 统一消息升级到 Exchange 2013 的过程中，您还需要将 Microsoft Exchange 系统邮箱移到 Exchange 2013 中。

有关升级到 Exchange 2013 的详细信息，请参阅下列主题：

  - [从 Exchange 2010 升级至 Exchange 2013](upgrade-from-exchange-2010-to-exchange-2013-exchange-2013-help.md)

  - [将 Exchange 2010 UM 升级到 Exchange 2013 UM](upgrade-exchange-2010-um-to-exchange-2013-um-exchange-2013-help.md)

## 在开始之前，您需要知道什么？

  - 估计完成时间：20 分钟。实际时间可能会有所不同，取决于系统邮箱的大小。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[收件人权限](recipients-permissions-exchange-2013-help.md)中的“邮箱移动和迁移权限”条目。

  - 在 Exchange 2013 中运行以下命令，以获取 Exchange 服务器的标识和版本以及包含组织系统邮箱的邮箱数据库。
    
    ```powershell
Get-Mailbox -Arbitration | FL Name,DisplayName,ServerName,Database,AdminDisplayVersion
```
    
    **AdminDisplayVersion** 属性指示服务器正在运行的 Exchange 的版本。值 `Version 14.x` 指示 Exchange 2010；值 `Version 15.x` 指示 Exchange 2013。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 使用 EAC 移动系统邮箱

1.  在 EAC 中，转到“收件人”\>“迁移”。

2.  单击“新建”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")，然后单击“移动到其他数据库”。

3.  在“新建本地邮箱移动”页上，单击“选择要移动的用户”，然后单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。

4.  在“选择邮箱”页上，添加具有以下属性的邮箱：
    
      - 显示名称为“Microsoft Exchange”。
    
      - 邮箱的电子邮件地址别名是“SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9}”。

5.  单击“确定”，然后单击“下一步”。

6.  在“移动配置”页上，键入迁移批处理的名称，然后单击“目标数据库”框旁边的“浏览”。

7.  在“选择邮箱数据库”页上，添加要将系统邮箱移动到的邮箱数据库。验证您选择的邮箱数据库版本是否为 Version 15. x，它表示数据库位于 Exchange 2013 服务器上。

8.  单击“确定”，然后单击“下一步”。

9.  在“开始批处理”页上，选择自动开始和完成迁移请求的选项，然后单击“新建”。

## 使用命令行管理程序移动系统邮箱

首先，在 Exchange 2013 中运行以下命令，以获取组织中所有邮箱数据库的名称和版本。

```powershell
Get-MailboxDatabase -IncludePreExchange2013 | FL Name,Server,AdminDisplayVersion
```

在确定组织中的邮箱数据库的名称之后，在 Exchange 2013 中运行以下命令，以将 Microsoft Exchange 系统邮箱移动到位于 Exchange 2013 服务器上的邮箱数据库。

    Get-Mailbox -Arbitration -Identity "SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9}" | New-MoveRequest -TargetDatabase <name of Exchange 2013 database>

## 您如何知道这有效？

若要验证您是否已成功将 Microsoft Exchange 系统邮箱移动到位于 Exchange 2013 服务器的邮箱数据库，则在命令行管理程序中运行以下命令。

    Get-Mailbox -Arbitration -Identity "SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9}" | FL Database,ServerName,AdminDisplayVersion

如果 **AdminDisplayVersion** 属性的值为“Version 15.x (Build xxx.x)”，这证实系统邮箱驻留在位于 Exchange 2013 服务器的邮箱数据库上。

将 Microsoft Exchange 系统邮箱移动到 Exchange 2013 后，您也可以成功执行以下管理任务：

  - 运行 **Search-AdminAuditLog** cmdlet。

  - 在 EAC 中，导出管理员审核日志。

  - 使用 EAC 或 Exchange 2013 中的命令行管理程序成功创建和启动电子数据展示搜索。

