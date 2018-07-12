---
title: '了解 Exchange UM 疑难解答工具: Exchange 2013 Help'
TOCTitle: 了解 Exchange UM 疑难解答工具
ms:assetid: cc11bf5e-2c87-4495-b2ad-3e9a6bc81dbc
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Gg584301(v=EXCHG.150)
ms:contentKeyID: 56271424
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 了解 Exchange UM 疑难解答工具

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2016-12-09_

Microsoft Exchange 2010 统一消息故障排除工具是一个名为 **Test-ExchangeUMCallFlow** 的 Exchange 命令行管理程序 cmdlet。可使用该工具对贵组织的统一消息 (UM) 执行一系列诊断测试。如果有任何测试失败，该工具会报告失败原因以及问题的可能解决方案。您只能在 Exchange 2010 或更高版本的服务器上使用 UM 故障排除工具。

UM 故障排除工具可用于测试语音邮件在内部部署和跨界部署的环境中是否都能正常运行。您可以在包括 Microsoft Office Communications Server 2007 R2 或 Microsoft Lync Server 2010 或更高版本的 UM 部署中，或在包括 VoIP 网关、IP 专用交换机 (IP PBX) 或会话边界控制器 (SBC) 的 UM 部署中使用此工具。

> [!NOTE]  
> UM 故障排除工具用于测试和故障排除。而 <strong>Test-UMConnectivity</strong> cmdlet 应当用于监视。<strong>Test-UMConnectivity</strong> cmdlet 与 System Center Operations Manager (SCOM) 管理包配合使用，这些管理包用于监视 Exchange 2010 UM 服务器或 Exchange 2013 客户端访问和邮箱服务器和电话组件。<strong>Test-UMConnectivity</strong> cmdlet 可对邮箱执行本地 SIP 测试和本地登录测试，并可作为 SCOM 任务运行。


