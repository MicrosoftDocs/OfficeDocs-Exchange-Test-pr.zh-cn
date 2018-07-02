---
title: '从文件导入自定义 DLP 策略模板: Exchange 2013 Help'
TOCTitle: 从文件导入自定义 DLP 策略模板
ms:assetid: 83f49dbd-f9b1-498e-b548-1529c5e1ccdb
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ150531(v=EXCHG.150)
ms:contentKeyID: 50489764
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 从文件导入自定义 DLP 策略模板

 

_**适用于：**Exchange Online, Exchange Server 2013_

_**上一次修改主题：**2016-08-09_

可以通过导入包含策略信息设置的文件并利用 DLP 策略管理敏感信息。DLP 策略模板可以从 Exchange 独立开发为 XML 文件。但是，策略必须满足特定格式要求才能正常工作。或者可以将从以前版本的 Exchange 导出的策略导入至 Microsoft Exchange Server 2013。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876845.Caution(EXCHG.150).gif" title="小心" alt="小心" />小心：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在生产环境中运行 DLP 策略时，应在测试模式下启用这些策略。在此类测试中，建议配置示例用户邮箱并发送调用测试策略的测试邮件以便确认结果。</td>
</tr>
</tbody>
</table>


## 在开始之前，您需要知道什么？

  - 估计完成时间：15 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[邮件策略和遵从性权限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主题中的“数据丢失防护 (DLP)”条目。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。</td>
</tr>
</tbody>
</table>


## 您想执行什么操作？

## 使用 EAC 从文件导入自定义 DLP 策略模板

使用以下过程从文件中导入自定义 DLP 策略模板。为了避免混淆，在选择提供自己的名称时，请为策略或规则的每个部分提供唯一的名称。

1.  在 EAC 中，导航至“符合性管理”\>“防止数据丢失”。

2.  单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标") 图标旁的箭头，然后单击“导入策略”。

3.  在“导入策略”页上，填写下列字段:
    
    1.  **选择要导入的文件**   添加要安装的策略文件的名称。
    
    2.  “名称”   添加将此策略与其他策略进行区分的名称。
    
    3.  **说明**   选择添加概括此策略的说明。
    
    4.  **更多选项**   为该策略选择模式或状态。在指定应启用新策略之前，不会完全启用新策略。策略的默认模式为不进行通知的测试。
    
    5.  单击“下一步”可验证和导入策略。

## 使用 Shell 从文件导入自定义 DLP 策略模板

此示例在文件 C:\\My Documents\\DLP Backup.xml 中导入自定义 DLP 策略模板文件。从 XML 文件导入 DLP 策略集合会删除或覆盖组织中已定义的所有预先存在的 DLP 策略。在导入并覆盖当前 DLP 策略前，请确保对当前 DLP 策略集合进行了备份。

    Import-DlpPolicyCollection -FileData ([Byte[]]$(Get-Content -Path " C:\My Documents\DLP Backup.xml " -Encoding Byte -ReadCount 0))

## 详细信息

[数据丢失预防](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

