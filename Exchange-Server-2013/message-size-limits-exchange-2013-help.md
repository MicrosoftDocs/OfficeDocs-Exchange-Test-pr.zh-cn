---
title: '邮件大小限制: Exchange 2013 Help'
TOCTitle: 邮件大小限制
ms:assetid: b6a3840d-b821-4e53-877b-59c16be77206
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb124345(v=EXCHG.150)
ms:contentKeyID: 50491411
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 邮件大小限制

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-08-20_

可以将此限制应用于在 Microsoft Exchange Server 2013 组织中移动的邮件。可以限制邮件的总大小，也可以限制邮件各部分的大小，例如邮件头、邮件附件和收件人数目。可以将这些限制全局应用到整个 Exchange 组织，或者专门应用到连接器或用户对象。

在规划 Exchange 组织的邮件大小限制时，请考虑以下问题：

  - 对所有传入邮件的大小限制应为多少？

  - 对所有传出邮件的大小限制应为多少？

  - 我的 Exchange 组织的邮箱配额是什么？

  - 如何将所选择的邮箱大小限制与邮箱配额大小相关联？

  - 我的 Exchange 组织中是否存在必须收发大于指定允许大小的邮件的用户？

  - 我的 Exchange 网络拓扑是否包括具有不同邮件大小限制的其他邮件系统或独立业务单位？

本主题提供了可帮助您回答这些问题的指导。

**目录**

邮件大小限制的类型

限制的作用域

邮件大小限制的优先级顺序

免受大小限制的邮件

## 邮件大小限制的类型

下面是可用于各个邮件的大小限制的基本类别：

  - **邮件头大小限制**   这些限制应用于邮件中存在的所有邮件头字段的总大小。不考虑邮件正文或附件的大小。因为邮件头字段是纯文本，所以邮件头的大小由每个邮件头的字符数和邮件头字段的总数确定。每个文本字符占用 1 字节。
    
    > [!NOTE]  
    > 某些第三方防火墙或代理服务器应用其自身的邮件头大小限制。这些第三方防火墙或代理服务器处理包含多于 50 个字符或包含非 US-ASCII 字符的附件文件名的邮件可能有困难。


  - **邮件大小限制**   这些限制应用于邮件的总大小，包括邮件头、邮件正文及所有附件。邮件大小限制可用于传入邮件和传出邮件。对于内部邮件流，Exchange 使用自定义 `X-MS-Exchange-Organization-OriginalSize:` 邮件头在邮件进入 Exchange 组织时记录其原始邮件大小。只要检查邮件的指定邮件大小限制，就会使用当前邮件大小或原始邮件大小头的较低值。邮件的大小可能会由于内容转换、编码和代理处理等原因而有所变化。

  - **附件大小限制**   这些限制应用于邮件内单个附件的最大允许大小。邮件中可能会包含许多附件，这样会大大增加邮件的总体大小。但是，附件大小限制仅适用于单个附件的大小。

  - **收件人限制**   这些限制应用于邮件收件人总数。首次撰写邮件时，收件人存在于 `To:`、`Cc:` 和 `Bcc:` 头字段中。提交邮件进行传递时，邮件收件人将转换为邮件信封中的 `RCPT TO:` 条目。邮件提交期间，通讯组将作为单个收件人进行计数。

返回顶部

## 限制的作用域

下面是可用于各个邮件的限制范围的基本类别：

  - **组织限制**   这些限制适用于所有存在于组织中的 Exchange 2013 邮箱服务器和 Exchange 2010 及 Exchange 2007 集线器传输服务器。如果在外围网络中已安装边缘传输服务器，则将指定的限制应用于特定服务器。

  - **连接器限制**   这些限制应用于使用指定发送连接器、接收连接器、传递代理连接器或外部连接器传递邮件的所有邮件。发送连接器在邮箱服务器和边缘传输服务器上的传输服务中进行定义。接收连接器在邮箱服务器的传输服务，以及客户端访问服务器和边缘传输服务器的前端传输服务中进行定义。

  - **Active Directory 站点链接**   邮箱服务器上的传输服务使用 Active Directory 站点和分配到 Active Directory IP 站点链接的成本作为确定组织中邮箱服务器之间成本最低的路由路径的因素之一。可以将特定邮件大小限制分配给组织中的 Active Directory 站点链接。

  - **服务器限制**   这些限制应用于特定邮箱服务器或边缘传输服务器。可以在每台邮箱服务器或边缘传输服务器上单独设置指定的邮件限制。
    
    在 Outlook Web App 中，客户端访问服务器上的最大 HTTP 请求大小限制设置还可控制 Outlook Web App 用户可以发送的邮件大小。

  - **用户限制**   这些限制应用于特定用户对象，例如邮箱、联系人、通讯组或公用文件夹。

