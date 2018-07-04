---
title: '创建组织关系: Exchange 2013 Help'
TOCTitle: 创建组织关系
ms:assetid: 5ea61b96-c8ca-44fc-b8b5-ca4341af36a6
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ657451(v=EXCHG.150)
ms:contentKeyID: 50490677
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 创建组织关系

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-04-07_

设置组织关系以便与外部商业合作伙伴共享日历信息。可以在两个联合 Exchange 2013 组织之间或在联合 Exchange 2013 组织与联合 Exchange 2010 组织之间配置组织关系。您还可以在本地 Exchange 组织和 Office 365 组织之间设置组织关系。

> [!important]
> 创建组织关系是在 Exchange 组织中设置联合共享的若干步骤之一，需要为内部部署 Exchange 组织配置联合身份验证信任。


若要了解有关联合共享的详细信息，请参阅[共享](sharing-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：15 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[收件人权限](recipients-permissions-exchange-2013-help.md)主题中的“日历和共享权限”部分。

  - 必须配置针对本地 Exchange 组织的活动联合信任。有关详细信息，请参阅[配置联合身份验证信任](configure-a-federation-trust-exchange-2013-help.md)。

  - 要在组织关系中配置的外部组织必须还与 Azure AD 身份验证系统建立联合身份验证信任。在配置组织关系时将主联盟域用于外部 Exchange 组织。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

## 您想执行什么操作？

## 使用 EAC 创建组织关系

1.  在本地组织中的 Exchange 2013 服务器上，导航到“组织”\>“共享”。

2.  在“组织共享”下，单击“新建”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。

3.  在“新建组织关系”中的“关系名称”框中，为组织关系键入友好名称。

4.  在“要共享的域”框中，为允许其查看日历的 Office 365 或 Exchange 本地组织键入联合域或联合子域。如果需要为外部组织输入多个域，可用逗号分隔各个域。例如，**contoso.com、service.contoso.com**。

5.  选中“启用日历忙/闲信息共享”复选框，以开启与列出的域的日历共享。设置日历忙/闲信息的共享级别，并设置可以共享日历忙/闲信息的用户。
    
    若要设置忙/闲访问级别，请选择以下项目之一：
    
      - **仅包含时间的日历忙/闲信息**
    
      - **包含时间、主题和位置的日历忙/闲信息**
    
    若要设置将共享日历忙/闲信息的用户，请选择以下项目之一：
    
      - **组织中的所有人**
    
      - **指定安全组**
        
        若要指定安全组，请单击“浏览”。

6.  单击“保存”创建组织关系。

## 使用命令行管理程序创建组织关系

本示例在满足下列条件的情况下创建与 Contoso, Ltd 的组织关系：

  - 为 contoso.com、northamerica.contoso.com 和 europe.contoso.com 启用了组织关系。

  - 忙/闲访问已启用。

  - 请求的组织接收来自目标组织的忙/闲时间、主题和位置信息。

<!-- end list -->

    New-OrganizationRelationship -Name "Contoso" -DomainNames "contoso.com","northamerica.contoso.com","europe.contoso.com" -FreeBusyAccessEnabled $true -FreeBusyAccessLevel LimitedDetails

本示例将尝试使用 **Get-FederationInformation** cmdlet 中提供的域名自动发现外部 Exchange 组织 Contoso.com 的配置信息。如果使用此方法创建组织关系，则必须首先确保已使用 **Set-FederatedOrganizationIdentifier** cmdlet 创建了组织标识符。

    Get-FederationInformation -DomainName Contoso.com | New-OrganizationRelationship -Name "Contoso" -FreeBusyAccessEnabled $true -FreeBusyAccessLevel -LimitedDetails

有关语法和参数的详细信息，请参阅 [Get-FederationInformation](https://technet.microsoft.com/zh-cn/library/dd351221\(v=exchg.150\)) 和 [New-OrganizationRelationship](https://technet.microsoft.com/zh-cn/library/ee332357\(v=exchg.150\))。

本示例将创建与 Fourth Coffee 的组织关系。本示例中提供了与外部 Exchange 组织的连接设置。适用下列情况：

  - 已与 Fourth Coffee 的联盟域 fourthcoffee.com 建立了组织关系。

  - Exchange Web 服务应用程序 URL 为 mail.fourthcoffee.com。

  - 自动发现 URL 为 https://mail.fourthcoffee.com/autodiscover/autodiscover.svc/wssecurity。

  - 忙/闲访问已启用。

  - 请求的组织仅收到包含时间的忙/闲信息。

<!-- end list -->

    New-OrganizationRelationship -Name "Fourth Coffee" -DomainNames "fourthcoffee.com" -FreeBusyAccessEnabled $true -FreeBusyAccessLevel -AvailabilityOnly -TargetAutodiscoverEpr "https://mail.fourthcoffee.com/autodiscover/autodiscover.svc/wssecurity" -TargetApplicationUri "mail.fourthcoffee.com"

有关语法和参数的详细信息，请参阅 [New-OrganizationRelationship](https://technet.microsoft.com/zh-cn/library/ee332357\(v=exchg.150\))。

## 您如何知道这有效？

成功完成“新建组织关系”向导将初步表明，组织关系的创建按预期正常进行。

要验证您是否已成功创建了组织关系，请运行下列命令行管理程序命令来验证组织关系的信息：

    Get-OrganizationRelationship | format-list

> [!tip]
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。

