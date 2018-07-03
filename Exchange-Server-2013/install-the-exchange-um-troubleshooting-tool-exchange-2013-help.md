---
title: '安装 Exchange UM 故障排除工具: Exchange 2013 Help'
TOCTitle: 安装 Exchange UM 故障排除工具
ms:assetid: 84223af0-a717-49ee-add6-86313bb30d17
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Ff844714(v=EXCHG.150)
ms:contentKeyID: 56271418
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 安装 Exchange UM 故障排除工具

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2016-12-09_

Microsoft Exchange 2010 UM 疑难解答工具是名为 **Test-ExchangeUMCallFlow** 的 Exchange 命令行管理程序 cmdlet。您可以使用此 cmdlet 来诊断电话应答方案的配置错误，并测试语音邮件能否同时在本地和跨界 Microsoft Exchange Server 2010 Service Pack 1 (SP1) 或更高版本 UM 部署中正常工作。您可以在使用 Microsoft Office、Microsoft Lync Server 2010 或更高版本进行部署时使用此 cmdlet，也可以在使用 VoIP 网关、IP PBX 或会话边界控制器 (SBC) 进行 UM 部署时使用此 cmdlet。

可以将 UM 故障排除工具安装在本地统一消息服务器、Exchange 2013 邮箱服务器上，或其他 64 位计算机上。

## 在开始之前，您需要知道什么？

  - 估计完成时间：3 分钟

  - UM 故障排除工具要求必须在运行 Windows Vista、Windows 7、Windows 8，或 64 位版本的 Windows Server 2008 或 Windows Server 2012 或更高版本的计算机上安装以下组件：
    
      - Microsoft .NET Framework 3.5 Service Pack 1 (SP1) 请参阅[Microsoft.NET Framework 3.5 版 Service Pack 1](https://go.microsoft.com/fwlink/p/?linkid=152380)。
    
      - 如果将Windows Vista或Windows Server 2008计算机上运行该工具，请参阅[Windows Server 2008 x64 Windows Vista x64，以及 Microsoft.NET Framework 3.5 系列更新](https://go.microsoft.com/fwlink/p/?linkid=178998)。
    
      - Windows 远程管理 (WinRM) 2.0 和 Windows PowerShell V2 (Windows6.0-KB968930.msu)。请参阅 Microsoft 知识库文章 968930，[Windows Management Framework Core 程序包（Windows PowerShell 2.0 和 WinRM 2.0）](http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=968930)。
    
      - Microsoft 统一通信托管的 API 2.0 的核心运行时 (UcmaRuntimeWebDownloadX64.msi)。请参阅[统一的通信管理 API 2.0，核心运行时 （64 位）](https://go.microsoft.com/fwlink/p/?linkid=198175)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.</td>
</tr>
</tbody>
</table>


## 安装 UM 疑难解答工具

1.  从[Microsoft 下载中心获取](https://go.microsoft.com/fwlink/p/?linkid=182625)，下载统一消息的疑难解答工具，然后双击 MicrosoftExchange2010UMTroubleshootingTool.msi 安装文件夹。

2.  在\&quot;欢迎使用 Microsoft Exchange 2010 UM 故障排除工具安装向导\&quot;页面上，单击\&quot;下一步\&quot;。

3.  在\&quot;最终用户许可协议\&quot;页面上，查看软件许可条款，如果您同意，请单击\&quot;我接受许可协议中的条款\&quot;，然后单击\&quot;下一步\&quot;。

4.  在\&quot;选择安装文件夹\&quot;页面上，检查安装文件夹的路径，然后单击\&quot;下一步\&quot;。

5.  在\&quot;确认安装\&quot;页面上，单击\&quot;下一步\&quot;，开始安装。

6.  在\&quot;安装完成\&quot;页面上，单击\&quot;关闭\&quot;。

