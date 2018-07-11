---
title: '对公用文件夹启用或禁用邮件: Exchange 2013 Help'
TOCTitle: 对公用文件夹启用或禁用邮件
ms:assetid: 3d69f76d-ff3c-46c1-b962-6a1baa425d8a
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa997560(v=EXCHG.150)
ms:contentKeyID: 50490393
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 对公用文件夹启用或禁用邮件

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2016-06-15_

公用文件夹专为共享访问设计，为收集、组织信息及与您的工作组或组织中的其他人共享信息提供了一种轻松、有效的方式。为公用文件夹启用邮件功能，可以让用户能够向公用文件夹发送电子邮件，借此向此文件夹发布信息。如果公用文件夹启用了邮件功能，Exchange 管理中心 (EAC) 中将可以使用该公用文件夹的其他设置，例如电子邮件地址和邮件配额。在命令行管理程序中，为公用文件夹启用邮件功能之前，您可以使用 **Set-PublicFolder** cmdlet 管理它的所有设置。为公用文件夹启用邮件功能之后，您需要使用 **Set-PublicFolder** 和 **Set-MailPublicFolder** cmdlet 管理这些设置。

如果希望 Internet 用户向启用了邮件功能的公用文件夹发送邮件，需要使用 **Add-PublicFolderClientPermission** cmdlet 设置其他权限。

有关管理公用文件夹相关的更多管理任务，请参阅[公用文件夹程序](public-folder-procedures-exchange-2013-help.md)。

有关与公用文件夹相关的其他管理任务，请参阅[Office 365 和 Exchange Online 中的公用文件夹程序](https://technet.microsoft.com/zh-cn/library/jj966272\(v=exchg.150\))。

## 在开始之前，您需要知道什么？

  - 估计完成时间：5 分钟

  - 若要确保 Internet 用户能够向启用了邮件功能的公用文件夹发送电子邮件，公用文件夹必须至少拥有授予匿名帐户的 *CreateItems* 访问权限。如果要了解如何执行此操作，请查看允许匿名用户向启用了邮件功能的公用文件夹发送电子邮件。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[共享和协作权限](sharing-and-collaboration-permissions-exchange-2013-help.md)主题中的“公用文件夹”条目。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!tip]
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 您想执行什么操作？

## 使用 EAC 为公用文件夹启用或禁用邮件功能

1.  导航到“公用文件夹”\>“公用文件夹”。

2.  在列表视图中，选择要启用或禁用邮件功能的公用文件夹。

3.  在详细信息窗格中的“邮件设置”下，单击“启用”或“禁用”。

4.  随即出现显示警告框，询问您是否确定要为该公用文件夹启用或禁用电子邮件功能。单击“是”继续。

如果您希望外部用户向此公用文件夹发送邮件，请确保按照允许匿名用户向启用了邮件功能的公用文件夹发送电子邮件中的步骤操作。

## 使用命令行管理程序为公用文件夹启用邮件

本示例将为公用文件夹 Help Desk 启用邮件功能。

    Enable-MailPublicFolder -Identity "\Help Desk"

本示例将为 Marketing 公用文件夹下的 Reports 公用文件夹启用邮件功能，但在地址列表中隐藏该文件夹。

    Enable-MailPublicFolder -Identity "\Marketing\Reports" -HiddenFromAddressListsEnabled $True

如果您希望外部用户向此公用文件夹发送邮件，请确保按照允许匿名用户向启用了邮件功能的公用文件夹发送电子邮件中的步骤操作。

有关语法和参数的详细信息，请参阅 [Enable-MailPublicFolder](https://technet.microsoft.com/zh-cn/library/aa998824\(v=exchg.150\))。

## 使用命令行管理程序为公用文件夹禁用邮件

本示例将为公用文件夹 Marketing\\Reports 禁用邮件。

    Disable-MailPublicFolder -Identity "\Marketing\Reports"

有关语法和参数的详细信息，请参阅 [Disable-MailPublicFolder](https://technet.microsoft.com/zh-cn/library/bb123781\(v=exchg.150\))。

## 允许匿名用户向启用了邮件功能的公用文件夹发送电子邮件

您可以使用 Outlook 或命令行管理程序设置公用文件夹匿名帐户的权限。您不能使用 EAC 设置匿名帐户的权限。

**使用 Outlook 设置匿名帐户的权限**

1.  使用已被授予启用了电子邮件功能的公用文件夹（您希望匿名用户向其发送邮件）的“所有者”权限的帐户打开 Outlook。

2.  导航到“公用文件夹 - \<用户名称\>”。

3.  导航到您想要更改的公用文件夹。

4.  右键单击该公用文件夹，单击“属性”，然后选择“权限”选项卡。

5.  选择“匿名帐户”，选择“写入”下的“创建项目”，然后单击“确定”。

**使用命令行管理程序设置匿名帐户的权限**

本示例将设置匿名帐户对“客户反馈”已启用邮件功能的公用文件夹的 `CreateItems` 权限。

    Add-PublicFolderClientPermission "\Customer Feedback" -AccessRights CreateItems -User Anonymous

有关详细的语法和参数信息，请参阅[Add-PublicFolderClientPermission](https://technet.microsoft.com/zh-cn/library/bb124743\(v=exchg.150\))。

