---
title: '修改组织关系: Exchange 2013 Help'
TOCTitle: 修改组织关系
ms:assetid: 3713ef83-f01a-41bb-b127-62ca242dd7a4
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ673055(v=EXCHG.150)
ms:contentKeyID: 50490311
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 修改组织关系

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-01-01_

组织关系可让 Exchange 组织中的用户与 Office 365 组织或其他本地 Exchange 组织共享日历忙/闲信息。您可能希望更改某个组织关系的设置，例如更改名称、临时禁用日历共享、更改访问级别或更改将共享日历的安全组。

您必须先设置与云的身份验证关系（亦称为\&quot;联合身份验证\&quot;）且必须满足最低软件要求，然后才能与其他组织共享日历。若要了解有关联合共享的详细信息，请参阅[共享](sharing-exchange-2013-help.md)。

有关与联合身份验证相关的更多管理任务，请参阅[联合程序](federation-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：15 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [收件人权限](recipients-permissions-exchange-2013-help.md)主题中的*Calendar and Sharing Permissions*条目。

  - 必须配置针对本地 Exchange 组织的活动联合信任。

  - 要在组织关系中配置的外部组织必须还与 Azure AD 身份验证系统建立联合身份验证信任。

  - 本主题中的步骤将对名为 Contoso 的组织关系作出更改。示例演示如何：
    
      - 将名为 service.contoso.com 的域添加到外部组织。
    
      - 禁用组织关系的忙/闲共享。
    
      - 将忙/闲访问级别从*Calendar free/busy information with time, subject, and location*更改为*Calendar free/busy information with time only*。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

## 您想执行什么操作？

## 使用 EAC 将域添加到组织关系

1.  在本地组织中的 Exchange 2013 服务器上，导航到\&quot;组织\&quot;\>\&quot;共享\&quot;。

2.  在列表视图的\&quot;组织共享\&quot;下，选择组织关系 Contoso，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在\&quot;组织关系\&quot;中，\&quot;常规\&quot;不更改组织关系的\&quot;名称\&quot;。

4.  在\&quot;要共享的域\&quot;框中，输入域\&quot;service.contoso.com\&quot;，然后单击\&quot;添加\&quot;![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。

5.  单击\&quot;保存\&quot;更新组织关系。

## 使用 EAC 禁用组织关系的忙/闲信息共享

1.  转到\&quot;组织\&quot;\>\&quot;共享\&quot;。

2.  在列表视图的\&quot;组织共享\&quot;下，选择组织关系 Contoso，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在\&quot;组织关系\&quot;中，单击\&quot;共享\&quot;

4.  选择\&quot;仅与时间有关的日历忙/闲信息\&quot;。

5.  单击\&quot;保存\&quot;更新组织关系。

## 使用 EAC 更改组织关系的忙/闲访问级别

1.  转到\&quot;组织\&quot;\>\&quot;共享\&quot;。

2.  在列表视图的\&quot;组织共享\&quot;下，选择组织关系 Contoso，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在\&quot;组织关系\&quot;中，单击\&quot;共享\&quot;

4.  选择\&quot;仅与时间有关的日历忙/闲信息\&quot;。

5.  单击\&quot;保存\&quot;更新组织关系。

## 使用命令行管理程序修改组织关系

  - 此示例将域名 service.contoso.com 添加到组织关系 Contoso。
    
        $domains = (Get-OrganizationRelationship Contoso).DomainNames
        $domains += 'service.contoso.com'
        Set-OrganizationRelationship -Identity Contoso -DomainNames $domains

  - 此示例将禁用组织关系 Contoso。
    
        Set-OrganizationRelationship -Identity Contoso -Enabled $false

  - 此示例将启用组织关系 WoodgroveBank 的日历可用性信息访问，并将访问级别设置为 `AvailabilityOnly`（仅包含时间的日历忙/闲信息）。
    
        Set-OrganizationRelationship -Identity Contoso -FreeBusyAccessEnabled $true -FreeBusyAccessLevel AvailabilityOnly

有关语法和参数的详细信息，请参阅 [Get-OrganizationRelationship](https://technet.microsoft.com/zh-cn/library/ee332343\(v=exchg.150\)) 和 [Set-OrganizationRelationship](https://technet.microsoft.com/zh-cn/library/ee332326\(v=exchg.150\))。

## 您如何知道这有效？

要验证您是否已成功更新了组织关系，请运行下列命令行管理程序命令来验证组织关系的信息。

    Get-OrganizationRelationship | format-list

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。

