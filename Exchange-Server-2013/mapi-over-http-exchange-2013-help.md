---
title: 'MAPI over HTTP: Exchange 2013 Help'
TOCTitle: MAPI over HTTP
ms:assetid: 4663b5db-5b30-4a5a-a302-be6fef7fe5da
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dn635177(v=EXCHG.150)
ms:contentKeyID: 61203674
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# MAPI over HTTP

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2017-05-10_

MAPI（邮件处理应用程序编程接口）over HTTP 是在 MicrosoftExchange Server 2013 Service Pack 1 (SP1) 中实现的新传输协议。MAPI over HTTP 可将传输层移动到行业标准的 HTTP 模型，从而提高 Outlook 和 Exchange 连接的可靠性和稳定性。这样可以提高传输错误的可见性级别，并增强可恢复性。其他功能包括支持显式暂停和继续功能。这使受支持的客户端可以更改网络或从休眠状态中恢复，同时保持相同的服务器上下文。

实现 MAPI over HTTP 并不意味着这是可由 Outlook 用于访问 Exchange 的唯一协议。不支持 MAPI over HTTP 的 Outlook 客户端仍可以使用 Outlook Anywhere (RPC over HTTP) 通过启用了 MAPI 的客户端访问服务器访问 Exchange。

## MAPI over HTTP 的优势

MAPI over HTTP 为支持它的客户端提供以下益处：

  - 通过使用基于 HTTP 的协议实现身份验证的未来创新。

  - 在通信中断后实现更快的重新连接，因为仅需要重建 TCP 连接（而非 RPC 连接）。通信中断的示例包括：
    
      - 设备休眠
    
      - 从有线网络更换到无线网络或移动电话网络

  - 提供不依赖连接的会话上下文。服务器在可配置的时间段内保持会话上下文，即使用户更改网络也是如此。

## 部署 MAPI over HTTP

启用 MAPI over HTTP 时，请考虑以下要求。

  - **可支持性**   验证预期配置版本是否受支持。

  - **先决条件**   确认已升级环境，并已准备好启用 MAPI over HTTP。

  - **配置**   配置虚拟目录，并为组织启用 MAPI。

## 可支持性

请使用以下矩阵验证客户端和服务器是否支持 MAPI over HTTP。


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>产品</th>
<th>Exchange 2013 SP1</th>
<th>Exchange 2013 RTM</th>
<th>Exchange 2010 SP3</th>
<th>Exchange 2007 SP3</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook 2013 SP1</p></td>
<td><ul>
<li><p>MAPI over HTTP</p></li>
<li><p>Outlook 无处不在</p></li>
</ul></td>
<td><p>Outlook 无处不在</p></td>
<td><ul>
<li><p>RPC</p></li>
<li><p>Outlook 无处不在</p></li>
</ul></td>
<td><ul>
<li><p>RPC</p></li>
<li><p>Outlook 无处不在</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Outlook 2013 RTM</p></td>
<td><p>Outlook 无处不在</p></td>
<td><p>Outlook 无处不在</p></td>
<td><ul>
<li><p>RPC</p></li>
<li><p>Outlook 无处不在</p></li>
</ul></td>
<td><ul>
<li><p>RPC</p></li>
<li><p>Outlook 无处不在</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Outlook 2010 SP2 和更新 KB2956191 以及 KB2965295（2015 年 4 月 14 日）</p></td>
<td><ul>
<li><p>MAPI over HTTP<span></span></p></li>
<li><p>Outlook 无处不在</p></li>
</ul></td>
<td><p>Outlook 无处不在</p></td>
<td><ul>
<li><p>RPC</p></li>
<li><p>Outlook 无处不在</p></li>
</ul></td>
<td><ul>
<li><p>RPC</p></li>
<li><p>Outlook 无处不在</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Outlook 2010 SP2 和更低版本</p></td>
<td><p>Outlook 无处不在</p></td>
<td><p>Outlook 无处不在</p></td>
<td><ul>
<li><p>RPC</p></li>
<li><p>Outlook 无处不在</p></li>
</ul></td>
<td><ul>
<li><p>RPC</p></li>
<li><p>Outlook 无处不在</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Outlook 2007</p></td>
<td><p>Outlook 无处不在</p></td>
<td><p>Outlook 无处不在</p></td>
<td><ul>
<li><p>RPC</p></li>
<li><p>Outlook 无处不在</p></li>
</ul></td>
<td><ul>
<li><p>RPC</p></li>
<li><p>Outlook 无处不在</p></li>
</ul></td>
</tr>
</tbody>
</table>


## 先决条件

请完成以下步骤，使客户端和服务器准备好支持 MAPI over HTTP。

1.  将 Outlook 客户端升级到 Outlook 2013 SP1 或 Outlook 2010 SP2 以及更新 KB2956191 和 KB2965295（2015 年 4 月 14 日）。

