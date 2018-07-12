---
title: '缺少主要的 DNS 后缀: Exchange 2013 Help'
TOCTitle: 缺少主要的 DNS 后缀
ms:assetid: 310765bf-a650-4a3d-a5e4-6173b559d4f6
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/ms.exch.setupreadiness.fqdnmissing(v=EXCHG.150)
ms:contentKeyID: 61203673
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 缺少主要的 DNS 后缀

 

_**适用于：** Exchange Server_

_**上一次修改主题：** 2014-01-15_

Microsoft Exchange Server 2013 安装程序无法继续运行，因为您正在安装 Exchange 的计算机未配置主要的域名系统 (DNS) 后缀。

要解决此问题，请通过下面的步骤在计算机上添加主要的 DNS 后缀，然后再次运行安装程序。

> [!important]
> 安装 Exchange 2013 后，不支持更改计算机名称或主要的 DNS 后缀。


1.  以本地 Administrators 组成员身份登录到您要在其上安装边缘传输角色的计算机。

2.  打开\&quot;控制面板\&quot;，然后双击\&quot;系统\&quot;。

3.  在\&quot;计算机名称、域和工作组设置\&quot;部分，单击\&quot;更改设置\&quot;。

4.  在\&quot;系统属性\&quot;窗口中，确保选择\&quot;计算机名称\&quot;选项卡，然后单击\&quot;更改…\&quot;。

5.  在\&quot;计算机名称/域更改\&quot;中，单击\&quot;更多…\&quot;。

6.  在\&quot;此计算机的主 DNS 后缀\&quot;中，输入边缘传输服务器的 DNS 域名。例如，contoso.com。

7.  单击\&quot;确定\&quot;关闭每个窗口。

遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

您找到所需内容了吗？请花一点时间[向我们发送反馈](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedbac)，告诉我们您希望找到的信息。

