---
title: '边缘传输服务器克隆配置: Exchange 2013 Help'
TOCTitle: 边缘传输服务器克隆配置
ms:assetid: 683a6b8a-59bf-43ed-96c8-504945c2f665
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa998622(v=EXCHG.150)
ms:contentKeyID: 61183391
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 边缘传输服务器克隆配置

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-03-09_

边缘传输服务器在 Active Directory 轻型目录服务 (AD LDS) 中存储其配置信息。您可以在外围网络中安装多个边缘传输服务器，并使用 DNS 轮循机制将网络通信均衡分布到所有边缘传输服务器上。轮循机制是一种 DNS 服务器用来共享和分配网络资源负载的简单机制。

若要确保所有边缘传输服务器使用相同的配置信息，使用所提供的克隆配置脚本将源服务器的配置复制到目标服务器。

*克隆配置*用于基于已配置的源服务器来部署新的边缘传输服务器。源服务器的配置信息将被复制然后导出到 XML 文件。然后将 XML 文件导入目标服务器。

本主题概述了克隆配置的过程。有关使用克隆配置配置边缘传输服务器的详细步骤，请参阅[使用克隆的配置来配置边缘传输服务器](configure-edge-transport-server-using-cloned-configuration-exchange-2013-help.md)。

**目录**

克隆配置和 EdgeSync

克隆配置过程

传输配置信息

## 克隆配置和 EdgeSync

在导入克隆配置后，请运行 EdgeSync 进程。若要执行收件人查找和邮件安全任务，边缘传输服务器需要驻留在 Active Directory 中的数据。*EdgeSync* 是一组进程，运行于 Exchange 2013 邮箱服务器上，可建立将收件人和配置信息从 Active Directory 复制到边缘传输服务器上的 AD LDS 实例的单向复制。EdgeSync 服务只复制边缘传输服务器执行反垃圾邮件任务时所需要的信息，以及启用端到端邮件流时所需的连接器配置的相关信息。EdgeSync 将按计划执行更新，使 AD LDS 中的信息保持最新状态。

克隆配置不会复制服务器的边缘订阅设置。不克隆 EdgeSync 所使用的证书。必须对每个边缘传输服务器单独运行 EdgeSync 进程。EdgeSync 覆盖包含在克隆配置信息和 EdgeSync 复制信息中的相应设置。这些设置包括发送连接器、接收连接器、接受域和远程域。

## 克隆配置过程

克隆配置过程由三个步骤组成：

1.  从源服务器导出配置信息。
    
    运行 ExportEdgeConfig.ps1 脚本（位于 %ExchangeInstallPath%Scripts 中）以将源服务器的配置信息导出到中间 XML 文件。

2.  在目标服务器上验证配置。
    
    运行 ImportEdgeConfig.ps1 脚本（位于 %ExchangeInstallPath%Scripts 中）。此脚本将检查中间 XML 文件中的现有信息，以确定所导出的设置对于目标服务器是否有效，然后创建应答文件。应答文件指定在目标服务器上导入配置时所使用的、特定于服务器的信息。应答文件包含对目标服务器无效的每个源服务器设置的条目。您可以修改这些设置，使其对目标服务器有效。如果所有设置都有效，则应答文件不包含任何条目。

3.  在目标服务器上导入配置。
    
    ImportEdgeConfig.ps1 脚本将使用中间 XML 文件和应答文件来克隆现有配置，或将该服务器还原到特定配置。

## 步骤 1：从源服务器导出配置信息

安装并配置边缘传输服务器角色之后，请运行 ExportEdgeConfig.ps1 脚本（位于 %ExchangeInsallPath%Scripts 中）。此脚本将检索源服务器的配置信息，并将这些信息存储在中间 XML 文件中。

以下信息将从源服务器导出并存储在中间 XML 文件中：

  - 与传输服务相关的信息和日志文件路径信息：
    
      - *ReceiveProtocolLogPath*
    
      - *SendProtocolLogPath*
    
      - *MessageTrackingLogPath*
    
      - *PickupDirectoryPath*
    
      - *RoutingTableLogPath*

  - 与传输代理相关的信息，包括每个传输代理的状态和优先级设置。

  - 所有与发送连接器相关的信息。如果将任意发送连接器配置为使用凭据，则密码将作为加密字符串写入中间 XML 文件。可在 ImportEdgeConfig.ps1 和 ExportEdgeConfig.ps1 脚本中使用 *-key* 参数来指定用于密码加密和解密的 32 字节字符串。如果不使用 *-key* 参数，则使用默认加密密钥。

  - 与接收连接器相关的信息。若要修改本地网络绑定和端口属性，必须修改在验证配置步骤中创建的应答文件中的配置信息。

  - 接受域配置。

  - 远程域配置。

  - 反垃圾邮件功能配置设置：
    
      - IP 允许列表信息。只导出由管理员手动配置的 IP 允许列表条目。
    
      - IP 阻止列表信息。
    
      - 内容筛选器配置。
    
      - 收件人筛选器配置。
    
      - 地址重写条目。
    
      - 附件筛选器条目。

