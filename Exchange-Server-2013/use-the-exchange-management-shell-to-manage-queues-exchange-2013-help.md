---
title: '使用 Exchange 命令行管理程序管理队列: Exchange 2013 Help'
TOCTitle: 使用 Exchange 命令行管理程序管理队列
ms:assetid: 5433c1d3-ad2e-4f82-b50d-b67964b32f26
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa998047(v=EXCHG.150)
ms:contentKeyID: 51408229
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 使用 Exchange 命令行管理程序管理队列

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-03-09_

与之前版本的 Exchange 一样，您可以使用 Microsoft Exchange Server 2013 中的 Exchange 命令行管理程序来查看有关队列和队列中邮件的信息，并对队列和邮件执行管理操作。在 Exchange 2013 中，队列存在于邮箱服务器和边缘传输服务器中。本主题将这些服务器称为*传输服务器*。

使用命令行管理程序在传输服务器上查看和管理队列以及队列中的邮件时，了解如何识别要管理的队列或邮件至关重要。通常，传输服务器中包含大量要传递的队列和邮件。可使用队列和邮件管理 cmdlet 上提供的筛选参数识别要查看或管理的队列或邮件。

请注意，也可以使用 Exchange 工具箱中的队列查看器管理队列和队列中的邮件。但是，与队列查看器相比，队列和邮件查看 cmdlet 支持更多的可筛选属性和筛选器选项。有关使用队列查看器的详细信息，请参阅[队列查看器](queue-viewer-exchange-2013-help.md)。

**目录**

  - Queue filtering parameters
    
      - Queue identity
    
      - Queue Filter parameter
    
      - Include and Exclude parameters

  - Get-QueueDigest

  - Message filtering parameters
    
      - Message identity
    
      - Message Filter parameter
    
      - Queue parameter

  - Comparison operators to use when filtering queues or messages

  - Advanced paging parameters

## 队列筛选参数

下表描述了队列管理 cmdlet 上提供的筛选参数。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Cmdlet</th>
<th>筛选参数</th>
<th>注释</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Get-Queue</strong></p></td>
<td><p><em>Identity</em></p>
<p><em>Filter</em></p>
<p><em>Include</em></p>
<p><em>Exclude</em></p></td>
<td><p>不能在同一命令中同时使用 <em>Identity</em> 参数和 <em>Filter</em> 参数。不能在同一命令中同时使用 <em>Include</em>、<em>Exclude</em> 和 <em>Filter</em> 参数。</p></td>
</tr>
<tr class="even">
<td><p><strong>Resume-Queue</strong></p>
<p><strong>Retry-Queue</strong></p>
<p><strong>Suspend-Queue</strong></p></td>
<td><p><em>Identity</em></p>
<p><em>Filter</em></p></td>
<td><p>需要使用 <em>Identity</em> 参数或 <em>Filter</em> 参数，但是不能在同一命令中同时使用。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Get-QueueDigest</strong></p></td>
<td><p><em>Server</em></p>
<p><em>Dag</em></p>
<p><em>Site</em></p>
<p><em>Forest</em></p>
<p><em>Filter</em></p></td>
<td><p>需要使用 <em>Server</em>、<em>Dag</em>、<em>Site</em> 或 <em>Forest</em> 参数，但是不能在同一命令中同时使用。可以将 <em>Filter</em> 参数与任何其他筛选参数一起使用。</p></td>
</tr>
</tbody>
</table>


请注意，所有队列管理 cmdlet 中都提供 *Server* 参数。在 **Get-QueueDigest** cmdlet 中，*Server* 参数是作用域参数，用于指定要在其中查看队列摘要信息的一个或多个服务器。在所有其他队列管理 cmdlet 中，使用 *Server* 参数连接到特定的服务器，并在该服务器上运行队列管理命令。可以将 *Server* 参数与 *Filter* 参数一起使用，也可以不一起使用，但是不能将 *Server* 参数与 *Identity* 参数一起使用。可以将传输服务器的主机名或 FQDN 与 *Server* 参数一起使用。

返回顶部

## 队列标识

队列管理 cmdlet 中的 *Identity* 参数用于标识特定队列。使用 *Identity* 参数时，不能指定任何其他队列筛选参数，因为您已唯一标识了该队列。*Identity* 参数使用基本语法 *\<Server\>*\\*\<Queue\>*。

