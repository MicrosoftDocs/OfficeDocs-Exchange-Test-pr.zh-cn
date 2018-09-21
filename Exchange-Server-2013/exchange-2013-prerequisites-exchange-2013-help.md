---
title: 'Exchange 2013 先决条件: Exchange 2013 Help'
TOCTitle: Exchange 2013 先决条件
ms:assetid: e21cf744-7813-48b3-9293-5cecd89a6c25
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb691354(v=EXCHG.150)
ms:contentKeyID: 50491829
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2013 先决条件

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2017-03-20_

本主题介绍了安装 Microsoft Exchange 2013 邮箱、客户端访问以及边缘传输服务器角色所必需的 Windows Server 2012 R2、Windows Server 2012 和 Windows Server 2008 R2 with Service Pack 1 (SP1) 操作系统必备项的步骤。它还介绍了在 Windows 8、Windows 8.1 和 Windows 7 客户端计算机上安装 Exchange 2013 管理工具所必需的必备项。

  - 在开始之前，您需要知道什么？

  - Active Directory 准备

  - Windows Server 2012 R2 和 Windows Server 2012 先决条件
    
      - 邮箱或客户端访问服务器角色
    
      - 边缘传输服务器角色

  - Windows Server 2008 R2 SP1 必备项
    
      - 邮箱或客户端访问服务器角色
    
      - 边缘传输服务器角色

  - Windows 7 先决条件（仅管理工具）（仅管理工具）

  - Windows 8 和 Windows 8.1 先决条件（仅管理工具）（仅管理工具）

