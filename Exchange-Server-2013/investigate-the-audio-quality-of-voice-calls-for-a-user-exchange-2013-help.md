---
title: '调查用户的语音呼叫音频质量: Exchange Online Help'
TOCTitle: 调查用户的语音呼叫音频质量
ms:assetid: 0c945886-3cfa-423e-9b46-0d6b1584a145
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ659059(v=EXCHG.150)
ms:contentKeyID: 50556522
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 调查用户的语音呼叫音频质量

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2013-02-21_

如果用户报告其统一消息 (UM) 呼叫的音频质量有问题，可使用\&quot;用户呼叫日志\&quot;报告来帮助您分析引起这些问题的原因。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>这些报告中未涵盖的因素也可能会影响呼叫的音频质量。例如，如果 Exchange 服务器遇到较大的内存或 CPU 负载，则即使这些报告表明音频质量较好，用户也可能会报告较差的呼叫质量。</td>
</tr>
</tbody>
</table>


有关与 UM 报告相关的其他任务，请参阅 [UM 报告过程](um-reports-procedures-exchange-2013-help.md)

## 在开始之前，您需要知道什么？

  - 估计完成时间：5 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 呼叫数据和摘要报告 cmdlet\&quot;条目。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.</td>
</tr>
</tbody>
</table>


## 使用 EAC 获取启用 UM 的用户的呼叫日志

1.  在 EAC 中，导航到\&quot;统一消息\&quot;\>\&quot;更多选项\&quot;![更多选项图标](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "更多选项图标")\>\&quot;用户呼叫日志\&quot;。

2.  单击\&quot;选择一个用户\&quot;，然后选择需要其数据的用户。

3.  若要获取报告中某一行的有关音频质量的更多详细信息，请选择此行并单击\&quot;音频质量详细信息\&quot;。将显示以下信息：
    
      - **日期和时间**   呼叫的日期和时间（针对所选用户在 Outlook Web App 中设置的时区）。
    
      - **用户**   所选的用户。
    
      - **UM 拨号计划**   呼叫的拨号计划。
    
      - **UM IP 网关**   用于呼叫的 UM IP 网关。
    
      - **音频编解码器**   呼叫期间使用的音频编解码器。
    
      - **NMOS**   呼叫的网络平均意见得分 (NMOS)。NMOS 用 1 到 5 的数字指示呼叫的音频质量好坏，5 表示最好。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>呼叫可能的最大 NMOS 取决于使用的音频编解码器。对于通话时间少于 10 秒的非常短的呼叫，NMOS 可能不可用。</td>
        </tr>
        </tbody>
        </table>
    
      - **NMOS 降级**   相对于使用的音频编解码器可能的最高值下降的音频 NMOS 值。例如，如果呼叫的 NMOS 下降值为 1.2，而报告的呼叫的 NMOS 为 3.3，则该特定呼叫的最高 NMOS 将为 4.5 (1.2 + 3.3)。
    
      - **抖动**   呼叫的数据包到达时间的平均变化量。
    
      - **数据包丢失**   所选呼叫数据包丢失的平均百分比。数据包丢失是连接是否可靠的一种指示。
    
      - **往返行程**   所选呼叫的音频的平均往返行程得分（以毫秒为单位）。往返行程得分用于度量连接的延迟时间。
    
      - **突发丢失持续时间**   所选呼叫在出现突发丢失事件过程中丢失数据包的平均持续时间。

