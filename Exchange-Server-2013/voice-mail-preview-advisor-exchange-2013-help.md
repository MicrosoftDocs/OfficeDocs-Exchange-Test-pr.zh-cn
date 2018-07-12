---
title: '语音邮件预览顾问: Exchange Online Help'
TOCTitle: 语音邮件预览顾问
ms:assetid: 0957dd54-df6d-4b50-9db5-4757f548b899
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Ee364730(v=EXCHG.150)
ms:contentKeyID: 51408193
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 语音邮件预览顾问

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2016-12-09_

Microsoft Exchange 统一消息 (UM) 包括一种名为\&quot;语言邮件预览\&quot;的功能，该功能使用自动语音识别 (ASR) 将文本版本的语音邮件音频文件添加到语音邮件。ASR 并不完全准确，尤其是在用于通过电话录制包含未知语音和噪音的音频时。某些组织要求以持续不出错（或几乎不出错）的方式转录语音邮件。语音邮件预览伙伴计划将帮助这类组织满足这些要求。

语音邮件预览使用 [Microsoft 语音技术](http://go.microsoft.com/fwlink/p/?linkid=187348)提供文本版本的音频录音。语音邮件文本在 MicrosoftOutlook Web App、Outlook 2010 或更高版本以及其他电子邮件程序的电子邮件中显示。

默认情况下，在内部部署或混合部署中为 UM 启用用户时，如果已安装支持的 UM 语言包，将会发送语音邮件预览。在 Exchange Online中为 UM 启用用户时，所有的 UM 语言包都已安装。但并非安装的所有语言都支持语音邮件预览。

有许多语音邮件预览伙伴可以为\&quot;语音邮件预览\&quot;功能提供增强型的转录支持和服务。这些合作伙伴雇用用户来更正使用自动语音识别 (ASR) 创建的语音邮件转录。各个语音邮件预览伙伴均必须符合一系列需要认证的要求，才能与 Exchange UM 进行交互操作。

如果您确定语音邮件预览发送到您的用户不能足够准确，可以联系一个经认证的语音邮件预览合作伙伴列出在[Microsoft 查明其](https://go.microsoft.com/fwlink/p/?linkid=281966)和符号组成与其花费额外的成本。

**目录**

概述

Exchange Unified Messaging Voice Mail Partner program

Voice Mail Preview partners certified for Exchange Unified Messaging

Configuring Voice Mail Preview partners

VoIP or media gateways and IP PBX support

## 概述

在统一消息录制语音邮件的音频时，使用 ASR 从音频文件创建语音邮件预览文本，然后提交整个语音邮件以传递给用户。对于创建的每个语音邮件，统一消息都要为该邮件附带的语音邮件预览确定可信度。衡量录音中的声音与邮件中的词语、数字和短语的匹配情况。如果系统容易找到匹配项，则可信度较高。较高可信度通常与较高准确性关联。

语音邮件预览文本的准确性取决于许多因素，有时无法控制这些因素。但是，在满足以下条件时，文本可能更加准确：

  - 留下的是简单的语音邮件，并且呼叫者没有使用俚语、技术术语或冷僻的词语或短语。

  - 呼叫者使用语音邮件系统容易识别和翻译的语言。通常，语速不太快或不太慢的呼叫者和没有很重口音的呼叫者所留下的语音邮件会生成更准确的句子和短语。

  - 语音邮件不包含背景噪音和回音，音频没有遗漏。

使用统一消息的大多数客户都发现，语音邮件预览对于其用户而言足够准确。然而，在将 ASR 应用于由未知语音和背景噪音通过电话构成的录音时，语音邮件预览文本通常并不完全准确。如果可信度持续较低，或收到的语音邮件预览不十分准确，则您可以按照以下方式提高用户收到的语音邮件预览的准确性：

  - 从语音邮件预览伙伴注册语音转录服务。

  - 如果您已注册语音邮件预览伙伴，将其设置为使用 UM。有关如何为语音邮件预览伙伴配置 UM 的详细信息，请参阅[配置语音邮件预览合作伙伴服务的用户](configure-voice-mail-preview-partner-services-for-users-exchange-2013-help.md)。

注册语音邮件预览伙伴后，组织中的 Exchange 服务器将附带音频文件的语音邮件重定向到语音邮件预览伙伴，而不为语音邮件生成语音邮件预览文本，也不将语音邮件提交到用户邮箱。然后将带有语音邮件预览伙伴生成的语音邮件预览文本的电子邮件提交到组织中的 Exchange 服务器，以传递到收件人邮箱。

> [!IMPORTANT]  
> 我们建议计划部署统一消息的所有客户都获取 UM 专家的协助。UM 专家可帮助您确保有平稳过渡到 UM 从传统语音邮件系统。执行新部署或升级旧的语音邮件系统需要有关 VoIP 网关，IP Pbx、 Pbx，会话边框控制器 (SBCs) 的重要知识和统一消息传递。有关如何联系 UM 专家的详细信息，请参阅<a href="http://go.microsoft.com/fwlink/p/?linkid=262708">Microsoft Exchange Server 2013年统一消息 (UM) 专家</a>或<a href="https://go.microsoft.com/fwlink/p/?linkid=261951">Microsoft 查明其统一消息</a>。


返回顶部

## Exchange 统一消息语音邮件伙伴计划

为了通过认证成为与 Exchange UM 进行互操作的语音邮件预览伙伴，合作伙伴必须实现语音邮件预览互操作性规范中包含的要求，并且合作伙伴解决方案必须经过独立证书供应商的认证。如果您需要认证转录服务以使用 Exchange UM，请向 [Exchange 统一消息的语音邮件预览伙伴](mailto:vmppp@microsoft.com)提交请求。

## 针对 Exchange 统一消息认证的语音邮件预览伙伴

如果还没有部署统一消息在您的组织中，要寻找有资质的语音邮件预览合作伙伴提供抄写的支持服务，请参阅[Microsoft 查明其](https://go.microsoft.com/fwlink/p/?linkid=281966)。这些软件供应商经过认证与 UM Exchange 互操作。

## 配置语音邮件预览伙伴

进行了配置的 UM 将包含音频的语音邮件转发到专用语音邮件预览伙伴，该语音邮件预览伙伴随后会采用音频文件并创建语音邮件预览文本。然而，若要使用户可以在邮箱中随其语音邮件一起接收语音邮件预览，您必须配置 UM 邮箱策略，将用户与 UM 邮箱策略关联，然后使用户验证他们是否可以在 Outlook 2010 或更高版本，或 Outlook Web App 的语音邮件中接收语音邮件预览。有关如何为语音邮件预览伙伴配置 UM 的详细信息，请参阅[配置语音邮件预览合作伙伴服务的用户](configure-voice-mail-preview-partner-services-for-users-exchange-2013-help.md)。

## VoIP 或媒体网关和 IP PBX 支持

为组织配置 VoIP 网关和 IP PBX 是十分困难的部署任务，必须正确完成该任务才能成功通过语音邮件预览伙伴部署统一消息。有关可帮助您配置 VoIP 网关和 IP PBX 的信息，以及有关如何配置 VoIP 网关和 IP PBX 的最新信息，请参阅 [Exchange 2013 电话顾问](telephony-advisor-for-exchange-2013-exchange-2013-help.md) 或[支持的 VoIP 网关、IP PBX 和 PBX 的配置说明](configuration-notes-for-supported-voip-gateways-ip-pbxs-and-pbxs-exchange-2013-help.md)。

测试的互操作性交换 UM VoIP 网关与已经集成了Microsoft统一通信开放互操作性计划。有关详细信息，请参阅[Microsoft 统一通信开放互操作性程序](https://go.microsoft.com/fwlink/p/?linkid=132071)。

返回顶部

