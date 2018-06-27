---
title: '停止的 Microsoft Exchange 统一消息呼叫路由器服务: Exchange 2013 Help'
TOCTitle: 停止的 Microsoft Exchange 统一消息呼叫路由器服务
ms:assetid: 79935528-1a8c-4f22-826c-8f9a60f4f6f4
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ673535(v=EXCHG.150)
ms:contentKeyID: 50556603
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 停止的 Microsoft Exchange 统一消息呼叫路由器服务

 

_**适用于：**Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：**2012-11-16_

可以使用服务管理单元中Microsoft管理控制台 (MMC) 或 cmd.exe 命令提示符处以停止客户端访问服务器上的MicrosoftExchange统一消息呼叫路由器服务。有时可能需要停止此服务，例如，当您必须将客户端访问服务器脱机。MicrosoftExchange统一消息呼叫路由器服务停止时，客户端访问服务器不能接受和处理传入呼叫。

有关与客户端访问服务器相关的其他管理任务，请参阅 [UM 服务过程](um-services-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：小于 1 分钟。

  - 若要执行以下过程，必须使用属于本地管理员组成员的帐户登录客户端访问服务器。

  - 验证客户端访问服务器是安装在与邮箱服务器相同的计算机上还是安装在单独的计算机上。

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

## 使用 MMC 服务管理单元停止 Microsoft Exchange 统一消息呼叫路由器服务

1.  单击\&quot;开始\&quot;，然后单击\&quot;控制面板\&quot;。

2.  在\&quot;控制面板\&quot;中，双击\&quot;管理工具\&quot;。

3.  在\&quot;管理工具\&quot;中，双击\&quot;服务\&quot;。

4.  在\&quot;服务\&quot;详细信息窗格中，右键单击\&quot;Microsoft Exchange 统一消息呼叫路由器\&quot;，然后单击\&quot;停止\&quot;。

## 使用命令提示符停止 Microsoft Exchange 统一消息呼叫路由器服务

1.  单击**开始**，然后单击**运行**。

2.  在\&quot;打开\&quot;框中，键入以下命令，然后按 Enter。
    
        net stop MSExchangeUMCR

