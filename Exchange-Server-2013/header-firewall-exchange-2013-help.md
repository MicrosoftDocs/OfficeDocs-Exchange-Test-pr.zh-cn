---
title: '邮件头防火墙: Exchange 2013 Help'
TOCTitle: 邮件头防火墙
ms:assetid: 9b148f7b-47a9-4379-a55b-8d5310c1772f
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb232136(v=EXCHG.150)
ms:contentKeyID: 52061540
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
f1_keywords:
- 邮件头防火墙, 林 X-header
- 邮件头防火墙, X-header
- 邮件头防火墙, 传输体系结构
- 邮件头防火墙, 路由邮件头
- 邮件头防火墙, 邮件头防火墙权限
- 邮件头防火墙, 组织 X-header
ms.translationtype: HT
---

# 邮件头防火墙

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2015-03-09_

在 Microsoft Exchange Server 2013 中，“邮件头防火墙”是从入站邮件和出站邮件中删除特定邮件头字段的机制。邮件头防火墙影响两种不同的头字段：

  - **X-header**   *X-header* 是用户定义的非正式头字段。X-header 未在 RFC 2822 中专门提及，但是使用以 **X-** 打头的未定义头字段已成为向邮件添加非正式头字段的普遍接受方式。邮件应用程序，例如反垃圾邮件应用程序、防病毒应用程序以及邮件服务器可以将其各自的 X-header 添加到邮件中。X-header 字段包含有关传输服务对邮件执行的操作的详细信息，例如，垃圾邮件可信度 (SCL)、内容筛选结果和规则处理状态。如果向未经授权的源泄露这些信息，可能会造成潜在的安全风险。

  - **路由邮件头**   路由邮件头是 RFC 2821 和 RFC 2822 中定义的标准 SMTP 邮件头字段。路由邮件头通过使用有关不同邮件传递服务器（用于将邮件传递到收件人）的信息标记邮件。恶意用户插入到邮件中的路由邮件头可用于篡改将邮件传递到收件人经由的路由路径。

邮件头防火墙通过从来自不可信源的进入 Exchange 组织的入站邮件中删除与 Exchange 相关的 X-header 来防止这些 X-header 欺骗。邮件头防火墙通过从发送到 Exchange 组织外不可信目标的出站邮件中删除与 Exchange 相关的 X-header 来防止这些 X-header 泄漏。邮件头防火墙还阻止用于跟踪邮件路由历史记录的标准路由邮件头的欺骗。

**目录**

Exchange 中受邮件头防火墙影响的邮件头字段

邮件头防火墙如何应用于接收连接器和发送连接器

接收连接器上入站邮件的邮件头防火墙

发送连接器上出站邮件的邮件头防火墙

其他邮件源的邮件头防火墙

Exchange 中的组织 X-header 和林 X-header

## Exchange 中受邮件头防火墙影响的邮件头字段

下列类型的 X-header 和路由邮件头受邮件头防火墙影响：

  - **组织 X-header**   这些 X-header 字段均以 **X-MS-Exchange-Organization-** 作为开头。

  - **林 X-header**   这些 X-header 字段均以 **X-MS-Exchange-Forest-** 作为开头。
    
    有关组织 X-header 和林 X-header 的示例，请参阅本主题结尾处的 Exchange 中的组织 X-header 和林 X-header部分。

  - **Received:路由邮件头**   接受并将邮件转发到收件人的每个邮件传递服务器向邮件头字段添加此邮件头字段的不同实例。**Received:**邮件头通常包含邮件传递服务器的名称和日期时间戳。

  - **Resent-\*:路由头**   Resent 头字段是信息性头字段，可用于确定邮件是否已由用户转发。以下是可用的 Resent 邮件头字段：**Resent-Date:**、**Resent-From:**、**Resent-Sender:**、**Resent-To:**、**Resent-Cc:**、**Resent-Bcc:** 和 **Resent-Message-ID:**。使用 **Resent-** 字段可使邮件在收件人处看似是由原始发件人直接发来的邮件。收件人可以查看该邮件头来了解邮件是谁转发的。

