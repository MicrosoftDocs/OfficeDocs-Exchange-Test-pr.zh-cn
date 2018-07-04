---
title: '拨号计划中设置的默认语言: Exchange Online Help'
TOCTitle: 拨号计划中设置的默认语言
ms:assetid: 7a1d2e7e-4053-40af-9ec1-ec714df12ad4
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa998914(v=EXCHG.150)
ms:contentKeyID: 50556602
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 拨号计划中设置的默认语言

 

_**适用于：** Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2016-12-09_

您可以设置统一邮件 (UM) 拨号计划的默认语言。您创建的每个拨号计划最初将为默认语言使用英语 (EN-US)。英语 (EN-US) 语言包安装在MicrosoftExchange Server 2013的所有版本，并不能删除。

如果要选择另一种语言作为默认语言，例如，德语 (DE-DE)，您必须首先下载从[Exchange Server 2013 UM 语言包](https://go.microsoft.com/fwlink/p/?linkid=266542) UM 德语语言包.exe 文件并使用 UMLanguagePack.de de.exe 安装文件在邮箱服务器上安装该语言包。安装语言包后，您可以您的 UM 拨号计划上设置默认语言设置为一种语言不是英语 (EN-US)。

有关与 UM 语言相关的其他任务，请参阅 [UM 语言、 提示和问候过程](um-languages-prompts-and-greetings-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：小于 1 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 拨号计划\&quot;条目。

  - 在执行这些步骤之前，先确认已创建 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!tip]
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 使用 EAC 设置 UM 拨号计划中的默认语言

1.  在 EAC 中，导航到\&quot;统一消息\&quot;\>\&quot;UM 拨号计划\&quot;。

2.  在列表视图中，选择要修改 UM 拨号计划，然后在工具栏上单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在\&quot;UM 拨号计划\&quot;页上，单击\&quot;配置\&quot;。

4.  在\&quot;设置\&quot;页上的\&quot;音频语言\&quot;下，从下拉列表中选择要设置的语言。

5.  单击\&quot;保存\&quot;接受更改。

## 使用命令行管理程序设置 UM 拨号计划中的默认语言

本示例将名为 `MyUMDialPlan` 的 UM 拨号计划中的默认语言设置为德语。

    Set-UMDialPlan -Identity MyUMDialPlan -DefaultLanguage de-DE

本示例将名为 `MyUMDialPlan` 的 UM 拨号计划中的默认语言设置为日语。

    Set-UMDialPlan -Identity MyUMDialPlan -DefaultLanguage ja-JP

本示例将名为 `MyUMDialPlan` 的 UM 拨号计划中的默认语言设置为澳大利亚英语。

    Set-UMDialPlan -Identity MyUMDialPlan -DefaultLanguage en-AU

