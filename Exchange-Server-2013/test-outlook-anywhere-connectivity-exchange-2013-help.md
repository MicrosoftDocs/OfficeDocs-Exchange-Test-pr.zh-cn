---
title: '测试 Outlook 无处不在 的连接: Exchange 2013 Help'
TOCTitle: 测试 Outlook 无处不在 的连接
ms:assetid: 0dc5b68f-2316-446a-84c9-5f1c50dc3776
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Ee633453(v=EXCHG.150)
ms:contentKeyID: 50556524
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 测试 Outlook 无处不在 的连接

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2016-12-09_

通过使用 Shell 或 Exchange Remote Connectivity Analyzer (ExRCA)，您可以测试端到端客户端的 Outlook Anywhere 连接。这包括通过自动发现服务、创建用户配置文件和登录用户邮箱执行的连接测试。从自动发现服务中检索所需的全部值。

有关与 Outlook 无处不在 相关的其他管理任务，请参阅 [Outlook 无处不在](outlook-anywhere-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：10 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[客户端和移动设备权限](clients-and-mobile-devices-permissions-exchange-2013-help.md)主题中的“Outlook 无处不在”条目。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 使用命令行测试 Outlook 无处不在 的连接性

若要使用命令行管理程序测试 Outlook 无处不在 连接，请使用 **Test-OutlookConnectivity** cmdlet。

运行以下命令。

    Test-OutlookConnectivity -ProbeIdentity 'OutlookMailboxDeepTestProbe' -MailboxId tony@contoso.com -Hostname contoso.com

> [!NOTE]  
> <em>OutlookMailboxDeepTestProbe</em> 参数值可测试邮箱服务器的连接。若要测试客户端访问服务器的连接，请将 <em>OutlookMailboxCTPProbe</em> 用于 <em>ProbeIdentity</em> 参数值。


## 使用 Exchange Remote Connectivity Analyzer 测试 Outlook 无处不在 连接

Exchange Remote Connectivity Analyzer (ExRCA) 是一款基于 Web 的工具，旨在测试与各种 Exchange 协议的连接。您可以在[此处](https://go.microsoft.com/fwlink/p/?linkid=167905)访问 ExRCA。

1.  在 ExRCA 网站上，在“Microsoft Office Outlook 连接测试”下，选择“Outlook 无处不在”，然后在页面底部选择“下一步”。

2.  在下一个屏幕中输入必填信息，其中包括电子邮件地址、域名、用户名和密码。

3.  选择是使用“自动发现”来检测服务器设置，还是手动指定服务器设置。

4.  接受免责声明，输入验证代码，然后选择“验证”。

5.  选择“执行测试”。

## 您如何知道这有效？

ExRCA 测试完成之后，输出结果将显示在网页中。所有故障均会列出。

