---
title: 'IIS 6 兼容组件未安装_LonghornIIS6MetabaseNotInstalled: Exchange 2013 Help'
TOCTitle: IIS 6 兼容组件未安装_LonghornIIS6MetabaseNotInstalled
ms:assetid: 0bd52987-d3cc-496c-ac8c-d35591405195
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/ms.exch.setupreadiness.longhorniis6metabasenotinstalled(v=EXCHG.150)
ms:contentKeyID: 50489977
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# IIS 6 兼容组件未安装\_LonghornIIS6MetabaseNotInstalled

 

_**适用于：** Exchange Server_

_**上一次修改主题：** 2012-06-05_

此主题中的内容尚未针对 Microsoft Exchange Server 2013 进行更新。虽然尚未更新，但仍可能适用于 Exchange 2013。如果您仍需要帮助，请查看下面的社区资源。

遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

Microsoft®Exchange Server 2007 安装程序无法继续尝试安装客户端访问服务器角色、邮箱服务器角色或 Exchange 2007 管理工具到以下 Windows 操作系统：

  - Windows Server 2008 R2

  - Windows Server 2008

  - Windows 7（仅管理工具）

  - Windows Vista （仅管理工具）

出现这个问题的原因是未安装 Internet 信息服务 (IIS) 6 元数据库兼容组件和 IIS 6 管理控制台组件。

Exchange 2007 安装程序要求即将安装 Exchange 2007 客户端访问服务器角色、邮箱服务器角色或 Exchange 2007 管理工具的计算机上安装有 IIS 6 元数据库兼容组件和 IIS 6 管理控制台组件。

若要解决此问题，请将 IIS 6 元数据库兼容组件安装到目标计算机，然后重新运行 Microsoft Exchange 安装程序。

使用服务器管理器工具，在 Windows Server 2008 R2 或 Windows Server 中安装 IIS 6.0 管理兼容组件。

1.  依次单击\&quot;开始\&quot;、\&quot;管理工具\&quot;和\&quot;服务器管理器\&quot;。

2.  在导航窗格中，展开\&quot;角色\&quot;，右键单击\&quot;Web 服务器 (IIS)\&quot;，然后单击\&quot;添加角色服务\&quot;。

3.  在\&quot;选择角色服务\&quot;窗格上，向下滚动到\&quot;IIS 6 管理兼容性\&quot;。

4.  依次选中\&quot;IIS 6 元数据兼容性\&quot;、\&quot;IIS 6 WMI 兼容性\&quot;和\&quot;IIS 6 管理控制台\&quot;复选框。

5.  在\&quot;选择角色服务\&quot;窗格上，单击\&quot;下一步\&quot;。

6.  在\&quot;确认安装选择\&quot;窗格上，单击\&quot;安装\&quot;。

7.  单击\&quot;关闭\&quot;，退出\&quot;添加角色服务\&quot;向导。

通过\&quot;控制面板\&quot;，在 Windows 7 或 Windows Vista 中安装 IIS 6.0 管理兼容组件

1.  依次单击\&quot;开始\&quot;、\&quot;控制面板\&quot;、\&quot;程序和功能\&quot;和\&quot;打开或关闭 Windows 功能\&quot;。

2.  打开\&quot;Internet Information Services\&quot;。

3.  打开\&quot;Web 管理工具\&quot;。

4.  打开\&quot;IIS 6.0 管理兼容性\&quot;。

5.  依次选中\&quot;IIS 6 元数据和 IIS 6 配置兼容性\&quot;、\&quot;IIS 6 WMI 兼容性\&quot;和\&quot;IIS 6 管理控制台\&quot;复选框。

6.  单击\&quot;确定\&quot;。

