---
title: '配置最大录制持续时间: Exchange Online Help'
TOCTitle: 配置最大录制持续时间
ms:assetid: 18eeb567-1048-4c82-93cf-612cb12ec5e3
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Ee423539(v=EXCHG.150)
ms:contentKeyID: 50489972
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 配置最大录制持续时间

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2012-11-09_

您可以指定的最大每个语音记录呼叫者留下语音邮件时所允许的分钟数。此值可以设置为一个数字，从 1 到 100 之间。对于大多数组织，此值应设置为默认值 20 分钟。将此值设置得过低会导致长语音邮件来他们在完成之前被中断。将冗长的语音邮件保存在收件箱中的用户可以设置此值太高。

此设置是重要信息 ︰ 如果您已实现的用户严格磁盘配额。它必须设置为较低的值比另一组用于**最长呼叫持续时间 （分钟）**。

有关与 UM 拨号计划相关的其他任务，请参阅[UM 拨号计划过程](um-dial-plan-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：小于 1 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 拨号计划\&quot;条目。

  - 在执行这些步骤之前，先确认已创建 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 使用 EAC 配置最长录音持续时间

1.  在 EAC 中，导航到\&quot;统一消息\&quot;\>\&quot;UM 拨号计划\&quot;。

2.  在列表视图中，选择要修改的 UM 拨号计划，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在\&quot;UM 拨号计划\&quot;页上，单击\&quot;配置\&quot;。

4.  在\&quot;设置\&quot;中的\&quot;最长录音持续时间(分钟)\&quot;下，输入以分钟为单位的数字。

5.  单击\&quot;保存\&quot;。

## 使用命令行配置最长录音持续时间

本示例针对名为 `MyUMDialPlan` 的 UM 拨号计划将最长录音持续时间设置为 10 分钟。

    Set-UMDialPlan -identity MyUMDialPlan -MaxRecordingDuration 10

