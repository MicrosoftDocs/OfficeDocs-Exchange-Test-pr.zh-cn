---
title: '在 Windows 7 或 Windows 8 上运行 Exchange UM 故障排除工具: Exchange 2013 Help'
TOCTitle: 在 Windows 7 或 Windows 8 上运行 Exchange UM 故障排除工具
ms:assetid: 98d6869d-ee4a-4088-849d-ef75b0f5d932
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Ff851872(v=EXCHG.150)
ms:contentKeyID: 56271419
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 在 Windows 7 或 Windows 8 上运行 Exchange UM 故障排除工具

 

_**适用于：** Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2016-12-09_

Microsoft Exchange 2010 UM 疑难解答工具是名为 **Test-ExchangeUMCallFlow** 的 Exchange 命令行管理程序 cmdlet。您可以使用此 cmdlet 来诊断电话应答方案的配置错误，并测试语音邮件能否同时在本地和跨界 Microsoft Exchange Server 2010 Service Pack 1 (SP1) 或更高版本 UM 部署中正常工作。您可以在使用 Microsoft Office、Microsoft Lync Server 2010 或更高版本进行部署时使用此 cmdlet，也可以在使用 VoIP 网关、IP PBX 或会话边界控制器 (SBC) 进行 UM 部署时使用此 cmdlet。

## 在开始之前，您需要知道什么？

  - 估计完成时间：3 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 服务器\&quot;或\&quot;UM 服务\&quot;条目。

  - 请确保您的 Exchange 2010 或 Exchange 2013 组织满足下列要求：
    
      - 已创建 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。
    
      - 已创建 UM 邮箱策略。有关详细步骤，请参阅[创建 UM 邮箱策略](create-a-um-mailbox-policy-exchange-2013-help.md)。
    
      - 已创建 UM IP 网关。有关详细步骤，请参阅[创建 UM IP 网关](create-a-um-ip-gateway-exchange-2013-help.md)。
    
      - Exchange 2010 UM 服务器添加到 UM 拨号计划。如果使用的 Exchange 2013 Lync 服务器，添加所有客户端访问和邮箱服务器 SIP URI 拨号计划。有关详细步骤，请参阅[添加 UM 服务器到拨号计划](https://go.microsoft.com/fwlink/p/?linkid=313051)或[将邮箱服务器和客户端访问服务器添加到 SIP URI 的拨号计划](add-mailbox-and-client-access-servers-to-a-sip-uri-dial-plan-exchange-2013-help.md)。

  - 如果您要在安装了 Exchange 2010 SP1 或更高版本的本地 UM 服务器上或在 Exchange 2013 邮箱服务器上运行 UM 疑难解答工具，则不必安装下面列出的所有先决条件。可能已经与 UM 服务器角色一起安装了先决条件。但如果在 64 位计算机上而不是在运行 UM 服务器角色的服务器上安装 UM 故障排除工具，则需要安装以下组件：
    
      - Microsoft .NET Framework 3.5 Service Pack 1 (SP1)。请参阅[Microsoft.NET Framework 3.5 版 Service Pack 1](https://go.microsoft.com/fwlink/p/?linkid=152380)。
    
      - 如果将Windows Vista 或Windows Server 2008计算机上运行该工具，请参阅[Windows Server 2008 x64 Windows Vista x64，以及 Microsoft.NET Framework 3.5 系列更新](https://go.microsoft.com/fwlink/p/?linkid=178998)。
    
      - Windows 远程管理 (WinRM) 2.0 和 Windows PowerShell V2 (Windows6.0-KB968930.msu)。请参阅 Microsoft 知识库文章 968930，[Windows Management Framework Core 程序包（Windows PowerShell 2.0 和 WinRM 2.0）](http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=968930)。
    
      - Microsoft 统一通信托管的 API 2.0 的核心运行时 (UcmaRuntimeWebDownloadX64.msi)。请参阅[统一的通信管理 API 2.0，核心运行时 （64 位）](https://go.microsoft.com/fwlink/p/?linkid=198175)。

  - 下载并安装 UM 故障排除工具。
    
      - 从 Microsoft 下载中心下载[统一消息疑难解答工具](https://go.microsoft.com/fwlink/p/?linkid=182625) 。
    
      - 安装此工具。有关详细信息，请参阅[安装 Exchange UM 故障排除工具](install-the-exchange-um-troubleshooting-tool-exchange-2013-help.md)。
        
        > [!important]
        > 如果要在<code>SIPClient</code>模式下使用 UM 故障排除工具，有几个办公室通信服务器 2007 R2 或Microsoft Lync Server 要求和必须满足的先决条件。有关详细信息，请参阅<a href="https://go.microsoft.com/fwlink/p/?linkid=311961">清单︰ 部署 Office 通信服务器 2007 R2 和 Exchange 2010 统一消息</a>。


  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!tip]
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 在 Windows Vista、Windows 7 或 Windows 8 上运行 UM 故障排除工具

1.  依次单击\&quot;开始\&quot;\>\&quot;所有程序\&quot;\>\&quot;附件\&quot;\> **Windows PowerShell**。

2.  右键单击\&quot;Windows PowerShell\&quot;，然后从弹出的菜单中选择\&quot;以管理员身份运行\&quot;。

3.  在 Windows PowerShell 命令提示符下，转到安装了 UM 故障排除工具的文件夹，并运行以下命令。
    
        C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe -psconsolefile .\Microsoft.Exchange.UM.TroubleshootingToolsnapin.psc1 -noexit -command ". '.\Microsoft.Exchange.UM.TroubleshootingTool.ps1' "

4.  如果要在 Windows Vista、Windows 7 或 Windows 8 上运行 UM 故障排除工具，请在 Windows PowerShell 命令提示符下运行以下命令。
    
        Set-ExecutionPolicy RemoteSigned

5.  从\&quot;开始\&quot;菜单中打开\&quot;Microsoft Exchange 2010 UM 故障排除工具\&quot;。

6.  在\&quot;Microsoft Exchange 2010 UM 故障排除工具\&quot;窗口中，在提示符下输入以下命令，然后按 Enter。
    
        $cred=Get-Credential

7.  在\&quot;Windows PowerShell 凭据请求\&quot;窗口中，键入域名\\用户名和密码，然后单击\&quot;确定\&quot;。

8.  在\&quot;Microsoft Exchange 2010 UM 故障排除工具\&quot;窗口中，指定必要的 cmdlet 参数对呼叫流进行测试。例如：
    
        Test-ExchangeUMCallFlow -Mode SIPClient -CallingParty tonysmith@contoso.com - CalledParty jamiestark@contoso.com NextHop ocsfe.contoso.com -Credential $cred

