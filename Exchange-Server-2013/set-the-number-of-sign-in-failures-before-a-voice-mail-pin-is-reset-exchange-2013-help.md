---
title: '设置语音邮件 PIN 重置之前登录失败的次数: Exchange Online Help'
TOCTitle: 设置语音邮件 PIN 重置之前登录失败的次数
ms:assetid: 4de38499-0a6f-4f00-8697-eeff805d7266
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa997939(v=EXCHG.150)
ms:contentKeyID: 50556573
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 设置语音邮件 PIN 重置之前登录失败的次数

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2013-02-22_

可以为 Outlook Voice Access 用户将重置 PIN 之前允许的登录失败次数配置为 1 到 998 之间的某个值。默认值为 5。先在统一消息 (UM) 邮箱策略中配置重置 PIN 之前允许的登录失败次数，然后将其应用于与该 UM 邮箱策略关联的所有 Outlook Voice Access 用户。

> [!NOTE]  
> 将&amp;quot;PIN 重置之前登录失败的次数&amp;quot;设置配置为小于 5 的数字可以提高安全性，而将其设置为大于 5 的数字会降低安全性。


有关与 Outlook Voice Access PIN 安全相关的其他任务，请参阅 [针的安全程序](pin-security-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：3 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 邮箱策略\&quot;条目。

  - 在执行这些步骤之前，先确认已创建 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

  - 在执行这些步骤之前，先确认已创建 UM 邮箱策略。有关详细步骤，请参阅[创建 UM 邮箱策略](create-a-um-mailbox-policy-exchange-2013-help.md)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 使用 EAC 配置重置 PIN 之前的登录失败次数

1.  在 EAC 中，导航到\&quot;统一消息\&quot;\>\&quot;UM 拨号计划\&quot;。

2.  在此列表视图中，选择您要更改的 UM 拨号计划，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在\&quot;UM 拨号计划\&quot;页面的\&quot;UM 邮箱策略\&quot;下，选择要更改的 UM 邮箱策略，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

4.  单击\&quot;PIN 策略\&quot;，然后在\&quot;PIN 重置之前登录失败的次数\&quot;旁边输入一个介于 0 至 999 之间的值。

5.  单击\&quot;保存\&quot;。

## 使用命令行管理程序配置 PIN 重置之前登录失败的次数

本示例针对与名为 `MyUMMailboxPolicy` 的 UM 邮箱策略关联而且启用了 UM 的用户，将重置用户的 PIN 之前登录失败的次数设置为 3。

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -LogonFailuresBeforePINReset 3

本示例针对与名为 `MyUMMailboxPolicy` 的 UM 邮箱策略关联并且启用了 UM 的用户，将重置用户的 PIN 之前登录失败的次数设置为 3，将尝试登录的最大次数设置为 5，并将 PIN 的最短长度设置为 9。

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -LogonFailuresBeforePINReset 3 -MaxLogonAttempts 5 -MinPINLength 9

