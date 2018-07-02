---
title: '建议不要在域控制器上安装 Exchange: Exchange 2013 Help'
TOCTitle: 建议不要在域控制器上安装 Exchange
ms:assetid: 48922de2-a68c-4092-96a5-d38c8e5f49f5
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/ms.exch.setupreadiness.warninginstallexchangerolesondomaincontroller(v=EXCHG.150)
ms:contentKeyID: 50490468
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 建议不要在域控制器上安装 Exchange

 

_**适用于：**Exchange Server_

_**上一次修改主题：**2013-03-22_

Microsoft Exchange Server 2013 安装程序检测到要在其上尝试安装 Exchange 2013 的计算机是 Active Directory 域控制器。建议不要在域控制器上安装 Exchange 2013。

如果要在域控制器上安装 Exchange 2013，请注意以下问题：

  - 不支持为 Exchange 2013 配置 Active Directory 拆分权限。

  - 在域控制器上安装 Exchange 时，会将“Exchange 受信任子系统”通用安全组 (USG) 添加到 Domain Admins 组中。发生这种情况时，域中的所有 Exchange 服务器都会获得该域中的域管理员权限。

  - Exchange Server 和 Active Directory 都是耗费资源的应用程序。当两者运行在同一台计算机上时，存在一些需要考虑的性能因素。

  - 必须确保安装 Exchange 2013 的域控制器是全局编录服务器。

  - 如果域控制器同时也是全局编录服务器，Exchange 服务可能无法正确启动。

  - 如果在关闭或重新启动服务器之前未停止 Exchange 的服务，则关闭系统所需的时间将大大延长。

  - 不支持将域控制器降级为成员服务器。

  - 不支持在同时也是 Active Directory 域控制器的群集节点上运行 Exchange 2013。

我们建议在成员服务器上安装 Exchange 2013。

遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

您找到所需内容了吗？请花一点时间[向我们发送反馈](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedbac)，告诉我们您希望找到的信息。

