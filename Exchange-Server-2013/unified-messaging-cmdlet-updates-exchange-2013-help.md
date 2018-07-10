---
title: '统一消息 cmdlet 更新: Exchange 2013 Help'
TOCTitle: 统一消息 cmdlet 更新
ms:assetid: a42c6643-67ed-4003-854a-ac1d66efb965
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ150557(v=EXCHG.150)
ms:contentKeyID: 50491333
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 统一消息 cmdlet 更新

 

_**适用于：** Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2015-03-09_

Exchange Server 2010 中的许多统一消息 (UM) cmdlet 适用于 Exchange Server 2013，但是其中一些 cmdlet 进行了更改。此外，还为 Exchange 2013 添加了新 cmdlet。

## 更新的参数和新 UM Cmdlet

下面是 Exchange 2013 更新的参数和新 Cmdlet 列表。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Cmdlet</th>
<th>参数</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>New-UMIPGateway</p></td>
<td><p><code>[-IPAddressFamily &lt;IPv4Only | IPv6Only | Any&gt;]</code></p></td>
</tr>
<tr class="even">
<td><p>Set-UMIPGateway</p></td>
<td><p><code>[-IPAddressFamily &lt;IPv4Only | IPv6Only | Any&gt;]</code></p></td>
</tr>
<tr class="odd">
<td><p>Get-UMMailbox</p></td>
<td><p><code>[-AccountPartition &lt;AccountPartitionIdParameter&gt;]</code></p></td>
</tr>
<tr class="even">
<td><p>Set-UMMailbox</p></td>
<td><p><code>[-ImListMigrationCompleted &lt;$true | $false&gt; -VoiceMailAnalysisEnabled &lt;$true | $false&gt;]</code></p></td>
</tr>
<tr class="odd">
<td><p>Test-Connectivity</p></td>
<td><p><code>[-CallRouter &lt;SwitchParameter&gt;]</code></p></td>
</tr>
<tr class="even">
<td><p>New-UMCallAnsweringRule</p></td>
<td><p><code>[-Name &lt;String&gt; [-CallerIds &lt;MultiValuedProperty&gt;] [-CallersCanInterruptGreeting &lt;$true | $false&gt;] [-CheckAutomaticReplies &lt;$true | $false&gt;] [-Confirm [&lt;SwitchParameter&gt;]] [-DomainController &lt;Fqdn&gt;] [-ExtensionsDialed &lt;MultiValuedProperty&gt;] [-KeyMappings &lt;MultiValuedProperty&gt;] [-Mailbox &lt;MailboxIdParameter&gt;] [-Organization &lt;OrganizationIdParameter&gt;] [-Priority &lt;Int32&gt;] [-ScheduleStatus &lt;Int32&gt;] [-TimeOfDay &lt;TimeOfDay&gt;] [-WhatIf [&lt;SwitchParameter&gt;]]</code></p></td>
</tr>
<tr class="odd">
<td><p>Remove-UMCallAnsweringRule</p></td>
<td><p><code>[-Identity &lt;UMCallAnsweringRuleIdParameter&gt; [-Confirm [&lt;SwitchParameter&gt;]] [-DomainController &lt;Fqdn&gt;] [-Mailbox &lt;MailboxIdParameter&gt;] [-WhatIf [&lt;SwitchParameter&gt;]]</code></p></td>
</tr>
<tr class="even">
<td><p>Get-UMCallAnsweringRule</p></td>
<td><p><code>[-Identity &lt;UMCallAnsweringRuleIdParameter&gt;] [-DomainController &lt;Fqdn&gt;] [-Mailbox &lt;MailboxIdParameter&gt;]</code></p></td>
</tr>
<tr class="odd">
<td><p>Set-UMCallAnsweringRule</p></td>
<td><p><code>[-Identity &lt;UMCallAnsweringRuleIdParameter&gt; [-CallerIds &lt;MultiValuedProperty&gt;] [-CallersCanInterruptGreeting &lt;$true | $false&gt;] [-CheckAutomaticReplies &lt;$true | $false&gt;] [-Confirm [&lt;SwitchParameter&gt;]] [-DomainController &lt;Fqdn&gt;] [-ExtensionsDialed &lt;MultiValuedProperty&gt;] [-KeyMappings &lt;MultiValuedProperty&gt;] [-Mailbox &lt;MailboxIdParameter&gt;] [-Name &lt;String&gt;] [-Priority &lt;Int32&gt;] [-ScheduleStatus &lt;Int32&gt;] [-TimeOfDay &lt;TimeOfDay&gt;] [-WhatIf [&lt;SwitchParameter&gt;]]</code></p></td>
</tr>
<tr class="even">
<td><p>Enable-UMCallAnsweringRule</p></td>
<td><p><code>[-Identity &lt;UMCallAnsweringRuleIdParameter&gt; [-Confirm [&lt;SwitchParameter&gt;]] [-DomainController &lt;Fqdn&gt;] [-Mailbox &lt;MailboxIdParameter&gt;] [-WhatIf [&lt;SwitchParameter&gt;]]</code></p></td>
</tr>
<tr class="odd">
<td><p>Disable-UMCallAnsweringRule</p></td>
<td><p><code>[-Identity &lt;UMCallAnsweringRuleIdParameter&gt; [-Confirm [&lt;SwitchParameter&gt;]] [-DomainController &lt;Fqdn&gt;] [-Mailbox &lt;MailboxIdParameter&gt;] [-WhatIf [&lt;SwitchParameter&gt;]]</code></p></td>
</tr>
<tr class="even">
<td><p>Get-UMCallRouterSettings</p></td>
<td><p><code>[-DomainController &lt;Fqdn&gt;] [-Server &lt;ServerIdParameter&gt;]</code></p></td>
</tr>
<tr class="odd">
<td><p>Set-UMCallRouterSettings</p></td>
<td><p><code>Set-UMCallRouterSettings [-Confirm [&lt;SwitchParameter&gt;]] [-DialPlans &lt;MultiValuedProperty&gt;] [-DomainController &lt;Fqdn&gt;] [-IPAddressFamily &lt;IPv4Only | IPv6Only | Any&gt;] [-IPAddressFamilyConfigurable &lt;$true | $false&gt;] [-Server &lt;ServerIdParameter&gt;] [-SipTcpListeningPort &lt;Int32&gt;] [-SipTlsListeningPort &lt;Int32&gt;] [-UMPodRedirectTemplate &lt;String&gt;] [-UMStartupMode &lt;TCP | TLS | Dual&gt;] [-WhatIf [&lt;SwitchParameter&gt;]]</code></p></td>
</tr>
<tr class="even">
<td><p>Disable-UMService</p></td>
<td><p><code>-Identity &lt;UMServerIdParameter&gt; [-Confirm [&lt;SwitchParameter&gt;]] [-DomainController &lt;Fqdn&gt;] [-Immediate &lt;$true | $false&gt;] [-WhatIf [&lt;SwitchParameter&gt;]]</code></p>

> [!NOTE]
> 此 cmdlet 仅适用于 Exchange 2007 和 2010 UM 服务器。

</td>
</tr>
<tr class="odd">
<td><p>Enable-UMService</p></td>
<td><p><code>-Identity &lt;UMServerIdParameter&gt; [-Confirm [&lt;SwitchParameter&gt;]] [-DomainController &lt;Fqdn&gt;] [-WhatIf [&lt;SwitchParameter&gt;]]</code></p>

> [!NOTE]
> 此 cmdlet 仅适用于 Exchange 2007 和 2010 UM 服务器。

</td>
</tr>
<tr class="even">
<td><p>Get-UMService</p></td>
<td><p><code>[-Identity &lt;UMServerIdParameter&gt;] [-DomainController &lt;Fqdn&gt;]</code></p></td>
</tr>
<tr class="odd">
<td><p>Set-UMService</p></td>
<td><p><code>Set-UMService -Identity &lt;UMServerIdParameter&gt; [-Confirm [&lt;SwitchParameter&gt;]] [-DialPlans &lt;MultiValuedProperty&gt;] [-DomainController &lt;Fqdn&gt;] [-GrammarGenerationSchedule &lt;ScheduleInterval[]&gt;] [-IPAddressFamily &lt;IPv4Only | IPv6Only | Any&gt;] [-IPAddressFamilyConfigurable &lt;$true | $false&gt;] [-IrmLogEnabled &lt;$true | $false&gt;] [-IrmLogMaxAge &lt;EnhancedTimeSpan&gt;] [-IrmLogMaxDirectorySize &lt;Unlimited&gt;] [-IrmLogMaxFileSize &lt;ByteQuantifiedSize&gt;] [-IrmLogPath &lt;LocalLongFullPath&gt;] [-MaxCallsAllowed &lt;Int32&gt;] [-SIPAccessService &lt;ProtocolConnectionSettings&gt;] [-UMStartupMode &lt;TCP | TLS | Dual&gt;] [-WhatIf [&lt;SwitchParameter&gt;]]</code></p></td>
</tr>
</tbody>
</table>


有关所有 UM cmdlet 的详细信息，请参阅[统一消息 cmdlet](https://technet.microsoft.com/zh-cn/library/aa997665\(v=exchg.150\))。

