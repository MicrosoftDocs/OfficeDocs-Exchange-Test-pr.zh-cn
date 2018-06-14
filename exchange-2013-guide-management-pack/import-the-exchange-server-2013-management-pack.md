---
title: 导入 Exchange Server 2013 管理包
TOCTitle: 导入 Exchange Server 2013 管理包
ms:assetid: dc929928-61b8-448b-9ae5-d3fa73a18ee9
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dn195914(v=EXCHG.150)
ms:contentKeyID: 53275726
ms.author:dstrome
ms.date: 04/03/2015
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 导入 Exchange Server 2013 管理包

 

_**上一次修改主题：** 2013-03-30_

让我们开始向 SCOM 部署中导入管理包。

## 先决条件

请先验证是否符合下列条件，如果符合，才能导入管理包：

  - 在组织中部署了下列 System Center Operations Manager 版本之一：
    
      - System Center Operations Manager 2012 RTM 或更高版本
    
      - System Center Operations Manager 2007 R2 或更高版本

  - 已向 Exchange Server 部署了 SCOM 代理。[验证代理部署状态](procedures-related-to-deployment.md).

  - Exchange Server 上的 SCOM 代理在本地系统帐户下运行。[验证代理安全配置](procedures-related-to-deployment.md).

  - Exchange Server 上的 SCOM 代理被配置为在其他计算机上发现托管对象的代理。[验证代理程序配置](procedures-related-to-deployment.md).

  - 用户帐户拥有 Operations Manager 管理员角色。

## 导入 Exchange Server 2013 管理包

请执行下列步骤来导入 Exchange Server 2013 管理包。此过程假定您已将管理包内容提取到 System Center Operations Manager (SCOM) 服务器上的本地驱动器中。您可以从其中下载 Exchange Server 2013 管理包。

1.  登录 SCOM 服务器，从 [Microsoft 下载中心](http://go.microsoft.com/fwlink/p/?linkid=268587)下载 Exchange Server 2013 管理包。

2.  通过运行 `ExchangeServerManagementPack.msi` 文件将管理包内容提取到系统中的一个文件夹。

3.  启动 SCOM 控制台。在 SCOM 控制台中，单击“管理”。

4.  右键单击“管理包”，然后单击“导入管理包”。

5.  此时将打开“导入管理包”向导。单击“添加”，然后单击“从磁盘中添加”。

6.  此时将显示“选择要导入的管理包”对话框。浏览从中提取管理包的目录。单击 `Microsoft.Exchange.15.mp` 文件，然后单击“打开”。

7.  此时“选择管理包”页面上列出了 Exchange Server 2013 管理包。单击“安装”。

8.  此时将显示“导入管理包”页面（其上显示有进度）。如果在导入过程中的任何阶段出错，可选择列表中的管理包，查看状态详细信息。

9.  导入完成后，单击“关闭”。

10. 依次单击“查看”和“刷新”或按 F5 查看管理包列表中是否有 Microsoft Exchange Server 2013 管理包。

现在您已导入管理包，请参阅 [Exchange Server 2013 Management Pack 入门](getting-started-with-exchange-server-2013-management-pack.md)了解新的仪表板。

