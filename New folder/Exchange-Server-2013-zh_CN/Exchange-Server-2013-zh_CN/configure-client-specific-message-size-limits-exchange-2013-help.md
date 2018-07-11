---
title: '配置客户端特定的邮件大小限制: Exchange 2013 Help'
TOCTitle: 配置客户端特定的邮件大小限制
ms:assetid: fef9ca78-b68f-4342-ada0-881ab985ce3c
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Hh529949(v=EXCHG.150)
ms:contentKeyID: 52061579
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 配置客户端特定的邮件大小限制

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2017-01-26_

在 Microsoft Exchange Server 2013 中，当邮件通过 Exchange 组织时，会应用多种不同的邮件大小限制。有关详细信息，请参阅[邮件大小限制](message-size-limits-exchange-2013-help.md)。

但是，你可以为使用 ActiveSync 或 Exchange Web 服务 (EWS) 的 Outlook Web App 和电子邮件客户端配置客户端特定的邮件大小限制。如果更改 Exchange 组织范围内的邮件大小限制，需要验证 Outlook Web App、ActiveSync 以及 Exchange Web 服务是否都相应地设置了邮件大小限制。在客户端访问服务器和邮箱服务器上的 web.config 文件中配置这些值。下表介绍了这些限制。

### ActiveSync

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>服务器角色</th>
<th>配置文件</th>
<th>键和默认值</th>
<th>大小</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>客户端访问</p></td>
<td><p><code>%ExchangeInstallPath%FrontEnd\HttpProxy\Sync\web.config</code></p></td>
<td><p><code>maxAllowedContentLength=&quot;30000000 bytes&quot;</code>   默认情况下不存在（请参阅注释）。</p></td>
<td><p>字节</p></td>
</tr>
<tr class="even">
<td><p>客户端访问</p></td>
<td><p><code>%ExchangeInstallPath%FrontEnd\HttpProxy\Sync\web.config</code></p></td>
<td><p><code>maxRequestLength=&quot;10240&quot;</code></p></td>
<td><p>千字节</p></td>
</tr>
<tr class="odd">
<td><p>邮箱</p></td>
<td><p><code>%ExchangeInstallPath%ClientAccess\Sync\web.config</code></p></td>
<td><p><code>maxAllowedContentLength=&quot;30000000 bytes&quot;</code>   默认情况下不存在（请参阅注释）。</p></td>
<td><p>字节</p></td>
</tr>
<tr class="even">
<td><p>邮箱</p></td>
<td><p><code>%ExchangeInstallPath%ClientAccess\Sync\web.config</code></p></td>
<td><p><code>maxRequestLength=&quot;10240&quot;</code></p></td>
<td><p>千字节</p></td>
</tr>
<tr class="odd">
<td><p>邮箱</p></td>
<td><p><code>%ExchangeInstallPath%ClientAccess\Sync\web.config</code></p></td>
<td><p><code>&lt;add key=&quot;MaxDocumentDataSize&quot; value=&quot;10240000&quot;&gt;</code></p></td>
<td><p>字节</p></td>
</tr>
</tbody>
</table>


**对 ActiveSync 限制的说明**

默认情况下，ActiveSync 的 `web.config` 文件中没有任何 *maxAllowedContentLength* 注册表项。但是，ActiveSync 的最大邮件大小会受到应用于服务器上所有网站的 **maxAllowedContentLength** 值的影响。默认值为 30000000 字节 (30 MB)。若要在 IIS 管理器中查看客户端访问服务器和邮箱服务器上用于 ActiveSync 的这些值，请执行以下步骤：

1.  采取以下步骤之一：
    
      - 在客户端访问服务器上，打开“IIS 管理器”，导航到“网站”\>“默认网站”，并选择“Microsoft-Server-ActiveSync”。
    
      - 在邮箱服务器上，打“IIS 管理器”，导航到“网站”\>“Exchange 后端”，并选择“Microsoft-Server-ActiveSync”。

2.  验证“功能视图”是否已选中，然后双击“管理”部分中的“配置编辑器”。

3.  单击“部分”字段中的下拉箭头，导航到“system.webServer”\>“安全”，并选择“requestFiltering”。