若要下载 UM 故障排除工具，请参阅[统一消息故障排除工具](https://go.microsoft.com/fwlink/p/?linkid=182625)。

**目录**

概述

UM 故障排除体系结构

VoIP 网关和 IP PBX 部署

Office Communications Server 2007 R2 和 Microsoft Lync Server 部署

安装 UM 故障排除工具

Cmdlet 参数

## 概述

UM 故障排除工具可简化 UM 部署中的测试和故障排除。UM 故障排除工具运行时，它会自动生成一组跟踪文件，这些文件存储在 C:\\Users\\%UserProfile%\\AppData\\Roaming\\Microsoft Exchange 2010 UM Troubleshooting 文件夹下。该工具会生成下列跟踪文件：

  - **UMTool\_Collaboration**   包括 RTC 堆栈跟踪。

  - **UMTool\_DiagnosticLog**   列出所运行的所有测试及其结果。

  - **UMTool\_S4**   包括 S4：信号堆栈跟踪。

  - **UMTool\_SIPMessageLogs**   包括所进行的测试呼叫的全部 SIP 跟踪。

UM 故障排除工具可直接连接到内部部署的会话边界控制器 (SBC)（如果存在），或者连接到数据中心的 SBC 并模拟传入呼叫，就像该呼叫是 PBX 通过 VoIP 网关或 IP PBX 发出的一样。UM 故障排除工具可用于诊断：

  - 部署了 Office Communications Server 2007 R2 或 Microsoft Lync Server 的内部部署或跨界 UM 部署中的不正确设置。

  - 包括 VoIP 网关及 PBX 或 IP PBX 的内部部署或跨界电话设备中的不正确设置。

  - 域名系统 (DNS) 问题。

  - 使用“SIP 安全”或“安全 UM”拨号计划时的证书问题。

  - DTMF（也称为按键）和音频的信号及媒体问题。

如果 UM 故障排除工具在配置中检测到故障，该工具会报告错误的原因以及所检测到问题的可能解决方案。在内部部署中使用 UM 故障排除工具时，可能会报告以下错误：

  - 已达到最大呼叫限制。

  - 该用户未启用统一消息。

  - 无法找到 UM IP 网关、拨号计划或智能寻线信息。

  - 安全类型与 UM 拨号计划不匹配。

  - 没有可处理呼叫的工作进程。

  - UM 服务或 UM 呼叫路由器服务已停止。

  - 无法找到 Active Directory 林。

  - 没有可用的磁盘空间。

  - 请求中使用了无效的 SIP 头。

  - 已向 Office Communications Server 2007 R2 服务器或 Lync Server 服务器进行呼叫。

  - UM IP 网关已禁用。

  - 被叫用户的 URI 无效。

在跨界部署中使用 UM 故障排除工具时，可能会报告以下错误：

  - 该用户未启用统一消息。

  - UM IP 网关已禁用。

  - 该用户的 URI 无效。

  - 安全类型与 UM 拨号计划不匹配。

  - 请求中使用了无效的 SIP 头。

  - 无法找到 UM IP 网关、拨号计划或智能寻线信息。

UM 故障排除工具发送一个时长为 15 秒的示例 .wav 文件。在发送并播放音频文件和 RTP 音频流之后，该工具会报告用于诊断与网络连接相关的音频质量问题的常规音质指标，如抖动和平均数据包丢失数量。这些报告包括发往和来自 UM 服务器的媒体流质量及下列项目：

  - 网络平均意见得分 (NMOS)

  - 编解码器

  - 延迟（毫秒）

  - 抖动（毫秒）

  - 数据包丢失的百分比

  - 将使用以下 NMOS 分类和分级来确定音频质量：
    
      - NMOS 小于 2 = 差
    
      - NMOS 大于 2 但小于 3 = 一般
    
      - NMOS 大于 3 但小于 4 = 好
    
      - NMOS 大于 4 但小于 5 = 极好

UM 故障排除工具支持测试使用“安全”、“SIP 安全”和“不安全”呼叫的 UM 拨号计划。如果选择“安全”或“SIP 安全”，将检查所用证书的指纹来确定该证书是否过期以及用于 TLS（传输层安全性）通信的证书类型。该证书用于正确标识及确保远程计算机的标识。选择“安全”或“SIP 安全”模式后，UM 故障排除工具会确认是否符合下列条件：

  - 已在本地计算机存储中找到本地证书。

  - 所使用的证书受到信任。

  - 证书中指定的目标名称有效。

  - 证书已过期。

  - 远程计算机信任该证书。

  - 证书已被吊销。

  - 证书没有所需的增强密钥用法。

UM 故障排除工具可在“网关”或 SIPClient 模式下运行，具体取决于部署的是 Office Communications Server 2007 R2 还是 Lync Server，或者统一消息服务器使用的是 VoIP 网关和 PBX 还是 IP PBX。当使用“网关”或 SIPClient 模式时，UM 故障排除工具支持使用以下格式进行呼叫。所使用的格式取决于 UM 拨号计划的 URI 类型：

  - 电话分机号   425-555-1010

  - E.164 电话号码   +1 (425) 555-1010

  - SIP 地址   tonysmith@contoso.com

使用 SIPClient 模式时，UM 故障排除工具会呼叫语音备忘录。在此呼叫中，电话或统一通信 (UC) 终结点不会发出响铃。而是直接将呼叫发送到语音邮件。以 SIPClient 模式运行 UM 故障排除工具时，该工具将确定：

  - 所呼叫的目标用户。

  - SIP 呼叫是否已成功建立。

  - SIP 呼叫是否已被 Exchange 2010 统一消息服务器或 Exchange 2013 邮箱服务器接受。

  - 接收的 DTMF 序列是否正确。

  - Exchange 2010 UM 服务器或 Exchange 2013 邮箱服务器是否已发送和接收诊断 .wav 文件。

  - 收到媒体或音频质量流时使用的指标。

UM 故障排除工具将模拟传入呼叫并运行一系列诊断测试，这些测试可帮助内部部署管理员和租户管理员测试呼叫流的呼叫应答并确定配置错误。尽管可在呼叫应答情形中使用 UM 故障排除工具，但是无法使用其来测试以下类型的呼叫：

  - Outlook Voice Access 呼叫，包括访问语音邮件、电子邮件、日历、目录、个人联系人或个人选项的呼叫

  - UM 自动助理

  - 在电话上播放

  - 呼叫应答规则

  - 传真

  - 提示设置

概述

## UM 故障排除体系结构

UM 故障排除工具可帮助您在跨界部署中排查、诊断及修复配置问题，您还可以将其用于内部部署的统一消息部署。在跨界部署中，此工具还将验证现场 SBC 配置。管理员可以测试统一消息使用的所有统一消息组件，包括 SBC。

## VoIP 网关和 IP PBX 部署

在以下示例中，网关模式被用来测试不包括 Office Communications Server 2007 R2 或 Lync Server 的环境中的呼叫流。该示例测试电话设备，包括 VoIP 网关、PBX 和 IP PBX 以及统一消息组件。此示例将 IP 语音 (VoIP) 安全模式设置为“不安全” ，使用 IP 地址 10.1.1.1 作为下一个跃点，并在转换信息中包括分机号码。

    Test-ExchangeUMCallFlow -Mode Gateway -VoIPSecurity Unsecured -NextHop 10.1.1.1 -Diversion 12345

概述

## Office Communications Server 2007 R2 和 Microsoft Lync Server 部署

设置 SIPClient 模式时，可在包括 Office Communications Server 2007 R2 或 Microsoft Lync Server 的内部部署或跨界部署中使用 UM 故障排除工具。以下示例使用 SIPClient 模式并在包含 Office Communications Server 2007 R2 或 Lync Server 服务器的环境中采用安全 UM 拨号计划测试呼叫流。默认情况下，在运行 UM 故障排除工具时，该工具使用当前登录到计算机的用户的凭据。运行以下示例时，系统将提示您要在运行 UM 故障排除工具时使用的凭据。有关详细信息，请参阅[设置要用于 Exchange UM 疑难解答工具的凭据](set-the-credentials-to-use-with-the-exchange-um-troubleshooting-tool-exchange-2013-help.md)。

    Test-ExchangeUMCallFlow -Mode SIPClient -VoIPSecurity Secured -CallingParty tony@contoso.com -CalledParty david@contoso.com -Credential $get

## 安装 UM 故障排除工具

可以将 UM 故障排除工具安装在本地统一消息服务器上或运行以下操作系统的其他 64 位计算机上：

  - Windows 7 或 Windows 8 操作系统。

  - Windows Server 2008 或 Windows Server 2008 R2 操作系统。

  - Windows Server 2012 或 Windows Server 2012 R2 操作系统。

如果在 64 位版本的 Windows 7、Windows8，或 64 位版本的 Windows Server 2008 上使用 UM 故障排除工具，必须在安装 UM 故障排除工具之前先安装下列组件：

  - Microsoft .NET Framework 3.5 Service Pack 1 (SP1)   请参阅 [Microsoft .NET Framework 3.5 Service Pack 1](https://go.microsoft.com/fwlink/p/?linkid=152380)。
    
    > [!NOTE]  
    > 如果将在 Windows Vista 或 Windows Server 2008 计算机上运行该工具，请参阅<a href="https://go.microsoft.com/fwlink/p/?linkid=178998">适用于 Windows Vista x64 和 Windows Server 2008 x64 的 Microsoft .NET Framework 3.5 产品系列更新</a>。


  - Windows 远程管理 (WinRM) 2.0 和 Windows PowerShell V2 (Windows6.0-KB968930.msu)   请参阅 Microsoft 知识库文章 968930，[Windows Management Framework Core 程序包（Windows PowerShell 2.0 和 WinRM 2.0）](http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=968930)。

  - Microsoft Unified Communications Managed API 2.0 Core Runtime (UcmaRuntimeWebDownloadX64.msi)   请参阅 [Unified Communications Managed API 2.0，Core Runtime（64 位）](https://go.microsoft.com/fwlink/p/?linkid=198175)。

UM 疑难解答工具 (**Test-ExchangeUMCallFlow** cmdlet) 不包含在 Exchange 2010 SP1 DVD、仅包括 Exchange 2010 的下载或 Exchange 2013 安装媒体中。但是，您可以从 [Microsoft 下载中心](https://go.microsoft.com/fwlink/p/?linkid=182625)下载 UM 故障排除工具。

有关详细信息，请参阅[安装 Exchange UM 故障排除工具](install-the-exchange-um-troubleshooting-tool-exchange-2013-help.md)。

概述

## Cmdlet 参数

下表显示了可与 **Test-ExchangeUMCallFlow** cmdlet 一起使用的参数以及这些参数的描述。您也可以使用命令行管理程序命令 `Get-help Test-ExchangeUMCallFlow -detailed` 来查找有关可与 **Test-ExchangeUMCallFlow** cmdlet 一起使用的每个参数的详细信息以及使用示例。

### 参数

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>参数</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>CalledParty</em></p></td>
<td><p><em>CalledParty</em> 参数指定已启用 Enterprise Voice 的 Office Communications Server 2007 R2 或 Lync Server 用户的 SIP URI。这是 <strong>Test-ExchangeUMCallFlow</strong> cmdlet 将对其进行语音呼叫的用户，例如：<code>-CalledParty tonysmith@contoso.com</code>。如果您以 SIPClient 模式运行该工具，请使用此参数。</p></td>
</tr>
<tr class="even">
<td><p><em>CallingParty</em></p></td>
<td><p><em>CallingParty</em> 参数指定已启用 Enterprise Voice 的 Office Communications Server 2007 R2 或 Lync Server 用户的 SIP URI。这是将进行传入呼叫的用户，例如：<code>-CallingParty tonysmith@contoso.com</code>。如果您以 SIPClient 模式运行该工具，请使用此参数。</p></td>
</tr>
<tr class="odd">
<td><p><em>Diversion</em></p></td>
<td><p><em>Diversion</em> 参数指定应作为传入呼叫的转换信息发送的字符串。这可以采用转换或历史信息头的形式。传入呼叫中包含的转换信息可以为分机号码，也可以包含其他转换信息。</p>
<p>在提供转换信息作为历史信息头时，请验证以下方面：</p>
<ul>
<li><p>至少有两个具有不同用户部分的不同条目。</p></li>
<li><p>最后一个条目包含用户的关联 UM 拨号计划的引导号码。</p></li>
<li><p>倒数第二个条目包含启用了 UM 的用户的分机号码。此条目还必须包括适当的原因文本。此文本必须按照标准 URL 参数转义规则进行正确转义。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><em>Mode</em></p></td>
<td><p><em>Mode</em> 参数指定是使用 VoIP 网关、IP PBX 还是 Office Communications Server 2007 R2 或 Lync Server 模式。当 UM 部署包括 VoIP 网关或 IP PBX 时，您可以指定“网关”模式，当 UM 部署包括 Office Communications Server 2007 R2 或 Lync Server 时，可以指定 SIPClient 模式。</p></td>
</tr>
<tr class="odd">
<td><p><em>NextHop</em></p></td>
<td><p><em>NextHop</em> 参数指定下一个跃点的 IP 地址或完全限定的域名 (FQDN)，还可以包括在模拟 VoIP 网关或 IP PBX 时，<strong>Test-ExchangeUMCallFlow</strong> cmdlet 必须连接到的下一个跃点的 TCP 端口。当包括 TCP 端口时，对于“不安全”模式必须指定端口 5060，对于“安全”或“SIP 安全”模式必须指定端口 5061。例如：<code>gateway.contoso.com:5061</code>.</p></td>
</tr>
<tr class="even">
<td><p><em>CertificateThumbprint</em></p></td>
<td><p><em>CertificateThumbprint</em> 参数指定用于 TLS 的证书的指纹。如果在 UM 拨号计划上配置“SIP 安全”或“安全”模式，此参数是必需的。此证书指纹是从 VoIP 网关、IP PBX 或 SBC 导出的证书。此外，安装了 UM 故障排除工具并用于测试呼叫流的计算机必须信任下一个跃点的颁发机构证书。</p></td>
</tr>
<tr class="odd">
<td><p><em>Credential</em></p></td>
<td><p><em>Credential</em> 参数指定用于运行 cmdlet 的凭据。</p></td>
</tr>
<tr class="even">
<td><p><em>HuntGroup</em></p></td>
<td><p><em>HuntGroup</em> 参数指定与要模拟的 VoIP 网关相关联的 UM 智能寻线。这通常是分机号码。如果您以“网关”模式运行该工具，请使用此参数。</p></td>
</tr>
<tr class="odd">
<td><p><em>VoIPSecurity</em></p></td>
<td><p><em>VoIPSecurity</em> 参数指定以“网关”模式使用 cmdlet 时的安全模式。可以使用下列 VoIP 安全模式之一：</p>
<ul>
<li><p>安全 (TLS/SRTP)</p></li>
<li><p>不安全 (TCP/RTP)（默认值）</p></li>
<li><p>SIP 安全 (TLS/RTP)</p></li>
</ul></td>
</tr>
</tbody>
</table>


概述

