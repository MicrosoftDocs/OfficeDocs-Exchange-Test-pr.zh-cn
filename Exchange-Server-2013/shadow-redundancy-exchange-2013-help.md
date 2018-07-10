---
title: '卷影冗余: Exchange 2013 Help'
TOCTitle: 卷影冗余
ms:assetid: a40dbe61-2a18-48a8-b2e0-4e81a6678d11
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd351027(v=EXCHG.150)
ms:contentKeyID: 50491256
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 卷影冗余

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-03-09_

Microsoft Exchange Server 2010 中引入了卷影冗余，以便在将邮件传递给邮箱之前，提供邮件的冗余备份。在 Exchange 2010 中，卷影冗余延迟了从传输服务器上的传输数据库删除邮件的时间，直到服务器验证邮件传递路径中的下一个跃点已完成传递。如果在向传输服务器返回成功传递报告之前下一个跃点失败，则传输服务器会向下一个跃点重新提交邮件。Exchange 2010 服务器使用 XSHADOW 动词来公布其卷影冗余支持。如果 SMTP 服务器不支持卷影冗余，Exchange 2010 将使用基于接收连接器上设定的时间间隔的延迟确认来制作邮件的冗余备份。

Microsoft Exchange Server 2013 中卷影冗余功能的主要改进体现在，现在传输服务器能够在确认成功接收发回给发送服务器的邮件之前，为所收到的任何邮件制作冗余备份。发送服务器是否支持卷影冗余并不重要。这将有助于确保 Exchange 2013 传输管道中的所有邮件在传输过程中都变得冗余。如果 Exchange 2013 确定原始邮件在传输过程中丢失，将重新传递邮件的冗余备份。

**目录**

卷影冗余组件

卷影冗余的要求

默认情况下启用卷影冗余

如何创建卷影邮件

SMTP 超时

如何维护卷影邮件

中断后的邮件处理

## 卷影冗余组件

下表介绍卷影冗余的组件。本主题中将使用以下术语。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>术语</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>传输服务器</p></td>
<td><p>包含邮件队列、负责路由邮件的 Exchange 服务器。在 Exchange 2013 中，传输服务器即邮箱服务器（邮箱服务器上的传输服务）。</p></td>
</tr>
<tr class="even">
<td><p>传输数据库</p></td>
<td><p>Exchange 2013 传输服务器上的邮件队列数据库。卷影队列和安全网络也存储在传输数据库中。</p></td>
</tr>
<tr class="odd">
<td><p>传输高可用性边界</p></td>
<td><p>数据库可用性组 (DAG) 环境中的 DAG，或非 DAG 环境中的 Active Directory 站点。当邮件到达传输高可用性边界中的传输服务器上时，Exchange 会尝试在边界内维护传输服务器上的 2 个邮件的冗余备份。当邮件离开传输高可用性边界时，Exchange 将不再维护邮件的冗余备份。</p></td>
</tr>
<tr class="even">
<td><p>主邮件</p></td>
<td><p>提交到传输管道用于传递的邮件。</p></td>
</tr>
<tr class="odd">
<td><p>卷影邮件</p></td>
<td><p>在确认主服务器已成功处理主邮件之前一直由卷影服务器保留的邮件的冗余副本。</p></td>
</tr>
<tr class="even">
<td><p>主服务器</p></td>
<td><p>当前正在处理主邮件的传输服务器。</p></td>
</tr>
<tr class="odd">
<td><p>卷影服务器</p></td>
<td><p>保留主服务器的卷影邮件的传输服务器。传输服务器可以是某些邮件的主服务器，同时还是其他邮件的卷影服务器。</p></td>
</tr>
<tr class="even">
<td><p>卷影队列</p></td>
<td><p>卷影服务器存储卷影邮件的传递队列。对于具有多个收件人的邮件，主邮件的每个下一个跃点都需要单独的卷影队列。</p></td>
</tr>
<tr class="odd">
<td><p>丢弃状态</p></td>
<td><p>传输服务器为卷影邮件维护的指示已成功处理主邮件的信息。</p></td>
</tr>
<tr class="even">
<td><p>丢弃通知</p></td>
<td><p>卷影服务器从主服务器接收的响应，指示准备何时丢弃卷影邮件。</p></td>
</tr>
<tr class="odd">
<td><p>Safety Net</p></td>
<td><p>传输垃圾站改进的 Exchange 2013 版本。已通过邮箱服务器上的传输服务成功处理或传递给邮箱收件人的邮件将被移动到安全网络。有关详细信息，请参阅<a href="safety-net-exchange-2013-help.md">Safety Net</a>。</p></td>
</tr>
<tr class="even">
<td><p>卷影冗余管理器</p></td>
<td><p>管理卷影冗余的传输组件。</p></td>
</tr>
<tr class="odd">
<td><p>检测信号</p></td>
<td><p>主服务器和卷影服务器验证彼此的可用性的过程。</p></td>
</tr>
</tbody>
</table>