4.  在结果中，展开“requestLimits”，您将看到“maxAllowedContentLength”和默认值 30000000（字节）。

若要更改 **maxAllowedContentLength** 值，请输入以字节为单位的新值，并单击“应用”。您需要在客户端访问服务器和邮箱服务器上更改值。在 IIS 管理器中更改值以后，新的 *maxAllowedContentLength* 注册表项就会写入到相应的 `web.config` 文件（客户端访问服务器上为 `%ExchangeInstallPath%FrontEnd\HttpProxy\Sync\web.config`，邮箱服务器上为 `%ExchangeInstallPath%ClientAccess\Sync\web.config`）。

若要更改 ActiveSync 客户端的最大邮件大小，您需要在客户端访问服务器和邮箱服务器上更改 `web.config` 文件中的 *maxRequestLength* 值，在邮箱服务器上更改 `web.config` 文件中的 *MaxDocumentDataSize* 值，并在客户端访问服务器和邮箱服务器上更改 IIS 管理器中的 *maxAllowedContentLength* 值。

### Exchange Web 服务

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>服务角色</th>
<th>配置文件</th>
<th>键和默认值</th>
<th>大小</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>客户端访问</p></td>
<td><p><code>%ExchangeInstallPath%FrontEnd\HttpProxy\ews\web.config</code></p></td>
<td><p><code>maxAllowedContentLength=&quot;67108864&quot;</code></p></td>
<td><p>字节</p></td>
</tr>
<tr class="even">
<td><p>邮箱</p></td>
<td><p><code>%ExchangeInstallPath%ClientAccess\exchweb\ews\web.config</code></p></td>
<td><p><code>maxAllowedContentLength=&quot;67108864&quot;</code></p></td>
<td><p>字节</p></td>
</tr>
<tr class="odd">
<td><p>邮箱</p></td>
<td><p><code>%ExchangeInstallPath%ClientAccess\exchweb\ews\web.config</code></p></td>
<td><p>14 个 <code>maxReceivedMessageSize=&quot;67108864&quot;</code> 实例</p></td>
<td><p>字节</p></td>
</tr>
</tbody>
</table>


**对 Exchange Web 服务限制的说明**

  - `maxReceivedMessageSize="67108864"` 值有 14 个单独的实例，对应绑定（http 和 https）和身份验证方法的不同组合。

  - 若要更改 Exchange Web 服务客户端的最大邮件大小，您需要在邮箱服务器上更改 `web.config` 文件以及 `web.config` 文件中 `maxReceivedMessageSize="67108864"` 的所有 14 个实例的 *maxAllowedContentLength* 值。

  - 在邮箱服务器的 `web.config` 文件中，也有 `maxReceivedMessageSize="1048576"` 值的两个实例，该值用于不需要修改的 **UMLegacyMessageEncoderSoap11Element** 绑定。

  - *maxRequestLength* 是这两个 web.config 文件中的 ASP.NET 设置，但不用于 Exchange Web 服务，因此您无需对其进行修改。

### Outlook Web App

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>服务器角色</th>
<th>配置文件</th>
<th>键和默认值</th>
<th>大小</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>客户端访问</p></td>
<td><p><code>%ExchangeInstallPath%FrontEnd\HttpProxy\owa\web.config</code></p></td>
<td><p><code>maxAllowedContentLength=&quot;35000000&quot;</code></p></td>
<td><p>字节</p></td>
</tr>
<tr class="even">
<td><p>客户端访问</p></td>
<td><p><code>%ExchangeInstallPath%FrontEnd\HttpProxy\owa\web.config</code></p></td>
<td><p><code>maxRequestLength=&quot;35000&quot;</code></p></td>
<td><p>千字节</p></td>
</tr>
<tr class="odd">
<td><p>邮箱</p></td>
<td><p><code>%ExchangeInstallPath%ClientAccess\Owa\web.config</code></p></td>
<td><p><code>maxAllowedContentLength=&quot;35000000&quot;</code></p></td>
<td><p>字节</p></td>
</tr>
<tr class="even">
<td><p>邮箱</p></td>
<td><p><code>%ExchangeInstallPath%ClientAccess\Owa\web.config</code></p></td>
<td><p><code>maxRequestLength=&quot;35000&quot;</code></p></td>
<td><p>千字节</p></td>
</tr>
<tr class="odd">
<td><p>邮箱</p></td>
<td><p><code>%ExchangeInstallPath%ClientAccess\Owa\web.config</code></p></td>
<td><p>2 个 <code>maxReceivedMessageSize=&quot;35000000&quot;</code> 实例</p></td>
<td><p>字节</p></td>
</tr>
<tr class="even">
<td><p>邮箱</p></td>
<td><p><code>%ExchangeInstallPath%ClientAccess\Owa\web.config</code></p></td>
<td><p>2 个 <code>maxStringContentLength=&quot;35000000&quot;</code> 实例</p></td>
<td><p>字节</p></td>
</tr>
</tbody>
</table>