Exchange 使用两种不同的方法将邮件头防火墙应用于邮件中存在的组织 X-header、林 X-header 和路由邮件头：

  - 向邮件通过连接器传输时用于在邮件中保留或删除特定邮件头类型的发送连接器或接收连接器分配权限。

  - 在其他类型的邮件提交过程中，自动为邮件中的特定邮件头类型实施邮件头防火墙。

返回顶部

## 邮件头防火墙如何应用于接收连接器和发送连接器

邮件头防火墙根据向连接器分配的特定权限，应用于通过发送连接器和接收连接器传输的邮件。

如果已向接收连接器或发送连接器分配权限，则邮件头防火墙不应用于通过连接器传输的邮件。受影响的邮件头字段保留在邮件中。

如果不向接收连接器或发送连接器分配权限，则邮件头防火墙应用于通过连接器传输的邮件。受影响的邮件头字段从邮件中删除。

下表描述用于应用邮件头防火墙的发送连接器和接收连接器上的权限，以及受影响的邮件头字段。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>连接器类型</th>
<th>权限</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>接收连接器 (Receive connector)</p></td>
<td><p><strong>Ms-Exch-Accept-Headers-Organization</strong></p></td>
<td><p>此权限影响入站邮件中以 <strong>X-MS-Exchange-Organization-</strong> 开头的组织 X-header 字段。</p></td>
</tr>
<tr class="even">
<td><p>接收连接器 (Receive connector)</p></td>
<td><p><strong>Ms-Exch-Accept-Headers-Forest</strong></p></td>
<td><p>此权限影响入站邮件中以 <strong>X-MS-Exchange-Forest-</strong> 开头的林 X-header 字段。</p></td>
</tr>
<tr class="odd">
<td><p>接收连接器 (Receive connector)</p></td>
<td><p><strong>Ms-Exch-Accept-Headers-Routing</strong></p></td>
<td><p>此权限影响入站邮件中的 <strong>Received:</strong> 和 <strong>Resent-*:</strong> 路由邮件头字段。</p></td>
</tr>
<tr class="even">
<td><p>发送连接器 (Send connector)</p></td>
<td><p><strong>Ms-Exch-Send-Headers-Organization</strong></p></td>
<td><p>此权限影响出站邮件中以 <strong>X-MS-Exchange-Organization-</strong> 开头的组织 X-header 字段。</p></td>
</tr>
<tr class="odd">
<td><p>发送连接器 (Send connector)</p></td>
<td><p><strong>Ms-Exch-Send-Headers-Forest</strong></p></td>
<td><p>此权限影响出站邮件中以 <strong>X-MS-Exchange-Forest-</strong> 开头的林 X-header 字段。</p></td>
</tr>
<tr class="even">
<td><p>发送连接器 (Send connector)</p></td>
<td><p><strong>Ms-Exch-Send-Headers-Routing</strong></p></td>
<td><p>此权限影响出站邮件中的 <strong>Received:</strong> 和 <strong>Resent-*:</strong> 路由邮件头字段。</p></td>
</tr>
</tbody>
</table>


## 接收连接器上入站邮件的邮件头防火墙

下表描述接收连接器上邮件头防火墙权限的默认应用。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>权限</th>
<th>具有分配的权限的默认 Exchange 安全主体</th>
<th>具有安全主体成员的权限组</th>
<th>将权限组分配给接收连接器的默认使用类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Ms-Exch-Accept-Headers-Organization</strong> 和 <strong>Ms-Exch-Accept-Headers-Forest</strong></p></td>
<td><ul>
<li><p>集线器传输服务器</p></li>
<li><p>边缘传输服务器</p></li>
<li><p>Exchange Servers</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>仅在集线器传输服务器上</td>
</tr>
</tbody>
</table>