返回顶部

## 卷影冗余的要求

显然，卷影冗余需要多个 Exchange 2013 邮箱服务器。邮箱服务器可以是独立的服务器，邮箱服务器和客户端访问服务器也可以安装在同一台计算机上。

  - 如果邮箱服务器不是 DAG 的成员，则本地 Active Directory 站点中必须存在其他邮箱服务器。

  - 如果邮箱服务器是 DAG 的成员，则其他邮箱服务器必须属于同一 DAG。其他属于 DAG 的邮箱服务器可以在本地 Active Directory 站点中，也可以在远程 Active Directory 站点中。如果 DAG 跨越多个 Active Directory 站点，则卷影冗余首选在远程 Active Directory 站点创建邮件的冗余备份，以实现站点恢复功能。

在以下位置，卷影冗余无法保护传输中的邮件：

  - 单个 Exchange 服务器环境。

  - 配置不充分的 DAG。

  - 涉及邮件卷影冗余的两个或更多传输服务器同时发生故障时。

返回顶部

## 默认情况下启用卷影冗余

默认情况下，使用 **Set-TransportConfig** cmdlet 上的 *ShadowRedundancyEnabled* 参数在所有邮箱服务器上的传输服务中全局启用卷影冗余。默认情况下，如果邮箱服务器上的传输服务无法创建邮件的冗余备份，则不会拒绝该邮件。但是，如果未使用 **Set-TransportConfig** cmdlet 上的 *RejectMessageOnShadowFailure* 参数创建邮件的冗余备份，则可以将 Exchange 2013 配置为拒绝该邮件。拒绝邮件时出现暂时性故障，但发送服务器可以再次传输该邮件。SMTP 响应代码为 `451 4.4.0 Message failed to be made redundant.` 您应该将 Exchange 2013 配置为拒绝仅当组织可以使用多个 Exchange 2013 邮箱服务器时才会变得冗余的邮件。

下表介绍启用卷影冗余的参数。

### 启用卷影冗余的参数

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>参数</th>
<th>默认值</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Set-TransportConfig</strong> 上的 <em>ShadowRedundancyEnabled</em></p></td>
<td><p><code>$true</code></p></td>
<td><ul>
<li><p><code>$true</code> 启用组织中的所有传输服务器的卷影冗余。</p></li>
<li><p><code>$false</code> 禁用组织中的所有传输服务器的卷影冗余。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>Set-TransportConfig</strong> 上的 <em>RejectMessageOnShadowFailure</em></p></td>
<td><p><code>$false</code></p></td>
<td><ul>
<li><p><code>$false</code>   当无法创建邮件的卷影副本时，组织中的传输服务器无论如何都会接受主邮件。这些邮件在传输时不冗余存在。</p></li>
<li><p><code>$true</code>   在成功创建邮件的卷影副本之前，组织中的任何传输服务器都不会接受或认可该邮件。如果无法创建该邮件的卷影副本，主邮件将因暂时性错误而被拒绝。组织中的所有邮件在传输时冗余存在。</p>
<p>仅当 DAG 或 Active Directory 站点中有多个可以创建邮件的卷影副本的 Exchange 2013 邮箱服务器时，才需要将此值设置为 <code>$true</code>。</p></li>
</ul>
<p>此参数仅当 <em>ShadowRedundancyEnabled</em> 为 <code>$true</code> 时才有意义。</p></td>
</tr>
</tbody>
</table>


