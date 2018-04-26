---
title: 解决 OWA.Protocol.Dep 运行状况设置的问题
TOCTitle: 解决 OWA.Protocol.Dep 运行状况设置的问题
ms:assetid: f39c63d5-f161-4eee-9415-05f3355e7cc7
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/ms.exch.scom.owa.protocol.dep(v=EXCHG.150)
ms:contentKeyID: 54652359
ms.date: 01/08/2016
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 解决 OWA.Protocol.Dep 运行状况设置的问题

 

_**适用于：**Exchange Server 2013, Project Server 2013_

_**上一次修改主题：**2015-11-10_

**OWA.Protocol.DEP** 运行状况设置监视在 Lync 2013 和 Exchange 2013 之间集成的 Outlook Web App 中的即时消息 (IM) 服务的整体运行状况。有关在 Outlook Web App 中启用即时消息的详细信息，请参阅[集成 Microsoft Lync Server 2013 和 Microsoft Outlook Web App 2013](http://go.microsoft.com/fwlink/p/?linkid=280418)。

如果您收到一条警报，指示 **OWA.Protocol.DEP** 运行状况设置不正常，这表示存在可能阻止即时消息在 Outlook Web App 中正常运行的问题。

## 说明

使用下列探测器和监视器监视 **OWA.Protocol.DEP** 服务。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>探测器</th>
<th>运行状况设置</th>
<th>关联监视器</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>无（通知或检查）</p></td>
<td><p>OWA.Protocol.DEP</p></td>
<td><p>OwaIMInitializationFailedMonitor</p></td>
</tr>
<tr class="even">
<td><p>无（通知或检查）</p></td>
<td><p>OWA.Protocol.DEP</p></td>
<td><p>WacDiscoveryFailureEventMonitor</p></td>
</tr>
</tbody>
</table>


有关探测器和监视器的详细信息，请参阅[服务器运行状况和性能](https://technet.microsoft.com/zh-cn/library/jj150551\(v=exchg.150\))。

## 用户操作

发出警报后服务可能会恢复。因此，当您收到指定 **OWA.Protocol.DEP** 运行状况设置不正常的警报时，请首先验证问题是否仍存在。若问题确实存在，执行以下部分介绍的相应恢复操作。

## 错误的恢复操作：“InstantMessageOCSProvider.InitializeEndpointManager。IM 提供程序没有注册表设置。”

此错误表明邮箱服务器上缺少必需的注册表项。在服务器上安装 Microsoft 统一通信托管 API (UCMA) 4.0 时，此注册表项应该已配置。缺少的注册表项为：

    HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\services\MSExchange OWA\InstantMessaging

此注册表项中应包含指向 `Microsoft.Rtc.Internal.Ucweb` DLL 的 **ImplementationDLLPath** 字符串。默认位置为 `C:\Program Files\Microsoft UCMA 4.0\Runtime\SSP\Microsoft.Rtc.Internal.Ucweb.dll`。

若要修复此问题，请重新安装 UCMA 4.0，或手动创建注册表项。您可以在此处下载 UCMA 4.0：[统一通信托管 API 4.0 运行时](http://go.microsoft.com/fwlink/p/?linkid=260990)。

## 错误的恢复操作：“InstantMessageOCSProvider.InitializeEndpointManager。未找到 IM 提供程序。”

此错误指示邮箱服务器上缺少 `Microsoft.Rtc.Internal.Ucweb` DLL 文件。在服务器上安装 UCMA 4.0 时，此文件应该已安装。默认位置为 `C:\Program Files\Microsoft UCMA 4.0\Runtime\SSP`。

若要解决此问题，请重新安装 UCMA 4.0。有关详细信息，请参阅[统一通信托管 API 4.0 运行时](http://go.microsoft.com/fwlink/p/?linkid=260990)。

## 错误的恢复操作：“在 web.config 上，即时消息服务器的名称设置为 null 或为空。”

此错误指示邮箱服务器上的 Outlook Web App 应用程序配置 (web.config) 文件中未定义 Lync 2013 服务器。此 `web.config` 文件位于 `%ExchangeInstallPath%ClientAccess\Owa`，其中应该包含一个名为 **IMServerName** 的注册表项，该注册表项指定 Lync 2013 服务器的 FQDN。要解决此问题，请执行下列步骤：

1.  在命令提示符窗口中，通过运行以下命令使用记事本打开 Outlook Web App web.config 文件：
    
        Notepad %ExchangeInstallPath%ClientAccess\Owa\web.config

2.  搜索名为 **IMServerName** 的注册表项。如果找到，验证 Lync 2013 服务器的 FQDN。如果找不到该注册表项，请执行以下步骤进行添加。
    
    1.  查找名为 **\<appSettings\>** 的标记。
    
    2.  在 **\<appSettings\>** 节点中，添加以下行：
        
            <add key="IMServerName" value="Lync Server FQDN" />
        
        例如：
        
            <add key="IMServerName" value="lync01.contoso.com" />
    
    3.  若要在 Outlook Web App 中应用更改，请运行以下命令：
        
            %windir%\system32\inetsrv\appcmd.exe recycle apppool /apppool.name:"MSExchangeOWAAppPool"

## 错误的恢复操作：“在 web.config 上，即时消息证书指纹为 null 或为空。”

此错误指示邮箱服务器上的 Outlook Web App 应用程序配置 (web.config) 文件中未定义用于集成 Lync 2013 和 Outlook Web App 的证书。此 `web.config` 文件位于 `%ExchangeInstallPath%ClientAccess\Owa`，其中应该包含一个名为 **IMCertificateThumbprint** 的注册表项，该注册表项指定证书的指纹（哈希）。

您可以通过使用 **Get-ExchangeCertificate** cmdlet，或在“服务器”\>“证书”的 Exchange 管理中心 (EAC) 中获取证书的指纹值。

要解决此问题，请执行下列步骤：

1.  在命令提示符窗口中，通过运行以下命令使用记事本打开 Outlook Web App web.config 文件：
    
        Notepad %ExchangeInstallPath%ClientAccess\Owa\web.config

2.  搜索名为 **IMCertificateThumbprint** 的注册表项。如果找到，则验证指纹值是否正确。如果找不到该注册表项，请执行以下步骤进行添加：
    
    1.  查找名为 **\<appSection\>** 的标记。
    
    2.  在 **\<appSection\>** 节点中，添加以下行：
        
            <add key="IMCertificateThumbprint" value="thumbprint"/>
        
        例如：
        
            <add key="IMCertificateThumbprint" value="35CB4C441D55506C88E59B7946B567A4F45B3B5C" />
    
    3.  若要在 Outlook Web App 中应用更改，请运行以下命令：
        
            %windir%\system32\inetsrv\appcmd.exe recycle apppool /apppool.name:"MSExchangeOWAAppPool"

## 错误的恢复操作：“找不到具有指纹 \<值\> 的 IM 证书。”

此错误指示在邮箱服务器上找不到用于集成 Lync 2013 和 Outlook Web App 的证书。此证书必须安装在邮箱服务器和 Lync 2013 服务器上，并且这两个服务器都必须信任该证书。有关证书要求的详细信息，请参阅[集成 Microsoft Lync Server 2013 和 Microsoft Outlook Web App 2013](http://go.microsoft.com/fwlink/p/?linkid=280418) 中 Outlook Web App 部分的“启用即时消息”。

您可以通过使用 **Get-ExchangeCertificate** cmdlet，或在“服务器”\>“证书”的 Exchange 管理中心 (EAC) 中匹配证书的错误指纹值。

## 错误的恢复操作：“IM 证书已过期。”

此错误指示，用于集成 Lync 2013 和 Outlook Web App 的证书已过期。若要解决此错误，您需要续订证书。

您可以通过使用 **Get-ExchangeCertificate** cmdlet，或在“服务器”\>“证书”的 Exchange 管理中心 (EAC) 中匹配证书的错误指纹值。

## 错误的恢复操作：“IM 证书未生效。”

此错误指示，用于集成 Lync 2013 和 Outlook Web App 的证书日期无效。若要解决此错误，您需要配置新证书，并将新的指纹值添加到 `%ExchangeInstallPath%ClientAccess\Owa\web.config` 中的 **IMCertificateThumbprint** 注册表项。有关证书要求的详细信息，请参阅[集成 Microsoft Lync Server 2013 和 Microsoft Outlook Web App 2013](http://go.microsoft.com/fwlink/p/?linkid=280418) 中 Outlook Web App 部分的“启用即时消息”。

## 错误的恢复操作：“IM 证书没有私钥。”

此错误指示，用于集成 Lync 2013 和 Outlook Web App 的证书没有私钥。若要解决此错误，您需要配置具有私钥的新证书，并将新的指纹值添加到 `%ExchangeInstallPath%ClientAccess\Owa\web.config` 中的 **IMCertificateThumbprint** 注册表项。有关证书要求的详细信息，请参阅[集成 Microsoft Lync Server 2013 和 Microsoft Outlook Web App 2013](http://go.microsoft.com/fwlink/p/?linkid=280418) 中 Outlook Web App 部分的“启用即时消息”。