2.  将客户端访问服务器和邮箱服务器升级到 Exchange 2013 SP1。有关如何升级的信息，请参阅[将 Exchange 2013 升级到最新累积更新或 Service Pack](upgrade-exchange-2013-to-the-latest-cumulative-update-or-service-pack-exchange-2013-help.md)。
    
    > [!NOTE]
    > 必须将所有客户端访问服务器升级到 Exchange 2013 SP1，然后再启用 MAPI over HTTP。否则，Outlook 将无法连接到邮箱。<br />
    > 数据库可用性组 (DAG) 中所有邮箱服务器升级失败将导致电子邮件延迟，并需要客户端在发生数据库故障转移时重新启动 Outlook。


3.  您需要在所有 Exchange 2013 服务器上安装 Microsoft.NET Framework 4.5.2。有关详细信息，请参阅[安装 .NET Framework](https://go.microsoft.com/fwlink/p/?linkid=518380)。

4.  在所有 Exchange 2013 SP1 客户端访问服务器上，通过执行以下步骤添加 **COMPLUS\_DisableRetStructPinning** Windows 环境变量：
    
    1.  在一个命令指示符窗口中，运行 `systempropertiesadvanced`，然后单击“环境变量”。
    
    2.  在“系统变量”部分中，单击“新建”，然后输入以下信息。
        
          - **变量名称**   `COMPLUS_DisableRetStructPinning`
        
          - **变量值**   1
    
    3.  完成后，单击“确定”。

## 配置

请完成以下步骤，为组织配置 MAPI over HTTP。

1.  **虚拟目录配置**   默认情况下，Exchange 2013 SP1 会创建 MAPI over HTTP 的虚拟目录。使用 **Set-MapiVirtualDirectory** cmdlet 配置虚拟目录。必须配置一个内部 UTL、一个外部 URL，或者两者。有关详细信息，请参阅 [Set-MapiVirtualDirectory](https://technet.microsoft.com/zh-cn/library/dn595082\(v=exchg.150\))。
    
    例如，若要通过将内部 URL 值设置为 https://contoso.com/mapi，将身份验证方法设置为 `Negotiate`，从而在本地 Exchange Server 上配置默认 MAPI 虚拟目录，请运行以下命令：
    
        Set-MapiVirtualDirectory -Identity "Contoso\mapi (Default Web Site)" -InternalUrl https://Contoso.com/mapi -IISAuthenticationMethods Negotiate

2.  **证书配置**   Exchange 环境使用的数字证书必须包括在 MAPI 虚拟目录中定义的相同的 *InternalURL* 和 *ExternalURL* 值。有关 Exchange 2013 证书管理的详细信息，请参阅[数字证书和 SSL](digital-certificates-and-ssl-exchange-2013-help.md)。确保 Exchange 证书在 Outlook 客户端工作站上受信任，且没有证书错误，访问在 MAPI 虚拟目录中配置的 URL 时更须如此。

3.  **更新服务器规则**   确认已配置负载平衡器、反向代理和防火墙，以允许访问 MAPI over HTTP 虚拟目录。

4.  **在 Exchange 组织中启用 MAPI over HTTP**
    
    运行以下命令：
    
        Set-OrganizationConfig -MapiHttpEnabled $true

## 测试 MAPI over HTTP 连接

可以使用 **Test-OutlookConnectivity** cmdlet 测试端到端 MAPI over HTTP 连接。若要使用 **Test-OutlookConnectivity** cmdle，必须启动 Microsoft Exchange 运行状况管理器 (MSExchangeHM) 服务。

以下示例测试来自名为 ContosoMail 的 Exchange Server 的 MAPI over HTTP 连接。

    Test-OutlookConnectivity -RunFromServerId ContosoMail -ProbeIdentity OutlookMapiHttpSelfTestProbe

测试成功将返回类似于以下示例的输出：

    MonitorIdentity                                          StartTime              EndTime                Result      Error     Exception
    ---------------                                          ---------              -------                ------      -----     ---------
    OutlookMapiHttp.Protocol\OutlookMapiHttpSelfTestProbe    2/14/2014 7:15:00 AM   2/14/2014 7:15:10 AM   Succeeded

有关详细信息，请参阅 [Test-OutlookConnectivity](https://technet.microsoft.com/zh-cn/library/dd638082\(v=exchg.150\))。

MAPI over HTTP 活动的日志位于以下位置：

  - %ExchangeInstallPath%Logging\\MAPI Address Book Service\\

  - %ExchangeInstallPath%Logging\\MAPI Client Access\\

  - %ExchangeInstallPath%Logging\\HttpProxy\\Mapi\\

## 管理 MAPI over HTTP

可以使用以下 cmdlet 管理 MAPI over HTTP 的配置：

  - [Set-MapiVirtualDirectory](https://technet.microsoft.com/zh-cn/library/dn595082\(v=exchg.150\))

  - [Get-MapiVirtualDirectory](https://technet.microsoft.com/zh-cn/library/dn595080\(v=exchg.150\))

  - [New-MapiVirtualDirectory](https://technet.microsoft.com/zh-cn/library/dn595081\(v=exchg.150\))

  - [Remove-MapiVirtualDirectory](https://technet.microsoft.com/zh-cn/library/dn595083\(v=exchg.150\))

