---
title: '部署 Exchange 2013 多林拓扑: Exchange 2013 Help'
TOCTitle: 部署 Exchange 2013 多林拓扑
ms:assetid: d51f2b7d-9045-40cf-8b9f-43787a6fff6d
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb124734(v=EXCHG.150)
ms:contentKeyID: 51408278
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 部署 Exchange 2013 多林拓扑

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2016-12-09_

本主题提供在多林拓扑中部署 Microsoft Exchange Server 2013 的概述。您将可以找到有关下列主题的信息：

  - **支持的多林拓扑**   Exchange 2013 支持两种类型的多林拓扑：跨林和资源林。

  - **GAL 同步**   如果有跨林环境，您需要确保任何给定林中的 GAL 包含来自其他林的邮件收件人。

  - **跨林移动邮箱**   Exchange 命令行管理程序中的 **New-MoveRequest** 和 **New-MigrationBatch** cmdlet 可用于将邮箱从一个林移动到另一个林。

  - **了解多林管理**   了解在林间配置和管理权限的权限模型。

## 支持的多林拓扑

Exchange 2013 支持以下类型的多林拓扑：

  - **跨林**   跨林拓扑是一个具有多个 Exchange 林的拓扑。以下是在多林拓扑中部署 Exchange 2013 所需操作的概述：
    
    1.  您必须首先在每个林中安装 Exchange 2013。有关详细信息，请参阅[部署 Exchange 2013 的新安装](deploy-a-new-installation-of-exchange-2013-exchange-2013-help.md)。
    
    2.  下一步，必须同步各个林中的收件人，以便在每个林中的全局地址列表 (GAL) 包含所有同步林中的用户。有关详细信息，请参阅下面的“GAL 同步”部分。
    
    3.  最后，必须配置可用性服务，以便一个林中的用户可以查看另一个林中用户的可用性数据。有关详细信息，请参阅[配置跨林拓扑的可用性服务](configure-the-availability-service-for-cross-forest-topologies-exchange-2013-help.md)。
    
    有关在跨林拓扑中部署 Exchange 2013 的详细信息，请参阅[在跨林拓扑中部署 Exchange 2013](deploy-exchange-2013-in-a-cross-forest-topology-exchange-2013-help.md)。

  - **资源林**   资源林拓扑具有一个 Exchange 林和一个或多个用户帐户林。以下是在资源林拓扑中部署 Exchange 2013 所需操作的概述：
    
    1.  您必须具有安装了 Exchange 的林。在 Exchange 林中，必须已禁用拥有 Exchange 邮箱的用户帐户。
    
    2.  您必须具有至少一个包含用户帐户的林。此林*不*应安装 Exchange。
    
    3.  然后，您必须将 Exchange 林中禁用的用户帐户与帐户林中的用户帐户相关联。
    
    有关在资源林拓扑中部署 Exchange 2013 的详细信息，请参阅[在 Exchange 资源林拓扑中部署 Exchange 2013](deploy-exchange-2013-in-an-exchange-resource-forest-topology-exchange-2013-help.md)。

## GAL 同步

默认情况下，GAL 包含来自单个林的邮件收件人。如果你有跨林环境，我们建议使用 Microsoft Identity Lifecycle Manager (ILM) 2007 Feature Pack 1 (FP1) 以确保任何给定林中的 GAL 都包含来自其他林的邮件收件人。ILM 2007 FP1 创建表示来自其他林的收件人的邮件用户，从而允许用户在 GAL 中查看它们并发送邮件。例如，林 A 中的用户在林 B 中显示为邮件用户，林 B 中的用户在林 A 中也显示为邮件用户。然后，目标林中的用户可以选择表示另一个林中的收件人的邮件用户对象，以发送邮件。

若要启用 GAL 同步，应创建管理代理，以便将已启用邮件的用户、联系人和组从指定的 Active Directory 服务导入到中心元目录。在元目录中，已启用邮件的对象表示为邮件用户。组表示为没有任何关联的成员身份的联系人。然后，管理代理将这些邮件用户导出到指定目标林中的组织单位。

有关 Forefront Identity Manager (FIM) 的详细信息，请参阅 [Forefront Identity Manager 2010](https://go.microsoft.com/fwlink/p/?linkid=279864)。

## 跨林移动邮箱

在跨林拓扑中，可能希望从一个林向另外一个林移动邮箱。为此，必须在 Exchange 命令行管理程序中使用 **New-MoveRequest** 或 **New-MigrationBatch** cmdlet。有关跨林移动邮箱的详细信息，请参阅下列主题：

  - [为跨林移动请求准备邮箱](prepare-mailboxes-for-cross-forest-move-requests-exchange-2013-help.md)

  - [在命令行管理程序中使用 Prepare-MoveRequest.ps1 脚本准备跨林移动的邮箱](prepare-mailboxes-for-cross-forest-moves-using-the-prepare-moverequest-ps1-script-in-the-shell-exchange-2013-help.md)

  - [使用示例代码准备跨林移动的邮箱](prepare-mailboxes-for-cross-forest-moves-using-sample-code-exchange-2013-help.md)

## 了解多林管理

Exchange 2013 使用新的权限功能来管理多林环境。

Exchange 2013 使用基于角色的访问控制 (RBAC) 权限模型。管理员所属的管理角色组以及为最终用户分配的管理角色分配策略共同决定每个管理员和最终用户可以执行的操作。要了解多林权限，您需要熟悉 RBAC。有关 RBAC、角色组、尤其是角色分配策略的详细信息，请参阅[了解基于角色的访问控制](understanding-role-based-access-control-exchange-2013-help.md)。

您可以使用 RBAC 权限模型来配置并管理林之间的权限。有关多林权限的详细信息，请参阅下列主题：

  - [了解多林权限](understanding-multiple-forest-permissions-exchange-2013-help.md)

  - [管理链接的角色组](manage-linked-role-groups-exchange-2013-help.md)

  - [创建链接的角色组的镜像内置角色组](create-linked-role-groups-that-mirror-built-in-role-groups-exchange-2013-help.md)

