---
title: '将通讯簿策略分配给邮件用户: Exchange 2013 Help'
TOCTitle: 将通讯簿策略分配给邮件用户
ms:assetid: bdfe6575-24c0-47d0-9cfb-ece910db248b
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Hh529942(v=EXCHG.150)
ms:contentKeyID: 50491539
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 将通讯簿策略分配给邮件用户

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2012-10-11_

在创建了通讯簿策略 (ABP) 之后，必须将其分配给邮箱用户。在创建用户的帐户时，不会向用户分配默认 ABP。如果不向用户分配 ABP，则用户可通过 Outlook 和 Outlook Web App 访问整个组织的全局地址列表 (GAL)。若要了解详细信息，请参阅[通讯簿策略](address-book-policies-exchange-2013-help.md)。

关于 ABP 的更多管理任务，请参阅[通讯簿策略程序](address-book-policy-procedures-exchange-2013-help.md)。

对使用此步骤的应用场景有兴趣吗？请参阅[方案：部署通讯簿策略](scenario-deploying-address-book-policies-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：不超过 5 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[电子邮件地址和通讯簿权限](email-address-and-address-book-permissions-exchange-2013-help.md)主题中的“通讯簿策略”条目。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!tip]
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 您想执行什么操作？

## 使用 EAC 向邮箱用户分配 ABP

1.  导航到“收件人”\>“邮箱”。

2.  在此列表视图中，选择您要为其分配策略的用户，然后单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  单击“邮箱功能”。

4.  在“通讯簿策略”列表中，选择要应用到此用户的 ABP。

5.  单击“保存”。

## 使用 EAC 向多个邮箱用户分配 ABP

1.  导航到“收件人”\>“邮箱”。

2.  在列表视图中使用 Ctrl 键选择多个用户。

3.  在详细信息窗格中，单击“更多选项”。

4.  在“通讯簿策略”下面单击“更新”。

5.  在“选择通讯簿策略”列表中，选择要应用到这些用户的 ABP。

6.  单击“保存”。

## 使用命令行管理程序向邮箱用户分配 ABP

此示例要将名为 All Fabrikam 的 ABP 分配给现有邮箱用户 joe@fabrikam.com。

    Set-Mailbox -Identity joe@fabrikam.com -AddressBookPolicy "All Fabrikam"

此示例要将名为 ABP\_EngineeringDepartment 的 ABP 分配给其 `CustomAttribute11` 值包含“Engineering Department”的所有邮箱用户。

    Get-Mailbox -Filter {(CustomAttribute11 -like "Engineering Department")} | Set-Mailbox -AddressBookPolicy ABP_EngineeringDepartment

有关语法和参数的详细信息，请参阅 [Set-Mailbox](https://technet.microsoft.com/zh-cn/library/bb123981\(v=exchg.150\)) 和 [Get-Mailbox](https://technet.microsoft.com/zh-cn/library/bb123685\(v=exchg.150\))。

