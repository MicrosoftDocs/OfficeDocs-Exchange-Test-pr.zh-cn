---
title: '在 DNS 数据库中找不到本地计算机的主机记录: Exchange 2013 Help'
TOCTitle: 在 DNS 数据库中找不到本地计算机的主机记录
ms:assetid: 2f18cb65-29fe-4b72-8d68-52fd503d5673
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/ms.exch.setupreadiness.hostrecordmissing(v=EXCHG.150)
ms:contentKeyID: 50490263
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 在 DNS 数据库中找不到本地计算机的主机记录

 

_**适用于：** Exchange Server_

_**上一次修改主题：** 2016-12-09_

因为在域名系统 (DNS) 数据库中找不到此计算机的主机 (A) 记录，所以 Microsoft Exchange Server 2013 安装程序无法继续进行。

Exchange 2013 安装程序要求本地计算机具有已在该域的权威 DNS 数据库中进行了注册的有效主机 (A) 记录。

Exchange 依靠其下一个内部或外部目标服务器的 IP 地址的 DNS 主机 (A) 记录。

若要解决该问题，请执行下列操作：

  - 验证本地 TCP/IP 配置是否指向正确的 DNS 服务器。有关详细信息，请参阅[配置 TCP/IP 设置](https://go.microsoft.com/fwlink/p/?linkid=108281)。

  - 使用 Nslookup.exe 验证 DNS 服务器上是否存在主机 (A) 记录。有关详细信息，请参阅[验证 A 资源记录是否在 DNS 中存在](https://go.microsoft.com/fwlink/?linkid=63001)。

有关 DNS 名称解析、疑难解答和主机 (A) 记录的信息，请参阅以下资源：

  - [DNS 疑难解答](https://go.microsoft.com/fwlink/p/?linkid=294828)

  - [管理资源记录](https://go.microsoft.com/fwlink/p/?linkid=294829)

遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

您找到所需内容了吗？请花一点时间[向我们发送反馈](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedbac)，告诉我们您希望找到的信息。

