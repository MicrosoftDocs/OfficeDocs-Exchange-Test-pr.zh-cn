---
title: '创建 UM 拨号计划: Exchange 2013 Help'
TOCTitle: 创建 UM 拨号计划
ms:assetid: 963ff2e1-515d-439a-953a-664174e5e283
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb123819(v=EXCHG.150)
ms:contentKeyID: 50491199
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Servers.UnifiedMessaging.CreateUMDialPlanWizardForm.CreateUMDialPlanWizardPage
ms.translationtype: HT
---

# 创建 UM 拨号计划

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2013-04-16_

统一消息 (UM) 拨号计划包含与您的电话服务网络相关的配置信息。UM 拨号计划在启用语音邮件功能的用户的电话分机号码与其邮箱之间建立链接。创建 UM 拨号计划时，可配置拨号计划的分机号码位数、统一资源标识符 (URI) 类型和 IP 语音 (VoIP) 安全性设置。

每次创建 UM 拨号计划时，都会创建一个 UM 邮箱策略。该 UM 邮箱策略名为 \<*DialPlanName*\> 默认策略。

有关与 UM 拨号计划相关的其他管理任务，请参阅[UM 拨号计划过程](um-dial-plan-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：3 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的“UM 拨号计划”条目。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 使用 EAC 创建 UM 拨号计划

1.  
    
    在 EAC 中，导航至“统一消息”\>“UM 拨号计划”，然后单击“新建”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。

2.  在“新建 UM 拨号计划”页面中，填写下列框：
    
      - **名称**：键入拨号计划的名称。UM 拨号计划名称是必需的，并且必须是唯一的。但是，此名称仅用于 EAC 和命令行管理程序中的显示。如果在已创建 UM 拨号计划之后需要更改其显示名，则必须首先删除现有的 UM 拨号计划，然后创建具有适当名称的其他 UM 拨号计划。如果您的组织使用多个 UM 拨号计划，则建议您对您的 UM 拨号计划使用有意义的名称。UM 拨号计划名称的最大长度为 64 个字符，可以包括空格。但是，不能包括下列任何字符：" / \\ \[ \] : ; | = , + \* ? \< \>.
        
        虽然可以在 UM 拨号计划名称中包含空格，但是，如果将统一消息与 Office Communications Server 2007 R2 或 Microsoft Lync Server 集成，则拨号计划名称不能包含空格。因此，如果创建的拨号计划的显示名称中包含空格，但要与 Office Communications Server 2007 R2 或 Lync Server 集成，则必须先删除该拨号计划，然后另外创建一个显示名称中不包含空格的拨号计划。
        
        > [!IMPORTANT]  
        > 尽管拨号计划名称的框可以接受 64 个字符，但是拨号计划的名称不得超过 49 个字符。如果尝试创建的拨号计划名称包含的字符数超过 49 个，将出现错误消息。此消息将告知因为 UM 拨号计划名称太长，所以 UM 邮箱策略无法生成。发生这种情况的原因是：如上所述，在创建拨号计划时，还创建了一个名为 <em>&lt;DialPlanName&gt;</em> 默认策略的默认 UM 邮箱策略。如果默认策略中的 15 个字符添加到拨号计划的名称，则总字符数超出限制。UM 拨号计划和 UM 邮箱策略的 <em>name</em> 参数都可以是 64 个字符。但是，如果拨号计划的名称超过 49 字符，默认 UM 邮箱策略的名称将超过 64 字符，则这是系统所不允许的。
    
      - **分机号码长度(位)**   输入拨号计划的位数。分机号码位数基于在专用交换机 (PBX) 或 IP PBX 上创建的电话拨号计划。例如，如果与电话拨号计划关联的用户拨打 4 位的分机号码来呼叫同一电话拨号计划中的另一个用户，则应选择 4 作为分机号码中的位数。
        
        这是一个必填框，该字段的值范围为 1 到 20。典型的分机号码长度为 3 位到 7 位。如果现有的电话环境包括分机号码，则必须指定与这些分机中的号码位数相匹配的位数。
        
        当创建会话初始协议 (SIP) 或 E.164 拨号计划并将启用 UM 的用户与该拨号计划关联时，仍然必须输入该用户将使用的分机号码。当 Outlook Voice Access 用户访问其邮箱时使用此号码。
    
      - **拨号计划类型**   统一资源标识符 (URI) 是标识或命名资源的一串字符。这种标识的主要目的是允许 VoIP 设备使用特定协议通过网络与其他设备进行通信。方案中定义的 URI 用于定义呼叫的特定语法、格式和协议。简单来说，该格式将从 IP PBX 或 PBX 传递。创建 UM 拨号计划之后，将无法更改 URI 类型，除非删除该拨号计划，然后重新创建拨号计划以包含正确的 URI 类型。可以选择拨号计划的以下 URI 类型之一：
        
          - **电话分机**   这是最常用的 URI 类型。将采用以下格式之一列出 VoIP 网关或 IP 专用交换机 (PBX) 中的呼叫者和被叫方信息：电话：512345 或 512345@\<*IP address*\>。这是拨号计划默认的 URI 类型。
        
          - **SIP URI** 如果必须具有会话初始协议 (SIP) URI 拨号计划（如支持 SIP 路由的 IP PBX）或者如果集成 Microsoft Office Communications Server 2007 R2 或 Microsoft Lync Server 和统一消息，则使用此 URI 类型。来自 VoIP 网关的呼叫者和被叫方信息。IP PBX、Communications Server 2007 R2 或 Lync Server 采用以下格式作为 SIP 地址列出：sip：\<*username*\>@\<*domain* 或 *IP address*\>:端口。
        
          - **E.164** E.164 是用于公共电话系统的国际编号计划，其中每个指定的号码都包含国家/地区代码、国内目的地代码和订阅者号码。将采用以下格式列出通过 VoIP 网关或 IP PBX 发送的呼叫方和被叫方信息：电话：+14255550123。
        
        > [!WARNING]  
        > 创建 UM 拨号计划后，必须先删除拨号计划，然后重新创建包括正确 URI 类型的拨号计划，这样才能更改 URI 类型。
    
      - **VoIP 安全模式**   使用此下拉列表为 UM 拨号计划选择 VoIP 安全设置。可以为拨号计划选择以下安全设置之一：
        
          - **不安全**  默认情况下，当您创建 UM 拨号计划时，它将设置为不加密 SIP 信号或 RTP 通信。在非安全模式下，与 UM 拨号计划关联的客户端访问服务器和邮箱服务器使用非加密方式处于与 VoIP 网关、IP PBX、SBC 以及其他客户端访问服务器和邮箱服务器之间的往来数据。在非安全模式下，实时传输协议 (RTP) 媒体通道与 SIP 信号信息都不会进行加密。
        
          - **SIP 安全**   选择“SIP 安全”时，只对 SIP 信号通信进行加密，RTP 媒体通道将仍然使用不进行加密的 TCP。通过 SIP 安全，使用相互传输层安全性 (TLS) 对 SIP 信号通信和 VoIP 数据进行加密。
        
          - **安全**   选择“安全”时，对 SIP 信号通信和 RTP 媒体通道进行加密。使用安全实时传输协议 (SRTP) 的安全信号媒体通道和 SIP 信号流量同时使用 TLS 来加密 VoIP 数据。
    
      - **音频语言**   使用此列表指定 Outlook Voice Access 用户使用的默认语言。此设置不适用于 UM 自动助理上的语言设置。您可以将 Outlook Voice Access 的语言设置为与 UM 自动助理使用的语言相同或不同。用户呼叫与拨号计划链接的用户时，音频语言是录音话务员使用的默认语言。呼叫者将听到的系统提示使用相同语言播放。根据 UM 拨号计划选择的语言用于阅读电子邮件、语音邮件和日历项目；如果没有记录个人问候语，请说出用户名称；使用“语音邮件预览”功能转录语音消息；启用自动语音识别 (ASR) 以使之正常运行。
    
      - “国家/地区代码”   使用此框可以键入用于拨出电话的国家/地区代码数字。将在拨打的电话号码前面加拨此号码。此框可接受 1 到 4 位数。例如，美国的国家/地区代码为 1，英国的为 44。

3.  单击“保存”。

## 使用命令行管理程序创建 UM 拨号计划

本示例可创建名为 `MyUMDialPlan` 且使用 4 位分机号的新 UM 拨号计划。

    New-UMDialplan -Name MyUMDialPlan -NumberofDigits 4

本示例创建名为 `MyUMDialPlan`、使用 5 位分机号且支持 SIP URI 的新 UM 拨号计划。

    New-UMDialplan -Name MyUMDialPlan -UriType SIPName -NumberofDigits 5

