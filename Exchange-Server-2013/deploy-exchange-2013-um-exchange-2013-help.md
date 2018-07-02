﻿---
title: '部署 Exchange 2013 UM: Exchange 2013 Help'
TOCTitle: 部署 Exchange 2013 UM
ms:assetid: d147d4b1-32d7-476b-b76f-ee3c0b35ba49
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ673564(v=EXCHG.150)
ms:contentKeyID: 50491599
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 部署 Exchange 2013 UM

 

_**适用于：**Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：**2016-12-09_

统一消息 (UM) 要求将 Exchange Server 部署与组织的现有电话系统集成起来。要成功进行部署，您需要仔细分析现有电话服务基础结构，并执行正确的计划步骤来部署和管理统一消息中的语音邮件。

**目录**

部署之前

部署统一消息

部署统一消息之后的任务

## 部署之前

在部署统一消息之前，我们建议熟悉以下主题中的概念：

  - [UM 拨号计划](um-dial-plans-exchange-2013-help.md)

  - [UM IP 网关](um-ip-gateways-exchange-2013-help.md)

  - [UM 服务](um-services-exchange-2013-help.md)

  - [UM 智能寻线](um-hunt-groups-exchange-2013-help.md)

  - [自动回答和路由传入呼叫](automatically-answer-and-route-incoming-calls-exchange-2013-help.md)

  - [UM 邮箱策略](um-mailbox-policies-exchange-2013-help.md)

  - [用户的语音邮件](voice-mail-for-users-exchange-2013-help.md)

## 部署统一消息

无论您使用 IP 专用交换机 (IP PBX)、VoIP 网关还是 Microsoft Lync Server 部署 UM，统一消息的所有部署选项都有数个共同步骤。需要这些步骤才能创建可扩展和高度可用的系统来支持大量的统一消息用户。这些步骤如下：

1.  为统一消息部署并配置电话组件。

2.  检查是否已正确安装了运行 Microsoft Exchange 统一消息呼叫路由器服务的客户端访问服务器以及运行 Microsoft Exchange 统一消息服务的邮箱服务器。

3.  创建和配置所需的统一消息组件。

4.  执行统一消息的所有张贴内容部署任务。

## 部署和配置电话组件

为了成功地在 Exchange 组织中部署统一消息，Exchange 管理员需要详细了解数据网络的概念以及电话术语和概念，并能够正确配置 UM 所需的电话组件。执行新部署或升级旧语音邮件系统需要大量有关电话网络和统一消息的知识。

通常，要成功配置 UM 所需的电话组件，需要完成三个任务。

1.  **设置 PBX 线：**部署具有可扩展性的 UM 解决方案的第一步是设置 PBX 线。

2.  **组织通道：**设置了基于 PBX 的语音通道后，可将通道组织为智能寻线。

3.  **部署 VoIP 网关：**将语音通道组织为智能寻线后，需要在 VoIP 网关结束这些通道。VoIP 网关与旧版 PBX 协作使用，可将电话网络上的电路交换协议转换为基于 IP 的分组交换协议。

在部署统一消息期间集成组织的电话网络和数据网络时，需要正确地配置电话和数据网络组件。还需要配置以下组件或接口，才能成功部署统一消息：

  - **配置组织中与 VoIP 网关进行通信的 PBX 的连接。**有关详细信息，请参阅[连接 VoIP 网关以便与 PBX 通信](connect-a-voip-gateway-to-communicate-with-a-pbx-exchange-2013-help.md)。

  - **配置从 VoIP 网关接口到 PBX 的连接。**有关如何将 PBX 接口配置为与支持的 VoIP 网关进行通信的详细信息，请参阅 PBX 特定的产品文档或参阅[连接 VoIP 网关以便与 PBX 通信](connect-a-voip-gateway-to-communicate-with-a-pbx-exchange-2013-help.md)。

  - **配置从 VoIP 网关接口到客户端访问和邮箱服务器的连接。**有关详细信息，请参阅[将 VoIP 网关、IP PBX 或会话边界控制器与 UM 连接](connect-a-voip-gateway-ip-pbx-or-session-border-controller-to-um-exchange-2013-help.md)。

  - **配置从客户端访问和邮箱服务器到 VoIP 网关接口的连接。**有关详细信息，请参阅[将 UM 连接到支持 VoIP 网关](connect-um-to-a-supported-voip-gateway-exchange-2013-help.md)。

