---
title: '音频编码解码器: Exchange 2013 Help'
TOCTitle: 音频编码解码器
ms:assetid: 6c39d65c-c2d3-4128-aae9-8596602819c3
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa998670(v=EXCHG.150)
ms:contentKeyID: 54652288
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 音频编码解码器

 

_**适用于：** Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2016-12-09_

在统一消息 (UM) 中，使用编解码器来存储语音邮件。另一个编解码器用于 VoIP 网关或 IP 专用交换机 (PBX) 以及运行 Microsoft Exchange 统一消息服务的邮箱服务器或运行 Microsoft Exchange 统一消息呼 叫路由器服务的客户端访问服务器之间。统一消息可以使用下列四种音频编解码器中的任意一种来创建和存储语音邮件：

  - MP3（默认）

  - Windows Media Audio (WMA)

  - Group System Mobile (GSM) 06.10

  - G.711 Pulse Code Modulation (PCM) Linear

<table>
<thead>
<tr class="header">
<th><img src="images/JJ898581.warning(EXCHG.150).gif" title="警告" alt="警告" />警告：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>G.711（PCMA 和 PCMU）和 G.723.1 编解码器是用于 IP 网关以及客户端访问和邮箱服务器之间的 VoIP 编解码器。</td>
</tr>
</tbody>
</table>


规划 UM 系统时，作为规划的一部分，需要根据组织的需求选择正确的音频编解码器。本主题讨论 UM 可以使用的音频编解码器，并将帮助您规划 UM 部署。

## 编解码器

*编解码器*一词是“编码”和“解码”两个词的组合，用于数字音频数据。编解码器是将数字数据转换为音频文件格式或流式音频格式的软件程序。使用编解码器将模拟语音信号转换为数字版本的语音信号。编解码器在音质、使用时所需的带宽以及执行编码时所需的系统要求等方面可能有所不同。

统一消息中使用两种类型的编解码器：

  - 用于 VoIP 网关、IP PBX 或启用 SIP 的 PBX 以及客户端访问和邮箱服务器之间，或者用于 PBX 和 VoIP 网关之间的编解码器。

  - 用于为用户编码和存储语音邮件的编解码器。

通过公用电话交换网 (PSTN) 使用普通电话时，语音以模拟格式通过电话线路进行传输。但是，在使用 IP 语音 (VoIP) 时，必须将语音转换为数字信号。此转换过程称为编码。编码通过编解码器来执行。数字化语音到达目的地后，必须经过解码回到原来的模拟格式，以便电话另一端的用户可以听到并理解呼叫者所说的内容。

## VoIP 编解码器

在 UM 中，VoIP 网关或 IP PBX 以及客户端访问和邮箱服务器之间可使用三种类型的编解码器：

  - G.711 µ-law

  - G.711 A-law

  - G.723.1

G.711 是为用于音频编码解码器而开发的一项标准。G.711 标准中定义了两种主要算法：在北美和日本使用的 µ-law 算法以及在欧洲和其他国家/地区使用的 A-law 算法。G.723.1 音频编码解码器主要用于 VoIP 应用程序，要求获得许可证才能使用。G.723.1 是一种高音质、高压缩率的编解码器。

客户端访问或邮箱服务器和受支持的 VoIP 网关或 IP PBX 均可以提供 G.711 和 G.723.1 编解码器。默认情况下，要使用的第一种编解码器是 G.723.1。如果要在客户端访问和邮箱服务器以及 VoIP 网关或 IP PBX 之间使用除 G.723.1 外的其他编解码器，建议您更改 VoIP 网关或 IP PBX 上的配置。下表总结了一些常用的 VoIP 编解码器。

### VoIP 编解码器

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>VoIP 编解码器</th>
<th>带宽 (Kbps)</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>G.711</p></td>
<td><p>64</p></td>
<td><p>此编解码器需要非常少的处理。需要至少 128 Kbps 用于双向通信。</p></td>
</tr>
<tr class="even">
<td><p>G.723.1</p></td>
<td><p>5.3/6.3</p></td>
<td><p>此编解码器提供高压缩率和高音质。所需的处理要多于 G.711 编解码器。G.723.1 编解码器占用的带宽较少，但是提供的音质较差。</p></td>
</tr>
</tbody>
</table>


## UM 语音邮件存储编解码器

统一消息拨号计划是 UM 操作不可或缺的一部分。默认情况下，在创建 UM 拨号计划时，UM 拨号计划使用 MP3 音频编解码器创建和存储语音邮件。但是，在创建 UM 拨号计划之后，可以将其配置为使用 WMA、GSM 06.10 或 G.711 PCM Linear 音频编解码器。

每种音频编码解码器都有各自的优缺点。选择 MP3 音频编解码器作为默认音频编解码器是由于其音质和压缩属性的原因。将 GSM 06.10 和 G.711 PCM Linear 音频编码解码器作为可用选项是由于其支持其他类型消息系统的能力。

