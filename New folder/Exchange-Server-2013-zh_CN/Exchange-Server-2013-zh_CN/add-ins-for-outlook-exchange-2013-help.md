---
title: '适用于 Outlook 的应用程序: Exchange 2013 Help'
TOCTitle: 适用于 Outlook 的应用程序
ms:assetid: 28b6f2a1-a235-4023-b561-6fd304962775
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ943753(v=EXCHG.150)
ms:contentKeyID: 52061489
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 适用于 Outlook 的应用程序

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2017-03-13_

**摘要：** 与 Windows 和 MacIntosh 计算机、移动设备上和 Outlook Web App 中的 Outlook 以及 Outlook 网页版一起使用的 Outlook 外接程序的概述。

Outlook 的外接程序是通过添加用户无需离开 Outlook 就能使用的信息或工具来扩展 Outlook 客户端实用性的应用程序。外接程序由第三方开发人员构建，可以从文件或 URL 或 Office 应用商店进行安装。默认情况下，所有用户都可以都安装外接程序。Exchange 管理员可以使用角色来控制用户安装外接程序的功能。

> [!tip]
> 有关从最终用户角度看待适用于 Outlook 的外接程序的信息，请查看 Office.com 上的帮助主题<a href="https://go.microsoft.com/fwlink/p/?linkid=2823">已安装的外接程序</a>。该主题提供了有关适用于 Outlook 的外接程序的概述，同时还展示了一些可能会默认安装的适用于 Outlook 的外接程序。


## Office 应用商店外接程序和自定义外接程序

Outlook 客户端支持各种各样的外接程序，可通过 Office 应用商店获取这些外接程序。Outlook 还支持自定义外接程序，你可以在组织中创建自定义外接程序并将其分发给用户。

> [!NOTE]
> 不支持特定区域内的邮箱或组织访问 Office 应用商店。如果在“<strong>组织</strong>”&gt;“<strong>外接程序</strong>”&gt; <img src="images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif" title="添加图标" alt="添加图标" /> 下的“<strong>Exchange 管理中心</strong>”中未看到“<strong>从 Office 应用商店添加</strong>”选项，则可以从 URL 或文件位置安装适用于 Outlook 的外接程序。有关详细信息，请与服务提供商联系。


> [!NOTE]
> 默认情况下，会安装一些适用于 Outlook 的外接程序。适用于 Outlook 的默认外接程序仅针对英语语言内容进行激活。例如，邮件正文中的德语邮政地址不会激活必应地图外接程序。


## 外接程序访问和安装

默认情况下，所有用户都可以都安装和删除外接程序。Exchange 管理员具有大量控件，可用于管理外接程序并允许用户对其进行访问。管理员可以禁止用户安装不是从 Office 应用商店下载（而是从文件或 URL 中“旁加载”获得）的外接程序。管理员还可以禁止用户安装 Office 应用商店外接程序，并禁止代表其他用户安装外接程序。还有可能为用户分配角色，允许他们在你的组织中为组织或用户子集安装外接程序。

若要阻止用户安装并非来自 Office 应用商店的外接程序，请删除他们的**我的自定义应用程序**角色。若要禁止用户安装来自 Office 应用商店的外接程序，请删除他们的**我的市场应用程序**角色。如需了解更多详情，请参阅[指定的管理员和用户可以安装和管理用于 Outlook 的外接程序](specify-the-administrators-and-users-who-can-install-and-manage-add-ins-for-outlook-exchange-2013-help.md)。

若要在组织中为部分或全部用户安装外接程序，请参阅[为组织安装或删除适用于 Outlook 的应用](install-or-remove-add-ins-for-outlook-for-your-organization-exchange-2013-help.md)。

如果需要，可以将外接程序的可用性限制为组织中的特定用户。有关详细信息，请参阅[管理用户对 Outlook 的应用程序的访问](manage-user-access-to-add-ins-for-outlook-exchange-online-help.md)。

## 使用 Outlook 相关外接程序执行的常见管理任务

Exchange 管理员在组织中进行管理有几个常见方案。

**如果想要防止最终用户在所有 Outlook 客户端上安装 Outlook 相关外接程序，可对 Exchange 管理中心的角色进行以下更改：** 

  - 若要阻止用户安装 Office 应用商店的外接程序，请删除他们的**我的市场**角色。

  - 若要阻止用户加载并非来自 Office 应用商店的源的外接程序，请删除他们的**我的自定义应用**角色。

  - 若要防止用户安装所有外接程序，请删除他们的以上两个角色。

有关详细信息，请参阅[指定的管理员和用户可以安装和管理用于 Outlook 的外接程序](specify-the-administrators-and-users-who-can-install-and-manage-add-ins-for-outlook-exchange-2013-help.md)。

**如果最终用户当前能够访问外接程序，并且你想要删除此访问权限，请使用 `Get-App` cmdlet 查看每个用户安装的外接程序。**

接下来，请使用 `Remove-App` cmdlet 删除一个或多个用户的任意外接程序。 

有关详细信息，请参阅 Exchange 2013 的 [Get-App](https://technet.microsoft.com/zh-cn/library/jj218673\(v=exchg.150\)) 和 [Remove-App](https://technet.microsoft.com/zh-cn/library/jj218709\(v=exchg.150\))。对于 Exchange Online 或 Exchange 2016，请转到[此处](https://go.microsoft.com/fwlink/p/?linkid=8447)。

## 允许管理员和用户安装外接程序

可以指定组织中的哪些管理员有权安装和管理适用于 Outlook 的外接程序。也可以指定组织中的哪些用户有权根据自己的使用需要安装并管理外接程序。有关详细信息，请参阅 [指定的管理员和用户可以安装和管理用于 Outlook 的外接程序](specify-the-administrators-and-users-who-can-install-and-manage-add-ins-for-outlook-exchange-2013-help.md)。