部署之前

## 安装邮箱和客户端访问服务器

计划部署 Exchange 统一消息的组织可以使用不同的部署方式。尽管这些方式都可以实现同样的结果 — 成功地部署统一消息 — 但是每种方式略有不同，因为每个客户的需求和起点不同。不过，所有受支持的部署方案通常都存在一些共同的起点和方式，包括全新安装和升级。遵照这些步骤来部署您的客户端访问和邮箱服务器：

1.  请验证您现有的基础结构是否满足某些先决条件。有关详细信息，请参阅 [Exchange 2013 先决条件](exchange-2013-prerequisites-exchange-2013-help.md)。

2.  部署新的 Exchange 2013 组织。有关详细信息，请参阅[使用安装向导安装 Exchange 2013](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md)。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ898581.warning(EXCHG.150).gif" title="警告" alt="警告" />警告：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>在配置 VoIP 网关或 IP PBX 以将 UM SIP 和 RTP 通信发送到 Exchange 2013 客户端访问服务器之前，您应在组织内部署至少一个 Exchange 2013 邮箱服务器。</td>
    </tr>
    </tbody>
    </table>


3.  验证是否已正确安装客户端访问和邮箱服务器。建议在安装服务器之后验证安装并检查服务器安装日志。有关详细信息，请参阅[验证 Exchange 2013 安装](verify-an-exchange-2013-installation-exchange-2013-help.md)。

## 添加所需的 UM 语言包

UM 语言包允许呼叫者和 Outlook Voice Access 用户能够用多种语言与语音邮件系统交互。在邮箱服务器上新安装一个语言包后，呼叫者和 Outlook Voice Access 用户可以使用该语言收听电子邮件以及与语音邮件系统交互。

首次安装 Exchange 时，美国英语将是默认语言，并且是拨号计划的唯一可用语言选项。在邮箱服务器上安装 UM 语言包后，当您配置拨号计划的默认语言时，与该语言包关联的语言将被列为可用选项。默认情况下，由于 UM 自动助理在创建时就与 UM 拨号计划关联，因此 UM 自动助理使用关联的 UM 拨号计划的默认语言设置。但是，创建 UM 自动助理后，可以更改此设置。