返回顶部

## 步骤 2：在目标服务器上验证配置

目标服务器是具有边缘传输服务器角色干净安装的 Exchange 2013 服务器。首先，在目标服务器上运行 ImportEdgeConfig.ps1 脚本（位于 %ExchangeInsallPath%Script 中），以验证中间 XML 文件中的现有信息，并创建应答文件。应答文件指定在目标服务器上导入配置时所使用的、特定于服务器的信息。应答文件包含对目标服务器无效的每个源服务器设置的条目。您需要修改这些设置，使其对目标服务器有效。如果所有设置都有效，则应答文件不包含任何条目。中间 XML 文件可以用于不同的目标服务器。应答文件特定于目标服务器。

ImportEdgeConfig.ps1 脚本（位于 %ExchangeInsallPath%Scripts 中）将执行以下任务：

  - 确认可以在目标服务器上创建数据路径和日志路径。如果无法创建路径，则会在应答文件中插入空白路径。

  - 对于 XML 文件中的每个发送连接器，该脚本将在应答文件中添加与源 IP 地址对应的空白条目。

  - 对于 XML 文件中的每个接收连接器，该脚本将在应答文件中添加与本地网络绑定对应的空白条目。

需要手动修改应答文件才能提供有关特定于服务器设置的下列信息：

  - 填充数据路径和日志路径。如果在应答文件中将这些路径留空，则会在下一个步骤中（在目标服务器上导入配置时）使用在中间 XML 文件内配置的路径。

  - 对于每个发送连接器条目，请填充源 IP 地址。如果将此字段留空，则会在导入配置步骤中发生错误。

  - 对于每个接收连接器条目，请填充本地网络绑定。如果将本地网络绑定留空，则会在目标服务器上尝试导入配置时发生错误。

返回顶部

## 步骤 3：在目标服务器上导入配置

通过在任何目标服务器上执行此步骤，可以克隆现有边缘传输服务器的配置，或将服务器还原到特定配置。运行 ImportEdgeConfig.ps1 脚本（位于 %ExchangeInsallPath%Scripts 中）脚本可以验证和导入新配置。运行此脚本之后，目标服务器的配置将与中间 XML 文件和应答文件中的设置匹配。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>建议您先备份现有服务器配置，然后再执行导入配置过程，以便在克隆操作失败时，可以将服务器还原到先前的稳定状态。</td>
</tr>
</tbody>
</table>


此步骤使用应答文件中提供的特定于服务器的信息。如果应答文件中未指定某项设置，则使用中间 XML 文件中的数据。在脚本修改配置之前，脚本将验证中间 XML 文件和应答文件中的数据。

导入配置将修改以下目标服务器配置设置：

  - 修改传输代理配置。

  - 在目标服务器上删除现有连接器，并添加中间 XML 文件中出现的连接器。

  - 删除现有接受域，并添加中间 XML 文件中的接受域条目。

  - 删除现有远程域，并添加中间 XML 文件中的远程域条目。

  - 删除现有 IP 允许列表条目，并添加中间远程域文件中的 IP 允许列表条目。

  - 删除现有 IP 阻止列表条目，并添加中间远程域文件中的 IP 阻止列表条目。

  - 下列反垃圾邮件配置将克隆到目标服务器：
    
      - 内容筛选器配置
    
      - 收件人筛选器配置
    
      - 地址重写条目
    
      - 附件筛选器条目

返回顶部

## 传输配置信息

传输配置对象的设置为边缘传输服务器定义服务器范围内的电子邮件传输设置。将中间 XML 文件导入到目标服务器时，会导入传输配置对象的所有设置，除了以下这些：

  - 来自导出的 XML 文件的常规名称和创建日期

  - 发送连接器信息

  - 接收连接器信息

  - 附件筛选器条目

  - **MaxDumpsterSizePerStorageGroup** 属性条目

