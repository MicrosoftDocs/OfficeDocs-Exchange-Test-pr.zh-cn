---
title: '删除组织关系: Exchange 2013 Help'
TOCTitle: 删除组织关系
ms:assetid: ff211394-f58b-4da7-bb3a-df6abcb5950e
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ657513(v=EXCHG.150)
ms:contentKeyID: 50492060
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 删除组织关系

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-01-04_

组织关系可让 Exchange 组织中的用户与 Office 365 组织或其他 Exchange 本地组织共享日历忙/闲信息。您可以通过删除组织关系来禁用与其他组织共享日历。

您必须先设置与 Azure Active Directory 身份验证系统（亦称为\&quot;联合身份验证\&quot;）的身份验证关系且必须满足最低软件要求，然后才能与其他组织共享日历。若要了解有关联合共享的详细信息，请参阅[共享](sharing-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：5 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [收件人权限](recipients-permissions-exchange-2013-help.md)主题中的\&quot;日历和共享权限\&quot;条目。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

## 您想执行什么操作？

## 使用 EAC 删除组织关系

1.  在本地组织中的 Exchange 2013 服务器上，导航到\&quot;组织\&quot;\>\&quot;共享\&quot;。

2.  在\&quot;组织共享\&quot;下，选择组织关系，然后单击\&quot;删除\&quot;![删除图标](images/JJ657511.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "删除图标")以删除组织关系。

3.  在随即显示的警告中，单击\&quot;是\&quot;。

## 使用命令行管理程序删除组织关系

本示例将删除 Exchange 组织的组织关系 Contoso

    Remove-OrganizationRelationship -Identity "Contoso"

有关语法和参数的详细信息，请参阅 [Remove-OrganizationRelationship](https://technet.microsoft.com/zh-cn/library/ee332362\(v=exchg.150\))。

## 您如何知道这有效？

验证是否已成功删除了组织关系，请执行以下操作之一：

  - 在 EAC 中，导航到\&quot;组织\&quot;\>\&quot;共享\&quot;并验证组织关系是否未显示在\&quot;组织共享\&quot;下的列表视图中。

  - 运行以下命令行管理程序命令以验证已删除组织关系信息。
    
        Get-OrganizationRelationship | Format-List

> [!tip]
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。