下表显示了邮件限制，其中包括有关如何在 Exchange 命令行管理程序或 Exchange 管理中心 (EAC) 中配置这些限制的信息。

### 组织限制

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>大小限制</th>
<th>默认值</th>
<th>命令行管理程序配置</th>
<th>EAC 配置</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>所接收邮件的最大大小</p></td>
<td><p>10 MB</p></td>
<td><p>Cmdlet：<strong>Set-TransportConfig</strong></p>
<p>参数：<em>MaxReceiveSize</em></p></td>
<td><p>“邮件流”&gt;“接收连接器”&gt;“更多选项”<img src="images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif" title="更多选项图标" alt="更多选项图标" /> &gt;“组织传输设置”&gt;“限制”选项卡 &gt;“最大接收邮件大小”</p></td>
</tr>
<tr class="even">
<td><p>所发送邮件的最大大小</p></td>
<td><p>10 MB</p></td>
<td><p>Cmdlet：<strong>Set-TransportConfig</strong></p>
<p>参数：<em>MaxSendSize</em></p></td>
<td><p>“邮件流”&gt;“接收连接器”&gt;“更多选项”<img src="images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif" title="更多选项图标" alt="更多选项图标" /> &gt;“组织传输设置”&gt;“限制”选项卡 &gt;“最大发送邮件大小”</p></td>
</tr>
<tr class="odd">
<td><p>每封邮件的最大收件人数</p>

> [!NOTE]  
> <p></p>

</td>
<td><p>5000</p></td>
<td><p>Cmdlet：<strong>Set-TransportConfig</strong></p>
<p>参数：<em>MaxRecipientEnvelopeLimit</em></p></td>
<td><p>“邮件流”&gt;“接收连接器”&gt;“更多选项”<img src="images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif" title="更多选项图标" alt="更多选项图标" /> &gt;“组织传输设置”&gt;“限制”选项卡 &gt;“最大收件人数”</p></td>
</tr>
<tr class="even">
<td><p>应用于组织中的所有邮箱服务器的传输规则中的最大附件大小</p></td>
<td><p>未配置</p></td>
<td><p>Cmdlet：<strong>New-TransportRule</strong>、<strong>Set-TransportRule</strong></p>
<p>参数：<em>AttachmentSizeOver</em></p></td>
<td><p>“邮件流”&gt;“规则”&gt;“添加”<img src="images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif" title="添加图标" alt="添加图标" />或“编辑”<img src="images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif" title="编辑图标" alt="编辑图标" />。</p>
<p>使用谓语“在以下情况应用此规则”&gt;“任何附件”&gt;“大于或等于”</p>
<p>使用谓语“在以下情况应用此规则”&gt;“邮件”&gt;“大小大于或等于”</p></td>
</tr>
<tr class="odd">
<td><p>应用于组织中的所有邮箱服务器的传输规则中的最大邮件大小</p></td>
<td><p></p></td>
<td><p>Cmdlet：<strong>New-TransportRule</strong>、<strong>Set-TransportRule</strong></p>
<p>参数：<em>MessageSizeOver</em></p></td>
<td><p>“邮件流” &gt; “规则” &gt; “添加”<img src="images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif" title="添加图标" alt="添加图标" /> 或“编辑”<img src="images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif" title="编辑图标" alt="编辑图标" />。</p>
<p>使用谓语“在以下情况应用此规则”&gt;“邮件” &gt; “大小大于或等于”</p></td>
</tr>
</tbody>
</table>


返回顶部

### 连接器限制

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>大小限制</th>
<th>默认值</th>
<th>命令行管理程序配置</th>
<th>EAC 配置</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>通过接收连接器的最大邮件头大小</p></td>
<td><p>128 KB</p></td>
<td><p>Cmdlet：<strong>New-ReceiveConnector</strong>、<strong>Set-ReceiveConnector</strong></p>
<p>参数：<em>MaxHeaderSize</em></p></td>
<td><p>不适用</p>
<p></p></td>
</tr>
<tr class="even">
<td><p>通过接收连接器的最大邮件大小</p>

> [!NOTE]  
> 由于邮件编码和内容转换，实际邮件大小可能较小。

