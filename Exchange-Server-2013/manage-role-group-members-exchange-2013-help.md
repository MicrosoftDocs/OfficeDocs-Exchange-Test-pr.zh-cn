---
title: '管理角色组成员: Exchange 2013 Help'
TOCTitle: 管理角色组成员
ms:assetid: c064729d-7cda-47fc-b105-acf4b300d430
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ657492(v=EXCHG.150)
ms:contentKeyID: 50491583
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 管理角色组成员

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2012-10-08_

本主题介绍如何在 Microsoft Exchange Server 2013 中添加、删除和查看管理角色组的成员。有关 Exchange 2013 中角色组的详细信息，请参阅[了解管理角色组](understanding-management-role-groups-exchange-2013-help.md)。

有关角色组相关的其他管理任务，请参阅 [权限](permissions-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤时间：5 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [角色管理权限](role-management-permissions-exchange-2013-help.md)主题中的\&quot;角色组\&quot;条目。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 您想执行什么操作？

## 向角色组添加成员

要向某个用户提供由角色组授予的权限，需要添加该用户、通用安全组 (USG) 或该用户所属的其他角色组作为角色组成员。

## 使用 EAC 向角色组添加成员

1.  在 Exchange 管理中心 (EAC) 中，导航到\&quot;权限\&quot;\>\&quot;管理员角色\&quot;。

2.  选择要向其添加成员的角色组，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在\&quot;成员\&quot;部分，单击\&quot;添加\&quot;![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。

4.  选择要添加到角色组的用户、USG 或其他角色组，单击\&quot;添加\&quot;，然后单击\&quot;确定\&quot;。

5.  单击\&quot;保存\&quot;以保存对角色组的更改。

## 使用命令行管理程序向角色组添加成员

示例

示例

## 您如何知道这有效？

要验证您是否已成功将一个或多个成员添加到角色组，请执行以下操作：

1.  在 EAC 中，导航到\&quot;权限\&quot; \> \&quot;管理员角色\&quot;。

2.  选择要添加成员的角色组。

3.  在角色组详细信息窗格中，确认您添加的成员是否已列出。

## 从角色组删除成员

若要删除用户的角色组授予的权限，则需要从角色组成员资格中删除该用户，或删除该用户所属的通用安全组 (USG)。

## 使用 EAC 从角色组中删除成员

1.  在 EAC 中，导航到\&quot;权限\&quot; \> \&quot;管理员角色\&quot;。

2.  选择要从中删除成员的角色组，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在\&quot;成员\&quot;部分中，选择要删除的成员，单击\&quot;删除\&quot;![删除图标](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "删除图标")，然后单击\&quot;保存\&quot;。

## 使用命令行管理程序从角色组中删除成员

示例

示例

## 您如何知道这有效？

要验证您是否已成功从角色组中删除一个或多个成员，请执行以下操作：

1.  在 EAC 中，导航到\&quot;权限\&quot; \> \&quot;管理员角色\&quot;。

2.  请选择要删除成员的角色组。

3.  在角色组详细信息窗格中，确认您删除的成员已不再列出。

## 查看角色组的成员

角色组的成员将获得分配给该角色组的管理角色提供的权限。你可以查看角色组成员，了解为哪些用户、通用安全组 (USG) 或其他角色组授予了你指定的角色组提供的权限。

## 使用 EAC 查看角色组成员

1.  在 EAC 中，导航到\&quot;权限\&quot; \> \&quot;管理员角色\&quot;。

2.  选择您要查看其成员的角色组。

3.  在角色组详细信息窗格中，查看角色组详细信息窗格中的成员。

## 使用命令行管理程序查看角色组成员

示例