在导入过程完成后，还可以使用 **Set-TransportConfig** cmdlet 配置这些设置。有关详细信息，请参阅 [Set-TransportConfig](https://technet.microsoft.com/zh-cn/library/bb124151\(v=exchg.150\))。

下表中的属性与传输配置对象和默认值关联。可以在邮箱服务器和边缘传输服务器上配置此对象。但许多属性仅适用于 Exchange 2013 邮箱服务器上的传输服务。在边缘传输服务器上配置这些属性不会有任何影响。

### 传输配置属性和默认值

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>属性</th>
<th>描述</th>
<th>默认值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>ClearCategories</strong></p></td>
<td><p>此属性指定在内容转换期间是否清除 Microsoft Outlook 类别。</p></td>
<td><p>True</p></td>
</tr>
<tr class="even">
<td><p><strong>GenerateCopyOfDSNFor</strong></p></td>
<td><p>此属性指定使 DSN 邮件复制到 postmaster 电子邮件地址的传递状态通知 (DSN) 代码。DSN 代码以 <em>x.y.z</em> 的格式输入，并使用逗号分隔。</p></td>
<td><p>5.4.8, 5.4.6, 5.4.4, 5.2.4, 5.2.0, 5.1.4</p></td>
</tr>
<tr class="odd">
<td><p><strong>InternalSMTPServers</strong></p></td>
<td><p>此属性指定发件人 ID 筛选和连接筛选应忽略的内部 SMTP 服务器 IP 地址或 IP 地址范围的列表。</p></td>
<td><p>Null</p></td>
</tr>
<tr class="even">
<td><p><strong>JournalingReportNdrTo</strong></p></td>
<td><p>此属性指定在日记邮箱不可用时，将日记报告发送到的电子邮件地址。此属性不适用于边缘传输服务器的配置。</p></td>
<td><p>空</p></td>
</tr>
<tr class="odd">
<td><p><strong>MaxDumpsterSizePerStorageGroup</strong></p></td>
<td><p>此属性指定邮箱服务器上的传输转储程序的最大大小。此属性不适用于边缘传输服务器的配置。</p></td>
<td><p>18 MB</p></td>
</tr>
<tr class="even">
<td><p><strong>MaxDumpsterTime</strong></p></td>
<td><p>此属性指定电子邮件在邮箱服务器上的传输转储程序中应保留的时间。此属性不适用于边缘传输服务器的配置。</p></td>
<td><p>7.00:00:00</p></td>
</tr>
<tr class="odd">
<td><p><strong>MaxReceiveSize</strong></p></td>
<td><p>此属性指定组织中的收件人可以接收的最大邮件大小。此属性不适用于边缘传输服务器的配置。</p></td>
<td><p>10 MB</p></td>
</tr>
<tr class="even">
<td><p><strong>MaxRecipientEnvelopeLimit</strong></p></td>
<td><p>此属性指定一封电子邮件允许的最大收件人数。此属性不适用于边缘传输服务器的配置。</p></td>
<td><p>5,000</p></td>
</tr>
<tr class="odd">
<td><p><strong>MaxSendSize</strong></p></td>
<td><p>此属性指定组织中的发件人可以发送的最大邮件大小。此属性不适用于边缘传输服务器的配置。</p></td>
<td><p>10 MB</p></td>
</tr>
<tr class="even">
<td><p><strong>TLSReceiveDomainSecureList</strong></p></td>
<td><p>此属性指定通过配置为支持域安全性的接收连接器将使用相互传输层安全性 (TLS) 身份验证的远程域。可以使用逗号分隔多个域。此属性中列出的域不支持通配符 (*)。</p></td>
<td><p>空</p></td>
</tr>
<tr class="odd">
<td><p><strong>TLSSendDomainSecureList</strong></p></td>
<td><p>此属性指定通过配置为支持域安全性和目标域地址空间的发送连接器发送电子邮件时，将使用相互 TLS 身份验证的远程域。可以使用逗号分隔多个域。此属性中列出的域不支持通配符 (*)。</p></td>
<td><p>空</p></td>
</tr>
<tr class="even">
<td><p><strong>VerifySecureSubmitEnabled</strong></p></td>
<td><p>此属性验证从邮箱服务器上的邮箱提交邮件的电子邮件客户端是否使用了加密的 MAPI 提交。此属性不适用于边缘传输服务器的配置。此属性的有效值是 <code>$true</code> 或 <code>$false</code>。</p></td>
<td><p>False</p></td>
</tr>
<tr class="odd">
<td><p><strong>VoicemailJournalingEnabled</strong></p></td>
<td><p>此属性指定日记代理是否记录统一消息语音邮件。此属性不适用于边缘传输服务器的配置。</p></td>
<td><p>True</p></td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果稍后将边缘传输服务器订阅到 Exchange 组织，<strong>InternalSMTPServers</strong> 属性的值将在 EdgeSync 进程中被覆盖。有关详细信息，请参阅<a href="edge-subscriptions-exchange-2013-help.md">边缘订阅</a>。</td>
</tr>
</tbody>
</table>


返回顶部

