---
title: '管道跟踪: Exchange 2013 Help'
TOCTitle: 管道跟踪
ms:assetid: e7780499-9a6f-48b1-aea8-df88ecd8b18a
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb125018(v=EXCHG.150)
ms:contentKeyID: 52061573
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 管道跟踪

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2015-03-09_

当特定发件人移动通过邮箱服务器上的传输服务、邮箱服务器上的邮箱传输传递服务、边缘传输服务器时，管道跟踪会捕获相应发件人的电子邮件副本。管道跟踪会在邮件快照文件中捕获每个传输代理向传输管道中的邮件应用的更改详细信息。通过检查邮件快照文件的内容，可以确定传输代理是否已将更改应用于预期的传输管道中的邮件。如果要对某个问题进行故障排除，您应该确定出错的是哪个传输代理。然后，您可以集中力量对相应代理进行故障排除，以解决问题。接着，您可以再次查看邮件快照文件，以验证解决方案是否成功。

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><img src="images/Dd876845.Caution(EXCHG.150).gif" title="小心" alt="小心" />小心：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li><p>管道跟踪将复制从发件人的电子邮件地址发送的电子邮件的完整内容。若要避免不需要的机密信息曝光，您需要在管道跟踪文件夹上设置适当的安全权限。</p></li>
<li><p>不要长时间启用管道跟踪。管道跟踪创建的文件会迅速累积。启用管道跟踪时，要始终监视可用磁盘空间。</p></li>
</ul></td>
</tr>
</tbody>
</table>


## 配置管道跟踪

启用管道跟踪之前，您需要指定要监视的发件人电子邮件地址。管道跟踪旨在记录从特定电子邮件地址发送的电子邮件。发件人的电子邮件地址可以在 Exchange 内部，也可以在 Exchange 外部。您还可以为指定邮箱服务器或边缘传输服务器上的传输服务生成的系统邮件启用管道跟踪，如自动答复、传递状态通知 (DSN) 邮件、日记报告以及系统生成的其他邮件。您还可以修改管道跟踪文件夹的位置。

下表总结了用于配置管道跟踪的参数。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Cmdlet</th>
<th>参数</th>
<th>默认值</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Set-TransportService</strong></p>
<p><strong>Set-MailboxTransportService</strong></p></td>
<td><p><em>PipelineTracingSenderAddress</em></p></td>
<td><p>空 (<code>$null</code>)</p></td>
<td><p>指定要监视的发件人电子邮件地址。</p>
<p>指定值 &quot;&lt;&gt;&quot; 可以监视由服务器上的指定传输服务发送的系统生成邮件。</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-TransportService</strong></p>
<p><strong>Set-MailboxTransportService</strong></p></td>
<td><p><em>PipelineTracingPath</em></p></td>
<td><p><strong>传输服务</strong>   <code>%ExchangeInstallPath%TransportRoles\Logs\Hub\PipelineTracing</code></p>
<p><strong>邮箱传输服务</strong>   <code>%ExchangeInstallPath%TransportRoles\Logs\Mailbox\PipelineTracing</code></p></td>
<td><p>必须为本地服务器上的路径。不支持 UNC 路径。</p>
<p>指定路径包含用于存储管道跟踪文件的 <code>MessageSnapshots</code> 文件夹。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-TransportService</strong></p>
<p><strong>Set-MailboxTransportService</strong></p></td>
<td><p><em>PipelineTracingEnabled</em></p></td>
<td><p><code>$false</code></p></td>
<td><p>在您配置要监视的发件人地址后，只能为服务器上的指定传输服务启用管道跟踪。</p></td>
</tr>
</tbody>
</table>


有关如何启用管道跟踪和配置管道跟踪的发件人地址的详细信息，请参阅[配置管道跟踪](configure-pipeline-tracing-exchange-2013-help.md)。

## 邮件快照文件

邮件快照文件捕获邮件代理向传输服务或邮箱传输传递服务中的邮件应用的更改。这些文件存储在 `MessageSnapshots` 文件夹中，该文件夹位于传输服务的对应管道跟踪路径。