在规划 UM 时，必须平衡将为语音邮件创建的音频文件的大小和相对质量的关系。通常，音频文件的比特率越高，质量也越高。还必须考虑音频文件是否已压缩。下表显示了用于 UM 的各音频编解码器的采样比特率（位/秒）和压缩属性。

### 默认 UM 语音邮件存储编解码器

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>语音邮件存储编解码器</th>
<th>位数</th>
<th>是否是压缩文件？</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MP3</p></td>
<td><p>16 位</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>WMA</p></td>
<td><p>16 位</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p>G.711 PCM</p></td>
<td><p>16 位</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p>GSM 06.10</p></td>
<td><p>8 位</p></td>
<td><p>是</p></td>
</tr>
</tbody>
</table>


在 UM 中，针对语音邮件创建的文件类型取决于创建语音邮件音频文件所使用的音频编解码器。MP3 音频编解码器创建 .mp3 音频文件，WMA 音频编解码器创建 .wma 音频文件，GSM 06.10 和 G.711 PCM Linear 音频编解码器生成 .wav 音频文件。所有这些音频文件均随电子邮件一起发送给语音邮件的收件人。

对数字数据进行编码和解码通常还会（但并非总会）涉及到压缩或解压缩。音频压缩是数据压缩的一种形式，可以减小音频数据文件的大小。音频编码解码器所使用的音频压缩算法将压缩 .wma 或 .wav 音频文件。在 UM 中，所使用的音频压缩算法类型取决于在 UM 拨号计划属性中选择的音频编解码器类型。创建并压缩音频文件之后，文件将附加到语音邮件中。

有时，在压缩和解压缩期间，数字数据中的信息会丢失。压缩音频文件所使用的压缩率越高，转换期间丢失的信息就越多。但是，由于减小了音频文件的大小，占用的磁盘空间也随之减少。反之，压缩率越低，丢失的信息就越少。但是，由于增大了每个音频文件的大小，必须占用更多的磁盘空间。

