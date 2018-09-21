---
title: '在 Exchange 2013 中配置 SSL 卸载: Exchange 2013 Help'
TOCTitle: 在 Exchange 2013 中配置 SSL 卸载
ms:assetid: 654cc2c2-918b-48fc-9532-9c8e3012810d
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dn635115(v=EXCHG.150)
ms:contentKeyID: 61203677
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 在 Exchange 2013 中配置 SSL 卸载

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2016-08-22_

下文将帮助您为安装了 Service Pack 1 (SP1) 的 Exchange 2013 客户端访问服务器上的协议和相关服务配置 SSL 卸载。如果您有多台客户端访问服务器，您必须为内部部署组织中安装了 SP1 的每台客户端访问服务器上的每个协议或服务执行所需步骤。更不用说组织中的每台客户端访问服务器必须使用相同配置。如果您正在升级到更高版本的累积更新 (CU) 或 Service Pack，并且您希望继续使用 SSL 卸载，则在 Exchange 2013 客户端访问服务器上升级或应用这些更新后，您必须再次执行这些步骤。

SSL 卸载的最大优势之一是能够更轻松地管理所使用的证书。无需为安装了 SP1 的每台客户端访问服务器安装单独的 SSL 证书，而是使用单个 SSL 证书并将此证书导入所有客户端访问服务器。所使用的证书可以是一个现有的或新创建的 SSL 证书。

> [!CAUTION]  
> 使用 Internet 信息服务 (IIS) 管理器、Exchange 命令行管理程序或命令行界面配置 SSL 卸载时，请注意存在“<strong>默认网站</strong>”和“<strong>Exchange 后端</strong>”网站。对于 SSL 卸载，仅配置“<strong>默认网站</strong>”，对“<strong>Exchange 后端</strong>”网站不做任何更改。


**目录**

为 Outlook Web App 配置 SSL 卸载

为 Exchange 管理员中心 (EAC) 配置 SSL 卸载

Configuring SSL offloading for Outlook 无处不在

为脱机通讯簿 (OAB) 配置 SSL 卸载

为 Exchange ActiveSync (EA) 配置 SSL 卸载

为 Exchange Web 服务 (EWS) 配置 SSL 卸载

为自动发现服务配置 SSL 卸载

为邮箱复制代理服务 (MRSProxy) 配置 SSL 卸载

为 Outlook 客户端（MAPI 虚拟目录）配置 SSL 卸载

使用脚本为所有协议和服务启用 SSL 卸载

配置与 Exchange 2007 和 Exchange 2010 共存

