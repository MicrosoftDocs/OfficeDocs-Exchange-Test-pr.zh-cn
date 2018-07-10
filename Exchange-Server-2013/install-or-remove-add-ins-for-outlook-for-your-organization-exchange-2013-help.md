---
title: '为组织安装或删除适用于 Outlook 的应用: Exchange 2013 Help'
TOCTitle: 为组织安装或删除适用于 Outlook 的应用
ms:assetid: 112f3ef7-9943-4a1e-8a42-e08e8e9f67f4
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ943752(v=EXCHG.150)
ms:contentKeyID: 52061482
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 为组织安装或删除适用于 Outlook 的应用

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2017-02-03_

可以使用 EAC 或 Shell 为组织安装或删除适用于 Outlook 的外接程序。

> [!NOTE]
> 默认情况下，为组织安装的外接程序对组织中的所有用户均可用。安装完成后，可使用 EAC 或 Shell 使外接程序成为用户可选或必需选择，并指定是否希望启用或禁用该外接程序。有关如何为外接程序更改默认设置的信息，请参阅 <a href="manage-user-access-to-add-ins-for-outlook-exchange-online-help.md">管理用户对 Outlook 的应用程序的访问</a>。若要在组织中限制外接程序对特定用户的可用性，必须使用 Shell。有关详细信息，请参阅 <a href="manage-user-access-to-add-ins-for-outlook-exchange-online-help.md">管理用户对 Outlook 的应用程序的访问</a>。


有关更多管理任务，请参阅 [适用于 Outlook 的应用程序](add-ins-for-outlook-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：5 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[收件人权限](recipients-permissions-exchange-2013-help.md)主题中的“Outlook 的应用”条目。

  - 可以分配管理员权限为组织安装和管理外接程序。也可以分配用户权限安装和管理供自己使用的外接程序。有关详细信息，请参阅 [指定的管理员和用户可以安装和管理用于 Outlook 的外接程序](specify-the-administrators-and-users-who-can-install-and-manage-add-ins-for-outlook-exchange-2013-help.md)。

  - 不支持特定区域内的邮箱或组织访问 Office 应用商店。如果在“**组织**”\>“**外接程序**”\> ![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标") 下的“**Exchange 管理中心**”中未看到“**从 Office 应用商店添加**”选项，则可以从 URL 或文件位置安装适用于 Outlook 的外接程序。有关详细信息，请与服务提供商联系。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!tip]
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 安装适用于 Outlook 的外接程序

## 使用 EAC 添加外接程序

1.  在 EAC 中，导航到“**组织**”\>“**外接程序**”。

2.  单击“**新建**”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")，然后选择你希望安装外接程序的位置。
    
      - “**从 Office 应用商店添加**”。从 Office 应用商店选择你希望安装的应用程序，然后单击“**添加**”。与 Outlook Web App 共同使用的应用程序均在“**Office 和 SharePoint 的外接程序**”\>“**Outlook**”下列出。
        
        > [!NOTE]
        > 不支持特定区域内的邮箱或组织访问 Office 应用商店。如果在“<strong>组织</strong>”&gt;“<strong>外接程序</strong>”&gt; <img src="images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif" title="添加图标" alt="添加图标" /> 下的“<strong>Exchange 管理中心</strong>”中未看到“<strong>从 Office 应用商店添加</strong>”选项，则可以从 URL 或文件位置安装适用于 Outlook 的外接程序。有关详细信息，请与服务提供商联系。
    
      - “**从 URL 添加**”。在“**URL**”中，输入你希望安装的外接程序清单文件完整的 URL。
    
      - “**从文件添加**”。选择“**浏览**”，然后导航到你希望安装的外接程序清单文件的位置。

3.  单击“保存”。

## 使用命令行管理程序添加外接程序

本示例显示如何从 URL 添加外接程序。

    New-App -OrganizationApp -Url <URL location for add-in manifest file>

本示例显示如何从文件添加外接程序。

    New-App -OrganizationApp -FileData <File location for add-in manifest file>

> [!tip]
> 使用命令行管理程序为组织安装外接程序时，可以在安装外接程序的同时为其配置设置。


有关语法和参数的详细信息，请参阅 [New-App](https://technet.microsoft.com/zh-cn/library/jj218722\(v=exchg.150\))。

## 删除适用于 Outlook 的外接程序

## 使用 EAC 删除外接程序

1.  在 EAC 中，导航到“**组织**”\>“**外接程序**”。

2.  在列表视图中，选择希望删除的应用程序，然后单击“删除”![删除图标](images/JJ657511.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "删除图标")。

## 使用 Shell 删除外接程序

可以使用 Shell 从组织中删除外接程序。

> [!NOTE]
> 运行以下命令，查找组织内安装的所有适用于 Outlook 的外接程序的显示名称和应用程序 ID。


    Get-App -OrganizationApp |FL DisplayName,AppID

运行以下命令，从组织中删除名为 Finance Test App-in 的自定义外接程序。

    Remove-App -OrganizationApp -Identity <GUID for Finance Test Add-in>

有关语法和参数的详细信息，请参阅 [Remove-App](https://technet.microsoft.com/zh-cn/library/jj218709\(v=exchg.150\))。

## 您如何知道操作成功？

若要查看组织中已安装的外接程序，请执行下列操作之一：

  - 在 EAC 中，导航到“**组织**”\>“**外接程序**”，然后查看已安装外接程序的列表。

  - 从命令行管理程序中运行 `Get-App`，然后查看已安装外接程序的列表。