用于记录语音邮件的 RTAudio 宽带或高保真音频也可作为音频编码解码器。但是，只有成功地将统一消息与 [Microsoft Lync Server](https://go.microsoft.com/fwlink/p/?linkid=202010) 集成之后，使用 RTAudio 的高保真音频才可用。若要启用 RTAudio 作为窄带或宽带线路编解码器，必须将 UM 拨号计划配置为会话初始协议 (SIP) URI 类型的拨号计划，并且必须将拨号计划上的呼叫应答编解码器设置为 MP3 或 WMA 格式，方可启用宽带音频 (16Khz)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在未部署 Lync Server 的环境中无法使用 RTAudio。这是因为，在未集成 Lync Server 的环境中，拨号计划会被设置为电话分机或 E.164，而不是 SIP URI。</td>
</tr>
</tbody>
</table>


每次传入呼叫有两种媒体流：入站到客户端访问服务器的媒体流和从邮箱服务器出站的媒体流。将拨号计划类型设置为 SIP URI 并将拨号计划上的呼叫应答编解码器设置为 MP3 或 WMA 格式时，客户端访问服务器将尝试为入站媒体流选择 RTAudio VoIP 编解码器。如果协商成功，入站媒体流的 RTAudio 编解码器将用于应答呼叫或从 Lync 客户端或服务器发起的呼叫。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>使用电话播放功能发出的呼叫不使用 RTAudio 编解码器。使用电话播放功能发出的呼叫的入站媒体流将使用 G.711 或 G.723.1 编解码器。</td>
</tr>
</tbody>
</table>


使用 RTAudio 编解码器时，将录制高保真的语音邮件，并根据拨号计划的配置方式将其存储为扩展名为 .mp3 或 .wma 的音频文件。在 Outlook 或 Outlook Web App 中为用户播放语音邮件时，用户将听到高保真的语音邮件。如果协商未成功，将使用 G.711 或 G.723.1 编解码器。G.711 和 G.723.1 编解码器均是窄带编解码器。使用这两种编解码器作为 VoIP 编解码器时，将录制语音邮件并将其存储为扩展名为 .mp3 或 .wma 的窄带音频文件。

出站媒体流将始终使用 G.711 或 G.723.1 编解码器进行协商。这意味着呼叫者通过电话听到的始终是窄带音频。这同样适用于使用 Microsoft Lync Server 2010 或之后版本执行呼叫的情况。

邮箱服务器用于在语音邮件中存储音频的音频格式和编解码器不仅取决于拨号计划上配置的音频编解码器，还取决于 UM 与 SIP 对等方协商的音频比特率。如果您的环境包含 Lync Server 或 SIP 终结点，邮箱服务器还将与 SIP 对等方协商要使用的音频编解码器。例如，经协商将宽带 RTAudio 作为线路编解码器时，随后邮箱服务器将在创建语音邮件时使用 32 Kbps MP3 或 WMA 9.2 格式，具体取决于拨号计划设置。下表显示语音邮件存储音频编码解码器与所使用的 VoIP 或线路编码解码器之间的关系。

### 存储音频编码解码器与 VoIP 或线路编码解码器之间的关系

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>UM 拨号计划上配置的音频编码解码器</th>
<th>VoIP 或线路编码解码器（窄带）- G.723、G.711 或 RTAudio (8KHz)</th>
<th>VoIP 或线路编码解码器（宽带）- RTAudio (16KHz)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>G.711</p></td>
<td><p>G.711</p></td>
<td><p>不适用。如果将拨号计划设置为 G.711，则客户端访问或邮箱服务器不协商宽带音频。</p></td>
</tr>
<tr class="even">
<td><p>WMA</p></td>
<td><p>WMA 9 Voice</p></td>
<td><p>WMA 9.2</p></td>
</tr>
<tr class="odd">
<td><p>GSM</p></td>
<td><p>GSM 6.10</p></td>
<td><p>不适用。如果将拨号计划设置为 GSM，则客户端访问或邮箱服务器不协商宽带音频。</p></td>
</tr>
<tr class="even">
<td><p>MP3</p></td>
<td><p>MP3 (16 Kbps)</p></td>
<td><p>MP3 (32 Kbps)</p></td>
</tr>
</tbody>
</table>


编解码器

## UM 邮件大小调整

可以将统一消息配置为使用下列四种音频编解码器中的任意一种来创建语音邮件：MP3、WMA、GSM 06.10 和 G.711 PCM Linear。默认情况下，选择 MP3 格式。

WMA 音频编码解码器始终存储为 Windows Media 格式，附件是文件扩展名为 .wma 的文件。使用 GSM 或 G.711 PCM Linear 音频编码解码器编码的音频文件始终存储为 RIFF/WAV 格式，附件是文件扩展名为 .wav 的文件。

UM 语音邮件的大小取决于包含语音数据的附件的大小。而附件的大小取决于下列因素：

  - 语音邮件录音的持续时间

  - 使用的音频编解码器

  - 音频文件的存储格式

下图显示了对于可以在 UM 中使用的三种音频编码解码器，音频文件的大小如何依赖于语音邮件录音的持续时间。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在此图中，用于应答呼叫的语音邮件的平均长度大约为 30 秒。</td>
</tr>
</tbody>
</table>


**音频文件大小**

![UM\_Message\_Sizing](images/Aa998670.76ca4891-450f-4ffd-9493-aac8d0d23a5d(EXCHG.150).gif "UM_Message_Sizing")

## MP3

默认情况下，会选择 MP3 格式，该格式是语音邮件的默认音频文件格式。MP3 格式是常见的音频文件格式，可显著减小音频文件的大小，是个人音频设备或 MP3 播放器最常用的格式。MP3 是跨平台的音频编解码器类型，可用于兼容许多移动电话和设备以及不同的计算机操作系统。

## WMA

WMA 是三种编解码器中压缩率最高的音频编码解码器。压缩率为每 10 秒的音频大约 11,000 个字节。但是，与 .wav 文件格式相比，.wma 文件格式的文件头部分要大得多。.wma 文件的文件头部分大约为 7 KB，而 .wav 文件的文件头部分小于 100 个字节。尽管 WMA 音频录音超过 15 秒，却仍小于 GSM 音频录音。因此，若要获得文件最小但是质量最高的音频文件，请使用 WMA 音频编解码器。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您对 OWA for Devices 使用从内部部署发送推送通知，则不能使用 WMA 格式。OWA for Devices 仅支持 MP3 文件格式。</td>
</tr>
</tbody>
</table>


## G.711 PCM Linear

G.711 PCM Linear 音频编码解码器创建未压缩的 .wav 音频文件。因此，与 GSM 和 WMA 音频编码解码器相比，G.711 PCM Linear .wav 音频文件在给定持续时间占用的空间最多。G.711 PCM Linear .wav 音频文件每 10 秒的音频占用的空间超过 160,000 个字节。在 UM 所使用的三种音频编解码器中，G.711 PCM Linear .wav 音频文件的音质最高。但是，大多数收听语音邮件的用户可以接受使用 WMA 和 GSM 音频编解码器创建的音质相当的音频文件。

## GSM

GSM 音频编码解码器创建压缩的 .wav 音频文件。GSM .wav 音频文件每 10 秒的音频占用的空间超过 16,000 个字节。但是，GSM 创建的音频文件大于 WMA 音频编码解码器创建的音频文件。因此，在平衡语音邮件的质量和大小时，此编解码器可能不是最佳的选择。

编解码器