## 在开始之前，您需要知道什么？

  - 在组织中安装所有所需的客户端访问服务器和邮箱服务器。

  - 在您组织中的每个客户端访问服务器和邮箱服务器上安装 Service Pack 1 (SP1)。若要下载 SP1，请参阅 [Exchange 2013 更新](updates-for-exchange-2013-exchange-2013-help.md)。

  - 参阅[功能权限](feature-permissions-exchange-2013-help.md)，确定 Exchange 2013 所需的权限。

  - 若要查看客户端访问服务器所需的权限，请参阅[客户端和移动设备权限](clients-and-mobile-devices-permissions-exchange-2013-help.md)中的“客户端访问服务器权限”。

  - 若要查看客户端访问服务器所需的权限，请参阅[客户端和移动设备权限](clients-and-mobile-devices-permissions-exchange-2013-help.md)中的“Outlook Web App 权限”。

  - 可能只能使用命令行管理程序执行某些过程。若要了解如何在本地 Exchange 组织中打开命令行管理程序，请参阅[打开命令行管理程序](https://technet.microsoft.com/zh-cn/library/dd638134\(v=exchg.150\))。

  - 要在客户端访问服务器上以及您与其终止 SSL 连接的设备上使用现有证书，请在客户端访问服务器上使用私钥导出证书，并在设备上导入或安装此证书。有关详细信息，请参阅[Export-ExchangeCertificate](https://technet.microsoft.com/zh-cn/library/aa996305\(v=exchg.150\))。

  - 若要使用新证书，必须使用 EAC 或命令行管理程序创建、导入并启用此新证书。有关详细信息，请参阅[Exchange 2013 证书管理 UI](exchange-2013-certificate-management-ui-exchange-2013-help.md)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 为 Outlook Web App 配置 SSL 卸载

要为 Outlook Web App 启用 SSL 卸载，您需要在“默认网站”上的“owa”虚拟目录中删除 SSL 要求：

  - **步骤 1**   您可以使用 Internet 信息服务 (IIS) 管理器或命令行在“owa”虚拟目录上禁用 SSL：
    
      - 使用 Internet 信息服务 (IIS) 管理器，展开“网站”\>“默认网站”，然后选择“owa”虚拟目录。在结果窗格中的“IIS”下，双击“SSL 设置”。在“SSL 设置”结果窗格中，取消选中“需要 SSL”复选框，然后在“操作”窗格中单击“应用”。
    
      - 使用命令行键入以下命令，然后按 Enter 键。
        
        ```powershell
appcmd set config "Default Web Site/owa" /section:access /sslFlags:None /commit:APPHOST
```

  - **步骤 2**   您需要使用以下方法之一回收相应的应用程序池或重新启动 Internet 信息服务：
    
      - 使用命令行：转到“开始”\>“运行”，键入“cmd”，然后按 Enter 键。在命令提示符窗口中，键入以下命令，然后按 Enter 键。
        
        ```powershell
appcmd Recycle AppPool MSExchangeOWAAppPool
```
    
      - 使用 Windows PowerShell cmdlet 键入以下命令，然后按 Enter 键。
        
        ```powershell
IIS:\>Restart-WebAppPool MSExchangeOWAAppPool
```
    
      - 使用命令行：转到“开始”\>“运行”，键入“cmd”，然后按 Enter 键。在命令提示符窗口中，键入以下命令，然后按 Enter 键。
        
        ```powershell
iisreset /noforce
```
    
      - 使用 Internet 信息服务 (IIS) 管理器：在 Internet 信息服务 (IIS) 管理器的“操作”窗格中，单击“重新启动”。

返回顶部

## 为 Exchange 管理员中心 (EAC) 配置 SSL 卸载

要为 EAC 启用 SSL 卸载，您需要在“默认网站”上的“ecp”虚拟目录中删除 SSL 要求：

  - **步骤 1**   您可以使用 Internet 信息服务 (IIS) 管理器或命令行在“ecp”虚拟目录上禁用 SSL：
    
      - 使用 Internet 信息服务 (IIS) 管理器，展开“网站”\>“默认网站”，然后选择“ecp”虚拟目录。在结果窗格中的“IIS”下，双击“SSL 设置”。在“SSL 设置”结果窗格中，取消选中“需要 SSL”复选框，然后在“操作”窗格中单击“应用”。
    
      - 使用命令行键入以下命令，然后按 Enter 键。
        
        ```powershell
appcmd set config "Default Web Site/ecp" /section:access /sslFlags:None /commit:APPHOST
```
        

  - **步骤 2**   您需要使用以下方法之一回收相应的应用程序池或重新启动 Internet 信息服务：
    
      - 使用命令行：转到“开始”\>“运行”，键入“cmd”，然后按 Enter 键。在命令提示符窗口中，键入以下命令，然后按 Enter 键。
        
        ```powershell
appcmd Recycle AppPool MSExchangeECPAppPool
```
    
      - 使用 Windows PowerShell cmdlet 键入以下命令，然后按 Enter 键。
        
        ```powershell
IIS:\>Restart-WebAppPool MSExchangeECPAppPool
```
    
      - 使用命令行：转到“开始”\>“运行”，键入“cmd”，然后按 Enter 键。在命令提示符窗口中，键入以下命令，然后按 Enter 键。
        
        ```powershell
iisreset /noforce
```
    
      - 使用 Internet 信息服务 (IIS) 管理器：在 Internet 信息服务 (IIS) 管理器的“操作”窗格中，单击“重新启动”。

返回顶部

## 为 Outlook 无处不在 配置 SSL 卸载

默认情况下已为 Outlook 无处不在 启用 SSL 卸载。Outlook 无处不在 可以从私有或公用网络获取电子邮件。默认情况下，服务器的内部主机名或 FQDN 用于启用内部 Outlook 客户端的连接。但是，如果 Outlook 无处不在 不在内部使用，则应删除内部主机名。要允许对 Outlook 客户端的内部和外部访问，必须配置内部和外部主机名，分别设置其身份验证方法，并将内部和外部客户端设置为需要 SSL。要为外部客户端配置身份验证方法，可以使用 EAC 或 Exchange 命令行管理程序；但对于内部客户端，必须使用命令行管理程序：

  - **步骤 1**   如果没有为 Outlook 无处不在 添加外部主机名，则可以使用 EAC 或命令行管理程序：
    
      - 使用 EAC 转到“服务器”，在列表中选择客户端访问服务器的名称，然后单击“编辑”。在“Exchange Server”窗口中，单击“Outlook 无处不在”，然后在“指定用户将用于连接到组织的外部主机名(例如，contoso.com)”框中输入外部主机名。确认“允许 SSL 卸载”选项已选中，然后单击“保存”。
    
      - 使用 Exchange 命令行管理程序，单击“开始”，然后在“开始”菜单上单击“Exchange 命令行管理程序”。在窗口中键入以下命令，然后按 Enter 键：
        
            Set-OutlookAnywhere -Identity ClientAccessServer1\Rpc* -Externalhostname ClientAccessServer1.contoso.com -ExternalClientsRequireSsl:$True -ExternalClientAuthenticationMethod Basic

  - **步骤 2**   默认情况下，SSL 卸载已启用。但是，如果 SSL 卸载已禁用，现在您希望将其启用，您可以使用 EAC 或 Exchange 命令行管理程序。
    
      - 使用 EAC 转到“服务器”，在列表中选择客户端访问服务器的名称，然后单击“编辑”。在“Exchange Sever”窗口中，依次单击“Outlook 无处不在”、“允许 SSL 卸载”选项、“保存”。
    
      - 使用命令行管理程序键入以下命令，然后按 Enter 键。
        
            Set-OutlookAnywhere -Identity ClientAccessServer1\Rpc* -SSLOffloading $true

  - **步骤 3**   默认情况下，“需要 SSL”在“Rpc”虚拟目录上未选中，但是如果您想要确认 SSL 已禁用，您可以使用 Internet 信息服务 (IIS) 管理器。
    
      - 使用 Internet 信息服务 (IIS) 管理器，展开“网站”\>“默认网站”，然后选择“Rpc”虚拟目录。在结果窗格中的“IIS”下，双击“SSL 设置”。在“SSL 设置”结果窗格中，确认“需要 SSL”复选框已取消选中，然后在“操作”窗格中单击“应用”。

  - **步骤 4**   您需要使用以下方法之一回收相应的应用程序池或重新启动 Internet 信息服务：
    
      - 使用命令行：转到“开始”\>“运行”，键入“cmd”，然后按 Enter 键。在命令提示符窗口中，键入以下命令，然后按 Enter 键。
        
        ```powershell
appcmd Recycle AppPool MSExchangeRpcProxyFrontEndAppPool
```
    
      - 使用 Windows PowerShell cmdlet 键入以下命令，然后按 Enter 键。
        
        ```powershell
IIS:\>Restart-WebAppPool MSExchangeRpcProxyFrontEndAppPool
```
    
      - 使用命令行：转到“开始”\>“运行”，键入“cmd”，然后按 Enter 键。在命令提示符窗口中，键入以下命令，然后按 Enter 键。
        
        ```powershell
iisreset /noforce
```
    
      - 使用 Internet 信息服务 (IIS) 管理器：在 Internet 信息服务 (IIS) 管理器的“操作”窗格中，单击“重新启动”。

> [!IMPORTANT]  
> 您必须等待服务主机进程将 Active Directory 中的任何更改应用到 Internet 信息服务 (IIS)，间隔为 15 分钟，即使当您在客户端访问服务器上重新启动 IIS 时也是如此。


返回顶部

## 为脱机通讯簿 (OAB) 配置 SSL 卸载

要为脱机通讯簿 (OAB) 启用 SSL 卸载，您需要在“默认网站”上的“OAB”虚拟目录中删除 SSL 要求：

  - **步骤 1**   您可以使用 Internet 信息服务 (IIS) 管理器或命令行在“OAB”虚拟目录上禁用 SSL：
    
      - 使用 Internet 信息服务 (IIS) 管理器，展开“网站”\>“默认网站”，然后选择“OAB”虚拟目录。在结果窗格中的“IIS”下，双击“SSL 设置”。在“SSL 设置”结果窗格中，取消选中“需要 SSL”复选框，然后在“操作”窗格中单击“应用”。
    
      - 使用命令行键入以下命令，然后按 Enter 键。
        
        ```powershell
appcmd set config "Default Web Site/OAB" /section:access /sslFlags:None /commit:APPHOST
```

  - **步骤 2**   您需要使用以下方法之一回收相应的应用程序池或重新启动 Internet 信息服务：
    
      - 使用命令行：转到“开始”\>“运行”，键入“cmd”，然后按 Enter 键。在命令提示符窗口中，键入以下命令，然后按 Enter 键。
        
        ```powershell
appcmd Recycle AppPool MSExchangeOABAppPool
```
    
      - 使用 Windows PowerShell cmdlet 键入以下命令，然后按 Enter 键。
        
        ```powershell
IIS:\>Restart-WebAppPool MSExchangeOABAppPool
```
    
      - 使用命令行：转到“开始”\>“运行”，键入“cmd”，然后按 Enter 键。在命令提示符窗口中，键入以下命令，然后按 Enter 键。
        
        ```powershell
iisreset /noforce
```
    
      - 使用 Internet 信息服务 (IIS) 管理器：在 Internet 信息服务 (IIS) 管理器的“操作”窗格中，单击“重新启动”。

返回顶部

## 为 Exchange ActiveSync (EA) 配置 SSL 卸载

要为 Exchange ActiveSync (EAS) 启用 SSL 卸载，您需要在“默认网站”上的“Microsoft-Server-ActiveSync”虚拟目录中删除 SSL 要求：

  - **步骤 1**   您可以使用 Internet 信息服务 (IIS) 管理器或命令行在“Microsoft-Server-ActiveSync”虚拟目录上禁用 SSL：
    
      - 使用 Internet 信息服务 (IIS) 管理器，展开“网站”\>“默认网站”，然后选择“Microsoft-Server-ActiveSync”虚拟目录。在结果窗格中的“IIS”下，双击“SSL 设置”。在“SSL 设置”结果窗格中，取消选中“需要 SSL”复选框，然后在“操作”窗格中单击“应用”。
    
      - 使用命令行键入以下命令，然后按 Enter 键。
        
            appcmd set config "Default Web Site/MSExchangeSyncAppPool" /section:access /sslFlags:None /commit:APPHOST

  - **步骤 2**   您需要使用以下方法之一回收相应的应用程序池或重新启动 Internet 信息服务：
    
      - 使用命令行：转到“开始”\>“运行”，键入“cmd”，然后按 Enter 键。在命令提示符窗口中，键入以下命令，然后按 Enter 键。
        
        ```powershell
appcmd Recycle AppPool MSExchangeSyncAppPool
```
    
      - 使用 Windows PowerShell cmdlet 键入以下命令，然后按 Enter 键。
        
        ```powershell
IIS:\>Restart-WebAppPool MSExchangeSyncAppPool
```
    
      - 使用命令行：转到“开始”\>“运行”，键入“cmd”，然后按 Enter 键。在命令提示符窗口中，键入以下命令，然后按 Enter 键。
        
        ```powershell
iisreset /noforce
```
    
      - 使用 Internet 信息服务 (IIS) 管理器：在 Internet 信息服务 (IIS) 管理器的“操作”窗格中，单击“重新启动”。

返回顶部

## 为 Exchange Web 服务 (EWS) 配置 SSL 卸载

要为 Exchange Web 服务 (EWS) 启用 SSL 卸载，您需要在“默认网站”上的“EWS”虚拟目录中删除 SSL 要求：

  - **步骤 1**   您可以使用 Internet 信息服务 (IIS) 管理器或命令行在“EWS”虚拟目录上禁用 SSL：
    
      - 使用 Internet 信息服务 (IIS) 管理器，展开“网站”\>“默认网站”，然后选择“EWS”虚拟目录。在结果窗格中的“IIS”下，双击“SSL 设置”。在“SSL 设置”结果窗格中，取消选中“需要 SSL”复选框，然后在“操作”窗格中单击“应用”。
    
      - 使用命令行键入以下命令，然后按 Enter 键。
        
        ```powershell
appcmd set config "Default Web Site/EWS" /section:access /sslFlags:None /commit:APPHOST
```

  - **步骤 2**   您需要使用以下方法之一回收相应的应用程序池或重新启动 Internet 信息服务：
    
      - 使用命令行：转到“开始”\>“运行”，键入“cmd”，然后按 Enter 键。在命令提示符窗口中，键入以下命令，然后按 Enter 键。
        
        ```powershell
appcmd Recycle AppPool MSExchangeServicesAppPool
```
    
      - 使用 Windows PowerShell cmdlet 键入以下命令，然后按 Enter 键。
        
        ```powershell
IIS:\>Restart-WebAppPool MSExchangeServicesAppPool
```
    
      - 使用命令行：转到“开始”\>“运行”，键入“cmd”，然后按 Enter 键。在命令提示符窗口中，键入以下命令，然后按 Enter 键。
        
        ```powershell
iisreset /noforce
```
    
      - 使用 Internet 信息服务 (IIS) 管理器：在 Internet 信息服务 (IIS) 管理器的“操作”窗格中，单击“重新启动”。

返回顶部

## 为自动发现服务配置 SSL 卸载

要为自动发现服务启用 SSL 卸载，您需要在“默认网站”上的“Autodiscover”虚拟目录中删除 SSL 要求：

  - **步骤 1**   您可以使用 Internet 信息服务 (IIS) 管理器或命令行在“Autodiscover”虚拟目录上禁用 SSL：
    
      - 使用 Internet 信息服务 (IIS) 管理器，展开“网站”\>“默认网站”，然后选择“Autodiscover”虚拟目录。在结果窗格中的“IIS”下，双击“SSL 设置”。在“SSL 设置”结果窗格中，取消选中“需要 SSL”复选框，然后在“操作”窗格中单击“应用”。
    
      - 使用命令行键入以下命令，然后按 Enter 键。
        
        ```powershell
appcmd set config "Default Web Site/autodiscover" /section:access /sslFlags:None /commit:APPHOST
```

  - **步骤 2**   您需要使用以下方法之一回收相应的应用程序池或重新启动 Internet 信息服务：
    
      - 使用命令行：转到“开始”\>“运行”，键入“cmd”，然后按 Enter 键。在命令提示符窗口中，键入以下命令，然后按 Enter 键。
        
        ```powershell
appcmd Recycle AppPool MSExchangeAutodiscoverAppPool
```
    
      - 使用 Windows PowerShell cmdlet 键入以下命令，然后按 Enter 键。
        
        ```powershell
IIS:\>Restart-WebAppPool MSExchangeAutodiscoverAppPool
```
    
      - 使用命令行：转到“开始”\>“运行”，键入“cmd”，然后按 Enter 键。在命令提示符窗口中，键入以下命令，然后按 Enter 键。
        
        ```powershell
iisreset /noforce
```
    
      - 使用 Internet 信息服务 (IIS) 管理器：在 Internet 信息服务 (IIS) 管理器的“操作”窗格中，单击“重新启动”。

返回顶部

## 为邮箱复制代理服务 (MRSProxy) 配置 SSL 卸载

在每个 Exchange 2013 客户端访问服务器上安装邮箱复制代理 (MRSProxy) 服务。MRSProxy 可帮助你在本地环境中发出跨林移动请求，以及将本地邮箱移动到 Office 365。但是默认情况下，MRSProxy 为禁用状态。如果要启用 MRSProxy，应在远程 Exchange 林中启用以进行跨林本地邮箱移动，或在本地 Exchange 林中启用以将邮箱移动到 Office 365。尽管 MRSProxy 服务在 Exchange Web 服务 (EWS) 下运行，但它不支持配置 SSL 卸载。

其原因是 MRSProxy 服务希望对通信进行签名/加密。任何硬件负载平衡器或防火墙都必须重新加密 MRSProxy 通信，然后再将其发送到客户端访问服务器。在这种情况下，建议您配置 SSL 桥接以使卸载正常运行。

**反向 SSL 或 SSL 桥接**   如果在硬件负载平衡器上启用反向 SSL 或 SSL 桥接，则无需在每台 CAS 服务器上执行上述步骤。但是，在硬件负载平衡器上启用反向 SSL 意味着 SSL 加密和解密都在客户端访问服务器上执行。在这种情况下，SSL 加密和解密将在硬件负载平衡器和客户端访问服务器上执行。选择使用 Exchange 2013 SSL 卸载还是反向 SSL（SSL 桥接）取决于组织目标和必须实施的安全实践。下图显示启用了 SSL 桥接（反向 SSL）的客户端连接。

![SSL 桥接](images/Dn635115.a08aacc1-0ab4-46b3-bdae-b9518a3f5748(EXCHG.150).jpg "SSL 桥接")

## 为 Outlook 客户端（MAPI 虚拟目录）配置 SSL 卸载

要为 Outlook 客户端用 SSL 卸载，您需要在“默认网站”上的“MAPI”虚拟目录中删除 SSL 要求：

  - **步骤 1**   您可以使用 Internet 信息服务 (IIS) 管理器或命令行在“MAPI”虚拟目录上禁用 SSL：
    
      - 使用 Internet 信息服务 (IIS) 管理器，展开“网站”\>“默认网站”，然后选择“MAPI”虚拟目录。在结果窗格中的“IIS”下，双击“SSL 设置”。在“SSL 设置”结果窗格中，取消选中“需要 SSL”复选框，然后在“操作”窗格中单击“应用”。
    
      - 使用命令行键入以下命令，然后按 Enter 键。
        
        ```powershell
appcmd set config "Default Web Site/MAPI" /section:access /sslFlags:None /commit:APPHOST
```

  - **步骤 2**   您需要使用以下方法之一回收相应的应用程序池或重新启动 Internet 信息服务：
    
      - 使用命令行：转到“开始”\>“运行”，键入“cmd”，然后按 Enter 键。在命令提示符窗口中，键入以下命令，然后按 Enter 键。
        
        ```powershell
appcmd Recycle AppPool MSExchangeMapiFrontEndAppPool
```
    
      - 使用 Windows PowerShell cmdlet 键入以下命令，然后按 Enter 键。
        
        ```powershell
IIS:\>Restart-WebAppPool MSExchangeMapiFrontEndAppPool
```
    
      - 使用命令行：转到“开始”\>“运行”，键入“cmd”，然后按 Enter 键。在命令提示符窗口中，键入以下命令，然后按 Enter 键。
        
        ```powershell
iisreset /noforce
```
    
      - 使用 Internet 信息服务 (IIS) 管理器：在 Internet 信息服务 (IIS) 管理器的“操作”窗格中，单击“重新启动”。

返回顶部

## 使用脚本为所有协议和服务启用 SSL 卸载

如果您在具有多台 Exchange 2013 客户端访问服务器的大型组织中工作，您可能希望加速已执行的前述步骤。您可以复制以下脚本中的命令并粘贴到记事本中，进行任何更改，使用 .ps1 扩展名保存文件，然后从 Exchange 命令行管理程序运行该文件。根据您的需要，可以使用两个脚本为单个或多个客户端访问服务器的所有协议和服务配置 SSL 卸载。

> [!NOTE]  
> 对于 <strong>Set-OutlookAnywhere</strong> cmdlet 条目，将“MyServer”替换为客户端访问服务器的名称。


**使用 Set-WebConfigurationProperty**

    Set-OutlookAnywhere -Identity MyServer\Rpc* -Externalhostname MyServer.mail.contoso.com -ExternalClientsRequireSsl $True -ExternalClientAuthenticationMethod Basic
    Set-OutlookAnywhere -Identity MyServer\Rpc* -SSLOffloading $true
    Set-WebConfigurationProperty -Filter //security/access -name sslflags -Value "None" -PSPath IIS:  -Location "Default Web Site/OWA"
    Set-WebConfigurationProperty -Filter //security/access -name sslflags -Value "None" -PSPath IIS: -Location "Default Web Site/ecp"
    Set-WebConfigurationProperty -Filter //security/access -name sslflags -Value "None" -PSPath IIS: -Location "Default Web Site/EWS"
    Set-WebConfigurationProperty -Filter //security/access -name sslflags -Value "None" -PSPath IIS: -Location "Default Web Site/Autodiscover"
    Set-WebConfigurationProperty -Filter //security/access -name sslflags -Value "None" -PSPath IIS: -Location "Default Web Site/Microsoft-Server-ActiveSync"
    Set-WebConfigurationProperty -Filter //security/access -name sslflags -Value "None" -PSPath IIS: -Location "Default Web Site/OAB"
    Set-WebConfigurationProperty -Filter //security/access -name sslflags -Value "None" -PSPath IIS: -Location "Default Web Site/MAPI"
```powershell
iisreset /noforce
```

**使用 appcmd**

> [!NOTE]  
> 对于 <strong>Set-OutlookAnywhere</strong> cmdlet 条目，将“MyServer”替换为客户端访问服务器的名称。


    Set-OutlookAnywhere -Identity MyServer\Rpc* -Externalhostname MyServer.mail.contoso.com -ExternalClientsRequireSsl $True -ExternalClientAuthenticationMethod Basic
    Set-OutlookAnywhere -Identity MyServer\Rpc* -SSLOffloading $true
    &$env:systemroot\system32\inetsrv\appcmd set config "Default Web Site/owa" /section:access /sslFlags:None /commit:APPHOST
    &$env:systemroot\system32\inetsrv\appcmd set config "Default Web Site/ecp" /section:access /sslFlags:None /commit:APPHOST
    &$env:systemroot\system32\inetsrv\appcmd set config "Default Web Site/EWS" /section:access /sslFlags:None /commit:APPHOST
    &$env:systemroot\system32\inetsrv\appcmd set config "Default Web Site/Autodiscover" /section:access /sslFlags:None /commit:APPHOST
    &$env:systemroot\system32\inetsrv\appcmd set config "Default Web Site/Microsoft-Server-ActiveSync" /section:access /sslFlags:None /commit:APPHOST
    &$env:systemroot\system32\inetsrv\appcmd set config "Default Web Site/OAB" /section:access /sslFlags:None /commit:APPHOST
    &$env:systemroot\system32\inetsrv\appcmd set config "Default Web Site/MAPI" /section:access /sslFlags:None /commit:APPHOST
```powershell
iisreset /noforce
```

返回顶部

## 配置与 Exchange 2007 和 Exchange 2010 共存

在组织中混合使用 Exchange 2003 和 Exchange 2010 服务器的共存场景中，部署 Exchange 2010 客户端访问服务器后需执行的首要步骤之一是更改 DNS，以便 Exchange 2003 用户可以从一组 Exchange 2010 客户端访问服务器访问邮箱。在此类场景中，用于在客户端访问服务器之间分配客户端流量的负载平衡器上完全支持启用 SSL 卸载。

**与其他版本的 Outlook Web App 共存**

当在 Exchange 2013 客户端访问服务器上配置 SSL 卸载时，共存适用于 Exchange 2007 和 Exchange 2010：

  - 要与 Exchange 2007 共存，需要早期的命名空间，仅对 Outlook Web App 和 Exchange Web 服务才会进行重定向。自动发现、Outlook 无处不在 和 Exchange ActiveSync 将通过代理转移至早期版本。

  - 如果您已设置外部 URL，要与 Exchange 2010 共存，将使用重定向，否则将使用代理。

返回顶部

