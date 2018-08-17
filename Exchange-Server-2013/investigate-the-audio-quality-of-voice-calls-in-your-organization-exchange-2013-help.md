---
title: '调查您的组织中的语音呼叫的音频质量: Exchange Online Help'
TOCTitle: 调查您的组织中的语音呼叫的音频质量
ms:assetid: 8a87694b-1678-4a01-859f-5ad3b2c73db5
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ659069(v=EXCHG.150)
ms:contentKeyID: 50556629
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 调查您的组织中的语音呼叫的音频质量

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2013-02-21_

如果您的组织遇到统一消息 (UM) 呼叫和语音邮件消息的音频质量问题，请使用<strong>呼叫统计信息</strong>报告帮助您了解引起这些问题的原因。

> [!NOTE]  
> 呼叫的音频质量可能受到不涉及报告中的内容的因素。例如，如果您的 Exchange 服务器有大量内存负载或 CPU 负载，用户可能会报告较差的通话质量，即使报告显示优良的音频质量。


有关与呼叫统计信息相关的其他任务，请参阅 [UM 报告过程](um-reports-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：3 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的<strong>UM 呼叫数据和摘要报告 cmdlet</strong>条目。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 使用 EAC 可获取组织的音频质量统计信息

1.  在 EAC 中，导航到<strong>统一消息</strong>\><strong>更多选项</strong>![更多选项图标](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "更多选项图标") \><strong>呼叫统计数据</strong>。

2.  选择要包括在报表中调用统计信息。当您选择下面的选项中的任何报表将自动更新。
    
      - **显示**  选择要查看的呼叫统计信息的类型：
        
          - <strong>每天(90 天)</strong>  选择<strong>每天</strong>可查看过去 90 天内的所有呼叫的详细信息。
        
          - <strong>按月(12 个月)</strong>   选择<strong>按月</strong>可按月查看过去 12 个月内的呼叫的摘要。
        
          - <strong>所有</strong>   选择<strong>所有</strong>可查看自 UM 开始处理呼叫以来接收到的所有呼叫的合并统计信息。
    
      - **UM 拨号计划**    如果您想要将报告中的数据仅限为特定 UM 拨号计划中的呼叫，则选择该拨号计划。
    
      - **UM IP 网关**  如果您想要限制可以仅调用一个特定的 UM IP 网关在报表中的数据，请选择该 UM IP 网关。如果先选择了 UM 拨号计划，只与所选的 UM 拨号计划关联的 UM IP 网关可在列表中。

3.  若要获取报告中某一行的有关音频质量的更多详细信息，请选择此行并单击<strong>音频质量详细信息</strong>。将显示以下信息：
    
      - **日期和时间**   捕获呼叫统计信息的 UTC 日期和时间。
    
      - **UM 拨号计划**   统计信息中所包含呼叫的拨号计划。
    
      - **UM IP 网关**   接收统计信息中所包含的呼叫的 UM IP 网关。
    
      - **NMOS**   呼叫的网络平均意见得分 (NMOS)。NMOS 用 1 到 5 的数字指示呼叫的音频质量好坏，5 表示最好。
        
        > [!NOTE]  
        > 最大的 NMOS 调用可能是依赖于正在使用的音频编解码器。NMOS 可能可以很短是长时间少于 10 秒的呼叫。
    
      - **NMOS 降级**   相对于使用的音频编解码器可能的最高值下降的音频 NMOS 值。例如，如果呼叫的 NMOS 下降值为 1.2，而报告的呼叫的 NMOS 为 3.3，则该特定呼叫的最高 NMOS 将为 4.5 (1.2 + 3.3)。
    
      - **抖动**   呼叫的数据包到达时间的平均变化量。
    
      - **数据包丢失**   所选呼叫数据包丢失的平均百分比。数据包丢失是连接是否可靠的一种指示。
    
      - **往返行程**   所选呼叫的音频的平均往返行程得分（以毫秒为单位）。往返行程得分用于度量连接的延迟时间。
    
      - **突发丢失持续时间**   所选呼叫在出现突发丢失事件过程中丢失数据包的平均持续时间。
    
      - **样本数**   为计算平均值而取样的呼叫数。

4.  有关特定呼叫的详细音频质量度量标准，请参阅[调查用户的语音呼叫音频质量](investigate-the-audio-quality-of-voice-calls-for-a-user-exchange-2013-help.md)。