从 [Exchange Server 2013 UM 语言包](https://go.microsoft.com/fwlink/p/?linkid=266542)下载 UM 语言包后，可以使用 Setup.exe 命令或运行 *\<UMLanguagePack\>*.exe 安装程序来添加 UM 语言包。然而，您必须使用 Setup.exe 命令以删除 UM 语言包。不存在可用于在邮箱服务器中添加或删除语言的 Exchange 命令行管理程序 cmdlet。有关如何安装 UM 语言包的详细信息，请参阅[安装 UM 语言包](install-a-um-language-pack-exchange-2013-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>默认情况下，当您安装邮箱服务器时，会安装语言“美国英语”(en-US)。它无法删除，除非您从计算机中删除邮箱服务器。</td>
</tr>
</tbody>
</table>


部署之前

## 创建和配置 UM 组件

在部署和操作统一消息时，需要几个 UM 组件。统一消息组件连接到统一消息环境中的电话基础结构。成功安装客户端访问和邮箱服务器后，执行以下步骤。

## 步骤 1：创建和配置 UM 拨号计划

UM 拨号计划是运行统一消息以及在网络上成功部署统一消息必不可少的。在成功安装客户端访问和邮箱服务器之后，UM 拨号计划将是您要创建的第一个组件。

默认情况下，UM 拨号计划和与该拨号计划关联的客户端访问和邮箱服务器在发送和接收数据时不使用加密。在不安全模式下，将不加密 VoIP 和 SIP 通信。创建拨号计划时，或者在已经创建拨号计划之后，可以通过使用相互传输层安全性（相互 TLS）配置拨号计划来加密 VoIP 和 SIP 通信。如果使用相互的 TLS，要将拨号计划设置为 SIP 安全或安全，将 UM 启动模式设置为 TLS 或双协议模式，并创建和分发为 Exchange 服务器和 VoIP 网关、IP PBX 或会话边界控制器 (SBC) 的受信任证书。在配置 VoIP 安全设置之后，必须为客户端访问和邮箱服务器配置启动模式。有关详细信息，请参阅[在邮箱服务器上配置的启动模式](configure-the-startup-mode-on-a-mailbox-server-exchange-2013-help.md)或[在客户端访问服务器上配置的启动模式](configure-the-startup-mode-on-a-client-access-server-exchange-2013-help.md)。

执行以下过程，创建一个新的 UM 拨号计划。

## 创建 UM 拨号计划

1.  在 Exchange 管理中心 (EAC) 中，导航至“统一消息”\>“UM 拨号计划”，然后单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。

2.  在“新建 UM 拨号计划”页上，填写下列框：
    
      - **名称**：键入拨号计划的名称。UM 拨号计划名称是必需的，并且必须是唯一的。键入的此名称在 EAC 和命令行管理程序中仅用于显示目的。UM 拨号计划名称的最大长度为 64 个字符，可以包括空格。但是，不能包括下列任何字符：" / \\ \[ \] : ; | = , + \* ? \< \>.
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>尽管拨号计划名称的框可以接受 64 个字符，但是拨号计划的名称不得超过 49 个字符。这是因为创建拨号计划时，还创建了其名称为 <em>&lt;DialPlanName&gt;</em> 默认策略的默认 UM 邮箱策略。UM 拨号计划和 UM 邮箱策略的 <em>name</em> 参数都可以是 64 个字符长。</td>
        </tr>
        </tbody>
        </table>
    
      - **分机号码长度(位)**   输入拨号计划中分机号码的位数。分机号码位数基于在 PBX 上创建的电话拨号计划。例如，如果与电话拨号计划关联的用户拨打 4 位的分机号码来呼叫同一电话拨号计划中的另一个用户，则应选择 4 作为分机号码中的位数。
        
        这是一个必填框，该字段的值范围为 1 到 20。典型的分机号码长度为 3 到 7 位。如果现有电话环境包含分机号码，则必须指定一个与这些分机号码的位数相匹配的位数。
        
        在创建电话分机拨号计划时，将需要在用户链接至电话分机拨号计划时输入用户的分机号码。当启用了 UM 的用户与 SIP URI 或 E.164 拨号计划关联时，对于会话初始协议 (SIP) 拨号计划或 E.164 拨号计划，也需要分机号码。当 Outlook Voice Access 用户访问其 Exchange 邮箱时使用此分机号码。
    
      - UNRESOLVED\_TOKENBLOCK\_VAL(UI\_URI 类型)
    
      - UNRESOLVED\_TOKENBLOCK\_VAL(UI\_VoIP 安全)
    
      - “国家/地区代码”：使用此框可以键入用于拨出电话的国家/地区代码数字。将在所拨打的电话号码前面加拨此号码。此框可接受 1 到 4 位数。例如，美国的国家/地区代码为 1，英国的为 44。

3.  单击“保存”。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>在以前的 Exchange 版本中，必须将统一消息服务器添加至 UM 拨号计划。在 Exchange 2013 中，客户端访问和邮箱服务器不能与电话分机或 E.164 拨号计划关联。客户端访问服务器和邮箱服务器将应答所有类型拨号计划的所有传入呼叫。但是，如果您将 UM 与 Microsoft Lync Server 集成，则必须将所有客户端访问和邮箱服务器添加至所有 SIP URI 拨号计划以使呼叫路由正常对 Lync Server 发挥作用。</td>
    </tr>
    </tbody>
    </table>


部署之前

## 步骤 2：创建和配置 UM IP 网关

UM IP 网关表示 VoIP 网关硬件设备或 IP PBX。结合使用 UM IP 网关与 UM 智能寻线功能，可以在 VoIP 网关、IP PBX 与 UM 拨号计划之间建立链接。

如果已经创建或启用拨号计划上的 VoIP 安全，通过使用以下过程之一创建的 UM IP 网关将与使用 VoIP 安全的 UM 拨号计划关联。在该情况中，必须使用完全限定域名 (FQDN)，才能创建 UM IP 网关，和不 IP 地址。还必须配置 UM IP 网关，才能在 TCP 端口 5061 上侦听。若要要在 TCP 端口 5061 上侦听配置 UM IP 网关，请运行以下命令：`Set-UMIPGateway -identity MyUMIPGateway -Port 5061`。还必须确保任何 VoIP 网关或 IP PBX 也已经过配置能在端口 5061 上侦听相互的 TLS。

执行以下过程，创建一个新的 UM IP 网关。

## 创建 UM IP 网关

1.  
    
    在 EAC 中，导航至“统一消息”\>“UM IP 网关”，然后单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。

2.  在“新建 UM IP 网关”页上，输入以下信息：
    
      - **名称**   使用此框指定 UM IP 网关的唯一名称。此名称是 EAC 中出现的显示名。如果在创建 UM IP 网关之后必须更改其显示名，则必须先删除现有的 UM IP 网关，然后再创建一个具有相应名称的 UM IP 网关。必须提供 UM IP 网关名，但是该名称仅用于显示。因为组织可能会使用多个 UM IP 网关，所以，建议您为该 UM IP 网关使用有意义的名称。UM IP 网关名称的最大长度为 64 个字符，并且可以包含空格。但是，不能包括下列任何字符：" / \\ \[ \] : ; | = , + \* ? \< \>.
    
      - “地址”   您可配置具有 IP 地址和完全限定域名 (FQDN) 的 UM IP 网关。使用该框指定在 VoIP 网关、启用了 SIP 的 PBX、IP PBX 或 SBC 或 FQDN 上配置的 IP 地址。此框只接受有效并且格式正确的 FQDN。
        
        您可以在此框中输入字母和数字字符。支持 IPv4 地址、IPv6 地址和 FQDN。若要在 UM IP 网关与在 SIP 安全或安全模式下运行的拨号计划之间使用相互传输层安全性（相互 TLS），则必须使用 FQDN 配置 UM IP 网关。还必须将其配置为在端口 5061 上侦听，并确保所有 VoIP 网关或 IP PBX 都已配置为在端口 5061 上侦听相互 TLS 请求。若要配置 UM IP 网关，请运行以下命令：`Set-UMIPGateway -identity MyUMIPGateway -Port 5061`.
        
        如果使用 FQDN，必须还要确保已为该 VoIP 网关正确地配置了 DNS 主机记录，以便可以正确地将主机名解析为 IP 地址。如果使用 FQDN 而不是 IP 地址，并更改了 UM IP 网关的 DNS 配置，则必须先禁用 UM IP 网关然后再启用它，以确保 UM IP 网关的配置信息已正确更新
    
      - “UM 拨号计划”   单击“浏览”选择要与 UM IP 网关关联的 UM 拨号计划。选择要与 UM IP 网关关联的 UM 拨号计划时，还会创建默认 UM 智能寻线并将其与所选的 UM 拨号计划关联。如果未选择 UM 拨号计划，则必须手动创建 UM 智能寻线并将该 UM 智能寻线与所创建的 UM IP 网关关联。

3.  
    
    单击“保存”。

## 步骤 3：创建和配置 UM 智能寻线

“智能寻线”一词用于描述由用户共享的一组 PBX 或者 IP PBX 资源或分机号码。使用智能寻线可以有效地将呼叫转接进或转接出给定的业务单位。

如果已经创建 UM IP 网关，并将 UM IP 网关与 UM 拨号计划相关联，则会创建默认的 UM 智能寻线。可以与相同或不同 UM IP 网关关联另一个 UM 智能寻线，取决于已经创建的 UM IP 网关的数字。

创建统一消息智能寻线之后，需要使 UM 拨号计划中指定的所有邮箱服务器均可以与 VoIP 网关进行通信。有关详细信息，请参阅 [UM 智能寻线](um-hunt-groups-exchange-2013-help.md)。

## 创建 UM 智能寻线

1.  在 EAC 中，导航到“统一消息”\>“UM 拨号计划”。在此列表视图中，选择您要更改的 UM 拨号计划，然后单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

2.  在“UM 拨号计划”页上的“UM 智能寻线”下，单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。

3.  在“新建 UM 智能寻线”页上，填写下列框：
    
      - “关联的 UM IP 网关”   此仅显示框显示将要与 UM 智能寻线关联的 UM IP 网关的名称。
    
      - “名称”   使用此文本框可创建 UM 智能寻线的显示名。UM 智能寻线名是必需的，并且必须是唯一的，但是该名称在 EAC 和命令行管理程序中仅用于显示目的。如果在创建智能寻线后必须更改其显示名，则必须首先删除现有的智能寻线，然后创建另一个具有适当名称的智能寻线。
        
        如果您的组织使用多个智能寻线，那么，建议对您的智能寻线使用有意义的名称。UM 智能寻线名的最大长度为 64 个字符，可以包括空格。但是，不能包括下列任何字符：" / \\ \[ \] : ; | = , + \* ? \< \>.
    
      - “拨号计划”   单击“浏览”可选择将要与 UM 智能寻线相关联的拨号计划。必须将智能寻线与拨号计划相关联。UM 智能寻线只能与一个 UM IP 网关和一个 UM 拨号计划相关联。
    
      - “引导标识”   使用此文本框可指定一个字符串，该字符串唯一标识在 PBX 或 IP PBX 上配置的引导标识符或引导 ID。
        
        在此框中可以使用分机号码或会话初始协议 (SIP) 统一资源标识符 (URI)。此框可接受字母数字字符。对于旧版 PBX，数字值将用作引导标识符。但是，某些 IP PBX 可以使用 SIP URI。

4.  单击“保存”。

部署之前

## 步骤 4：创建和配置 UM 邮箱策略

为用户启用统一消息时，需要使用 UM 邮箱策略。每个启用 UM 的用户的邮箱必须链接到一个 UM 邮箱策略。创建 UM 邮箱策略之后，要将一个或多个启用 UM 的邮箱链接到该 UM 邮箱策略。这样可以控制 PIN 安全设置，例如 PIN 中的最小位数或与 UM 邮箱策略关联的启用 UM 用户的最大登录尝试次数。

每次创建 UM 拨号计划时，都会创建一个 UM 邮箱策略。该 UM 邮箱策略名为 \<*DialPlanName*\> 默认策略。但是，如果必须创建新 UM 邮箱策略，则执行以下过程。

## 创建 UM 邮箱策略

1.  
    
    在 EAC 中，导航到“统一消息”\>“UM 拨号计划”。在此列表视图中，选择您要修改的 UM 拨号计划，然后单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

2.  在“UM 拨号计划”页上的“UM 邮箱策略”下，单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。

3.  在“新建 UM 邮箱策略”页面上，在“名称”文本框中，输入新的 UM 邮箱策略的名称。
    
    使用此框可为 UM 邮箱策略指定唯一名称。此名称是 EAC 中出现的显示名。如果在创建 UM 邮箱策略后必须要更改其显示名，则必须首先删除现有的 UM 邮箱策略，然后创建具有相应名称的其他 UM 邮箱策略。如果有任何启用了 UM 的用户与 UM 邮箱策略关联，则不能删除该策略。
    
    UM 邮箱策略名称是必需的，但其仅用于显示目的。由于您的组织可能使用多个 UM 邮箱策略，因此建议您使用对 UM 邮箱策略有意义的名称。UM 邮箱策略名称的最大长度为 64 个字符，可以包括空格。但是，不能包括下列任何字符：" / \\ \[ \] : ; | = , + \* ? \< \>.

4.  单击“保存”来保存新的 UM 邮箱策略。在保存 UM 邮箱策略时，会启用所有默认设置，包括 PIN 策略、语音邮件功能以及“受保护的语音邮件”设置。如果想自定义或更改任何默认设置，可使用 **Set-UMMailbox** cmdlet 来更改刚创建的 UM 邮箱策略的设置。

## 步骤 5：创建和配置 UM 自动助理（可选）

通过 统一消息可以根据组织的需要创建一个或多个 UM 自动助理。创建 UM 自动助理时，需要为组织创建语音菜单系统。来自组织内部或外部的呼叫者然后可以滚动菜单系统，以找到并呼叫组织中的公司用户或部门，或将呼叫转接给他们。

呼叫者可以使用双音调多频率 (DTMF) 输入（也称为按键或语音输入）浏览菜单系统。自动语音识别 (ASR) 只有正常运行，用户才可以使用语音输入，因此必须启用语音 UM 自动助理。

在统一消息中，创建和使用自动助理是可选的。但是，如果希望创建新的 UM 自动助理，请执行下列过程。

## 创建 UM 自动助理

1.  
    
    在 EAC 中，导航至“统一消息”\>“UM 拨号计划”，选择要对其添加自动助理的 UM 拨号计划，然后单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

2.  在“UM 拨号计划”页上，在“UM 自动助理”下，单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。

3.  在“新建 UM 自动助理”页上，填写以下框：
    
      - **名称**   使用此框可以创建 UM 自动助理的显示名。UM 自动助理名称是必需的，并且必须是唯一的。但是，此名称在 EAC 和命令行管理程序中仅用于显示目的。
        
        如果在已创建自动助理之后必须更改它的显示名，则必须首先删除现有 UM 自动助理，然后创建另一个有合适名称的自动助理。如果您的组织使用多个 UM 自动助理，则建议您的 UM 自动助理使用有意义的名称。UM 自动助理名称的最大长度是 64 个字符，并且可以包括空格。
        
        虽然您可以命名一个新的 UM 自动助理以包含空格，但是，如果将统一消息与 Office Communications Server 2007 R2 或 Microsoft Lync Server 集成，则自动助理的名称不能包含空格。因此，如果您创建的自动助理的显示名称中包含空格，但要与 Office Communications Server 2007 R2 或 Lync Server 集成，则必须先删除该自动助理，然后另外创建一个显示名称中不包含空格的自动助理。
    
      - **将此自动助理创建为已启用**   完成创建 UM 自动助理后，选择此复选框可使自动助理能够应答传入呼叫。默认情况下，新建的自动助理为禁用状态。
        
        如果决定创建被禁用的 UM 自动助理，可以在完成自动助理创建之后使用 EAC 或命令行管理程序启用自动助理。
    
      - “设置此自动助理以响应语音命令”   选择该复选框来对 UM 自动助理启用语音。通过对自动助理启用语音，呼叫者可以通过使用按键或语音输入来响应 UM 自动助理所使用的系统或自定义提示。默认情况下，自动助理在创建时不会启用语音。
        
        为了让呼叫者使用语言为美国英语 (en-US) 以外的启用语音的自动助理，必须安装合适的 UM 语言包，并将自动助理的属性配置为使用此语言。默认情况下，当您安装邮箱服务器时，会安装 en-US UM 语言包。
    
      - “访问号码”   使用此框可以输入呼叫者将用于联系自动助理的分机或电话号码。请在该框中键入分机号码，然后单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")，将分机号码添加到列表中。您提供的分机号码的位数或电话号码无需与在关联的 UM 拨号计划中配置的分机号码的位数匹配。这是因为允许直接呼叫 UM 自动助理。
        
        输入的分机号码或引导号码的数目不受限制。但是，可以新建自动助理，而不列出分机号码或电话号码。分机号码或电话号码并非必需。
        
        可以编辑或删除现有分机号码或引导号码。若要编辑现有分机号码或电话号码，请单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。若要从列表中删除现有分机号码或电话号码，请单击“删除”![删除图标](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "删除图标")。

4.  单击“保存”。

部署之前

## 部署统一消息之后的任务

完成新客户端访问和邮箱服务器的安装并成功部署统一消息之后，应当完成部署后任务。部署后任务将帮助您为用户启用统一消息，保护您的 UM 部署以及为启用 UM 的用户部署传入传真。

## 为用户启用语音邮件

在部署了 VoIP 网关或 IP PBX，安装了客户端访问和邮箱服务器并创建了统一消息所需的组件后，需要为用户启用统一消息。有关详细信息，请参阅[为用户启用语音邮件](enable-a-user-for-voice-mail-exchange-2013-help.md)。

## 保护语音邮件

统一消息 (UM) 可配置为使用 Active Directory 权限管理服务 (AD RMS) 来保护组织的语音邮件。此功能称为“受保护的语音邮件”。当语音邮件受保护时，不但会阻止收件人转发此邮件，而且 UM 也会确保只有邮件的预期收件人可以访问其内容。使用 Microsoft Outlook 2010 或更高版本、Outlook Web App 或 Outlook Voice Access 可以访问受保护的语音邮件。有关详细信息，请参阅[保护语音邮件](protect-voice-mail-exchange-2013-help.md)。

## 用于 UM 的相互 TLS

若要使用相互 TLS 加密由客户端访问和邮箱服务器发送和接收的 SIP 和实时传输协议 (RTP) 通信，请执行以下任务：

  - 运行 Exchange 证书向导。有关详细信息，请参阅[为 UM 部署证书](deploying-certificates-for-um-exchange-2013-help.md)。

  - 在客户端访问和邮箱服务器上导入证书。

  - 在组织中的 VoIP 网关和 IP PBX 以及客户端访问和邮箱服务器上导入所需证书。

  - 在 UM 拨号计划中配置 VoIP 安全性。有关详细信息，请参阅[配置 VoIP 安全设置](configure-the-voip-security-setting-exchange-2013-help.md)。

  - 配置客户端访问和邮箱服务器上的启动模式。有关详细信息，请参阅[在邮箱服务器上配置的启动模式](configure-the-startup-mode-on-a-mailbox-server-exchange-2013-help.md)和[在客户端访问服务器上配置的启动模式](configure-the-startup-mode-on-a-client-access-server-exchange-2013-help.md)。

  - 配置 UM IP 网关以侦听端口 5061。有关详细信息，请参阅[配置侦听端口](configure-the-listening-port-exchange-2013-help.md)。

## 为启用了 UM 的用户设置 PIN 策略

在统一消息中，可以在 UM 邮箱策略中定义和配置 PIN 策略。为用户启用统一消息时，使该用户与现有 UM 邮箱策略相关联。在 UM 邮箱策略上配置的 UM PIN 策略应当基于组织的安全要求。有关如何为启用了 UM 的用户配置 PIN 设置的详细信息，请参阅[设置 Outlook Voice Access 针的安全性](set-outlook-voice-access-pin-security-exchange-2013-help.md)。

## 设置客户端语音邮件功能

在部署完服务器和所需 UM 组件后，还可以配置几项与语音邮件相关的可选功能。有关详细信息，请参阅下列内容：

  - [设置 Outlook Voice Access](setting-up-outlook-voice-access-exchange-2013-help.md)

  - [允许语音邮件用户转接来电](allow-voice-mail-users-to-forward-calls-exchange-2013-help.md)

  - [允许用户查看语音邮件成绩单](allow-users-to-see-a-voice-mail-transcript-exchange-2013-help.md)

  - [为语音邮件用户启用接收传真功能](enable-voice-mail-users-to-receive-faxes-exchange-2013-help.md)

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果要将统一消息环境与 Microsoft Lync Server 集成，则应考虑其他规划因素。有关详细信息，请参阅<a href="deploying-exchange-2013-um-and-lync-server-overview-exchange-2013-help.md">部署 Exchange 2013 UM 和 Lync Server 概述</a>。</td>
</tr>
</tbody>
</table>


部署之前

