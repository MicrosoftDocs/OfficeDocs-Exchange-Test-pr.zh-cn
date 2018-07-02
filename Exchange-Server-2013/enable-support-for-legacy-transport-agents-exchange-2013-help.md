---
title: '启用对旧版传输代理的支持: Exchange 2013 Help'
TOCTitle: 启用对旧版传输代理的支持
ms:assetid: 00617e87-7199-406e-b4a3-94378f657f1f
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ591524(v=EXCHG.150)
ms:contentKeyID: 50489817
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 启用对旧版传输代理的支持

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-03-09_

在 Microsoft Exchange Server 2013 中，默认情况下支持使用 Microsoft .NET Framework 版本 4.0 创建的传输代理。Exchange 2013 支持使用以前版本的 .NET Framework 创建的传输代理，但是默认情况下不会启用对这些旧版传输代理的支持。若要启用对旧版传输代理的支持，需要修改相应的 XML 应用程序配置文件。需要修改的文件取决于传输代理的安装位置：


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>服务器</th>
<th>应用程序配置文件</th>
<th>Microsoft Windows 服务</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>客户端访问服务器</p></td>
<td><p>%ExchangeInstallPath%Bin\MSExchangeFrontendTransport.exe.config</p></td>
<td><p>Microsoft Exchange 前端传输 (MSExchangeFrontendTransport)</p></td>
</tr>
<tr class="even">
<td><p>邮箱服务器</p></td>
<td><ul>
<li><p>%ExchangeInstallPath%Bin\EdgeTransport.exe.config</p></li>
<li><p>%ExchangeInstallPath%Bin\MSExchangeTransport.exe.config</p></li>
</ul></td>
<td><p>Microsoft Exchange 传输 (MSExchangeTransport)</p></td>
</tr>
</tbody>
</table>


对旧版传输代理的支持通过应用程序配置文件中的项进行控制。默认情况下，应用程序配置文件中不存在任何必需项。必须手动添加项。下表对每个键进行了详细的说明。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>按键</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>useLegacyV2RuntimeActivationPolicy</em></p></td>
<td><p>此项可启用或禁用对旧版传输代理的支持。此键的有效值为 <code>true</code> 或 <code>false</code>。如果未指定此项，则默认值为 <code>false</code>。</p></td>
</tr>
<tr class="even">
<td><p><em>supportedRuntime version</em></p></td>
<td><p>此项可指定代理所需的 Microsoft .NET Framework 的版本。该关键字的有效值如下：</p>
<ul>
<li><p><code>v4.0</code> 或者 <code>v4.0.30319</code></p></li>
<li><p><code>v3.5</code> 或者 <code>v3.5.21022</code></p></li>
<li><p><code>v3.0</code> 或者 <code>v3.0.4506</code></p></li>
<li><p><code>v2.0</code> 或者 <code>v2.0.50727</code></p></li>
</ul>
<p>可使用 <em>supportedRuntime version</em> 项的多个单独实例指定多个值。</p>
<p>在使用 <em>useLegacyV2RuntimeActivationPolicy</em> 项启用旧版传输代理支持时，除了旧版传输代理所需的值之外，还应始终指定值 <code>v4.0</code>。</p></td>
</tr>
</tbody>
</table>


## 在开始之前，您需要知道什么？

  - 估计完成时间：15 分钟

  - Exchange 权限不适用于本主题中的过程。这些过程在 Exchange Server 的操作系统中执行。

  - 保存到应用程序配置文件中的更改会在重新启动对应服务之后应用。

  - 当重新启动与应用程序配置文件关联的任何服务时，服务器上的邮件流会暂时中断。

  - 在您安装 Exchange 累积更新 (CU) 时，您在 Exchange XML 应用程序配置文件（例如，客户端访问服务器上的 web.config 文件，或邮箱服务器上的 EdgeTransport.exe.config 文件）中针对每个服务器所做的任何自定义设置都将被覆盖。请务必保存此类信息，以便在安装累积更新后，您可以轻松地重新配置服务器。安装 Exchange CU 后，您必须重新配置这些设置。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。</td>
</tr>
</tbody>
</table>


## 使用命令提示符配置对旧版传输代理的支持

使用以下过程可启用对旧版传输代理的支持：

1.  在命令提示符窗口中，在要配置旧版传输代理支持的 Exchange 2013 服务器上，通过运行以下命令在记事本中打开相应的应用程序配置文件：
    
        Notepad %ExchangeInstallPath%Bin\<AppConfigFile>
    
    例如，若要在邮箱服务器上打开 EdgeTransport.exe.config 文件，请运行以下命令：
    
        Notepad %ExchangeInstallPath%Bin\EdgeTransport.exe.config

2.  在文件末尾处找到 *\</configuration\>* 项，然后将以下项粘贴到 *\</configuration\>* 项之前：
    
        <startup useLegacyV2RuntimeActivationPolicy="true">
           <supportedRuntime version="v4.0" />
           <supportedRuntime version="v3.5" />
           <supportedRuntime version="v3.0" />
           <supportedRuntime version="v2.0" />
        </startup>

3.  完成后，保存并关闭应用程序配置文件。

4.  重复步骤 1 到 3 以修改其他应用程序配置文件。

5.  通过运行以下命令重新启动关联的 Windows 服务：
    
        net stop <service> && net start <service>
    
    例如，如果修改了 EdgeTransport.exe.config 文件，则需要通过运行以下命令来重新启动 Microsoft Exchange 传输服务：
    
        net stop MSExchangeTransport && net start MSExchangeTransport

6.  重复步骤 5 以重新启动与其他修改的应用程序配置文件关联的服务。

## 您如何知道这有效？

如果旧版传输代理安装成功，则表明此过程有效。如果尝试安装旧版传输代理而不执行本主题中的过程，则会收到类似于下面这样的错误：

    Mixed mode assembly is built against version '<version>' of the runtime and cannot be loaded in the 4.0 runtime without additional configuration information.