</td>
<td><p><strong>邮箱服务器上的传输服务</strong></p>
<p>35 MB（对于默认和客户端代理接收连接器）</p>
<p><strong>客户端访问服务器上的前端传输服务</strong></p>
<p>36 MB（对于默认前端和出站代理前端接收连接器）。</p>
<p>35 MB（对于客户端前端接收连接器）。</p></td>
<td><p>Cmdlet：<strong>New-ReceiveConnector</strong>、<strong>Set-ReceiveConnector</strong></p>
<p>参数：<em>MaxMessageSize</em></p></td>
<td><p>“邮件流”&gt;“接收连接器”&gt;“编辑”<img src="images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif" title="编辑图标" alt="编辑图标" />&gt;“常规”选项卡 &gt;“最大接收邮件大小”</p></td>
</tr>
<tr class="odd">
<td><p>通过接收连接器的每封邮件收件人的最大数量</p></td>
<td><p><strong>邮箱服务器上的传输服务</strong></p>
<p>5,000（对于默认接收连接器）</p>
<p>200（对于客户端代理接收连接器）</p>
<p><strong>客户端访问服务器上的前端传输服务</strong></p>
<p>200（对于默认前端、客户端前端和客户端代理前端接收连接器）。</p>

> [!NOTE]  
> 如果因为匿名发件人致使收件人数目超出，则只接受前 200 个收件人的邮件。大多数 SMTP 邮件服务器都会检测收件人限制是否有效。SMTP 邮件服务器在将邮件传递给所有收件人之前，会在 200 个收件人的组中继续重新发送邮件。

</td>
<td><p>Cmdlet：<strong>New-ReceiveConnector</strong>、<strong>Set-ReceiveConnector</strong></p>
<p>参数：<em>MaxRecipientsPerMessage</em></p></td>
<td><p>不适用</p></td>
</tr>
<tr class="even">
<td><p>通过发送连接器的最大邮件大小</p></td>
<td><p>10 MB</p></td>
<td><p>Cmdlet：<strong>New-SendConnector</strong>、<strong>Set-SendConnector</strong></p>
<p>参数：<em>MaxMessageSize</em></p></td>
<td><p>“邮件流”&gt;“发送连接器”&gt;“编辑”<img src="images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif" title="编辑图标" alt="编辑图标" />&gt;“常规”选项卡 &gt;“最大发送邮件大小”</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p>通过 Active Directory 站点链接的最大邮件大小</p></td>
<td><p>无限制</p></td>
<td><p>Cmdlet：<strong>Set-AdSiteLink</strong></p>
<p>参数：<em>MaxMessageSize</em></p></td>
<td><p>不适用</p></td>
</tr>
<tr class="even">
<td><p>通过传递代理连接器的最大邮件大小</p></td>
<td><p>无限制</p></td>
<td><p>Cmdlet：<strong>New-DeliveryAgentConnector</strong>、<strong>Set-DeliveryAgentConnector</strong></p>
<p>参数：<em>MaxMessageSize</em></p></td>
<td><p>不适用</p></td>
</tr>
<tr class="odd">
<td><p>通过外部连接器的最大邮件大小</p></td>
<td><p>无限制</p></td>
<td><p><strong>Cmdlet: Set-ForeignConnector</strong> Parameter：<em>MaxMessageSize</em></p></td>
<td><p>不适用</p></td>
</tr>
</tbody>
</table>


返回顶部

### 服务器限制

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>大小限制</th>
<th>默认值</th>
<th>命令行管理程序配置</th>
<th>EAC 配置</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>分拣目录中的邮件头的最大大小</p></td>
<td><p>64 KB</p></td>
<td><p>Cmdlet：<strong>Set-TransportService</strong></p>
<p>参数：<em>PickupDirectoryMaxHeaderSize</em></p></td>
<td><p>不适用</p></td>
</tr>
<tr class="even">
<td><p>分拣目录中的每封邮件的最大收件人数</p></td>
<td><p>100</p></td>
<td><p>Cmdlet：<strong>Set-TransportService</strong></p>
<p>参数：<em>PickupDirectoryMaxRecipientsPerMessage</em></p></td>
<td><p>不适用</p></td>
</tr>
<tr class="odd">
<td><p>Outlook Web App、Exchange ActiveSync 和 Exchange Web 服务客户端的客户端特定最大邮件大小限制</p></td>
<td><p>Outlook Web App   35 MB</p>
<p>Exchange ActiveSync   10 MB</p>
<p>Exchange Web 服务   64 MB</p>

> [!NOTE]  
> 与 Base64 编码相关的开销导致这些值会比实际可用的最大邮件大小高出大约 33%。

</td>
<td><p>您可以在客户端访问服务器上的相应 web.config XML 应用程序配置文件中配置这些值。有关详细信息，请参阅<a href="configure-client-specific-message-size-limits-exchange-2013-help.md">配置客户端特定的邮件大小限制</a>。</p></td>
<td><p>不适用</p></td>
</tr>
</tbody>
</table>


返回顶部