</li>
</ul></td>
<td><p><strong>ExchangeServers</strong></p></td>
<td><p><code>Internal</code></p></td>
</tr>
<tr class="even">
<td><p><strong>Ms-Exch-Accept-Headers-Routing</strong></p></td>
<td><p>匿名用户帐户</p></td>
<td><p><strong>匿名</strong></p></td>
<td><p><code>Internet</code></p></td>
</tr>
<tr class="odd">
<td><p><strong>Ms-Exch-Accept-Headers-Routing</strong></p></td>
<td><p>通过身份验证的用户帐户</p></td>
<td><p><strong>ExchangeUsers</strong></p></td>
<td><p><code>Client</code>（在边缘传输服务器上不可用）</p></td>
</tr>
<tr class="even">
<td><p><strong>Ms-Exch-Accept-Headers-Routing</strong></p></td>
<td><ul>
<li><p>集线器传输服务器</p></li>
<li><p>边缘传输服务器</p></li>
<li><p>Exchange Servers</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>仅集线器传输服务器</td>
</tr>
</tbody>
</table>

</li>
<li><p>外部安全服务器</p></li>
</ul></td>
<td><p><strong>ExchangeServers</strong></p></td>
<td><p><code>Internal</code></p></td>
</tr>
<tr class="odd">
<td><p><strong>Ms-Exch-Accept-Headers-Routing</strong></p></td>
<td><p>合作伙伴服务器帐户</p></td>
<td><p><strong>合作伙伴</strong></p></td>
<td><p><code>Internet</code> 和<code>Partner</code></p></td>
</tr>
</tbody>
</table>


返回顶部

## 自定义接收连接器上的邮件头防火墙

如果要对自定义接收连接器方案中的邮件应用邮件头防火墙，请使用以下任意一种方法：

  - 创建具有将邮件头防火墙自动应用于邮件的使用类型的接收连接器。请注意，只有当创建接收连接器时才可以设置使用类型。
    
      - 若要从邮件中删除组织 X-header 或林 X-header，请创建接收连接器，并选择除 `Internal` 之外的其他使用类型。
    
      - 若要从邮件中删除路由邮件头，请执行下列操作之一：
        
          - 创建一个接收连接器，选择使用类型 `Custom`。不要向接收连接器分配任何权限组。
        
          - 修改现有的接收连接器，并将 *PermissionGroups* 参数的值设置为 `None`。
        
        请注意，如果您有一个未分配权限组的接收连接器，则需要根据最后一步中所述，向接收连接器中添加安全主体。

  - 使用 **Remove-ADPermission** cmdlet 从在接收连接器上配置的安全主体中删除 **Ms-Exch-Accept-Headers-Organization** 权限、**Ms-Exch-Accept-Headers-Forest** 权限和 **Ms-Exch-Accept-Headers-Routing** 权限。此方法不适用于已在接收连接器上使用权限组向安全主体分配权限的情况，因为您无法修改权限组的权限分配或组成员身份。

  - 使用 **Add-ADPermission** cmdlet 添加接收连接器上邮件流所需的相应安全主体。确保没有向任何安全主体分配 **Ms-Exch-Accept-Headers-Organization** 权限、**Ms-Exch-Accept-Headers-Forest** 权限和 **Ms-Exch-Accept-Headers-Routing** 权限。如有必要，使用 **Add-ADPermission** cmdlet 拒绝向接收连接器上配置的安全主体分配 **Ms-Exch-Accept-Headers-Organization** 权限、**Ms-Exch-Accept-Headers-Forest** 权限和 **Ms-Exch-Accept-Headers-Routing** 权限。