返回顶部

## 如何创建卷影邮件

卷影冗余的主要目标是在邮件传输过程中始终在传输高可用性边界内保留两个邮件副本。何时何地创建邮件的冗余备份取决于邮件的收件人和发件人。有三个主要决定因素：

  - 从传输高可用性边界外接收的邮件。

  - 传输高可用性边界外发送的邮件。

  - 从传输高可用性边界内的邮箱服务器的邮箱传输提交服务收到的邮件。

*传输高可用性边界*可以是下列之一：

  - DAG，表示属于 DAG 的邮箱服务器。这包括跨越多个 Active Directory 站点的 DAG。

  - Active Directory 站点，表示不属于 DAG 的邮箱服务器。

卷影冗余从不跨传输高可用性边界跟踪卷影邮件。当邮件跨过传输高可用性边界时，卷影冗余便会开始或重新启动。这会减少卷影邮件维护通信量，并防止整个传输高可用性边界发生卷影邮件重新提交。Exchange 2010 集线器传输服务器是一种特殊情况，将在本主题后文讨论。

## 从传输高可用性边界外接收的邮件

当 Exchange 2013 邮箱服务器上的传输服务从传输高可用性边界外收到一封邮件时，邮箱服务器并不关心发送服务器是否支持卷影冗余。只要启用卷影冗余，收到该邮件的邮箱服务器便会在传输高可用性边界内的另一台邮箱服务器上制作该邮件的冗余备份，然后确认收到返回给发送服务器的邮件。以下是此过程工作方式的示例：

![卷影邮件创建](images/Dd351027.a97d383b-6ae4-458d-af3a-1ac0a41cd52b(EXCHG.150).gif "卷影邮件创建")

1.  SMTP 服务器向邮箱服务器上的传输服务传输邮件。邮箱服务器是主服务器，邮件是主邮件。

2.  当 SMTP 服务器的原始 SMTP 会话仍处于活动状态时，主服务器上的传输服务会打开与组织中的另一个邮箱服务器上的传输服务同时发生的新 SMTP 会话，以创建邮件的冗余备份。
    
      - 如果主服务器是 DAG 的成员，则主服务器会连接到同一 DAG 中的不同邮箱服务器。如果 DAG 跨越多个 Active Directory 站点，则默认情况下首选不同 Active Directory 站点的邮箱服务器。此设置由 **Set-TransportService** cmdlet 上的 *ShadowMessagePreference* 参数控制。默认值为 `PreferRemote`，不过您可以将其更改为 `RemoteOnly` 或 `LocalOnly`。
    
      - 如果主服务器不是 DAG 的成员，则主服务器连接到同一 Active Directory 站点的不同邮箱服务器，无论 *ShadowMessagePreference* 参数的值如何。

3.  主服务器向其他邮箱服务器上的传输服务传输邮件的副本，同时其他邮箱服务器上的传输服务确认已成功创建邮件的副本。该邮件的副本是卷影邮件，而其所在的邮箱服务器是主服务器的卷影服务器。该邮件在卷影服务器上的卷影队列中。

4.  当主服务器收到卷影服务器的确认后，主服务器向原始 SMTP 服务器的原始 SMTP 会话确认收到主邮件，同时 SMTP 会话关闭。

## 传输高可用性边界外发送的邮件

当 Exchange 2013 传输服务器在传输高可用性边界外传输邮件时，另一侧的 SMTP 服务器确认成功收到邮件，传输服务器会将邮件移动到安全网络中。在整个传输高可用性边界内成功传输主邮件后，不会从安全网络重新提交邮件。有关安全网络的详细信息，请参阅[Safety Net](safety-net-exchange-2013-help.md)。

## 传输高可用性边界内传输的邮件

