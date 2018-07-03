---
title: '管理 DLP 策略: Exchange 2013 Help'
TOCTitle: 管理 DLP 策略
ms:assetid: ba81fabd-7f7f-4ef7-968f-ce851ada9d70
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ673559(v=EXCHG.150)
ms:contentKeyID: 50491518
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 管理 DLP 策略

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2015-01-14_

通过使用 Exchange 管理中心 (EAC) 或命令行管理程序您可以查看、更改或删除 Microsoft Exchange 中现有的数据丢失防护 (DLP) 策略。

有关与 DLP 相关的更多管理任务，请参阅 [DLP 过程](dlp-procedures-exchange-2013-help.md) (Exchange Server 2013) 或 [DLP 过程](https://technet.microsoft.com/zh-cn/library/jj938003\(v=exchg.150\)) (Exchange Online)。

有关 Exchange 命令行管理程序的详细信息，请参阅 [将 PowerShell 与 Exchange 2013 结合使用 (Exchange Management Shell)](https://technet.microsoft.com/zh-cn/library/bb123778\(v=exchg.150\))。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤时间：15-60 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[邮件策略和遵从性权限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主题中的“数据丢失防护 (DLP)”条目。

  - 对于任何 DLP 策略，您可以选择以下三种模式之一：
    
      -    **强制**   针对所有邮件和受支持的文件类型评估策略中的规则。如果检测到符合策略条件的数据，则可能会中断邮件流。会执行策略中所述的所有操作。
    
      -    **使用测量提示测试 DLP 策略**   针对所有邮件和受支持的文件类型评估策略中的规则。如果检测到符合策略条件的数据，则不会中断邮件流。即，不会阻止邮件。如果配置了策略提示，则会向用户显示这些策略提示。
    
      -    **不使用策略提示测试 DLP 策略**   针对所有邮件和受支持的文件类型评估策略中的规则。如果检测到符合策略条件的数据，则不会中断邮件流。即，不会阻止邮件。如果配置了策略提示，则不会向用户显示这些策略提示。

  - DLP 策略中的每个规则均有自己的模式设置。当策略模式与此策略中的规则模式不同时，规则设置具有较高优先级，将根据其模式进行评估。

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

## 查看现有 DLP 策略的详细信息

需要查看已为组织建立的现有 DLP 策略的规则和操作。如果遇到意外邮件流问题或是如果组织更改需要对敏感信息进行监视的方式，则这可能会比较有用。

## 使用 EAC 查看现有 DLP 策略的详细信息

1.  在 EAC 中，导航至“符合性管理”\>“防止数据丢失”。

2.  双击策略列表中的任一策略，或是突出显示其中一个项目然后单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在“编辑 DLP 策略”页上，单击“规则”。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>可以创建 DLP 策略并将其保留为非激活或禁用模式。在此模式下，不强制执行策略，并且可以在测试或开始强制执行它之前更改与其规则关联的任何谓词、操作或值。</td>
</tr>
</tbody>
</table>


## 使用命令行管理程序查看现有 DLP 策略的详细信息

此示例返回有关名为 Employee Numbers 的虚构 DLP 策略的信息。此命令将通过管道传递给 **Format-List** cmdlet，以显示指定 DLP 策略的详细配置。

    Get-DlpPolicy "Employee Numbers" | Format-List

有关语法和参数的信息，请参阅 [Get-DlpPolicy](https://technet.microsoft.com/zh-cn/library/jj215752\(v=exchg.150\))。

## 更改 DLP 策略

可以通过修改策略名称或更改控制策略效果的规则，来更改现有 DLP 策略。示例规则更改可以包括针对在特定域中发送并且检测到包含敏感信息的邮件，向邮件正文和 RMS 保护添加自定义免责声明文本。请记住，DLP 策略模板只是 Exchange 2013 中可以帮助为邮件环境设计和应用可靠策略和合规性系统的功能之一。

## 使用 EAC 更改现有 DLP 策略

1.  在 EAC 中，导航至“符合性管理”\>“防止数据丢失”。

2.  双击策略列表中的任一基于模板的策略，或是突出显示一个项目并单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在“编辑 DLP 策略”页上，单击“规则”。

4.  若要更改现有规则，请突出显示该规则并单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

5.  若要添加可以完全自定义的新空白规则，请单击“新建”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。

6.  若要添加有关发件人通知、阻止邮件按或允许替代的规则，请单击“新建”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")图标旁的箭头。

7.  若要删除规则，请突出显示该规则并单击“删除”![删除图标](images/JJ657511.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "删除图标")。

8.  单击“保存”完成策略修改并保存更改。

## 使用命令行管理程序更改现有 DLP 策略

您可以使用命令行管理程序指定策略的操作和通知级别。此示例为名为 Employee Numbers 的虚构 DLP 策略设置模式，因此不会执行任何操作，也不会显示任何通知消息。

    Set-DlpPolicy "Employee Numbers" -Mode Audit

有关语法和参数的信息，请参阅 [Set-DlpPolicy](https://technet.microsoft.com/zh-cn/library/jj215778\(v=exchg.150\))。

## 删除 DLP 策略

您可以使用 EAC 永久删除 DLP 策略。一旦删除了某个策略，将不再执行该策略，并且不会保存任何规则和操作。

或者，可以将策略的操作状态或模式设置为“在不使用策略提示的情况下测试 DLP 策略”。这会停止在邮件环境中强制执行它，但是会保留策略本身的详细配置设置。如果将来可能需要再次强制执行策略，则这可能会十分有用。

## 使用 EAC 删除现有的 DLP 策略

1.  在 EAC 中，导航至“符合性管理”\>“防止数据丢失”。

2.  在策略列表中选择要删除的策略，然后单击“删除”![删除图标](images/JJ657511.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "删除图标")。

## 使用命令行管理程序删除现有 DLP 策略

此示例删除名为 Employee Numbers 的虚构 DLP 策略。

    Remove-DlpPolicy "Employee Numbers"

有关语法和参数的信息，请参阅 [Remove-DlpPolicy](https://technet.microsoft.com/zh-cn/library/jj215677\(v=exchg.150\))。

## 详细信息

[数据丢失预防](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[策略提示](technical-overview-of-policy-tips-in-exchange-online-and-exchange-2013.md)

