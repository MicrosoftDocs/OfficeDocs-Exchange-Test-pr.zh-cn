---
title: '查看 DLP 策略检测报告: Exchange 2013 Help'
TOCTitle: 查看 DLP 策略检测报告
ms:assetid: 5c3f1cf6-d8c7-4d83-bb24-641ea9d50cbc
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ150520(v=EXCHG.150)
ms:contentKeyID: 50489673
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 查看 DLP 策略检测报告

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2016-12-16_

数据丢失预防 (DLP) 策略检测管理宽泛地定义组织为标识、调查和解决 DLP 策略违反而执行的活动。为了管理事件，需要访问标识 DLP 策略已检测内容的信息。此检测信息与现有 Microsoft Exchange Server 2013 数据和日志格式集成，以便您能够利用现有的丰富数据系统管理您的邮件流事件。

有关创建事件报告和单个策略检测事件的信息，请参阅[创建 DLP 策略检测的事件报告](create-incident-reports-for-dlp-policy-detections-exchange-2013-help.md)。有关邮件日志的详细信息，请参阅[使用送达报告跟踪邮件](track-messages-with-delivery-reports-exchange-2013-help.md)。

> [!NOTE]
> Exchange 2013：DLP 是一项高级功能，要求使用 Exchange 企业客户端访问许可证 (CAL)。有关 CAL 和服务器授权的详细信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?linkid=237292">Exchange Server Licensing</a>（Exchange Server 授权）。


## 审核信息

Exchange 中与 DLP 检测管理相关的数据会集成到邮件跟踪日志（也称为送达报告）中。功能会重用系统中提供的许多现有日志记录框架。有关常规信息（包括了解邮件跟踪日志文件的结构），请查看[了解邮件跟踪](message-tracking-exchange-2013-help.md)或[使用送达报告跟踪邮件](track-messages-with-delivery-reports-exchange-2013-help.md)的现有内容。

送达报告是在邮箱服务器上运行传输服务的计算机上收发邮件时的所有邮件活动的详细日志。可以使用 **Get-MessageTrackingLog** cmdlet，通过 Exchange 命令行管理程序访问邮件跟踪日志。DLP 数据会按照现有数据格式和约定集成到送达报告中。

## 数据日志记录格式

邮件跟踪日志包含来自邮件流内容处理所涉及的代理的数据。对于 DLP，传输规则代理 (TRA) 用于调用深度邮件内容扫描并应用作为 ETR 的一部分定义的策略。现有 AgentInfo 事件用于在邮件跟踪日志中添加 DLP 相关条目。

代理名称在 AgentInfo 事件中为“TRA”或“传输规则代理”。会对每封邮件记录一个 AgentInfo 事件，用于描述应用于邮件的 DLP 处理。邮件跟踪日志条目字段的“CustomData”字段是传输规则代理记录的 DLP 数据出现的位置。此字段可能包含多个条目：一个数据分类和客户端信息行（用于在邮件中发现的每个数据分类），一个规则行（用于应用于邮件的每个规则），以及一个运行状况监视行（用于超过加载或执行时间阈值的每个规则）。

此处显示了 DLP 日志条目的示例。输出内容进行了格式设置，以在单独行中显示字符串（各行之间为新行）。

来源：AGENT

EventId:AGENTINFO

CustomData:S:TRA=DC|dcid=41BFDBC6C9D811E0816A3CD34824019B|count=10|conf=77;

S:TRA=DC|dcid=C7ECCBA0CA0011E0B6C00B124924019B|count=3|conf=81;

S:TRA=CI|sndOverride=or|just=Business Reason;

S:TRA=CI|sndOverride=fp;

S:TRA=ETR|ruleId=FC2AA60C9D811E0AFC076D34824019B|dlpid=1B81CC82C9DB11E09052C5D64824019B|st=2010-11-03 15:30T|action=PrependSubject|action=Encrypt|sev=2|mode=audit|dcid=41BFDBC6C9D811E0816A3CD34824019B|sndOverride=or;

S:TRA=ETR|ruleId=AB2AA60C9D811E0AFC076D34824019B|dlpid=1B81CC82C9DB11E09052C5D64824019B|st=2010-11-03 15:30T|action=Encrypt|sev=1|mode=enabled|dcid=C7ECCBA0CA0011E0B6C00B124924019B|sndOverride=fp;

S:TRA=ETRP|ruleId=C27D21EECA0311E0BCB896154924019B|LoadW=200|LoadC=100|ExecW=5500|ExecC=200;

传输规则代理需要对规则 ID、DLP 策略 ID（可选）、上次修改日期、操作、严重性、模式、检测到的数据分类（可选）以及基于规则 ID 的发件人替代（可选）进行分组（通过日志行中的“TRA=ETR”指示）。它还需要按分类名称对分类的数据分类 ID、计数和可信度级别进行分组（通过日志行中的“TRA=DC”指示）。

其他分组包括针对在客户端上检测到的所有分类的数据分类 ID、发件人替代（可选）以及基于数据分类 ID 的替代理由（可选）（通过日志行中的“TRA=CI”指示）。传输规则代理还对超过加载或执行普通或 CPU 时钟阈值的所有规则，按规则 ID 对规则 ID、加载普通时钟（可选）、执行普通时钟（可选）和执行 CPU 时钟（可选）进行分组（通过日志行中的“TRA=ETRP”指示）。