Exchange 2013 中已对邮件路由进行优化，因此当最终目标是位于 DAG 或 Active Directory 站点中时，该 DAG 或 Active Directory 站点的邮箱服务器上的传输服务之间通常不需要多个跃点。当保留邮件最终目标的 DAG 或 Active Directory 站点的邮箱服务器上的传输服务接受邮件后，该邮件的下一个跃点通常是最终目标本身。当 DAG 或 Active Directory 站点内的任何地方存在邮件的卷影副本时，卷影冗余将实现保存两个传输中邮件的副本的目标。通常，只有在 DAG 中需要用 **Redirect-Message** cmdlet 来耗尽邮箱服务器上的活动队列的故障转移方案，才需要同一传输高可用性边界内存在多个跃点。

## 同一 Active Directory 站点的 Exchange 2010 集线器传输服务器上的卷影冗余

当 Exchange 2010 集线器传输服务器向同一个 Active Directory 站点的 Exchange 2013 邮箱服务器传输邮件时，Exchange 2010 集线器传输服务器将使用 XSHADOW 命令公布卷影冗余支持，但邮箱服务器不公布此支持。这可以防止 Exchange 2010 集线器传输服务器在 Exchange 2013 邮箱服务器上创建邮件的卷影副本。

当 Exchange 2013 邮箱服务器上的传输服务向同一个 Active Directory 站点的 Exchange 2010 集线器传输服务器传输邮件时，Exchange 2013 邮箱服务器会对此 Exchange 2010 集线器传输服务器隐藏该邮件。当 Exchange 2013 邮箱服务器从 Exchange 2010 集线器传输服务器收到成功收到该邮件的确认后，Exchange 2013 邮箱服务器会将成功处理的邮件移动到安全网络中。但是，由 Exchange 2013 邮箱服务器存储在安全网络中的成功处理的邮件永远不会重新提交到 Exchange 2010 集线器传输服务器。

返回顶部

## SMTP 超时

在尝试制作邮件的冗余备份时，发送 SMTP 服务器和主服务器之间的 SMTP 连接或主服务器和卷影服务器之间的 SMTP 会话可能超时。接收连接器和发送连接器都有一个 *ConnectionInactivityTimeOut* 参数，表示连接器实际传输数据的时间。接收连接器还有一个绝对 *ConnectionTimeOut* 参数。

如果在成功创建和确认邮件的卷影副本之前有任何 SMTP 会话超时，将由 **Set-TransportConfig** cmdlet 上的 *RejectMessageOnShadowFailure* 参数来控制其结果。默认情况下，此参数的值为 `$false`，这表示无需创建卷影副本即可接受主邮件。如果此参数的值为 `$true`，主邮件将因暂时性错误 `451 4.4.0` 而被拒绝。

如果成功创建邮件的卷影副本，但是发送 SMTP 服务器和主服务器之间的 SMTP 会话超时，则主服务器会接受和处理主邮件。发送 SMTP 服务器将重新传递未确认的邮件，但是重复邮件检测将阻止 Exchange 邮箱用户看到重复邮件。当发送 SMTP 服务器重新提交邮件时，主服务器会创建邮件的另一个卷影副本。邮件重新提交期间发送 SMTP 服务器创建的卷影邮件之间没有任何关系。

下表介绍控制卷影邮件创建的参数

