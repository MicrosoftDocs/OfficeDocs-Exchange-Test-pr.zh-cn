---
title: '在 Exchange 中分配电子数据展示权限: Exchange 2013 Help'
TOCTitle: 在 Exchange 中分配电子数据展示权限
ms:assetid: 729e09d8-614b-431f-ae04-ae41fb4c628e
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd298059(v=EXCHG.150)
ms:contentKeyID: 50490836
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 在 Exchange 中分配电子数据展示权限

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2014-10-02_

如果希望用户能够使用 Microsoft Exchange Server 2013 就地电子数据展示，则必须首先通过将他们添加到发现管理角色组来对他们进行授权。发现管理 角色组的成员拥有 Exchange 安装程序创建的发现邮箱的完全访问邮箱权限。

> [!CAUTION]  
> 发现管理角色组的成员可以访问敏感邮件内容。具体而言，这些成员可以使用 <a href="in-place-ediscovery-exchange-2013-help.md">就地电子数据展示</a> 搜索 Exchange 组织中的所有邮箱，预览邮件（以及其他邮箱项目），将邮件复制到发现邮箱并将复制的邮件导出到 .pst 文件。在大多数组织中，会向法律、遵从性或人力资源部人员授予此权限。


有关发现管理角色组的详细信息，请参阅[发现管理](discovery-management-exchange-2013-help.md)。有关基于角色的访问控制 (RBAC) 的详细信息，请参阅[了解基于角色的访问控制](understanding-role-based-access-control-exchange-2013-help.md)。

对本程序使用的方案感兴趣？请参阅下列主题：

  - [创建就地电子数据展示搜索](create-an-in-place-ediscovery-search-exchange-2013-help.md)

  - [创建或删除就地保留](create-or-remove-an-in-place-hold-exchange-2013-help.md)

## 在开始之前，您需要知道什么？

  - 估计完成时间：1 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[角色管理权限](role-management-permissions-exchange-2013-help.md)主题中的“角色组”条目。

  - 默认情况下，发现管理 角色组不包含任何成员。具有 组织管理 角色的管理员如果不添加到 发现管理 角色组，也无法创建或管理发现搜索。

  - 在 Exchange 2013 中，组织管理 角色组的成员可以创建 [就地保留和诉讼保留](in-place-hold-and-litigation-hold-exchange-2013-help.md) 以将所有邮箱内容置于保留中。但是，要创建基于查询的就地保留，用户必须是发现管理角色组的成员或分配有邮箱搜索角色。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

## 使用 EAC 将用户添加到发现管理角色组

1.  转到“权限”\>“管理员角色”。

2.  在列表视图中，选择“发现管理”，然后单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在“角色组”中的“成员”下，单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。

4.  在“选择成员”中，选择一个或多个用户，单击“添加”，然后单击“确定”。

5.  在“角色组”中，单击“保存”。

## 使用命令行管理程序将用户添加到“发现管理”角色组

此示例会将用户 Bsuneja 添加到发现管理角色组中。

    Add-RoleGroupMember -Identity "Discovery Management" -Member Bsuneja

有关语法和参数的详细信息，请参阅 [Add-RoleGroupMember](https://technet.microsoft.com/zh-cn/library/dd638207\(v=exchg.150\))。

## 您如何知道这有效？

若要验证是否已将用户添加到发现管理角色组，请执行以下操作：

1.  在 EAC 中，转到“权限”\>“管理员角色”。

2.  在列表视图中，选择“发现管理”。

3.  在“详细信息”窗格中，验证该用户是否列在“成员”下。

还可以运行此命令列出发现管理角色组的成员。

    Get-RoleGroupMember -Identity "Discovery Management"

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。

