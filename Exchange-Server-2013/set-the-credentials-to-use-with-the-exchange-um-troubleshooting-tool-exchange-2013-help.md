---
title: '设置要用于 Exchange UM 疑难解答工具的凭据: Exchange 2013 Help'
TOCTitle: 设置要用于 Exchange UM 疑难解答工具的凭据
ms:assetid: 542b7718-9345-40cc-bcb2-e307e70a1fa2
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Ff630916(v=EXCHG.150)
ms:contentKeyID: 56271412
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 设置要用于 Exchange UM 疑难解答工具的凭据

 

_**适用于：** Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2016-12-09_

Microsoft Exchange 2010 UM 疑难解答工具是名为 **Test-ExchangeUMCallFlow** 的 Exchange 命令行管理程序 cmdlet。您可以使用此 cmdlet 来诊断电话应答方案的配置错误，并测试语音邮件能否同时在本地和跨界 Microsoft Exchange Server 2010 Service Pack 1 (SP1) 或更高版本 UM 部署中正常工作。您可以在使用 Microsoft Office、Microsoft Lync Server 2010 或更高版本进行部署时使用此 cmdlet，也可以在使用 VoIP 网关、IP PBX 或会话边界控制器 (SBC) 进行 UM 部署时使用此 cmdlet。

默认情况下，在运行 UM 故障排除工具时，该工具使用在您登录计算机时使用的凭据。使用的凭据是为呼叫方指定的凭据。您必须设置或指定在以 `SIPClient` 模式运行 UM 故障排除工具时要使用的凭据。不过，您无需设置在以 `Gateway` 模式运行 UM 故障排除工具时使用的凭据。

## 在开始之前，您需要知道什么？

  - 估计完成时间：3 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 服务器\&quot;或\&quot;UM 服务\&quot;条目。

  - 请确保您的 Exchange 2010 或 Exchange 2013 组织满足下列要求：
    
      - 已创建 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。
    
      - 已创建 UM 邮箱策略。有关详细步骤，请参阅[创建 UM 邮箱策略](create-a-um-mailbox-policy-exchange-2013-help.md)。
    
      - 已创建 UM IP 网关。有关详细步骤，请参阅[创建 UM IP 网关](create-a-um-ip-gateway-exchange-2013-help.md)。
    
      - Exchange 2010 UM 服务器添加到 UM 拨号计划。如果您使用 Lync Server 使用 Exchange 2013，添加所有客户端访问和邮箱服务器 SIP URI 拨号计划。有关详细步骤，请参阅[添加 UM 服务器到拨号计划](https://go.microsoft.com/fwlink/p/?linkid=313051)或[将邮箱服务器和客户端访问服务器添加到 SIP URI 的拨号计划](add-mailbox-and-client-access-servers-to-a-sip-uri-dial-plan-exchange-2013-help.md)。

  - 安装 UM 疑难解答工具。有关详细步骤，请参阅[安装 Exchange UM 故障排除工具](install-the-exchange-um-troubleshooting-tool-exchange-2013-help.md)。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果要在<code>SIPClient</code>模式下使用 UM 故障排除工具，还有其他几个办公室通信服务器 2007 R2 或 Microsoft Lync Server 要求和先决条件。有关详细信息，请参阅<a href="https://go.microsoft.com/fwlink/p/?linkid=311961">清单︰ 部署 Office 通信服务器 2007 R2 和 Exchange 2010 统一消息</a>或<a href="checklist-integrate-exchange-2013-um-with-lync-server-exchange-2013-help.md">检查表：将 Exchange 2013 UM 与 Lync Server 集成</a>。</td>
    </tr>
    </tbody>
    </table>


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


## 设置要用于 UM 故障排除工具的凭据

1.  从\&quot;开始\&quot;菜单中打开\&quot;Microsoft Exchange 2010 UM 故障排除工具\&quot;。

2.  在\&quot;Microsoft Exchange 2010 UM 故障排除工具\&quot;窗口中，在提示符下输入以下命令，然后按 Enter 键。
    
        $cred=Get-Credential

3.  在\&quot;Windows PowerShell 凭据请求\&quot;窗口中，键入域名\\用户名和密码，然后单击\&quot;确定\&quot;。

4.  在\&quot;Microsoft Exchange 2010 UM 故障排除工具\&quot;窗口中，指定必要的 cmdlet 参数对呼叫流进行测试。例如：
    
        Test-ExchangeUMCallFlow -Mode SIPClient -CallingParty tonysmith@contoso.com - CalledParty jamiestark@contoso.com NextHop ocsfe.contoso.com -Credential $cred