在 `MessageSnapshots` 文件夹中，Exchange 会为移动通过指定传输服务的受监视发件人发送的每封邮件都创建一个文件夹。每个文件夹均用分配给邮件的 GUID 进行命名。如果您为同一邮箱服务器上的传输服务和邮箱传输服务启用管道跟踪，且每个传输服务向同一邮件分配的 GUID 不同，那么传输服务的 `MessageSnapshots` 文件夹中的邮件对应的文件夹名称将不同于邮箱传输服务的 `MessageSnapshots` 文件夹中的同一邮件对应的文件夹名称。如果您在多个 Exchange 服务器上启用管道跟踪，那么当同一邮件通过每个 Exchange 服务器上的指定传输服务时，邮件所分配的 GUID 不同。

在每个邮件文件夹中，Exchange 会创建多个文件扩展名为 .eml 的邮件快照文件。这些邮件快照文件包含邮件在遇到每个 SMTP 事件和传输代理时的内容。

如果某个 SMTP 事件上注册了传输代理，则 Exchange 会在邮件遇到任何传输代理之前创建该邮件的邮件快照。这样就可以在邮件遇到该事件上注册的传输代理前捕获该邮件的副本。然后，Exchange 会为该邮件遇到的每个传输代理都新建邮件快照，无论传输代理是否修改了邮件的内容。但是，如果某个事件上没有注册任何代理，则 Exchange 不会为该事件创建任何邮件快照。

例如，如果 **OnEndofData** 事件上注册了三个代理，但只有两个传输代理修改了邮件，则 Exchange 会创建四个邮件快照。第一个邮件快照在该事件上注册的传输代理进行任何修改之前在邮件遇到 **OnEndofData** 事件时捕获该邮件。然后，Exchange 会针对每个传输代理都创建一个邮件快照，无论传输代理是否修改了邮件。

以下列表介绍了所创建的邮件快照文件：

  - **Original.eml**   此类文件包含电子邮件在遇到任何 SMTP 事件或传输代理之前的原始、未经修改的内容。

  - **Routingnnnn.eml**   此类文件包含电子邮件在传输服务的分类部分期间遇到传输 SMTP 事件和这些事件上注册的传输代理时的内容。占位符 *nnnn* 代表以 `0001` 开头的整数值。该值针对每个 SMTP 事件和这些事件上注册的传输代理按照这些事件和代理对邮件起作用的顺序递增。邮箱传输传递服务不生成这些 **Routing** 快照文件。

  - **SmtpReceivennnn.eml**   此类文件包含电子邮件在传输服务或邮箱传输传递服务的 SMTP 接收部分期间遇到 **OnEndofData** 和 **OnEndOfHeaders** SMTP 事件和这些事件上注册的传输代理时的内容。占位符 *nnnn* 代表以 `0001` 开头的整数值。该值针对每个 SMTP 事件和这些事件上注册的传输代理按照这些事件和代理对邮件起作用的顺序递增。

可以使用文本编辑器（如记事本）打开邮件快照文件。

每个邮件快照文件均以头开头，这些头被添加到邮件内容中，并列出与邮件快照文件有关的 SMTP 事件和传输代理。这些头以 `X-CreatedBy: MessageSnapshot-Begin injected headers` 开头，并以 `X-EndOfInjectedXHeaders: MessageSnapshot-End injected headers` 结尾。在每个邮件快照文件中，每个后续传输代理和 SMTP 事件将替换这些头。下面的示例展示了被添加到电子邮件文件中的头：

    X-CreatedBy: MessageSnapshot-Begin injected headers
    X-MessageSnapshot-UTC-Time: 2013-01-23T23:20:18.138Z
    X-MessageSnapshot-Record-Id: 21474836486
    X-MessageSnapshot-Source: OnSubmittedMessageX-Sender: michelle@nwtraders.com
    X-Receiver: chris@contoso.com
    X-EndOfInjectedXHeaders: MessageSnapshot-End injected headers

在邮件快照文件头的后面是邮件的内容，包括所有原始邮件头。如果传输代理修改了邮件的内容，则更改将合并到邮件内容中。传输代理处理邮件时，每个传输代理所作的更改都将应用于邮件内容。如果某个传输代理未对邮件内容进行任何更改，则该代理创建的邮件快照将与上一传输代理创建的邮件快照相同。