下面是数据字段的完整列表。MTL 中的所有数据都是类型字符串。“格式”列描述如何识别邮件跟踪日志中的每个字段。“可选字段”列指定当规则匹配时不能记录的字段。“特定于 DLP”列显示特定于 DLP 功能的字段。


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>字段名</strong></p></td>
<td><p><strong>描述</strong></p></td>
<td><p><strong>格式</strong></p></td>
<td><p><strong>可选字段</strong></p></td>
<td><p><strong>特定于 DLP</strong></p></td>
</tr>
<tr class="even">
<td><p>TRA</p></td>
<td><p>传输规则代理；类型 AgentName</p></td>
<td><p>TRA=DC、ETR、CI 或 ETRP</p></td>
<td><p>强制</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p>DC</p></td>
<td><p>数据分类；类型 groupName</p></td>
<td><p>TRA=DC</p></td>
<td><p>可选</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>ETR</p></td>
<td><p>Exchange 传输规则；类型 groupName</p></td>
<td><p>TRA=ETR</p></td>
<td><p>强制</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p>CI</p></td>
<td><p>客户端信息，类型 groupName</p></td>
<td><p>TRA=CI</p></td>
<td><p>可选</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>ETRP</p></td>
<td><p>Exchange 传输规则性能；类型 groupName</p></td>
<td><p>TRA=ETRP</p></td>
<td><p>可选</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p>dcid</p></td>
<td><p>数据分类的 ID</p></td>
<td><p>dcid=GUID</p></td>
<td><p>可选</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>计数</p></td>
<td><p>数据分类的计数</p></td>
<td><p>count=整数</p></td>
<td><p>可选</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p>conf</p></td>
<td><p>数据分类的可信度级别</p></td>
<td><p>conf=整数（百分比）</p></td>
<td><p>可选</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>sndOverride</p></td>
<td><p>发件人替代；该字段是可选的。</p>
<p>在 TRA=CI 行中，当该字段设置为“or”时，表示已替代数据分类。如果该字段设置为“fp”，则表示将数据分类报告为误报。</p>
<p>在 TRA=ETR 行中，当该字段设置为“or”时，表示已替代规则或规则的一部分。如果该字段设置为“fp”，则表示将规则或规则的一部分报告为误报。</p></td>
<td><p>sndOverride=or 或 fp</p>
<p>其中“or”表示替代，而“fp”表示误报。当最终用户对某个规则报告了替代或误报时，存在 sndOverride 字段。</p></td>
<td><p>可选</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p>just</p></td>
<td><p>理由；该字段是可选的，仅当发件人替代字段在 TRA=CI 行中等于“or”时才可用。理由文本由最终用户提供作为应替代数据分类的原因。</p></td>
<td><p>just=IW 输入理由字符串</p>
<p>仅当最终用户报告替代时才记录理由字段。</p></td>
<td><p>可选</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>ruleId</p></td>
<td><p>规则的 ID</p></td>
<td><p>ruleId=GUID</p></td>
<td><p>强制</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p>dlpId</p></td>
<td><p>DLP 策略的 ID。该字段是可选的；如果不存在 dlpId，则规则不属于 DLP 策略。</p></td>
<td><p>dlpId=GUID</p></td>
<td><p>可选</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>st</p></td>
<td><p>规则的上次修改日期</p></td>
<td><p>st=UTC 日期-时间</p></td>
<td><p>强制</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p>action</p></td>
<td><p>规则执行的操作；每个规则可能具有多个操作</p></td>
<td><p>action=单个操作</p>
<p>如果对规则应用了多个操作，则存在多个操作字段。</p></td>
<td><p>强制</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p>sev</p></td>
<td><p>审核规则的严重性</p></td>
<td><p>sev=1、2 或 3</p>
<p>其中 1 表示低，2 为中，3 表示高。</p></td>
<td><p>可选</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p>mode</p></td>
<td><p>命中规则时的规则状态（enforcement、audit 或 auditandnotify）。</p></td>
<td><p>mode=audit、auditandnotify 或 enforcement</p></td>
<td><p>强制</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p>loadW</p></td>
<td><p>加载普通时钟；该字段是可选的</p></td>
<td><p>loadW=时间（毫秒）</p></td>
<td><p>可选</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p>loadC</p></td>
<td><p>加载 CPU 时钟；该字段是可选的</p></td>
<td><p>loadC=时间（毫秒）</p></td>
<td><p>可选</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p>execW</p></td>
<td><p>执行普通时钟；该字段是可选的</p></td>
<td><p>execW=时间（毫秒）</p></td>
<td><p>可选</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p>execC</p></td>
<td><p>执行 CPU 时钟；该字段是可选的</p></td>
<td><p>execC=时间（毫秒）</p></td>
<td><p>可选</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p>message-id</p></td>
<td><p>邮件 ID</p></td>
<td><p>message-id=邮件 ID</p></td>
<td><p>强制</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p>date-time</p></td>
<td><p>发送邮件的日期和时间（通用时间）</p></td>
<td><p>date-time=UTC 日期-时间</p></td>
<td><p>强制</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p>sender-address</p></td>
<td><p>发件人字段中指定的电子邮件地址</p></td>
<td><p>sender-address=电子邮件地址</p></td>
<td><p>强制</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p>recipient-address</p></td>
<td><p>邮件收件人的电子邮件地址</p></td>
<td><p>recipient-address=电子邮件地址</p></td>
<td><p>强制</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p>message-subject</p></td>
<td><p>邮件主题字段中发现的数据</p></td>
<td><p>message-subject=最终用户输入主题字符串</p></td>
<td><p>强制</p></td>
<td><p>否</p></td>
</tr>
</tbody>
</table>


## 详细信息

[数据丢失预防](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[创建 DLP 策略检测的事件报告](create-incident-reports-for-dlp-policy-detections-exchange-2013-help.md)

[使用送达报告跟踪邮件](track-messages-with-delivery-reports-exchange-2013-help.md)

