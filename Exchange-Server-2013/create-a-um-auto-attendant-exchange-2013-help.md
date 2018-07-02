---
title: '创建 UM 自动助理: Exchange Online Help'
TOCTitle: 创建 UM 自动助理
ms:assetid: 773f53fb-d80f-4a79-8bd3-bd753942489f
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa998875(v=EXCHG.150)
ms:contentKeyID: 50490946
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.OrganizationConfiguration.UnifiedMessaging.CreateAutoAttendantWizardForm.CreateAutoAttendantWizardPage
ms.translationtype: MT
---

# 创建 UM 自动助理

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2013-03-08_

创建统一邮件 (UM) 自动助理后，由自动助理回答到人工接线员通常会回答外部电话号码的来电。与不同与其他统一消息组件中，如 UM 拨号计划和 UM IP 网关，您无需创建 UM 自动助理。但是，自动助理帮助内部和外部调用方查找用户或组织中存在并传输调用它们的部门。

有关与 UM 自动助理相关的更多管理任务，请参阅 [UM 自动助理过程](um-auto-attendant-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：3 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 自动助理\&quot;条目。

  - 在执行这些步骤之前，先确认已创建 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.</td>
</tr>
</tbody>
</table>


## 您想执行什么操作？

## EAC 用于创建 UM 自动助理

1.  
    
    在 EAC 中，导航至\&quot;统一消息\&quot;\>\&quot;UM 拨号计划\&quot;，选择要对其添加自动助理的 UM 拨号计划，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

2.  在**UM 拨号计划**上下**UM 自动助理**，, 单击**新建**![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。

3.  在**新建 UM 自动助理**页中，输入以下信息 ︰
    
      - **名称**   使用此框可以创建 UM 自动助理的显示名。UM 自动助理名称是必需的，并且必须是唯一的。但是，此名称在 EAC 和命令行管理程序中仅用于显示目的。
        
        如果在已创建自动助理之后必须更改它的显示名，则必须首先删除现有 UM 自动助理，然后创建另一个有合适名称的自动助理。如果您的组织使用多个 UM 自动助理，则建议您的 UM 自动助理使用有意义的名称。UM 自动助理名称的最大长度是 64 个字符，并且可以包括空格。
        
        虽然您可以命名新的 UM 自动助理，包含空格，如果与办公室通讯服务器 2007 R2 或 Microsoft Lync Server 集成统一消息，自动助理的名称不能包含空格。因此，如果在显示名称中，空格创建自动助理，您正在集成与办公室通讯服务器 2007 R2 或 Lync 服务器，必须首先删除该自动助理，然后创建另一个在显示名称中并不包含空格的自动助理。
    
      - **该自动助理创建为已启用**  选中此复选框以启用自动助理应答传入呼叫完成新建 UM 自动助理向导时。默认情况下，新建自动助理创建为已禁用。
        
        如果您决定创建 UM 自动助理为禁用，可用于 EAC 或外壳程序在完成该向导后启用自动助理。
    
      - \&quot;设置此自动助理以响应语音命令\&quot;   选择该复选框来对 UM 自动助理启用语音。通过对自动助理启用语音，呼叫者可以通过使用按键或语音输入来响应 UM 自动助理所使用的系统或自定义提示。默认情况下，自动助理在创建时不会启用语音。
        
        调用程序使用启用语音的自动助理，必须安装适当的 UM 语言包包含自动语音识别 (ASR) 支持并配置要使用这种语言的自动助理的属性。
    
      - **访问号码**  使用此框可以输入分机号码或呼叫者将用于到达自动助理的电话号码。在框中，键入电话号码的分机号码，然后单击**添加**![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")将数字添加到列表。您提供的电话号码的分机号码中位数不必匹配对关联的 UM 拨号计划配置分机号码的位数。这是因为直接调用不允许与 UM 自动助理。
        
        分机号码或电话号码输入的数量是没有限制的。但是，可能没有列出的分机号的情况下创建新的自动助理。分机号码或电话号码并不是必需。
        
        您可以编辑或删除现有的分机号码或电话号码。若要编辑现有的分机号码或电话号码，请单击**编辑**![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。要从列表中删除现有的分机号码或电话号码，请单击**删除**![删除图标](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "删除图标")。

4.  单击\&quot;保存\&quot;。

## 使用外壳程序创建 UM 自动助理

本示例将创建一个名为 `MyUMAutoAttendant` 的 UM 自动助理，该助理可接受传入呼叫，但不启用语音。

    New-UMAutoAttendant -Name MyUMAutoAttendant -UMDialPlan MyUMDialPlan -PilotIdentifierList 55000 -Enabled $false

本示例将创建一个名为 `MyUMAutoAttendant` 的启用语音的 UM 自动助理。

    New-UMAutoAttendant -Name MyUMAutoAttendant -UMDialPlan MyUMDialPlan -PilotIdentifierList 56000,56100 -SpeechEnabled $true