**对 Outlook Web App 限制的说明**

  - 在邮箱服务器上的 `web.config` 文件中，`maxReceivedMessageSize="35000000"` 和 `maxStringContentLength="35000000"` 值有两个单独实例，对应于 http 和 https 绑定。

  - 若要更改 Outlook Web App 客户端的最大邮件大小，您需要更改两个文件中的所有这些值，包括邮箱服务器的 `web.config` 文件中 *maxReceivedMessageSize* 和 *maxStringContentLength* 的两个实例。

  - 在邮箱服务器上的 `web.config` 文件中，还有一个不需要进行修改的 **MsOnlineShellService** 绑定所对应的 `maxStringContentLength="102400"` 值的实例。

对于所有邮件大小限制，需要将值设置为大于想要强制应用的实际大小。邮件附件和任意其他二进制数据经过 Base64 编码后，邮件大小必然会增加，因此，这种数值上的增加是必要的。Base64 编码会使邮件大小增加约 33%，因此为任何邮件大小限制指定的值要比实际可以使用的邮件大小大约高出 33%。例如，如果指定邮件大小的最大值为 64 MB，则可以预计实际邮件大小的最大值约为 48 MB。

## 在开始之前，您需要知道什么？

  - 估计完成时间：15 分钟

  - Exchange 权限不适用于本主题中的过程。这些过程在 Exchange Server 的操作系统中执行。

  - 保存的 Web.config 配置文件更改在重新启动 IIS 后应用。

  - 考虑到因 Base64 编码导致的 33% 的大小增长，请将所需的新最大大小值 (MB) 乘以 4/3。要将该值转换成 KB，乘以 1024。要将该值转换成字节，则乘以 1048756 (1024\*1024)。请注意，Base64 编码导致的大小增长可能会大于 33%，这取决于多种因素，例如，附件文件的大小、类型、压缩和用于撰写和发送邮件的电子邮件客户端。

  - 在您安装 Exchange 累积更新 (CU) 时，您在 Exchange XML 应用程序配置文件（例如，客户端访问服务器上的 web.config 文件，或邮箱服务器上的 EdgeTransport.exe.config 文件）中针对每个服务器所做的任何自定义设置都将被覆盖。请务必保存此类信息，以便在安装累积更新后，您可以轻松地重新配置服务器。安装 Exchange CU 后，您必须重新配置这些设置。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!tip]
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 使用记事本配置客户端特定的邮件大小限制

1.  在记事本中打开相应的 web.config 文件。例如，要打开 Exchange Web 服务 客户端的 web.config 文件，运行以下命令：
    
        Notepad %ExchangeInstallPath%ClientAccess\exchweb\ews\web.config
        Notepad %ExchangeInstallPath%FrontEnd\HttpProxy\ews\web.config

2.  查找本主题前面的表格介绍的相应 web.config 文件中的相关注册表项。例如，对于 Exchange Web 服务 客户端，在邮箱服务器上找到两个文件中的 *maxAllowedContentLength* 项和 `web.config` 文件中 `maxReceivedMessageSize="67108864"` 值的所有 14 个实例。
    
        <requestLimits maxAllowedContentLength="67108864" />
        ...maxReceivedMessageSize="67108864"...
    
    例如，若要允许经过 Base64 编码的邮件的大小上限约为 64MB，您可以将 `67108864` 的所有实例更改为 `89478486` (64\*4/3\*1048756)：
    
        <requestLimits maxAllowedContentLength="89478486" />
        ...maxReceivedMessageSize="89478486"...