### 卷影邮件创建参数

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>来源</th>
<th>默认值</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Set-TransportConfig</strong> 上的 <em>ShadowMessagePreferenceSetting</em></p></td>
<td><p><code>PreferRemote</code></p></td>
<td><ul>
<li><p><code>PreferRemote</code>   尝试在不同的 Active Directory 站点的邮箱服务器上制作邮件卷影副本。如果操作失败，尝试在本地 Active Directory 站点的服务器上制作邮件的卷影副本。</p></li>
<li><p><code>LocalOnly</code>   邮件的卷影副本只能在本地 Active Directory 站点的传输服务器上制作。</p></li>
<li><p><code>RemoteOnly</code>： 邮件的卷影副本只能在不同 Active Directory 站点的传输服务器上制作。</p></li>
</ul>
<p>此参数仅当尝试制作邮件的卷影副本的主服务器是属于跨越多个 Active Directory 站点的 DAG 的邮箱服务器时才有意义。</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-TransportConfig</strong> 上的 <em>MaxRetriesForRemoteSiteShadow</em></p></td>
<td><p>4</p></td>
<td><p>当邮箱服务器是跨越多个 Active Directory 站点的 DAG 成员时使用此参数。</p>
<ul>
<li><p>如果 <em>ShadowMessagePreferenceSetting</em> 被设置为 <code>PreferRemote</code>，邮箱服务器将首先尝试在远程 Active directory 站点上的另一个邮箱服务器中创建邮件的卷影副本 <em>MaxRetriesForRemoteSiteShadow</em> 指定的次数。如果操作失败，邮箱服务器将尝试在 Active Directory 站点上的不同邮箱服务器创建邮件副本 <em>MaxRetriesForLocalSiteShadow</em> 指定的次数。</p></li>
<li><p>如果 <em>ShadowMessagePreferenceSetting</em> 被设置为 <code>RemoteOnly</code>，邮箱服务器将仅尝试在远程 Active Directory 站点的邮箱服务器中创建邮件的卷影副本 <em>MaxRetriesForRemoteSiteShadow</em> 指定的次数。</p></li>
<li><p></p></li>
</ul>
<p>当无法成功创建邮件的卷影副本时：</p>
<ul>
<li><p>如果 <em>RejectMessageOnShadowFailure</em> 为 <code>$true</code>，主邮件将拒绝并出现暂时性错误。</p></li>
<li><p>如果 <em>RejectMessageOnShadowFailure</em> 为 <code>$false</code>，将无论如何都结束主邮件，但是不冗余存在。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>Set-TransportConfig</strong> 上的 <em>MaxRetriesForLocalSiteShadow</em></p></td>
<td><p>2</p></td>
<td><p>请在下列情况中使用此参数：</p>
<ul>
<li><p>当邮箱服务器是跨越多个 Active Directory 站点的 DAG 成员。</p>
<ol>
<li><p>如果 <em>ShadowMessagePreferenceSetting</em> 被设置为 <code>PreferRemote</code>，邮箱服务器将首先尝试在远程 Active directory 站点上的另一个邮箱服务器中创建邮件的卷影副本 <em>MaxRetriesForRemoteSiteShadow</em> 指定的次数。如果操作失败，邮箱服务器将尝试在 Active Directory 站点上的不同邮箱服务器创建邮件副本 <em>MaxRetriesForLocalSiteShadow</em> 指定的次数。</p></li>
<li><p>如果 <em>ShadowMessagePreferenceSetting</em> 被设置为 <code>LocalOnly</code>，邮箱服务器将仅尝试在本地 Active Directory 站点的不同邮箱服务器中创建邮件的卷影副本 <em>MaxRetriesForLocalSiteShadow</em> 指定的次数。</p></li>
</ol></li>
<li><p>如果邮箱服务器不是 DAG 的成员，或者邮箱服务器是同一 Active Directory 站点中的 DAG 的成员，邮箱服务器将仅尝试在本地 Active Directory 站点的不同邮箱服务器中创建邮件的卷影副本 <em>MaxRetriesForLocalSiteShadow</em> 指定的次数。</p></li>
</ul>
<p>当无法成功创建邮件的卷影副本时：</p>
<ul>
<li><p>如果 <em>RejectMessageOnShadowFailure</em> 为 <code>$true</code>，主邮件将拒绝并出现暂时性错误。</p></li>
<li><p>如果 <em>RejectMessageOnShadowFailure</em> 为 <code>$false</code>，将无论如何都结束主邮件，但是不冗余存在。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>Set-ReceiveConnector</strong> 上的 <em>ConnectionInactivityTimeout</em></p></td>
<td><p>在邮箱服务器上的传输服务 5 分钟</p>
<p>在客户端访问服务器上的前端传输服务 5 分钟。</p>
<p>在边缘传输服务器上 1 分钟。</p></td>
<td><p>此参数指定在关闭连接之前，已打开的、与源邮件传递服务器的 SMTP 连接可以保持空闲的最长时间。该参数的值必须小于 <em>ConnectionTimeout</em> 参数指定的值。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-ReceiveConnector</strong> 上的 <em>ConnectionTimeout</em></p></td>
<td><p>在邮箱服务器上的传输服务 10 分钟</p>
<p>在客户端访问服务器上的前端传输服务 10 分钟。</p>
<p>在边缘传输服务器上 5 分钟。</p></td>
<td><p>此参数指定与源邮件传递服务器的 SMTP 连接可以保持打开状态的最长时间（即使源邮件传递服务器正在传输数据）。该参数的值必须大于 <em>ConnectionInactivityTimeout</em> 参数指定的值。</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-SendConnector</strong> 上的 <em>ConnectionInactivityTimeOut</em></p></td>
<td><p>10 分钟</p></td>
<td><p>此参数指定在关闭连接之前，已打开的、与目标邮件传递服务器的 SMTP 连接可以保持空闲的最长时间。</p></td>
</tr>
</tbody>
</table>


