---
title: '启用或禁用邮箱的 Exchange ActiveSync: Exchange 2013 Help'
TOCTitle: 启用或禁用邮箱的 Exchange ActiveSync
ms:assetid: dcf7c05b-b1b9-4b0f-800d-fec9f2ddc9e4
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb124809(v=EXCHG.150)
ms:contentKeyID: 50556688
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 启用或禁用邮箱的 Exchange ActiveSync

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2012-11-13_

可以使用 EAC 或命令行管理程序启用或禁用用户邮箱的 Microsoft Exchange ActiveSync。 Exchange ActiveSync 是一种客户端协议，允许用户将移动设备与其 Exchange 邮箱同步。 在创建用户邮箱时，会默认启用 Exchange ActiveSync。 有关详细信息，请参阅[Exchange ActiveSync](exchange-activesync-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：2 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[客户端和移动设备权限](clients-and-mobile-devices-permissions-exchange-2013-help.md)主题中的“Exchange ActiveSync 设置”条目。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!tip]
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 使用 EAC 启用或禁用 Exchange ActiveSync

1.  在 EAC 中，导航到“收件人”\>“邮箱”。

2.  在用户邮箱列表中，单击要为其启用或禁用 Exchange ActiveSync 的邮箱，然后单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在邮箱属性页上，单击“邮箱功能”。

4.  在“移动设备”下，执行下列操作之一：
    
      - 若要禁用 Exchange ActiveSync，请单击“禁用 Exchange ActiveSync”。
        
        此时将显示一条警告，询问是否确实要禁用 Exchange ActiveSync。单击“是”。
    
      - 若要启用 Exchange ActiveSync，请单击“启用 Exchange ActiveSync”。

5.  单击“保存”以保存您所做的更改。

> [!NOTE]
> 可以使用 EAC 的批量编辑功能，为多个用户邮箱启用和禁用 Exchange ActiveSync。 有关如何执行此操作的详细信息，请参阅<a href="manage-user-mailboxes-exchange-2013-help.md">管理用户邮箱</a>中的“批量编辑用户邮箱”部分。


## 使用命令行管理程序启用或禁用 Exchange ActiveSync

此示例为 Yan Li 的邮箱禁用 Exchange ActiveSync。

    Set-CASMailbox -Identity "Yan Li" -ActiveSyncEnabled $false

此示例为 Elly Nkya 的邮箱启用 Exchange ActiveSync。

    Set-CASMailbox -Identity Ellyn@contoso.com -ActiveSyncEnabled $true

有关语法和参数的详细信息，请参阅 [Set-CASMailbox](https://technet.microsoft.com/zh-cn/library/bb125264\(v=exchg.150\))。

## 您如何知道这有效？

若要验证是否为用户邮箱成功启用或禁用了 Exchange ActiveSync，请执行下列操作之一：

  - 在 EAC 中，导航到“收件人”\>“邮箱”，单击相应的邮箱，然后单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

  - 在邮箱属性页上，单击“邮箱功能”。

  - 在“移动设备”下，验证 Exchange ActiveSync 是处于启用状态还是禁用状态。

或

  - 在命令行管理程序中运行以下命令。
    
        Get-CASMailbox <identity>
    
    如果已启用 Exchange ActiveSync，*ActiveSyncEnabled* 属性的值为 `True`。如果已禁用 Exchange ActiveSync，则该值为 `False`。

