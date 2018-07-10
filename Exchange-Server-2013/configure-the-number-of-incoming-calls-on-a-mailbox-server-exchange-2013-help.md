---
title: '在邮箱服务器上配置拨入呼叫的数: Exchange 2013 Help'
TOCTitle: 在邮箱服务器上配置拨入呼叫的数
ms:assetid: 419e1de9-2bf8-48a8-824d-2a536b0a6d90
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa997637(v=EXCHG.150)
ms:contentKeyID: 50556556
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 在邮箱服务器上配置拨入呼叫的数

 

_**适用于：** Exchange Server, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2013-02-23_

您可以配置传入邮箱服务器运行 Microsoft Exchange 统一消息服务将接受的并发连接数。这包括所有包括 Outlook Voice Access、 呼叫应答、 自动助理和传真呼叫的传入呼叫。增加在邮箱服务器上的并发连接数，更多系统资源将需要比如果您减少并发调用的次数。减少并发调用的数量是在速度较慢的计算机安装了统一消息服务尤为重要。并发语音呼叫数的范围是 0 到 200 个。默认设置为 100。

对于与统一消息和邮箱服务器相关的其他任务，请参阅 [UM 服务过程](um-services-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：小于 1 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;邮箱服务器（UM 服务）\&quot;条目。

  - 验证是否已正确安装客户端访问服务器和邮箱服务器。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!tip]
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 使用 EAC 配置邮箱服务器上的传入呼叫数

1.  在 EAC 中，导航到\&quot;服务器\&quot;\>\&quot;服务器\&quot;。

2.  在列表视图中，选择要修改的 Exchange 服务器，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在\&quot;Exchange 服务器\&quot;页上，单击\&quot;统一消息\&quot;。

4.  在\&quot;UM 服务设置\&quot;下的\&quot;允许的最大呼叫数\&quot;下，输入一个介于 0 到 200 之间的数字，然后单击\&quot;保存\&quot;。

## 使用命令行管理程序配置邮箱服务器上的传入呼叫数

此示例将名为 `MyMailboxServer1` 的邮箱服务器可接受的传入语音、Outlook Voice Access 和传真呼叫数设置为 50。

    Set-UMService -Identity MyMailboxServer1 -MaxCallsAllowed 50