返回顶部

## 如何维护卷影邮件

成功创建卷影邮件后，卷影冗余工作才刚刚开始。主服务器和卷影服务器彼此之间需要保持联系，以跟踪邮件进度。

当主服务器成功地将邮件传输到下一个跃点，并且下一个跃点确认收到此邮件时，主服务器会在传递完成时更新邮件的*丢弃状态*。丢弃状态基本上是一封包含受监视的邮件列表的邮件。成功传递的邮件不需要保留在卷影队列中，因此当卷影服务器得知主服务器成功地将邮件传输到下一个跃点时，卷影服务器便会将卷影队列中的卷影邮件移动到安全网络中。

卷影服务器通过查询主服务器来确定卷影队列中卷影邮件的丢弃状态。如果卷影服务器出于其他无关邮件传输等任何原因打开主服务器的 SMTP 会话，卷影服务器将会发出 **XQDISCARD** 命令来确定主邮件的丢弃状态。如果在经过预先设定的时间间隔后卷影服务器未打开主服务器的 SMTP 会话，卷影服务器将会打开主服务器的 SMTP 会话并发出**XQDISCARD** 命令。时间间隔由 **Set-TransportConfig** cmdlet 上的 *ShadowHeartbeatFrequentcy* 参数控制。默认值为 2 分钟。卷影服务器打开主服务器的 SMTP 会话后，主服务器将发出*丢弃通知*响应适用于查询卷影服务器的邮件。在 Exchange 2013 中，丢弃通知存储在磁盘上，不在内存中。因此，如果 Microsoft Exchange 传输服务重新启动，丢弃通知将继续存在。服务启动后，主服务器仍然知道成功处理的邮件，并且卷影服务器可以使用这些邮件。

卷影服务器和主服务器之间的 SMTP 通信可用作*检测信号*来确定服务器的可用性。 如果卷影服务器无法在预先设定的时间间隔后打开主服务器的 SMTP 会话，或者主服务器的传输数据库有不同的数据库 ID，则卷影服务器会将自身提升为主服务器，将卷影邮件提升为主邮件，并向下一个跃点传输邮件。时间间隔由 **Set-TransportConfig** cmdlet 上的 *ShadowResubmitTimeSpan* 参数控制。默认值为 3 小时。

*卷影冗余管理器*是负责管理卷影冗余的 Exchange 2013 传输服务器的核心组件。卷影冗余管理器负责维护服务器当前正在处理的所有主邮件的以下信息：

  - 每个正在处理的主邮件的卷影服务器。

  - 要发送到卷影服务器的丢弃状态。

卷影冗余管理器负责卷影服务器在其卷影队列中包含的所有卷影邮件的下列内容：

  - 维护每个卷影邮件的主服务器的列表。

  - 比较存储邮件主副本的队列数据库的原始数据库 ID 和当前数据库 ID。

  - 核查每个主服务器是否可以对卷影邮件进行排队。

  - 处理来自主服务器的丢弃通知。

  - 在收到所有预期的丢弃通知之后将卷影邮件从卷影队列中删除。

  - 决定卷影服务器何时应该取得卷影邮件的所有权，从而成为主服务器。

  - 跟踪邮件分流和其他副作用邮件（如传递状态通知 (DSN) 和日志报告），以验证在邮件的所有支流得到全面处理之前不会发布邮件的冗余备份。

