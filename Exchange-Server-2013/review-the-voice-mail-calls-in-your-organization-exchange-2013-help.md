---
title: '查看您的组织中语音邮件拨打: Exchange Online Help'
TOCTitle: 查看您的组织中语音邮件拨打
ms:assetid: f6fdbe17-d1d2-442a-aa13-06b908d9c33a
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ659073(v=EXCHG.150)
ms:contentKeyID: 50556687
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 查看您的组织中语音邮件拨打

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2013-02-22_

调用统计信息报告可用于查看信息的类型和由您组织中的 Exchange 服务器处理传入呼叫的状态。该报告提供了统计信息的调用转发给或为您的组织中放置的统一邮件 (UM)。您可以使用此信息来跟踪使用情况以进行容量规划、 监视和疑难解答的可用性和 UM，音频质量和排查故障的调用。

本主题回答以下问题：

  - How do I get call statistics for UM?

  - How do I interpret UM call statistics?

有关 UM 报告相关的其他任务，请参阅 [UM 报告过程](um-reports-procedures-exchange-2013-help.md)。

## 如何获得 UM 的呼叫统计信息？

1.  在 Exchange 管理中心 (EAC) 中，单击\&quot;统一消息\&quot;\>\&quot;更多选项\&quot;![更多选项图标](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "更多选项图标") \>\&quot;呼叫统计信息\&quot;。

2.  选择要在报表中包含的信息。当您选择下面的选项中的任何报表将自动更新 ︰
    
      - **显示 **  选择要查看的呼叫统计信息的类型：
        
          - **每天(90 天)**  选择\&quot;每天\&quot;可查看过去 90 天内的所有呼叫的详细信息。
        
          - \&quot;按月(12 个月)\&quot;   选择\&quot;按月\&quot;可按月查看过去 12 个月内的呼叫的摘要。
        
          - \&quot;所有\&quot;   选择\&quot;所有\&quot;可查看自 UM 开始处理呼叫以来接收到的所有呼叫的合并统计信息。
    
      - **UM 拨号计划**    如果您想要将报告中的数据仅限为特定 UM 拨号计划中的呼叫，则选择该拨号计划。
    
      - **UM IP 网关**  如果您想要限制可以仅调用一个特定的 UM IP 网关在报表中的数据，请选择该网关。如果先选择了 UM 拨号计划，只与所选的 UM 拨号计划关联的 UM IP 网关可在列表中。

3.  若要在报表中的行获取更多详细信息的音频质量，选择行，然后单击**音频质量详细信息**。有关如何解释音频质量的详细信息，请参阅[调查您的组织中的语音呼叫的音频质量](investigate-the-audio-quality-of-voice-calls-in-your-organization-exchange-2013-help.md)。

4.  若要将报告复制到剪贴板，请单击\&quot;复制\&quot;。

5.  对于\&quot;每天\&quot;报告，可将特定日期的详细信息导出到一个 .csv 文件中。
    
    1.  选择相应日期，然后单击\&quot;导出日期\&quot;。
    
    2.  在\&quot;文件下载\&quot;确认框中，单击\&quot;打开\&quot;或\&quot;保存\&quot;。
    
    导出的文件将被命名为 um\_cdr\_*YYYY-MM-DD*.csv，其中*YYYY-MM-DD*是年、 月和日运行报告。有关详细信息，请参阅[解释语音邮件呼叫记录](interpret-voice-mail-call-records-exchange-2013-help.md)。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>在报告页面上，可以下载 Microsoft Excel 模板用来导入特定日期的 .csv 文件。</td>
    </tr>
    </tbody>
    </table>


返回顶部

## 如何解释 UM 呼叫统计信息？

UM 呼叫统计信息报告包括以下信息：

  - **日期**  调用数据的 UTC 日期。日期格式取决于您选择的报表和区域设置的类型。您可以从以下选项中进行选择 ︰
    
      - **--- **  显示所有呼叫。
    
      - **MMM/日**  调用的月份。例如，日/13。
    
      - **MM/DD/YY**  调用的某一天。例如，6/23/13。

  - \&quot;总数\&quot;   相应日期内选定 UM 拨号计划或 UM IP 网关的呼叫总数。

  - \&quot;语音邮件\&quot;   UM 代表用户应答的传入呼叫中呼叫者留下语音邮件的呼叫所占的百分比。

  - **未接**   UM 代表用户应答的传入呼叫中呼叫者未留下语音邮件从而导致生成未接来电通知的呼叫所占的百分比。

  - **Outlook Voice Access**   传入呼叫中用户需要登录到 UM 并通过身份验证才能访问其电子邮件、日历和语音邮件的呼叫所占的百分比。

  - **发送**  调用已放置或由 UM 代表经过身份验证或未经身份验证的用户的百分比。此统计信息包括找到我，在电话上播放和电话问候调用类型上的重头戏。

  - \&quot;自动助理\&quot;   由 UM 自动助理应答的传入呼叫所占的百分比。

  - \&quot;传真\&quot;   重定向到传真合作伙伴的传入呼叫所占的百分比。

  - **其他**  任何其他传入或放置调用，不属于任何上述类别中所占百分比。这些调用包含 Outlook Voice Access 数字用户在未登录和未经过身份验证的调用。

  - **失败或拒绝**  失败或被拒绝的 UM 呼叫的百分比。请注意调用失败不统计两次。例如，如果对 Outlook Voice Access 的调用失败，则将其只计失败调用，而且不还作为 Outlook Voice Access 调用。

  - \&quot;音频质量\&quot;   选定时间段内组织的总体音频质量的图形表示。

返回顶部

## 详细信息

[调查您的组织中的语音呼叫的音频质量](investigate-the-audio-quality-of-voice-calls-in-your-organization-exchange-2013-help.md)

[解释语音邮件呼叫记录](interpret-voice-mail-call-records-exchange-2013-help.md)