3.  完成后，保存并关闭 web.config 文件。

4.  运行以下命令重新启动 IIS：
    
        IISReset /noforce

## 配置命令行中客户端特定的邮件大小限制

如果不使用记事本，还可以配置命令行中客户端特定的邮件大小限制。打开 Exchange 服务器上提升的命令提示符（通过选择“**以管理员身份运行**”打开一个命令提示符窗口）并为要配置的限制运行相应命令。

**注意：** 

  - 命令中的大小值为默认值，可能需要对其进行更改。

  - 请注意值的单位是字节还是千字节。

**ActiveSync**

    %windir%\system32\inetsrv\appcmd.exe set config "Default Web Site/Microsoft-Server-ActiveSync/" -section:system.webServer/security/requestFiltering /requestLimits.maxAllowedContentLength:30000000
    %windir%\system32\inetsrv\appcmd.exe set config "Default Web Site/Microsoft-Server-ActiveSync/" -section:system.web/httpRuntime /maxRequestLength:10240
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/Microsoft-Server-ActiveSync/" -section:system.webServer/security/requestFiltering /requestLimits.maxAllowedContentLength:30000000
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/Microsoft-Server-ActiveSync/" -section:system.web/httpRuntime /maxRequestLength:10240
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/Microsoft-Server-ActiveSync/" -section:appSettings /[key='MaxDocumentDataSize'].value:10240000

**Exchange Web 服务**

    %windir%\system32\inetsrv\appcmd.exe set config "Default Web Site/ews/" -section:system.webServer/security/requestFiltering /requestLimits.maxAllowedContentLength:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.webServer/security/requestFiltering /requestLimits.maxAllowedContentLength:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSAnonymousHttpsBinding'].httpsTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSAnonymousHttpBinding'].httpTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSBasicHttpsBinding'].httpsTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSBasicHttpBinding'].httpTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSNegotiateHttpsBinding'].httpsTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSNegotiateHttpBinding'].httpTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSWSSecurityHttpsBinding'].httpsTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSWSSecurityHttpBinding'].httpTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSWSSecuritySymmetricKeyHttpsBinding'].httpsTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSWSSecuritySymmetricKeyHttpBinding'].httpTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSWSSecurityX509CertHttpsBinding'].httpsTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSWSSecurityX509CertHttpBinding'].httpTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /webHttpBinding.[name='EWSStreamingNegotiateHttpsBinding'].maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /webHttpBinding.[name='EWSStreamingNegotiateHttpBinding'].maxReceivedMessageSize:67108864

**Outlook Web App**

    %windir%\system32\inetsrv\appcmd.exe set config "Default Web Site/owa/" -section:system.webServer/security/requestFiltering /requestLimits.maxAllowedContentLength:35000000
    %windir%\system32\inetsrv\appcmd.exe set config "Default Web Site/owa/" -section:system.web/httpRuntime /maxRequestLength:35000
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/owa/" -section:system.webServer/security/requestFiltering /requestLimits.maxAllowedContentLength:35000000
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/owa/" -section:system.web/httpRuntime /maxRequestLength:35000
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/owa/" -section:system.serviceModel/bindings /webHttpBinding.[name='httpsBinding'].maxReceivedMessageSize:35000000
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/owa/" -section:system.serviceModel/bindings /webHttpBinding.[name='httpBinding'].maxReceivedMessageSize:35000000
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/owa/" -section:system.serviceModel/bindings /webHttpBinding.[name='httpsBinding'].readerQuotas.maxStringContentLength:35000000
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/owa/" -section:system.serviceModel/bindings /webHttpBinding.[name='httpBinding'].readerQuotas.maxStringContentLength:35000000

## 您如何知道操作成功？

若要验证是否已成功配置客户端特定的邮件大小限制，您需要在受影响的客户端访问的邮箱上发送和接收测试邮件。可以尝试添加一些更小的附件或一个大的附件，以使测试邮件的大小比配置的值约小 33%。例如，如果配置的值为 85 MB，则实际邮件的最大大小约为 64 MB。

