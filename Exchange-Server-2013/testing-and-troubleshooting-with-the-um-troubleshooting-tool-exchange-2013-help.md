---
title: '使用 UM 疑难解答工具进行测试和疑难解答: Exchange 2013 Help'
TOCTitle: 使用 UM 疑难解答工具进行测试和疑难解答
ms:assetid: 1fab2e52-bd2d-4e46-b222-53fee9d34cba
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Gg621148(v=EXCHG.150)
ms:contentKeyID: 56271410
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 使用 UM 疑难解答工具进行测试和疑难解答

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2016-12-09_

Microsoft Exchange 2010 UM 疑难解答工具是名为 **Test-ExchangeUMCallFlow** 的 Exchange 命令行管理程序 cmdlet。您可以使用此 cmdlet 来诊断电话应答方案的配置错误，并测试语音邮件能否同时在本地和跨界 Microsoft Exchange Server 2010 Service Pack 1 (SP1) 或更高版本 UM 部署中正常工作。您可以在使用 Microsoft Office、Microsoft Lync Server 2010 或更高版本进行部署时使用此 cmdlet，也可以在使用 VoIP 网关、IP PBX 或会话边界控制器 (SBC) 进行 UM 部署时使用此 cmdlet。

## 概述

此 cmdlet 模拟呼叫并运行一系列诊断测试，这些测试可帮助本地管理员识别电话设备和 Exchange 2010 SP1 或更高版本统一消息设置中的配置错误，以及 Exchange 2010 SP1 或更高版本统一消息的本地和跨界部署之间的连接问题。

在运行该 cmdlet 时，它可指出已检测到的问题的原因和可能解决方案。它还输出用于诊断与网络连接相关的音频质量问题的常规音频质度量指标，如抖动和平均数据包丢失数量。**Test-ExchangeUMCallFlow** cmdlet 支持在 `Secured`、`SIP Secured` 和 `Unsecured` 呼叫中测试 UM 组件，它可以在 `Gateway` 或 `SIPClient` 模式下运行。

默认情况下，当您在运行该 UM 故障排除工具，它使用登录到该计算机时使用的凭据。所使用的凭据是指那些为调用方指定了。您必须设置或指定您在`SIPClient`模式下运行 UM 故障诊断工具时要使用的凭据。但是，您不需要在`Gateway`模式下运行 UM 故障诊断工具时设置凭据。如果您将在`SIPClient`模式下使用 UM 故障诊断工具，必须满足几个其他办公室通信服务器 2007 R2 或 Lync Server 要求和先决条件。有关详细信息，请参阅[清单︰ 部署 Office 通信服务器 2007 R2 和 Exchange 2010 统一消息](https://go.microsoft.com/fwlink/p/?linkid=311961)或[检查表：将 Exchange 2013 UM 与 Lync Server 集成](checklist-integrate-exchange-2013-um-with-lync-server-exchange-2013-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>Test-ExchangeUMCallFlow</strong> cmdlet 必须仅用于测试已安装 Exchange 2010 Service Pack 1 (SP1) 的 Microsoft Exchange Server 2010 统一消息服务器或 Microsoft Exchange 2013 的语音邮件功能。</td>
</tr>
</tbody>
</table>


**Test-ExchangeUMCallFlow** cmdlet 可以安装在本地 Exchange 2010 统一消息服务器、Exchange 2013 邮箱服务器，或运行下列操作系统的其他 64 位计算机上：

  - Windows 7 或 Windows 8 操作系统

  - Windows Server 2008 或 Windows Server 2008 R2 操作系统

  - Windows Server 2012 或 Windows Server 2012 R2 操作系统

**Test-ExchangeUMCallFlow** cmdlet 要求先将下列组件安装在 Windows 7、Windows 8、Windows Server 2008 或 Windows Server 2012 64 位计算机上，然后再安装该 cmdlet：

  - Microsoft .NET Framework 3.5 Service Pack 1 (SP1)。若要下载该 service pack，请参阅[Microsoft.NET Framework 3.5 Service Pack 1](https://go.microsoft.com/fwlink/p/?linkid=152380)。

  - Microsoft .NET Framework 3.5 Windows Vista x64 和Windows Server 2008 x64 系列更新更新如果将Windows Vista或Windows Server 2008计算机上运行该工具。若要下载此更新，请参阅[Windows Server 2008 x64 Windows Vista x64，以及 Microsoft.NET Framework 3.5 系列更新](https://go.microsoft.com/fwlink/p/?linkid=178998)。

  - Windows Remote Management (WinRM) 2.0 和 Windows PowerShell V2 (Windows6.0-KB968930.msu)。有关详细信息，请参阅 Microsoft 知识库文章 968930 [Windows Management Framework Core 程序包（Windows PowerShell 2.0 和 WinRM 2.0）](http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=968930)。

  - 统一的通信管理 AP1 2.0，核心运行时 （64 位）。下载 UcmaRuntimeWebDownloadX64.msi 程序文件，请参阅[托管 API 2.0 统一通信、 核心运行时 （64 位）](https://go.microsoft.com/fwlink/p/?linkid=198175)。

**Test-ExchangeUMCallFlow** cmdlet 并不包含在Exchange 2010 SP1 DVD、 Exchange 2010 SP1 仅下载或交换 2013年安装介质;但是，您可以从[Microsoft 下载中心](https://go.microsoft.com/fwlink/p/?linkid=182625)下载该 cmdlet。

有关语法和参数的详细信息，请参阅 [Test-ExchangeUMCallFlow](https://technet.microsoft.com/zh-cn/library/ff630913\(v=exchg.150\))。

