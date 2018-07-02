---
title: '管理 UM 的邮箱服务器上的设置: Exchange 2013 Help'
TOCTitle: 管理 UM 的邮箱服务器上的设置
ms:assetid: 6df4853d-21d2-473f-b0ca-ebc996d8794a
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa998815(v=EXCHG.150)
ms:contentKeyID: 50556595
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Servers.UnifiedMessaging.UMServerPropertiesPropertyPage
ms.translationtype: MT
---

# 管理 UM 的邮箱服务器上的设置

 

_**适用于：**Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：**2013-02-11_

安装运行 Microsoft Exchange 统一消息服务的邮箱服务器之后，您可以配置多个选项，其中包括：并发来电数、TCP 和传输层安全性 (TLS) 侦听端口、状态以及 UM 启动模式。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>它不具有必需的 UM 拨号计划加入邮箱服务器，它可以处理之前调用的统一邮件 (UM)，除正在集成 UM 和 Microsoft Office 通信服务器 2007 R2 或 Microsoft Lync Server 时。默认情况下，组织中的所有邮箱服务器都都可以应答传入呼叫。</td>
</tr>
</tbody>
</table>


有关统一消息和邮箱服务器相关的其他管理任务，请参阅 [UM 服务过程](um-services-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：5 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;邮箱服务器（UM 服务）\&quot;条目。

  - 验证邮箱服务器是安装在与客户端访问服务器相同的计算机中，还是安装在单独的计算机中。

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

## 使用命令行管理程序在邮箱服务器中配置统一消息属性

本示例从所有会话初始协议 (SIP) 拨号计划中删除名为 `MyMailboxServer` 的邮箱服务器。

    Set-UMService -Identity MyMailboxServer -DialPlans $null

本示例在名为 `MySIPDialPlanName` 的 UM SIP 拨号计划中添加名为 `MyMailboxServer` 的邮箱服务器，还设置了传入语音呼叫的最大次数。

    Set-UMService -Identity MyMailboxServer -DialPlans MySIPDialPlanName -MaxCalls 150 

本示例在名为 `MyUMServer` 的邮箱服务器中将启动模式设置为双模式。

    Set-UMService -Identity MyMailboxServer -DialPlans MySIPDialPlanName -UMStartUpMode -Dual 

## 使用命令行管理程序查看邮箱服务器属性

本示例显示所有邮箱服务器的列表。

    Get-UMService

本示例显示名为 `MyMailboxServer` 的邮箱服务器属性的格式化列表。

    Get-UMService -Identity MyMailboxServer | Format-List

