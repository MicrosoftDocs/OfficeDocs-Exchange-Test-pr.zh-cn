---
title: '共享邮箱: Exchange 2013 Help'
TOCTitle: 共享邮箱
ms:assetid: 1d71c01b-e261-408e-a633-1d1c9d00032a
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ150498(v=EXCHG.150)
ms:contentKeyID: 50490007
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 共享邮箱

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-06-04_

了解 Microsoft Exchange Server 2013 中的 Exchange 共享邮箱、使用理由，以及如何将委派邮箱转换为 Exchange 共享邮箱。

共享邮箱是一个可供多个用户读取和发送电子邮件的邮箱。共享邮箱还可用于提供常见日历，允许多个用户计划和查看度假时间或轮班。

不支持在移动设备上共享邮箱。

**为什么设置共享邮箱？**

  - 提供客户可用于询问贵公司信息的通用电子邮件地址（如 info@contoso.com 或 sales@contoso.com）。

  - 允许向员工提供集中服务的部门（如技术支持部门、人力资源部门或打印服务部门）对员工的问题做出回应。

  - 允许多个用户监控和回应发送到电子邮件地址（如技术支持部门指定的地址）的电子邮件。

## 什么是共享邮箱？

共享邮箱是一种没有自身用户名和密码的用户邮箱。因此，用户无法直接登录该邮箱。若要访问共享邮箱，必须先授予用户对邮箱的“代理发送”或“完全访问”权限。完成此操作后，用户便可登录自己的邮箱，然后通过将共享邮箱添加到其 Outlook 的个人资料中，即可访问共享邮箱。在 Exchange 2003 和更早版本中，共享邮箱只是一个管理员可以向其授予委派访问权限的常规邮箱。从 Exchange 2007 开始，共享邮箱变为其自己的收件人类型：

  - **RecipientType：** UserMailbox

  - **RecipientTypeDetails：** SharedMailbox

在上一版本的 Exchange 中，创建共享邮箱是一个多步骤过程，在该过程中您必须使用 Exchange 命令行管理程序来完成某些任务。在 Exchange 2013 中，您可以使用 Exchange 管理中心 (EAC) 来创建共享邮箱，只需一个步骤即可完成。有关详细信息，请参阅[创建共享邮箱](create-a-shared-mailbox-exchange-2013-help.md)。事实上，EAC 具有一个专用于共享邮箱的功能区域。仅需导航到“收件人”\>“共享邮箱”，即可查看共享邮箱的所有管理任务。

您可以使用共享邮箱的以下权限。

  - **完全访问权限** 完全访问权限允许用户登录共享邮箱并作为该邮箱的所有者。访问共享邮箱后，用户可以创建日历项目；读取、查看、删除和更改电子邮件消息；创建任务和日历联系人。然而，具有完全访问权限的用户无法从共享邮箱发送电子邮件，除非他们同时拥有“发送为”或“代表发送”权限。

  - **发送为**   “发送为”权限允许用户在发送邮件时模仿共享邮箱。例如，如果 Kweku 登录共享邮箱“Marketing Department”并发送电子邮件，这将显示为是“Marketing Department”发送的邮件。

  - **代表发送**   “代表发送”权限允许用户代表共享邮箱发送电子邮件。例如，如果 John 登录共享邮箱“Reception Building 32”并发送电子邮件，邮件将显示为由“John 代表 Reception Building 32”发送。您不能使用 EAC 来授予“代表发送”权限，您必须结合使用 [Set-Mailbox](https://technet.microsoft.com/zh-cn/library/bb123981\(v=exchg.150\)) cmdlet 和 *GrantSendonBehalf* 参数。

## 转换共享邮箱

在早期版本的 Exchange 中，您可以使用常规邮箱作为委派邮箱。若您拥有委派邮箱，则可以使用命令行管理程序将这些委派邮箱转换为共享邮箱。有关详细信息，请参阅[转换邮箱](https://technet.microsoft.com/zh-cn/library/jj710164(v=exchg.150))。

