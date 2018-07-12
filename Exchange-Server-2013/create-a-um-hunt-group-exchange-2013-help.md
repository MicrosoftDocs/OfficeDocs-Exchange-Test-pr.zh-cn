---
title: '创建 UM 智能寻线: Exchange Online Help'
TOCTitle: 创建 UM 智能寻线
ms:assetid: 43ecb1ec-5f82-4516-9010-de8f954d3758
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa997679(v=EXCHG.150)
ms:contentKeyID: 50556558
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Servers.UnifiedMessaging.CreateUMHuntGroupWizardForm.CreateUMHuntGroupWizardPage1
ms.translationtype: MT
---

# 创建 UM 智能寻线

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2013-04-16_

统一消息 (UM) 寻是专用分组交换机 (PBX) 或 IP PBX 查寻组的逻辑表示形式。连接或链接之间的 UM IP 网关和 UM 拨号计划充当 UM 查寻组。

> [!NOTE]  
> 如果创建 UM IP 网关时将 UM 拨号计划与 UM IP 网关相关联，则将同时创建 UM 智能寻线。


> [!NOTE]  
> 如果要更改 UM 智能寻线设置，则必须删除该智能寻线，然后创建另一个具有适当设置的智能寻线。


有关与 UM 智能寻线相关的其他管理任务，请参阅 [UM 查寻组过程](um-hunt-group-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：2 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 智能寻线\&quot;条目。

  - 在执行这些步骤之前，先确认已创建 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

  - 在执行这些步骤之前，请确认已创建 UM IP 网关。有关详细步骤，请参阅[创建 UM IP 网关](create-a-um-ip-gateway-exchange-2013-help.md)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 使用 EAC 创建 UM 智能寻线

1.  在 EAC 中，导航到\&quot;统一消息\&quot;\>\&quot;UM 拨号计划\&quot;。在此列表视图中，选择您要修改的 UM 拨号计划，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

2.  在\&quot;UM 拨号计划\&quot;页上的\&quot;UM 智能寻线\&quot;下，单击\&quot;新建\&quot;![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。

3.  在\&quot;新建 UM 智能寻线\&quot;页上，输入以下信息：
    
      - \&quot;名称\&quot;   使用此文本框可创建 UM 智能寻线的显示名。UM 智能寻线名是必需的，并且必须是唯一的，但是该名称在 EAC 和命令行管理程序中仅用于显示目的。如果在创建智能寻线后必须更改其显示名，则必须首先删除现有的智能寻线，然后创建另一个具有适当名称的智能寻线。
        
        如果您的组织使用多个智能寻线，那么，建议对您的智能寻线使用有意义的名称。UM 智能寻线名的最大长度为 64 个字符，可以包括空格。但是，不能包括下列任何字符：" / \\ \[ \] : ; | = , + \* ? \< \>.
    
      - **UM IP 网关**  使用此框可以指定要使用的 UM IP 网关。单击**浏览**以选择 UM IP 网关，然后再单击**确定**。
    
      - **引导标识**   使用此框可指定一个字符串，该字符串唯一标识在 PBX 或 IP PBX 上配置的引导标识符。
        
        在此框中可以使用分机号码或会话初始协议 (SIP) 统一资源标识符 (URI)。此框可接受字母数字字符。对于旧版 PBX，数字值将用作引导标识符。但是，某些 IP PBX 可以使用 SIP URI。

4.  
    
    单击\&quot;保存\&quot;。

## 使用命令行管理程序创建 UM 智能寻线

本示例创建一个名为 `MyUMHuntGroup` 并且引导标识为 12345 的 UM 智能寻线。

    New-UMHuntGroup -Name MyUMHuntGroup -PilotIdentifier 12345 -UMDialplan MyUMDialPlan -UMIPGateway MyUMIPGateway

本示例创建一个名为 `MyUMHuntGroup` 并有多个引导标识的 UM 智能寻线。

    New-UMHuntGroup -Name MyUMHuntGroup -PilotIdentifier 5551234,55555 -UMDialplan MyUMDialPlan -UMIPGateway MyUMIPGateway