## 在开始之前，您需要知道什么？

  - 本主题中的信息适用于 Service Pack 1 和 Exchange 2013 的更高版本。

  - 从 Exchange 2013 SP1 开始可以使用边缘传输服务器角色。

  - 请确保林的功能级别至少为 Windows Server 2003，并确保架构主机运行的是 Windows Server 2003 Service Pack 2 或更高版本。有关 Windows 功能级别的详细信息，请参阅[管理域和林](https://go.microsoft.com/fwlink/p/?linkid=137037)。

  - 必须对运行 Exchange 2013 服务器角色或管理工具的所有服务器使用 Windows Server 2012 R2、Windows Server 2012 和 Windows Server 2008 R2 SP1 的完全安装选项。

  - 必须首先将计算机加入恰当的内部 Active Directory 林和域。

  - 一些必备项要求您重启服务器才能完成安装。

  - 在计算机上安装最新的 Windows 更新。有关详细信息，请参阅[部署安全性核对清单](deployment-security-checklist-exchange-2013-help.md)。
    
    > [!NOTE]  
    > 如果您要安装邮箱服务器角色，并计划将服务器设置为数据库可用性组 (DAG) 的成员，则必须运行 Windows Server 2012 R2 Standard 或 Datacenter Edition、Windows Server 2012 Standard 或 Datacenter Edition 或 Windows Server 2008 R2 SP1 Enterprise Edition。Windows Server 2008 R2 SP1 Standard Edition 不支持 DAG 所需的功能。<br />
    > 如果在服务器上安装了 Exchange，将无法升级 Windows。<br />
    > 若要升级至 Microsoft Unified Communications Managed API (UCMA) 4.0，您必须先卸载通过“添加/删除程序”安装的任何以前版本的 UCMA。


> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## Active Directory 准备

要用于为 Exchange 2013 准备 Active Directory 的计算机必须具备特定的必备项。

在用于准备 Active Directory 的计算机上，按所示顺序安装以下软件：

1.  [.NET Framework 4.6.2](https://go.microsoft.com/fwlink/p/?linkid=808659)

2.  [Windows Management Framework 4.0](https://go.microsoft.com/fwlink/p/?linkid=390234)（随附于 Windows Server 2012 R2）

在您安装上面所列软件后，完成以下步骤来安装远程工具管理包。安装远程工具管理包后，您将能够使用计算机来准备 Active Directory。有关 Active Directory 的详细信息，请参阅 [准备 Active Directory 和域](prepare-active-directory-and-domains-exchange-2013-help.md)。

1.  打开 Windows PowerShell。

2.  安装远程工具管理包。
    
      - 在 Windows Server 2012 R2 或 Windows Server 2012 计算机上，运行下列命令：
        
        ```powershell
Install-WindowsFeature RSAT-ADDS
```
    
      - 在 Windows Server 2008 R2 SP1 计算机上，运行下列命令：
        
        ```powershell
Add-WindowsFeature RSAT-ADDS
```

## Windows Server 2012 R2 和 Windows Server 2012 先决条件

在 Windows Server 2012 R2 或 Windows Server 2012 计算机上安装 Exchange 2013 所需的先决条件取决于您要安装哪些 Exchange 角色。请阅读以下与您想要安装的角色一致的部分。

## 邮箱或客户端访问服务器角色

请遵循本部分中的说明，在您想要进行下列操作之一的 Windows Server 2012 R2 或 Windows Server 2012 计算机上安装必备项：

  - 仅在计算机上安装邮箱服务器角色。

  - 仅在计算机上安装客户端访问服务器角色。

  - 在同一计算机上同时安装邮箱服务器角色和客户端访问服务器角色。

请执行下列操作，安装必需的 Windows 角色和功能：

1.  打开 Windows PowerShell。

2.  运行以下命令，安装必需的 Windows 组件。
    
        Install-WindowsFeature AS-HTTP-Activation, Desktop-Experience, NET-Framework-45-Features, RPC-over-HTTP-proxy, RSAT-Clustering, RSAT-Clustering-CmdInterface, RSAT-Clustering-Mgmt, RSAT-Clustering-PowerShell, Web-Mgmt-Console, WAS-Process-Model, Web-Asp-Net45, Web-Basic-Auth, Web-Client-Auth, Web-Digest-Auth, Web-Dir-Browsing, Web-Dyn-Compression, Web-Http-Errors, Web-Http-Logging, Web-Http-Redirect, Web-Http-Tracing, Web-ISAPI-Ext, Web-ISAPI-Filter, Web-Lgcy-Mgmt-Console, Web-Metabase, Web-Mgmt-Console, Web-Mgmt-Service, Web-Net-Ext45, Web-Request-Monitor, Web-Server, Web-Stat-Compression, Web-Static-Content, Web-Windows-Auth, Web-WMI, Windows-Identity-Foundation, RSAT-ADDS

在您安装操作系统角色和功能后，请按以下显示的顺序安装下列软件：

1.  [.NET Framework 4.6.2](https://go.microsoft.com/fwlink/p/?linkid=808659)
    
    > [!IMPORTANT]  
    > Exchange 2013 CU16 及更高版本<strong>要求</strong>具备 .NET Framework 4.6.2。先将服务器升级到 .NET Framework 4.6.2，然后再安装 Exchange 2013 CU16，否则将会收到错误消息。如果你在 Exchange 服务器上安装了 .NET Framework 4.5.2，请在安装 .NET Framework 4.6.2 前，先将服务器升级到 Exchange 2013 CU15。


2.  [Windows Management Framework 4.0](https://go.microsoft.com/fwlink/p/?linkid=390234)（随附于 Windows Server 2012 R2）

3.  [Microsoft Unified Communications Managed API 4.0 Core Runtime（64 位）](https://go.microsoft.com/fwlink/p/?linkid=258269)

## 边缘传输服务器角色

请遵循本部分中的说明，在您想要安装边缘传输服务器角色的 Windows Server 2012 R2 或 Windows Server 2012 计算机上安装必备项。

请执行下列操作，安装必需的 Windows 角色和功能：

1.  打开 Windows PowerShell。

2.  运行以下命令，安装必需的 Windows 组件。
    
    ```powershell
Install-WindowsFeature ADLDS
```

安装与您安装的 Exchange 2013 版本对应的 Microsoft .NET Framework 版本：

1.  [.NET Framework 4.6.2](https://go.microsoft.com/fwlink/p/?linkid=808659)
    
    > [!IMPORTANT]  
    > Exchange 2013 CU16 及更高版本<strong>要求</strong>具备 .NET Framework 4.6.2。先将服务器升级到 .NET Framework 4.6.2，然后再安装 Exchange 2013 CU16，否则将会收到错误消息。如果你在 Exchange 服务器上安装了 .NET Framework 4.5.2，请在安装 .NET Framework 4.6.2 前，先将服务器升级到 Exchange 2013 CU15。


2.  [Windows Management Framework 4.0](https://go.microsoft.com/fwlink/p/?linkid=390234)（随附于 Windows Server 2012 R2）

## Windows Server 2008 R2 SP1 必备项

在 Windows Server 2008 R2 SP1 计算机上安装 Exchange 2013 所需的先决条件取决于您要安装哪些 Exchange 角色。请阅读以下与您想要安装的角色一致的部分。

## 邮箱或客户端访问服务器角色

请遵循本部分中的说明，在您想要进行下列操作之一的 Windows Server 2008 R2 SP1 计算机上安装必备项：

  - 仅在计算机上安装邮箱服务器角色。

  - 仅在计算机上安装客户端访问服务器角色。

  - 在同一计算机上同时安装邮箱服务器角色和客户端访问服务器角色。

请执行下列操作，安装必需的 Windows 角色和功能：

1.  打开 Windows PowerShell。

2.  运行以下命令，加载服务器管理器模块。
    
    ```powershell
Import-Module ServerManager
```

3.  运行以下命令，安装必需的 Windows 组件。
    
        Add-WindowsFeature Desktop-Experience, NET-Framework, NET-HTTP-Activation, RPC-over-HTTP-proxy, RSAT-Clustering, RSAT-Web-Server, WAS-Process-Model, Web-Asp-Net, Web-Basic-Auth, Web-Client-Auth, Web-Digest-Auth, Web-Dir-Browsing, Web-Dyn-Compression, Web-Http-Errors, Web-Http-Logging, Web-Http-Redirect, Web-Http-Tracing, Web-ISAPI-Ext, Web-ISAPI-Filter, Web-Lgcy-Mgmt-Console, Web-Metabase, Web-Mgmt-Console, Web-Mgmt-Service, Web-Net-Ext, Web-Request-Monitor, Web-Server, Web-Stat-Compression, Web-Static-Content, Web-Windows-Auth, Web-WMI, RSAT-ADDS

在您安装操作系统角色和功能后，请按以下显示的顺序安装下列软件：

1.  [.NET Framework 4.6.2](https://go.microsoft.com/fwlink/p/?linkid=808659)
    
    > [!IMPORTANT]  
    > Exchange 2013 CU16 及更高版本<strong>要求</strong>具备 .NET Framework 4.6.2。先将服务器升级到 .NET Framework 4.6.2，然后再安装 Exchange 2013 CU16，否则将会收到错误消息。如果你在 Exchange 服务器上安装了 .NET Framework 4.5.2，请在安装 .NET Framework 4.6.2 前，先将服务器升级到 Exchange 2013 CU15。


2.  [Windows Management Framework 4.0](https://go.microsoft.com/fwlink/p/?linkid=390234)

3.  [Microsoft Unified Communications Managed API 4.0 Core Runtime（64 位）](https://go.microsoft.com/fwlink/p/?linkid=258269)

4.  [Microsoft 知识库文章 KB974405 (Windows Identity Foundation)](http://go.microsoft.com/fwlink/?linkid=3052&kbid=974405)

5.  [知识库文章 KB2619234（启用 HTTP 上的 RPC 使用的关联 Cookie/GUID，以同时用于 Windows 7 和 Windows Server 2008 R2 的 RPC 层）](http://go.microsoft.com/fwlink/?linkid=3052&kbid=2619234)

6.  [知识库文章 KB2533623（不安全的库加载可能允许远程代码执行）](http://go.microsoft.com/fwlink/?linkid=3052&kbid=2533623)
    
    > [!NOTE]  
    > 如果您已经配置 Windows Update 以在计算机上安装安全更新，则该修补程序可能已经安装。


## 边缘传输服务器角色

请遵循本部分中的说明，在您想要安装边缘传输服务器角色的 Windows Server 2008 R2 SP1 计算机上安装必备项。

请执行下列操作，安装必需的 Windows 角色和功能：

1.  打开 Windows PowerShell。

2.  运行以下命令，加载服务器管理器模块。
    
    ```powershell
Import-Module ServerManager
```

3.  运行以下命令，安装必需的 Windows 组件。
    
    ```powershell
Add-WindowsFeature NET-Framework, ADLDS
```

在您安装操作系统角色和功能后，请按以下显示的顺序安装下列软件：

1.  [.NET Framework 4.6.2](https://go.microsoft.com/fwlink/p/?linkid=808659)
    
    > [!IMPORTANT]  
    > Exchange 2013 CU16 及更高版本<strong>要求</strong>具备 .NET Framework 4.6.2。先将服务器升级到 .NET Framework 4.6.2，然后再安装 Exchange 2013 CU16，否则将会收到错误消息。如果你在 Exchange 服务器上安装了 .NET Framework 4.5.2，请在安装 .NET Framework 4.6.2 前，先将服务器升级到 Exchange 2013 CU15。


2.  [Windows Management Framework 4.0](https://go.microsoft.com/fwlink/p/?linkid=390234)

3.  [Microsoft Unified Communications Managed API 4.0 Core Runtime（64 位）](https://go.microsoft.com/fwlink/p/?linkid=258269)

## Windows 7 先决条件（仅管理工具）

遵照该部分中的说明在要安装 Exchange 管理工具的加入域的 Windows Server 7 64 位计算机上安装必备项。

1.  打开“控制面板”，然后选择“程序”。

2.  单击“打开或关闭 Windows 功能”。

3.  导航至“Internet 信息服务”\>“Web 管理工具”\>“IIS 6 管理兼容性”。

4.  选中“IIS 6 管理控制台”对应的复选框，然后单击“确定”。

在您安装操作系统功能后，请按以下显示的顺序安装下列软件：

1.  [.NET Framework 4.6.2](https://go.microsoft.com/fwlink/p/?linkid=808659)

2.  [Windows Management Framework 4.0](https://go.microsoft.com/fwlink/p/?linkid=390234)

3.  [知识库文章 KB974405 (Windows Identity Foundation)](http://go.microsoft.com/fwlink/?linkid=3052&kbid=974405)

## Windows 8 和 Windows 8.1 先决条件（仅管理工具）

[.NET Framework 4.6.2](https://go.microsoft.com/fwlink/p/?linkid=808659)