### 用户限制

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>大小限制</th>
<th>默认值</th>
<th>命令行管理程序配置</th>
<th>EAC 配置</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>该收件人可以发送的最大邮件大小</p></td>
<td><p>无限制</p></td>
<td><p>Cmdlet：</p>
<p><strong>Set-DistributionGroup</strong></p>
<p><strong>Set-DynamicDistributionGroup</strong></p>
<p><strong>Set-Mailbox</strong></p>
<p><strong>Set-MailContact</strong></p>
<p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailPublicFolder</strong></p>
<p><strong>Set-RemoteMailbox</strong></p>
<p>参数：<em>MaxSendSize</em></p></td>
<td><p>对于邮箱：</p>
<p>“收件人”&gt;“邮箱”&gt;“编辑”<img src="images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif" title="编辑图标" alt="编辑图标" />&gt;“邮箱功能”&gt;“邮箱流”&gt;“邮件大小限制”&gt;“查看详细信息”&gt;“已发送邮件”</p>

> [!NOTE]  
> 对于其他收件人类型，不可使用 EAC 配置该设置。

</td>
</tr>
<tr class="even">
<td><p>可发送给该收件人的最大邮件大小</p></td>
<td><p>无限制</p>
<p>对于站点邮箱设置策略：36 MB</p></td>
<td><p>Cmdlet：</p>
<p><strong>Set-DistributionGroup</strong></p>
<p><strong>Set-DynamicDistributionGroup</strong></p>
<p><strong>Set-Mailbox</strong></p>
<p><strong>Set-MailContact</strong></p>
<p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailPublicFolder</strong></p>
<p><strong>New-SiteMailboxProvisioningPolicy</strong></p>
<p><strong>Set-SiteMailboxProvisioningPolicy</strong></p>
<p>参数：<em>MaxReceiveSize</em></p></td>
<td><p>对于邮箱：</p>
<p>“收件人”&gt;“邮箱”&gt;“编辑”<img src="images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif" title="编辑图标" alt="编辑图标" />&gt;“邮箱功能”&gt;“邮箱流”&gt;“邮件大小限制”&gt;“查看详细信息”&gt;“已接收邮件”</p>

> [!NOTE]  
> 对于其他收件人类型，不可使用 EAC 配置该设置。

</td>
</tr>
<tr class="odd">
<td><p>该收件人发送的每封邮件的最大收件人数量</p></td>
<td><p>无限制</p></td>
<td><p>Cmdlet：</p>
<p><strong>Set-Mailbox</strong>, <strong>Set-MailUser</strong></p>
<p>参数：<em>RecipientLimits</em></p>
<p></p></td>
<td><p>不适用</p></td>
</tr>
</tbody>
</table>


返回顶部

## 邮件大小限制的优先级顺序

可在 Exchange 组织中的不同级别设置不同的邮件大小限制。当邮件通过传输基础结构进行路由时，此邮件可能要受到多种不同邮件大小限制。在计划邮件大小限制时，应确保如果传输管道中的邮件违反了邮件大小限制，要尽可能早地拒绝这些邮件。一般来说，应该在邮件进入基础结构中的位置设置更为严格的限制。例如，从 Internet 接收邮件的接收连接器上的邮件大小限制应小于或等于为内部 Exchange 组织配置的邮件大小限制。Exchange 服务器接受和处理来自 Internet 的会被邮箱服务器上传输服务拒绝的邮件，这会造成系统资源的浪费。配置组织、服务器和连接器限制时，务必要最大限度地减少任何不必要的邮件处理。

此方法的一个例外是用户限制。用户级别限制优先于其他邮件大小限制。因此，可以配置一个用户，超出组织的默认邮件大小限制。例如，可以通过为一组特定的用户邮箱配置自定义发送和接收限制，允许该组用户邮箱发送比组织的其他邮箱更大的邮件。

用户限制的例外仅适用于经过身份验证的用户之间的邮件交换。如果收件人通过 Internet 发送或接收邮件，将应用组织限制。例如，假定您的组织邮件大小限制为 10 MB，但您将所在营销部门中的用户配置为发送和接收最大 50 MB 的邮件。这些用户将能互相交换大邮件，但仍无法接收来自 Internet 用户的大邮件，因为此类邮件将来自于未经身份验证的发件人。

返回顶部

## 免受大小限制的邮件

下表显示了由邮箱服务器或边缘传输服务器生成并免受所有邮件大小限制的邮件类型：

  - 系统邮件

  - 代理生成的邮件

  - 传递状态通知 (DSN) 邮件

  - 日记报告邮件

  - 被隔离的邮件

但是，这些邮件仍要受组织中邮件的最大收件人数的值的限制。

返回顶部