下表介绍控制卷影邮件维护方式的参数。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>参数</th>
<th>默认值</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Set-TransportConfig</strong> 上的 <em>ShadowHeartbeatFrequency</em></p></td>
<td><p>2 分钟</p></td>
<td><p>打开 SMTP 与主服务器的连接检查邮件丢弃状态之前卷影服务器等待的最长时间。</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-TransportConfig</strong> 上的 <em>ShadowResubmitTimeSpan</em></p></td>
<td><p>3 小时</p></td>
<td><p>在确定主服务器出现故障前服务器等待时间的长短，并为无法访问的主服务器假定卷影队列中的卷影邮件的所有权。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-TransportConfig</strong> 上的 <em>ShadowMessageAutoDiscardInterval</em></p></td>
<td><p>2 天</p></td>
<td><p>服务器为成功传递的邮件保留丢弃事件的时间长短。主服务器队列将丢弃事件，直到由卷影服务器查询为止。但是，如果卷影服务器不在此参数中指定的持续时间内查询主服务器，主服务器将删除排队的丢弃事件。</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-TransportConfig</strong> 上的 <em>SafetyNetHoldTime</em></p></td>
<td><p>2 天</p></td>
<td><p>成功处理的邮件在安全网络中保留的时间长短。安全网络中未确认的卷影邮件最终将于达到 <strong>Set-TransportService</strong> 上的 <em>SafetyNetHoldTime</em> 和 <em>MessageExpirationTimeout</em> 总和后过期。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-TransportService</strong> 上的 <em>MessageExpirationTimeout</em></p></td>
<td><p>2 天</p></td>
<td><p>邮件在到期之前可以保留在队列中多长时间。</p></td>
</tr>
</tbody>
</table>


返回顶部

## 中断后的邮件处理

卷影冗余可以最大限度地减少由于服务器中断而造成的邮件丢失。传输服务器在中断后重新联机时，可能会出现下列两个情况：

  - **服务器使用新的传输数据库重新联机**   在这种情况下，传输数据库会由于数据损坏或硬件故障而无法恢复。此时，因为传输服务器将具有新的数据库 ID，组织中的其他传输服务器会将其识别为新路由。这同样适用于服务器无法恢复的情况，此时会将新服务器设置为替代服务器。

  - **服务器使用同一传输数据库重新联机**   在这种情况下，特定的传输服务器没有失败，而是长时间处于脱机状态，以便卷影服务器确定邮件的所有权并重新提交邮件。例如，网卡故障、长期维护服务器可能导致这种情况。

下表总结了卷影冗余对下面两种方案的响应方式。为清晰起见，假定中断的服务器名为 Mailbox01。

### 恢复方案中的邮件处理

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>恢复方案</th>
<th>执行的操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Mailbox01 会使用新的数据库重新联机。</p></td>
<td><p>当 Mailbox01 不可用时，每个为 Mailbox01 进行卷影邮件排队的服务器将承担这些邮件的所有权并重新提交邮件。然后将邮件传递到目的地。</p>
<p>邮件的最大延迟是 <strong>Set-TransportConfig</strong> cmdlet 上的 <em>ShadowHeartbeatFrequency</em> 参数的值。默认值为 2 分钟。</p></td>
</tr>
<tr class="even">
<td><p>Mailbox01 使用同一数据库重新联机。</p></td>
<td><p>Mailbox01 重新联机后，它会传递队列中的邮件，为 Mailbox01 保留邮件卷影副本的服务器已传递这些邮件。这将导致重复传递这些邮件。由于采用了重复邮件检测，Exchange 邮箱用户看不到这些重复邮件。然而，非 Exchange 邮件系统中的收件人可能会收到重复的邮件副本。</p>
<p>邮件的最大延迟是 <strong>Set-TransportConfig</strong> cmdlet 上的 <em>ShadowResubmitTimeSpan</em> 参数的值。默认值为 3 小时。</p></td>
</tr>
</tbody>
</table>


返回顶部