*\<Server\>* 占位符是 Exchange 服务器的主机名或 FQDN，例如 `mailbox01` 或 `mailbox01.contoso.com`。如果省略 *\<Server\>* 限定符，则表示使用本地主机。

\<*Queue*\> 占位符接受下列值之一：

  - **永久队列名**   永久队列在所有邮箱或边缘传输服务器中拥有唯一、一致的名称。永久队列名为：
    
      - **提交**   此队列包含等待分类程序处理的邮件。
    
      - **无法到达**   此队列包含无法路由的邮件。放入邮件之前，此队列不存在。
    
      - **带毒**   此队列包含被确定为对 Exchange 服务器有害的邮件。放入邮件之前，此队列不存在。

  - **传递队列名称**   传递队列的名称为队列 **NextHopDomain** 属性的值。例如，队列名称可以是发送连接器的地址空间、Active Directory 站点的名称或 DAG 的名称。有关详细信息，请参阅[队列](queues-exchange-2013-help.md)主题中的\&quot;NextHopSolutionKey\&quot;一节。

  - **队列整数**   在队列数据库中为传递队列和卷影队列分配了唯一的整数值。但是，需要运行 **Get-Queue** cmdlet 在 **Identity** 或 **QueueIdentity** 属性中查找队列的整数值。

  - **卷影队列名称**   卷影队列使用语法 `Shadow\`*\<QueueInteger\>*

下表总结了可以在队列管理 cmdlet 中与 *Identity* 参数一起使用的语法。在所有的值中，*\<Server\>* 是服务器的主机名或 FQDN。

### 队列标识格式

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>标识参数值</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>&lt;Server&gt;\&lt;PersistentQueueName&gt;</code> 或者<code>&lt;PersistentQueueName&gt;</code></p></td>
<td><p>指定服务器或本地服务器上的永久队列。</p>
<p><em>&lt;PersistentQueueName&gt;</em> 为 <code>Submission</code>、<code>Unreachable</code> 或 <code>Poison</code>。</p></td>
</tr>
<tr class="even">
<td><p><code>&lt;Server&gt;\&lt;NextHopDomain&gt;</code> 或者<code>&lt;NextHopDomain&gt;</code></p></td>
<td><p>指定服务器或本地服务器上的传递队列。</p>
<p><em>&lt;NextHopDomain&gt;</em> 是队列中邮件的路由目标或传递组。有关详细信息，请参阅<a href="queues-exchange-2013-help.md">队列</a>主题中的&amp;quot;NextHopSolutionKey&amp;quot;一节。</p></td>
</tr>
<tr class="odd">
<td><p><code>&lt;Server&gt;\&lt;QueueInteger&gt;</code> 或者<code>&lt;QueueInteger&gt;</code></p></td>
<td><p>指定服务器或本地服务器上的传递队列。</p>
<p><em>&lt;QueueInteger&gt;</em> 是队列的唯一整数值，显示在 <strong>Get-Queue</strong> cmdlet 的 <strong>Identity</strong> 属性中。</p></td>
</tr>
<tr class="even">
<td><p><code>&lt;Server&gt;\Shadow\&lt;QueueInteger&gt;</code> 或者<code>Shadow\&lt;QueueInteger&gt;</code></p></td>
<td><p>指定服务器或本地服务器上的卷影队列。</p></td>
</tr>
<tr class="odd">
<td><p><code>&lt;Server&gt;\*</code> 或者<code>*</code></p></td>
<td><p>指定服务器或本地服务器上的所有队列。请注意，这些值只能与 <strong>Get-Queue</strong> cmdlet 一起使用。</p></td>
</tr>
</tbody>
</table>


返回顶部

## 队列筛选器参数

可以在所有队列管理 cmdlet 中使用 *Filter* 参数，以根据队列的属性指定要查看或管理的队列。*Filter* 参数使用比较运算符创建表达式，该表达式将队列操作限制为满足筛选器条件的队列。可以使用 `-and` 逻辑运算符来指定结果必须匹配的多个条件。

有关可以与 *Filter* 参数一起使用的队列属性的完整列表，请参阅[队列](queues-exchange-2013-help.md)。

有关可以与 *Filter* 参数一起使用的比较运算符的列表，请参阅本主题中的Comparison operators to use when filtering queues or messages部分。

有关使用 *Filter* 参数查看和管理队列过程的示例，请参阅[管理队列](manage-queues-exchange-2013-help.md)。

返回顶部

## 包括和排除参数

Exchange 2013 在 `Get-Queue` cmdlet 中有可用参数 *Include* 和 *Exclude*。可以单独、一起或与 *Filter* 参数一起使用这些参数，在本地或指定传输服务器上对队列结果进行微调。例如，可以：

  - 从结果中排除空队列。

  - 从结果中排除指向外部目标的队列。

  - 在结果中包含拥有特定 **DeliveryType** 值的队列。

*Include* 和 *Exclude* 参数使用以下队列属性筛选队列：


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>值</th>
<th>描述</th>
<th>命令行管理程序代码示例</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>DeliveryType</code></p></td>
<td><p>此值根据 <strong>DeliveryType</strong> 属性包括或排除队列。可以指定用逗号分隔的多个值。<strong>DeliveryType</strong> 的有效值在<a href="queues-exchange-2013-help.md">队列</a>主题中的&amp;quot;NextHopSolutionKey&amp;quot;部分进行了说明。</p></td>
<td><p>此示例返回本地服务器上的所有传递队列，其中，下一个跃点是本地服务器上针对智能主机路由进行配置的发送连接器：</p>
<p><code>Get-Queue -Include SmartHostConnectorDelivery</code></p></td>
</tr>
<tr class="even">
<td><p><code>Empty</code></p></td>
<td><p>此值包括或排除空队列。空队列在 <strong>MessageCount</strong> 属性中拥有值 <code>0</code>。</p></td>
<td><p>此示例返回本地服务器上包含邮件的所有队列</p>
<p><code>Get-Queue -Exclude Empty</code></p></td>
</tr>
<tr class="odd">
<td><p><code>External</code></p></td>
<td><p>此值包括或排除在 <strong>NextHopCategory</strong> 属性中值为 <code>External</code> 的队列。</p>
<p>外部队列的 <strong>DeliveryType</strong> 值始终是以下项之一：</p>
<ul>
<li><p><code>DeliveryAgent</code></p></li>
<li><p><code>DnsConnectorDelivery</code></p></li>
<li><p><code>NonSmtpGatewayDelivery</code></p></li>
<li><p><code>SmartHostConnectorDelivery</code></p></li>
</ul>
<p>有关详细信息，请参阅<a href="queues-exchange-2013-help.md">队列</a>主题中的&amp;quot;NextHopSolutionKey&amp;quot;一节。</p></td>
<td><p>此示例返回本地服务器上的所有内部队列</p>
<p><code>Get-Queue -Exclude External</code></p></td>
</tr>
<tr class="even">
<td><p><code>Internal</code></p></td>
<td><p>此值包括或排除在 <strong>NextHopCategory</strong> 属性中值为 <code>Internal</code> 的队列。有关详细信息，请参阅<a href="queues-exchange-2013-help.md">队列</a>主题中的&amp;quot;NextHopSolutionKey&amp;quot;一节。</p></td>
<td><p>此示例返回本地服务器上的所有内部队列。</p>
<p><code>Get-Queue -Include Internal</code></p></td>
</tr>
</tbody>
</table>


请注意，可以使用 *Filter* 参数复制 *Include* 和 *Exclude* 参数的功能。例如，命令 `Get-Queue -Exclude Empty` 得到的结果与 `Get-Queue -Filter {MessageCount -gt 0}` 相同。但是，*Include* 和 *Exclude* 参数的语法更简单且更容易记忆。

返回顶部

## Get-QueueDigest

Exchange 2013 添加一个名为 **Get-QueueDigest** 的新队列 cmdlet。此 cmdlet 让您能够使用单个命令查看有关 Exchange 组织中部分或全部队列的信息。具体来说，**Get-QueueDigest** cmdlet 让您能够根据队列在服务器、DAG、Active Directory 站点或整个 Active Directory 林中的位置来查看队列信息。请注意，外围网络中已订阅的边缘传输服务器上的队列不包括在结果中。此外，**Get-QueueDigest** 在边缘传输服务器中可用，但结果仅限于边缘传输服务器上的队列。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>默认情况下，<strong>Get-QueueDigest</strong> cmdlet 显示包含 10 封或更多邮件的传递队列，而且结果每一到两分钟更新一次。有关如何更改这些默认值的说明，请参阅 <a href="configure-get-queuedigest-exchange-2013-help.md">配置 Get-QueueDigest</a>。</td>
</tr>
</tbody>
</table>


下表中介绍了适用于 **Get-QueueDigest** cmdlet 的筛选和排序参数。


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
<td><p><em>Dag</em>、<em>Server</em> 或 <em>Site</em></p></td>
<td><p>这些参数是互斥的，用于设置 cmdlet 的作用域。需要指定其中一个参数或 <em>Forest</em> 开关。通常，您会使用服务器、DAG 或 Active Directory 站点的名称，但是您也可以使用唯一标识服务器、DAG 或站点的任何值。可以指定用逗号分隔的多个服务器、DAG 或站点。</p></td>
</tr>
<tr class="even">
<td><p><em>Forest</em></p></td>
<td><p>如果不使用 <em>Dag</em>、<em>Server</em> 或 <em>Site</em> 参数，则需要此开关。不为此开关指定值。通过使用此开关，您可以获取来自 Active Directory 林中所有 Exchange 2013 邮箱服务器的队列。不能使用 <em>Forest</em> 开关查看远程 Active Directory 林中的队列。</p></td>
</tr>
<tr class="odd">
<td><p><em>DetailsLevel</em></p></td>
<td><p>此参数接受值 <code>None</code>、<code>Normal</code> 和 <code>Verbose</code>。默认值为 <code>Normal</code>。使用值 <code>None</code> 时，会在结果中的&amp;quot;详细信息&amp;quot;列中省略队列名称。</p></td>
</tr>
<tr class="even">
<td><p><em>Filter</em></p></td>
<td><p>此参数让您能够根据队列属性筛选队列。可以使用<a href="queue-filters-exchange-2013-help.md">队列筛选器</a>主题中描述的任何可筛选队列属性。</p></td>
</tr>
<tr class="odd">
<td><p><em>GroupBy</em></p></td>
<td><p>此参数对队列结果进行分组。可以按以下属性之一对结果进行分组：</p>
<ul>
<li><p>DeliveryType</p></li>
<li><p>LastError</p></li>
<li><p>NextHopCategory</p></li>
<li><p>NextHopDomain</p></li>
<li><p>NextHopKey</p></li>
<li><p>Status</p></li>
<li><p>ServerName</p></li>
</ul>
<p>默认情况下，会按 <code>NextHopDomain</code> 对结果进行分组。有关这些队列属性的详细信息，请参阅<a href="queue-filters-exchange-2013-help.md">队列筛选器</a>。</p></td>
</tr>
<tr class="even">
<td><p><em>ResultSize</em></p></td>
<td><p>此参数将队列结果限制为您指定的值。队列根据其中包含的邮件数按降序进行排序，并按照 <em>GroupBy</em> 参数指定的值进行分组。默认值为 1000。也就是说，默认情况下，该命令显示按 <strong>NextHopDomain</strong> 分组的前 1000 个队列，并按照从包含最多邮件的队列到包含最少邮件的队列顺序排序。</p></td>
</tr>
<tr class="odd">
<td><p><em>Timeout</em></p></td>
<td><p>参数指定操作在多少秒后超时。默认值是 <code>00:00:10</code> 或 10 秒。</p></td>
</tr>
</tbody>
</table>


此示例返回名为 Mailbox01、Mailbox02 和 Mailbox03 的 Exchange 2013 邮箱服务器上的所有非空外部队列。

    Get-QueueDigest -Server Mailbox01,Mailbox02,Mailbox03 -Include External -Exclude Empty

返回顶部

## 邮件筛选参数

下表描述了邮件管理 cmdlet 上提供的筛选参数。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Cmdlet</th>
<th>筛选参数</th>
<th>注释</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Get-Message</strong></p></td>
<td><p><em>Identity</em></p>
<p><em>Filter</em></p>
<p><em>Queue</em></p></td>
<td><p>所有筛选参数都是互斥的，可以在同一个命令中一起使用。</p></td>
</tr>
<tr class="even">
<td><p><strong>Remove-Message</strong></p>
<p><strong>Resume-Message</strong></p>
<p><strong>Suspend-Message</strong></p></td>
<td><p><em>Identity</em></p>
<p><em>Filter</em></p></td>
<td><p>需要使用 <em>Identity</em> 参数或 <em>Filter</em> 参数，但是不能在同一命令中同时使用。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Export-Message</strong></p></td>
<td><p><em>Identity</em></p></td>
<td><p><em>Identity</em> 参数为必要参数。</p></td>
</tr>
</tbody>
</table>


请注意，*Server* 参数在所有邮件管理 cmdlet 上可用，除了 **Export-Message** cmdlet。使用 *Server* 参数连接到特定服务器，并在该服务器上运行邮件管理命令。可以将 *Server* 参数与 *Filter* 参数一起使用，也可以不一起使用，但是不能将 *Server* 参数与 *Identity* 参数一起使用。可以将传输服务器的主机名或 FQDN 与 *Server* 参数一起使用。

返回顶部

## 邮件标识

邮件管理 cmdlet 中的 *Identity* 参数标识一个或多个队列中的特定邮件。使用 *Identity* 参数时，不能指定任何其他邮件筛选参数，因为您已唯一标识了该邮件。*Identity* 参数使用基本语法 *\<Server\>*\\*\<Queue\>*\\*\<MessageInteger\>*。

*\<Server\>* 占位符是 Exchange 服务器的主机名或 FQDN，例如 `mailbox01` 或 `mailbox01.contoso.com`。如果省略 *\<Server\>* 限定符，则表示使用本地主机。

\<*Queue*\> 占位符接受本主题中\&quot;队列标识\&quot;部分描述的队列标识。例如，可以使用队列数据库中的永久队列名、**NextHopDomain** 值，或队列的唯一整数值。

*\<MessageInteger\>* 占位符代表邮件首次进入服务器中的队列数据库时为其分配的唯一整数值。如果将邮件发送给需要多个队列的多个收件人，则队列数据库中所有队列中的全部邮件副本具有相同的整数值。但是，需要运行 **Get-Message** cmdlet 在 **Identity** 或 **MessageIdentity** 属性中查找邮件的整数值。

下表总结了可以在邮件管理 cmdlet 中与 *Identity* 参数一起使用的语法。在所有的值中，*\<Server\>* 是服务器的主机名或 FQDN。

### 邮件标识格式

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>标识参数值</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>&lt;Server&gt;\&lt;Queue&gt;\&lt;MessageInteger&gt;</code> 或者<code>&lt;Queue&gt;\&lt;MessageInteger&gt;</code></p></td>
<td><p>指定服务器或本地服务器上的特定队列中的邮件。</p>
<p><em>&lt;MessageInteger&gt;</em> 是邮件的唯一整数值，显示在 <strong>Get-Message</strong> cmdlet 的 <strong>Identity</strong> 属性中。</p>
<p><em>&lt;Queue&gt;</em>   代表以下值之一：</p>
<ul>
<li><p><strong>永久队列名</strong>   值 <code>Submission</code>、<code>Unreachable</code> 或 <code>Poison</code>。</p></li>
<li><p><strong>传递队列名称</strong>   队列的 <strong>NextHopDomain</strong> 属性的值，实际上是队列的名称。此值可能是路由目标或传递组。有关详细信息，请参阅<a href="queues-exchange-2013-help.md">队列</a>主题中的&amp;quot;NextHopSolutionKey&amp;quot;一节。</p></li>
<li><p><strong>队列整数</strong>   显示在 <strong>Get-Message</strong> 或 <strong>Get-Queue</strong> cmdlet 的 <strong>Identity</strong> 属性中的传递队列或卷影队列的唯一整数值。</p></li>
<li><p><strong>卷影队列标识</strong>   卷影队列标识使用语法 <code>Shadow\&lt;QueueInteger&gt;</code>。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><code>&lt;Server&gt;\*\&lt;MessageInteger&gt;</code> 或 <code>*\&lt;MessageInteger&gt;</code> 或 <code>&lt;MessageInteger&gt;</code></p></td>
<td><p>指定服务器或本地服务器上队列数据库中所有队列中的全部邮件副本。</p></td>
</tr>
</tbody>
</table>


返回顶部

## 邮件筛选器参数

可以使用 **Get-Message**、**Remove-Message**、**Resume-Message** 和 **Suspend-Message** cmdlet 上的 *Filter* 参数根据邮件的属性指定要查看或管理的邮件。*Filter* 参数使用比较运算符创建表达式，该表达式将邮件操作限制为满足筛选器条件的邮箱。可以使用 `-and` 逻辑运算符来指定结果必须匹配的多个条件。

有关可以与 *Filter* 参数一起使用的邮件属性的完整列表，请参阅[队列](queues-exchange-2013-help.md)。

有关可以与 *Filter* 参数一起使用的比较运算符的列表，请参阅本主题中的Comparison operators to use when filtering queues or messages部分。

有关使用 *Filter* 参数查看和管理邮件过程的示例，请参阅[管理队列](manage-queues-exchange-2013-help.md)。

返回顶部

## 队列参数

*Queue* 参数只能与 **Get-Message** cmdlet 一起使用。可以使用此参数获取特定队列中的所有邮件，或使用通配符 (\*) 获取来自多个队列的所有邮件。使用 *Queue* 参数时，使用本主题中\&quot;队列标识\&quot;部分描述的队列标识格式 *\<Server\>*\\*\<Queue\>*。

返回顶部

## 筛选队列或邮件时使用的比较运算符

使用 *Filter* 参数创建队列或邮件筛选器表达式时，需要为要匹配的属性值包含比较运算符。下表列出了可在筛选表达式中使用的比较运算符以及各个运算符的功能。对于所有运算符，比较的值不区分大小写。

### 比较运算符

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>运算符</th>
<th>功能</th>
<th>命令行管理程序代码示例</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>-eq</code></p></td>
<td><p>该运算符用于指定结果必须与表达式中提供的属性值完全匹配。</p></td>
<td><p>若要显示状态为&amp;quot;重试&amp;quot;的所有队列的列表，请运行以下命令：</p>
<p><code>Get-Queue -Filter {Status -eq &quot;Retry&quot;}</code></p>
<p>显示处于&amp;quot;Retry&amp;quot;状态的所有邮件的列表：</p>
<p><code>Get-Message -Filter {Status -eq &quot;Retry&quot;}</code></p></td>
</tr>
<tr class="even">
<td><p><code>-ne</code></p></td>
<td><p>该运算符用于指定结果应与表达式中提供的属性值匹配。</p></td>
<td><p>若要显示状态不为&amp;quot;活动&amp;quot;的所有队列的列表，请运行以下命令：</p>
<p><code>Get-Queue -Filter {Status -ne &quot;Active&quot;}</code></p>
<p>若要显示状态不为&amp;quot;活动&amp;quot;的所有邮件的列表，请运行以下命令：</p>
<p><code>Get-Message -Filter {Status -ne &quot;Active&quot;}</code></p></td>
</tr>
<tr class="odd">
<td><p><code>-gt</code></p></td>
<td><p>该运算符用于值以整数或日期/时间形式表示的属性。筛选结果只包含指定属性值大于表达式中提供的值的队列或邮件。</p></td>
<td><p>若要显示当前包含的邮件数大于 1,000 的队列的列表，请运行以下命令：</p>
<p><code>Get-Queue -Filter {MessageCount -gt 1000}</code></p>
<p>显示当前重试次数超过 3 的邮件列表：</p>
<p><code>Get-Message -Filter {RetryCount -gt 3}</code></p></td>
</tr>
<tr class="even">
<td><p><code>-ge</code></p></td>
<td><p>该运算符用于值以整数或日期/时间形式表示的属性。筛选结果只包含指定属性值大于或等于表达式中提供的值的队列或邮件。</p></td>
<td><p>若要显示当前包含的邮件数等于或大于 1,000 的队列的列表，请运行以下命令：</p>
<p><code>Get-Queue -Filter {MessageCount -ge 1000}</code></p>
<p>显示当前重试次数等于或大于 3 的邮件列表：</p>
<p><code>Get-Message -Filter {RetryCount -ge 3}</code></p></td>
</tr>
<tr class="odd">
<td><p><code>-lt</code></p></td>
<td><p>该运算符用于值以整数或日期/时间形式表示的属性。筛选结果只包含指定属性值小于表达式中提供的值的队列或邮件。</p></td>
<td><p>若要显示当前包含的邮件数小于 1,000 的队列的列表，请运行以下命令：</p>
<p><code>Get-Queue -Filter {MessageCount -lt 1000}</code></p>
<p>显示 SCL 值小于 6 的邮件列表：</p>
<p><code>Get-Message -Filter {SCL -lt 6}</code></p></td>
</tr>
<tr class="even">
<td><p><code>-le</code></p></td>
<td><p>该运算符用于值以整数或日期/时间形式表示的属性。筛选结果只包含指定属性值小于或等于表达式中提供的值的队列或邮件。</p></td>
<td><p>若要显示当前包含的邮件数等于或小于 1,000 的队列的列表，请运行以下命令：</p>
<p><code>Get-Queue -Filter {MessageCount -le 1000}</code></p>
<p>显示 SCL 值等于或小于 6 的邮件列表：</p>
<p><code>Get-Message -Filter {SCL -le 6}</code></p></td>
</tr>
<tr class="odd">
<td><p><code>-like</code></p></td>
<td><p>该运算符用于以文本字符串形式表示的属性值。筛选结果只包含指定属性值包含表达式中提供的文本字符串的队列或邮件。可以在应用于文本字符串字段（而不是枚举类型的字段）的 <strong>-like</strong> 表达式中包含通配符 (*)。</p></td>
<td><p>若要显示目标为以 Contoso.com 结尾的任何 SMTP 域的传递队列的列表，请运行以下命令：</p>
<p><code>Get-Queue -Filter {Identity -like &quot;*contoso.com&quot;}</code></p>
<p>显示主题中包含&amp;quot;payday loan&amp;quot;文本的邮件列表：</p>
<p><code>Get-Messages -Filter {Subject -like &quot;*payday loan*&quot;}</code></p></td>
</tr>
</tbody>
</table>


可以使用 **-and** 比较运算符指定评估多个表达式的筛选器。队列或邮件必须满足要包含在结果中的筛选器的所有条件。

此示例显示目标为以 Contoso.com 结尾的任何 SMTP 域名并且当前包含的邮件数大于 500 的队列的列表。

    Get-Queue -Filter {Identity -like "*contoso.com*" -and MessageCount -gt 500}

此示例显示从 SCL 大于 5 的 contoso.com 域中的任何电子邮件地址发送的邮件的列表。

    Get-Message -Filter {FromAddress -like "*Contoso.com*" -and SCL -gt 5}

返回顶部

## 高级分页参数

基于当前邮件流，对队列和邮件的查询可能会返回较大的对象集。可以使用高级分页参数来控制如何检索和显示查询结果。

使用命令行管理程序查看队列和队列中的邮件时，查询每次将检索一页信息。高级分页参数可以控制结果集的大小，还可用于对结果进行排序。所有高级分页参数都是可选的，并且可以与任何一个用于 **Get-Queue** 和 **Get-Message** cmdlet 的参数集结合使用。如果未指定任何高级分页参数，则查询将按标识的升序返回结果。

默认情况下，如果指定了排序顺序，则会始终包括邮件标识属性，并以升序排序该属性。这是默认的顺序关系。由于可以按排序顺序包括的其他属性都不是唯一的，因此会包括邮件标识属性。通过按排序顺序显式包括邮件标识属性，可以指定结果显示按降序排序的邮件标识。

可以使用 *BookmarkIndex* 和 *BookmarkObject* 参数来标记排序结果集中的位置。如果在检索下一页结果时书签对象不再存在，则默认顺序关系会确保结果集将从最接近书签的对象开始。最接近的对象取决于所指定的排序顺序。

下表介绍了高级分页参数。

### 高级分页参数

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
<td><p><em>BookmarkIndex</em></p></td>
<td><p>此参数指定所显示的结果在结果集中的起始位置。此参数的值是结果集总数中从 1 开始的索引。如果值小于或等于零，则返回第一个完整的结果页。如果将值设置为 <code>Int.MaxValue</code>，则返回最后一个完整的结果页。</p></td>
</tr>
<tr class="even">
<td><p><em>BookmarkObject</em></p></td>
<td><p>此参数指定所显示的结果在结果集中的起始对象。如果指定书签对象，则该对象将被用作搜索起点。是检索该对象之前还是之后的行，取决于 <em>SearchForward</em> 参数的值。不能将 <em>BookmarkObject</em> 参数和 <em>BookmarkIndex</em> 参数在单个查询中组合使用。</p></td>
</tr>
<tr class="odd">
<td><p><em>IncludeBookmark</em></p></td>
<td><p>此参数指定是否在结果集中包括书签对象。默认情况下，该值设置为 <code>$true</code>，即包括书签对象。可以运行有限结果大小的查询，然后将该结果集中最后一个项目指定为下一个查询的书签。在这种情况下，可能需要将 <em>IncludeBookmark</em> 设置为 <code>$false</code>，以使对象不会同时包括在两个结果集中。</p></td>
</tr>
<tr class="even">
<td><p><em>ResultSize</em></p></td>
<td><p>此参数指定每页显示的结果数。如果不指定值，则使用默认结果大小 1,000 个对象。Exchange 将结果集限制为 250,000。</p></td>
</tr>
<tr class="odd">
<td><p><em>ReturnPageInfo</em></p></td>
<td><p>此参数是隐藏参数。它返回有关结果总数和当前页第一个对象的索引的信息。默认值为 <code>$false</code>。</p></td>
</tr>
<tr class="even">
<td><p><em>SearchForward</em></p></td>
<td><p>此参数指定在结果集中是向前搜索还是向后搜索。此参数不影响结果集的返回顺序。它确定相对于书签索引或对象的搜索方向。如果不指定书签索引或对象，则 <em>SearchForward</em> 参数将确定搜索是从结果集中的第一个对象开始还是从最后一个对象开始。</p>
<p>此参数的默认值是 <code>$true</code>。如果将此参数设置为 <code>$true</code> 并指定书签，则查询将从该书签向前搜索。如果使用此配置，并且结果没有超过书签，则查询将返回最后一个完整的结果页。</p>
<p>如果将 <em>SearchForward</em> 参数设置为 <code>$false</code>，并指定书签，则查询将从该书签向后搜索。如果使用此配置，并且结果没有超过书签，则查询将返回最后一个完整的结果页。</p></td>
</tr>
<tr class="odd">
<td><p><em>SortOrder</em></p></td>
<td><p>此参数指定一个邮件属性数组，用于控制结果集的排序顺序。排序顺序属性将以优先级的降序顺序来指定。每个属性均以逗号分隔，并附加加号 (+) 以按升序排序，或附加减号 (-) 以按降序排序。</p>
<p>如果不使用此参数指定显式的排序顺序，则将按各个对象类型的 Identity 字段排序和显示与查询匹配的记录。如果不显式指定排序顺序，则结果始终按标识以升序进行排序。</p></td>
</tr>
</tbody>
</table>


下列代码示例显示如何在查询中使用高级分页参数。在此示例中，该命令将连接到指定的服务器，并检索包含 500 个对象的结果集。结果以排序顺序进行显示，首先按发件人地址以升序显示，然后按邮件大小以降序显示。

`Get-Message -Server mailbox01.contoso.com -ResultSize 500 -SortOrder +FromAddress,-Size`

如果要查看连续的页，可以为在结果集中检索到的最后一个对象设置书签，并运行其他查询。需要使用命令行管理程序的脚本功能来执行此过程。

以下示例使用脚本来检索第一个结果页，然后设置书签对象，并从结果集中排除书签对象，然后在指定的服务器上检索随后的 500 个对象。

1.  打开命令行管理程序，并键入以下命令以检索第一个结果页。
    
        $Results=Get-message -Server mailbox01.contoso.com -ResultSize 500 -SortOrder +FromAddress,-Size

2.  若要设置书签对象，请键入以下命令以将第一页中的最后一个元素保存到变量中。
    
        $temp=$results[$results.length-1]

3.  若要在指定的服务器上检索接下来的 500 个对象，并排除书签对象，请键入以下命令。
    
        Get-message -Server mailbox01.contoso.com -BookmarkObject:$temp -IncludeBookmark $False -ResultSize 500 -SortOrder +FromAddress,-Size

返回顶部