有关详细信息，请参阅下列主题：

  - [接收连接器](receive-connectors-exchange-2013-help.md)

  - [Add-ADPermission](https://technet.microsoft.com/zh-cn/library/bb124403\(v=exchg.150\))

  - [Remove-ADPermission](https://technet.microsoft.com/zh-cn/library/aa996048\(v=exchg.150\))

返回顶部

## 发送连接器上出站邮件的邮件头防火墙

下表描述发送连接器上邮件头防火墙权限的默认应用。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>权限</th>
<th>拥有分配的权限的默认 Exchange 安全主体</th>
<th>将安全主体分配给发送连接器的默认使用类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Ms-Exch-Send-Headers-Organization</strong> 和 <strong>Ms-Exch-Send-Headers-Forest</strong></p></td>
<td><ul>
<li><p>集线器传输服务器</p></li>
<li><p>边缘传输服务器</p></li>
<li><p>Exchange Servers</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>仅在集线器传输服务器上</td>
</tr>
</tbody>
</table>

</li>
<li><p>外部安全服务器</p></li>
<li><p><strong>ExchangeLegacyInterop</strong> 通用安全组</p></li>
</ul></td>
<td><p><code>Internal</code></p></td>
</tr>
<tr class="even">
<td><p><strong>Ms-Exch-Send-Headers-Routing</strong></p></td>
<td><ul>
<li><p>集线器传输服务器</p></li>
<li><p>边缘传输服务器</p></li>
<li><p>Exchange Servers</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>仅在集线器传输服务器上</td>
</tr>
</tbody>
</table>

</li>
<li><p>外部安全服务器</p></li>
<li><p><strong>ExchangeLegacyInterop</strong> 通用安全组</p></li>
</ul></td>
<td><p><code>Internal</code></p></td>
</tr>
<tr class="odd">
<td><p><strong>Ms-Exch-Send-Headers-Routing</strong></p></td>
<td><p>匿名用户帐户</p></td>
<td><p><code>Internet</code></p></td>
</tr>
<tr class="even">
<td><p><strong>Ms-Exch-Send-Headers-Routing</strong></p></td>
<td><p>伙伴服务器</p></td>
<td><p><code>Partner</code></p></td>
</tr>
</tbody>
</table>


返回顶部

## 自定义发送连接器上的邮件头防火墙

如果要对自定义发送连接器方案中的邮件应用邮件头防火墙，请使用以下任意一种方法：

  - 创建具有将邮件头防火墙自动应用于邮件的使用类型的发送连接器。请注意，只有当创建发送连接器时才可以设置使用类型。
    
      - 若要从邮件中删除组织 X-header 或林 X-header，请创建发送连接器，并选择除 `Internal` 或 `Partner` 之外的其他使用类型。
    
      - 若要从邮件中删除路由邮件头，请创建发送连接器，并选择 `Custom` 使用类型。可将 **Ms-Exch-Send-Headers-Routing** 权限分配给除 `Custom` 之外的所有发送连接器使用类型。

  - 从连接器删除分配 **Ms-Exch-Send-Headers-Organization** 权限、**Ms-Exch-Send-Headers-Forest** 和 **Ms-Exch-Send-Headers-Routing** 权限的安全主体。

  - 使用 **Remove-ADPermission** cmdlet 从在发送连接器上配置的安全主体之一中删除 **Ms-Exch-Send-Headers-Organization** 权限、**Ms-Exch-Send-Headers-Forest** 权限和 **Ms-Exch-Send-Headers-Routing** 权限。

  - 使用 **Add-ADPermission** cmdlet 拒绝向发送连接器上配置的安全主体之一添加 **Ms-Exch-Send-Headers-Organization** 权限、**Ms-Exch-Send-Headers-Forest** 权限和 **Ms-Exch-Send-Headers-Routing** 权限。

有关详细信息，请参阅下列主题：

  - [发送连接器](send-connectors-exchange-2013-help.md)

  - [Add-ADPermission](https://technet.microsoft.com/zh-cn/library/bb124403\(v=exchg.150\))

  - [Remove-ADPermission](https://technet.microsoft.com/zh-cn/library/aa996048\(v=exchg.150\))

返回顶部

## 其他邮件源的邮件头防火墙

邮件不使用发送连接器或接收连接器就可以进入邮箱服务器或边缘传输服务器上的传输管道中。邮件头防火墙应用于下表所述的其他邮件源：

  - **分拣目录和重播目录**   分拣目录由管理员或应用程序用来提交邮件文件。重播目录用于重新提交从 Exchange 邮件队列中导出的邮件。有关分拣目录和重播目录的详细信息，请参阅[拾取目录和重播目录](pickup-directory-and-replay-directory-exchange-2013-help.md)。
    
    组织 X-header、林 X-header 和路由邮件头从分拣目录中的邮件文件中删除。
    
    路由邮件头保留在重播目录提交的邮件中。
    
    是否在重播目录中的邮件内保留组织 X-header 和林 X-header 由 **X-CreatedBy:** 控制。邮件文件中的邮件头字段：
    
      - 如果 **X-CreatedBy:** 的值是 `MSExchange15`，则组织 X-header 和林 X-header 会保留在邮件中。
    
      - 如果 **X-CreatedBy:** 的值不是 `MSExchange15`，则组织 X-header 和林 X-header 会从邮件中删除。
    
      - 如果邮件文件中不存在 **X-CreatedBy:** 邮件头字段，则组织 X-header 和林 X-header 会从邮件中删除。

  - **投递目录**   投递目录由邮箱服务器上的外部连接器使用，用于将邮件发送到不使用 SMTP 来传输邮件的邮件传递服务器。有关外部连接器的详细信息，请参阅[外部连接器](foreign-connectors-exchange-2013-help.md)。
    
    在邮件文件放入投递目录之前，组织 X-header 和林 X-header 从邮件文件中删除。
    
    路由邮件头保留在投递目录提交的邮件中。

  - **邮箱传输**   邮箱服务器上装有邮箱传输服务，用于在邮箱服务器上向邮箱和从邮箱传输邮件。有关邮箱传输服务的详细信息，请参阅[邮件流](mail-flow-exchange-2013-help.md)。
    
    组织 X-header、林 X-header 和路由邮件头从通过邮箱传输提交服务从邮箱发送的传出邮件中删除。
    
    路由邮件头保留在通过邮箱传输提交服务发送给邮箱收件人的入站邮件中。下列组织 X-header 保留在通过邮箱传输提交服务发送给邮箱收件人的入站邮件中：
    
      - **X-MS-Exchange-Organization-SCL**
    
      - **X-MS-Exchange-Organization-AuthDomain**
    
      - **X-MS-Exchange-Organization-AuthMechanism**
    
      - **X-MS-Exchange-Organization-AuthSource**
    
      - **X-MS-Exchange-Organization-AuthAs**
    
      - **X-MS-Exchange-Organization-OriginalArrivalTime**
    
      - **X-MS-Exchange-Organization-OriginalSize**

  - **DSN 邮件**   组织 X-header、林 X-header 和路由邮件头从原始邮件或附加到 DSN 邮件的原始邮件头中删除。有关 DSN 邮件的详细信息，请参阅[Exchange 2013 中的 DSN 和 NDR](dsns-and-ndrs-in-exchange-2013-exchange-2013-help.md)。

  - **传输代理提交**   组织 X-header、林 X-header 和路由邮件头保留在传输代理提交的邮件中。

返回顶部

## Exchange 中的组织 X-header 和林 X-header

邮箱服务器或边缘传输服务器上的传输服务将自定义 X-header 字段插入到邮件头中。

组织 X-header 均以 **X-MS-Exchange-Organization-** 作为开头。林 X-header 均以 **X-MS-Exchange-Forest-** 作为开头。下表介绍了一些在 Exchange 组织内的邮件中使用的组织 X-header 和林 X-header。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>X-header</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>X-MS-Exchange-Forest-RulesExecuted</strong></p></td>
<td><p>对邮件施加的传输规则。</p></td>
</tr>
<tr class="even">
<td><p><strong>X-MS-Exchange-Organization-Antispam-Report</strong></p></td>
<td><p>内容筛选器代理应用于邮件的反垃圾邮件筛选结果的摘要。</p></td>
</tr>
<tr class="odd">
<td><p><strong>X-MS-Exchange-Organization-AuthAs</strong></p></td>
<td><p>指定身份验证源。在对邮件的安全性进行评估之后，该 X-header 始终存在。可能的值是 <code>Anonymous</code>、<code>Internal</code>、<code>External</code> 或 <code>Partner</code>。</p></td>
</tr>
<tr class="even">
<td><p><strong>X-MS-Exchange-Organization-AuthDomain</strong></p></td>
<td><p>在域安全身份验证期间进行填充。该值是经过身份验证的远程域的 FQDN。</p></td>
</tr>
<tr class="odd">
<td><p><strong>X-MS-Exchange-Organization-AuthMechanism</strong></p></td>
<td><p>为提交邮件指定身份验证机制。它的值是 2 位的十六进制数字。</p></td>
</tr>
<tr class="even">
<td><p><strong>X-MS-Exchange-Organization-AuthSource</strong></p></td>
<td><p>指定代表组织对邮件的身份验证进行评估的服务器计算机的 FQDN。</p></td>
</tr>
<tr class="odd">
<td><p><strong>X-MS-Exchange-Organization-Journal-Report</strong></p></td>
<td><p>标识传输中的日记报告。一旦邮件离开传输服务之后，邮件头会变为 <strong>X-MS-Journal-Report</strong>。</p></td>
</tr>
<tr class="even">
<td><p><strong>X-MS-Exchange-Organization-OriginalArrivalTime</strong></p></td>
<td><p>标识邮件第一次进入 Exchange 组织的时间。</p></td>
</tr>
<tr class="odd">
<td><p><strong>X-MS-Exchange-Organization-Original-Sender</strong></p></td>
<td><p>在隔离邮件第一次进入 Exchange 组织时标识该邮件的原始发件人。</p></td>
</tr>
<tr class="even">
<td><p><strong>X-MS-Exchange-Organization-OriginalSize</strong></p></td>
<td><p>在隔离邮件第一次进入 Exchange 组织时标识该邮件的原始大小。</p></td>
</tr>
<tr class="odd">
<td><p><strong>X-MS-Exchange-Organization-Original-Scl</strong></p></td>
<td><p>在隔离邮件第一次进入 Exchange 组织时标识该邮件的原始 SCL。</p></td>
</tr>
<tr class="even">
<td><p><strong>X-MS-Exchange-Organization-PCL</strong></p></td>
<td><p>标识仿冒可能性等级。可能的仿冒可能性等级值在 1 到 8 之间。较大的值表明邮件是可疑邮件。有关详细信息，请参阅<a href="anti-spam-stamps-exchange-2013-help.md">反垃圾邮件标记</a>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>X-MS-Exchange-Organization-Quarantine</strong></p></td>
<td><p>表示邮件已被隔离在垃圾邮件隔离邮箱中，并且已发送发送状态通知 (DSN)。或者，它表明邮件曾被隔离，但又被管理员释放。该 X-header 字段防止将释放的邮件再次提交到垃圾邮件隔离邮箱中。有关详细信息，请参阅<a href="release-quarantined-messages-from-the-spam-quarantine-mailbox-exchange-2013-help.md">从垃圾邮件隔离邮箱中释放隔离的邮件</a>。</p></td>
</tr>
<tr class="even">
<td><p><strong>X-MS-Exchange-Organization-SCL</strong></p></td>
<td><p>标识邮件的 SCL。可能的 SCL 值在 0 到 9 之间。较大的值表明邮件是可疑邮件。特殊值 -1 可使内容筛选器代理不处理邮件。有关详细信息，请参阅<a href="content-filtering-exchange-2013-help.md">内容筛选</a>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>X-MS-Exchange-Organization-SenderIdResult</strong></p></td>
<td><p>包含发件人 ID 代理的结果。发件人 ID 代理使用发送方策略框架 (SPF) 比较邮件的源 IP 地址与发件人的电子邮件地址中使用的域。发件人 ID 结果用于计算邮件的 SCL。有关详细信息，请参阅<a href="sender-id-exchange-2013-help.md">发件人 ID</a>。</p></td>
</tr>
</tbody>
</table>


返回顶部

