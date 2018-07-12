---
title: '指定的管理员和用户可以安装和管理用于 Outlook 的外接程序: Exchange Online Help'
TOCTitle: 指定的管理员和用户可以安装和管理用于 Outlook 的外接程序
ms:assetid: 7ee4302d-b8bb-40a0-9810-10d3a0271bcb
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ943754(v=EXCHG.150)
ms:contentKeyID: 52061526
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 指定的管理员和用户可以安装和管理用于 Outlook 的外接程序

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2017-02-08_

您可以指定您的组织中的管理员有权安装和管理用于 Outlook 的外接程序。您还可以指定您的组织中哪些用户具有权限进行安装和管理供自己使用的加载项。

这是通过分配或删除特定于外接程序的管理角色。有五个可用的内置角色。

管理角色

  - **组织市场应用程序**  使管理员能够安装和管理程序可从 Office 商店为其组织的外接程序。

  - **组织结构图自定义应用程序**  使管理员能够安装并管理其组织的加载项自定义。

用户角色

  - **我市场上的应用程序**  使用户能够安装和管理办公商店外接程序供自己使用。

  - **我的自定义应用程序**  使用户能够安装和管理自定义外接供自己使用。

  - **我的 ReadWriteMailbox 应用程序**  使用户能够安装和管理请求在其清单中的 ReadWriteMailbox 权限级别的外接程序。

默认情况下，有**组织管理**角色组的所有管理员都使用上述管理角色启用。默认情况下，最终用户还有上述启用的用户角色。

有关上述每个角色的信息，请参阅[组织市场应用角色](org-marketplace-apps-role-exchange-2013-help.md)、 [组织的自定义应用角色](org-custom-apps-role-exchange-2013-help.md)、 [我的市场应用角色](my-marketplace-apps-role-exchange-2013-help.md)、 [我的自定义应用角色](my-custom-apps-role-exchange-2013-help.md)和[我的 ReadWriteMailbox 应用角色](my-readwritemailbox-apps-role-exchange-2013-help.md)。

有关外接程序的信息，请参阅[适用于 Outlook 的应用程序](add-ins-for-outlook-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：5 分钟。

  - 您必须先获得权限，然后才能运行此 cmdlet。虽然此主题中列出了该 cmdlet 的所有参数，但如果这些参数未包含在分配给您的权限中，则您无法使用这些参数。若要查看所需的权限，请参阅 [角色管理权限](role-management-permissions-exchange-2013-help.md)主题中的"角色分配"条目。

  - 不支持特定区域内的邮箱或组织访问 Office 应用商店。如果在\&quot;**组织**\&quot;\>\&quot;**外接程序**\&quot;\> ![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标") 下的\&quot;**Exchange 管理中心**\&quot;中未看到\&quot;**从 Office 应用商店添加**\&quot;选项，则可以从 URL 或文件位置安装适用于 Outlook 的外接程序。有关详细信息，请与服务提供商联系。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 指定管理员安装和管理外接程序为您的组织所需的权限

## 使用 EAC 向管理员分配权限

EAC 可用于分配管理员安装和管理办公商店为您的组织从外接程序，它提供所需的权限。有关如何执行此操作的详细信息，请参阅[管理角色组](manage-role-groups-exchange-2013-help.md)。

## 将用户分配安装和管理供自己使用的外接程序所需的权限

## 使用 EAC 向用户分配权限

EAC 可用于指定用户可以查看和修改他们自己使用的加载项自定义所需的权限。有关如何执行此操作的详细信息，请参阅[管理角色组](manage-role-groups-exchange-2013-help.md)。

## 您如何知道操作成功？

要验证您已成功为用户分配权限，请运行使用 `Get-ManagementRoleAssignment -Role <Role Name> -GetEffectiveUsers` 格式的命令行管理程序命令，其中 `Role Name` 是您要为其验证分配的权限的角色。

此示例演示如何验证其归入权从办公室存储为组织安装外接程序。

1.  运行 `Get-ManagementRoleAssignment -Role "Org Marketplace Apps" -GetEffectiveUsers`。

2.  在结果中，查看\&quot;Effective Users\&quot;列中的条目。

有关语法和参数的详细信息，请参阅 [Get-ManagementRoleAssignment](https://technet.microsoft.com/zh-cn/library/dd351024\(v=exchg.150\))。

