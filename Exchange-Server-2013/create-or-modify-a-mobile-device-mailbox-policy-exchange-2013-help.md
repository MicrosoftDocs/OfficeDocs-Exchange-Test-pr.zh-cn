---
title: '创建或修改移动设备邮箱策略: Exchange 2013 Help'
TOCTitle: 创建或修改移动设备邮箱策略
ms:assetid: b4a37a81-25e3-40ff-a18a-a62ae4493635
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb124315(v=EXCHG.150)
ms:contentKeyID: 50491430
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 创建或修改移动设备邮箱策略

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2012-10-16_

通过移动设备邮箱策略可以将一组通用的安全和移动设备设置应用于一组用户。可以创建多个移动设备邮箱策略。组织中的每个收件人必须拥有已分配给他们的移动设备邮箱策略。安装 Microsoft Exchange Server 2013 时，会创建默认移动设备邮箱策略，并且会将新用户自动分配给此策略。若要将特定用户分配到移动设备邮箱策略，请参阅[从移动邮箱策略添加或删除用户](add-or-remove-users-from-a-mobile-mailbox-policy-exchange-2013-help.md)。

有关移动设备邮箱策略的更多信息，请参阅[移动设备邮箱策略](mobile-device-mailbox-policies-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤时间：10 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[客户端和移动设备权限](clients-and-mobile-devices-permissions-exchange-2013-help.md)主题中的“移动设备邮箱策略”条目。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 新建移动设备邮箱策略

可以使用 EAC 或命令行管理程序创建新的移动设备邮箱策略。

您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[客户端和移动设备权限](clients-and-mobile-devices-permissions-exchange-2013-help.md)主题中的“移动设备邮箱策略”条目。

## 使用 EAC 创建新的移动设备邮箱策略

可以使用 EAC 创建新的移动设备邮箱策略。

> [!NOTE]  
> 只能在 EAC 中设置移动设备邮箱策略设置的子集。若要设置所有移动设备邮箱策略设置，则需要使用命令行管理程序。


1.  在 EAC 中，单击“移动”\>“移动设备邮箱策略”，然后单击“新建”。

2.  使用各种复选框和下拉列表来配置移动设备邮箱策略的设置。
    
    > [!WARNING]  
    > 选择“这是默认策略”，以使新的移动邮箱策略成为默认移动邮箱策略。将移动邮箱策略设置为默认策略后，在新建用户时会将所有新用户自动分配到此策略。


3.  单击“保存”。

## 使用命令行管理程序创建新的移动设备邮箱策略

可以使用 New-MobileDeviceMailboxPolicy cmdlet 创建新的移动设备邮箱策略。

> [!WARNING]  
> 有两个 cmdlet 可用来创建新的移动设备邮箱策略。<strong>New-ActiveSyncMailboxPolicy</strong> cmdlet 和 <strong>New-MobileDeviceMailboxPolicy</strong> cmdlet 可执行相同的任务。在未来版本的 Microsoft Exchange Server 中，<strong>New-ActiveSyncMailboxPolicy</strong> cmdlet 将被删除。我们建议更新脚本和使用 <strong>New-MobileDeviceMailboxPolicy</strong> cmdlet 的过程。


1.  在此命令行管理程序中，运行以下命令。
    
        New-MobileDeviceMailboxPolicy -Name:"Management" -AllowBluetooth:$true -AllowBrowser:$true -AllowCamera:$true -AllowPOPIMAPEmail:$false -PasswordEnabled:$true -AlphanumericPasswordRequired:$true -PasswordRecoveryEnabled:$true -MaxEmailAgeFilter:10 -AllowWiFi:$true -AllowStorageCard:$true -AllowPOPIMAPEmail:$false

## 您如何知道这有效？

要验证是否已成功创建移动设备邮箱策略，可使用以下选项之一：

1.  在 EAC 中，单击“移动”\>“移动设备邮箱策略”，然后验证新策略是否已在列表视图中显示。

2.  在此命令行管理程序中，运行以下命令。
    
        Get-MobileDeviceMailboxPolicy -Identity <PolicyName> 

## 编辑现有移动设备邮箱策略

如果要编辑移动设备邮箱策略，可以使用 EAC 或命令行管理程序。

您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[客户端和移动设备权限](clients-and-mobile-devices-permissions-exchange-2013-help.md)主题中的“移动设备邮箱策略”条目。

## 使用 EAC 编辑移动设备邮箱策略

可以使用 EAC 编辑移动设备邮箱策略。

> [!NOTE]  
> 只能在 EAC 中编辑移动设备邮箱策略设置的子集。若要编辑所有移动设备邮箱策略设置，则需要使用命令行管理程序。


1.  在 EAC 中，单击“移动”\>“移动设备邮箱策略”。

2.  从列表视图中选择策略，然后单击“编辑”按钮。

3.  使用“常规”和“安全”选项卡来编辑移动设备邮箱策略设置。

4.  单击“保存”更新策略。

## 使用命令行管理程序编辑移动设备邮箱策略设置

可以使用命令行管理程序编辑移动设备邮箱策略。

> [!WARNING]  
> 有两个 cmdlet 可用来编辑移动设备邮箱策略。Set-ActiveSyncMailboxPolicy cmdlet 和 Set-MobileDeviceMailboxPolicy cmdlet 可执行相同的任务。在未来版本的 Microsoft Exchange Server 中，<strong>Set-ActiveSyncMailboxPolicy</strong> cmdlet 将被删除。我们建议更新脚本和使用 <strong>Set-MobileDeviceMailboxPolicy</strong> cmdlet 的过程。


1.  在此命令行管理程序中，运行以下命令。
    
        Set-MobileDeviceMailboxPolicy -Identity:Default -DevicePasswordEnabled:$true -AlphanumericDevicePasswordRequired:$true -PasswordRecoveryEnabled:$true -MaxEmailAgeFilter:ThreeDays -AllowWiFi:$false -AllowStorageCard:$true -AllowPOPIMAPEmail:$false -IsDefault:$true -AllowTextMessaging:$true -Confirm:$true

## 您如何知道这有效？

要验证是否已成功编辑移动设备邮箱策略，请执行以下操作之一：

1.  在 EAC 中，单击“移动”\>“移动设备邮箱策略”，然后选择特定策略。在“详细信息”窗格中，您将看到很多列出的策略设置。

2.  在此命令行管理程序中，运行以下命令。
    
        Get-MobileDeviceMailboxPolicy -Identity <PolicyName>

