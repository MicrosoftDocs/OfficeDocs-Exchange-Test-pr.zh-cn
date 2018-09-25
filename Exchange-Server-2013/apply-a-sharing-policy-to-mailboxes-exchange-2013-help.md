---
title: '将共享策略应用于邮箱: Exchange 2013 Help'
TOCTitle: 将共享策略应用于邮箱
ms:assetid: dd4cc765-8469-4176-bb6e-d5b0f5235927
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ657501(v=EXCHG.150)
ms:contentKeyID: 50491753
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 将共享策略应用于邮箱

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2014-02-15_

共享策略是联合共享的一部分并允许与不同类型的外部用户进行用户建立的、人对人的日历信息共享。管理员应用于用户邮箱的共享策略决定了用户可以共享的访问级别，以及可以与谁共享。如果不做任何更改，则默认共享策略适用于所有用户。如果创建了新的共享策略，必须将该策略应用到邮箱，才能生效。共享策略可应用至单个用户邮箱或同时应用至多个用户邮箱。管理员还可以禁用用户的共享策略，以阻止对日历的外部访问。

若要了解有关联合共享的详细信息，请参阅[共享](sharing-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：5 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[收件人权限](recipients-permissions-exchange-2013-help.md)主题中的*Recipient Provisioning Permissions*条目。

  - 必须有共享策略。有关详细信息，请参阅[创建共享策略](create-a-sharing-policy-exchange-2013-help.md)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

## 您想执行什么操作？

## 使用 EAC 将共享策略应用于单个邮箱

1.  导航到“收件人”\>“邮箱”。

2.  在列表视图中，选择需要的邮箱，然后单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在“用户邮箱”中，单击“邮箱功能”。

4.  在“共享策略”列表中，选择要应用至该游戏的共享策略。

5.  单击“保存”应用此共享策略。

## 使用 EAC 将共享策略应用于多个邮箱

1.  导航到“收件人”\>“邮箱”。

2.  在列表视图中，按住 Ctrl 键选择多个邮箱。

3.  在详细信息窗格中，将配置邮箱属性以进行批量编辑。单击“更多选项”。

4.  在“共享策略”下单击“更新”。

5.  在“批量分配共享策略”中使用“选择共享策略”列表来选择要分配给邮箱的共享策略。

6.  单击“保存”将共享策略应用至所选邮箱。

## 使用命令行管理程序将共享策略应用至一个或多个邮箱

该示例将共享策略 Contoso 应用至用户 Barbara 的单个邮箱。

```powershell
Set-Mailbox -Identity Barbara -SharingPolicy "Contoso"
```

本示例指定市场部门中的所有用户邮箱均使用 Contoso Marketing 共享策略。

```powershell
Get-Mailbox -Filter {Department -eq "Marketing"} | Set-Mailbox -SharingPolicy "Contoso Marketing"
```

本示例返回所有应用了 Contoso 共享策略的邮箱，并将用户分类放置到仅显示其别名和电子邮件地址的表中。

```powershell
Get-Mailbox -ResultSize unlimited | Where {$_.SharingPolicy -eq "Contoso" } | format-table Alias, EmailAddresses
```

有关语法和参数的详细信息，请参阅 [Set-Mailbox](https://technet.microsoft.com/zh-cn/library/bb123981\(v=exchg.150\)) 和 [Get-Mailbox](https://technet.microsoft.com/zh-cn/library/bb123685\(v=exchg.150\))。

## 您如何知道这有效？

要检查是否成功将共享策略应用至用户邮箱，可进行以下操作之一：

  - 在 EAC 中，导航到“收件人”\>“邮箱”，然后选择要对其应用共享策略的邮箱。单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")，单击“邮箱功能”，然后确认在“共享策略”列表中出现的共享策略是否正确。

  - 运行以下命令行管理程序命令，验证是否将共享策略指定至用户邮箱。验证列在 *SharingPolicy* 参数中的共享策略是否正确。
    
    ```powershell
    Get-Mailbox <user name> | format-list
    ```

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。

