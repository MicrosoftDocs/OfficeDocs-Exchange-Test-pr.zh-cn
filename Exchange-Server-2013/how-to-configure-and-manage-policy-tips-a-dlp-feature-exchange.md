---
title: '管理策略提示: Exchange 2013 Help'
TOCTitle: 管理策略提示
ms:assetid: cec50a35-1d00-47b3-b72f-ac1bb0fd630e
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ619307(v=EXCHG.150)
ms:contentKeyID: 50489794
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 管理策略提示

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2016-12-09_

策略提示为信息性通知，将在电子邮件发件人编写邮件时对其显示。策略提示的用途是告知用户他们可能违反了您按照您已确立的数据丢失防护 (DLP) 策略强制实施的业务实践或策略。下面的过程将帮助您开始使用策略提示。请观看此视频了解更多内容。

> [!VIDEO https://www.microsoft.com/zh-cn/videoplayer/embed/dd629bb7-063d-49f3-b7e1-8f2e0aa4de13]  

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤时间：30 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[邮件策略和遵从性权限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主题中的“数据丢失防护 (DLP)”条目。

  - 仅当满足了以下条件时，才会对电子邮件发件人显示策略提示：
    
    1.  发件人的邮件客户端程序为 Microsoft Outlook 2013。如果您的组织已部署 Exchange 2013 SP1 或正在使用 Exchange Online，则 Outlook Web App 和 适用于设备的 OWA 中也会显示策略提示。
    
    2.  存在调用策略提示通知的传输规则。您可通过配置包含操作“通过策略提示通知发件人”的 DLP 策略来创建这样的传输规则。
    
    3.  您的传输代理扫描的邮件头、邮件正文或邮件附件的内容符合在也包含策略提示通知规则的 DLP 策略中规定的条件。换句话说，仅当最终用户进行导致关联规则采取操作的行为时，才会显示策略提示。

  - 如果您没有使用策略提示设置功能来自定义您的策略提示文本，则会显示您内置于系统中的默认策略提示通知文本。有关默认文本的详细信息，请参阅 [策略提示](technical-overview-of-policy-tips-in-exchange-online-and-exchange-2013.md)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 您想执行什么操作？

## 创建或修改仅进行通知的策略提示

该过程会导致在满足特定规则的条件时，对电子邮件发送者显示信息性策略提示。在 Microsoft Outlook 中，发送者可通过使用策略提示选项对话框阻止显示该提示。要配置自定义策略提示文本，请参阅 创建自定义策略提示通知文本。

## 使用 EAC 配置只进行通知的策略提示

1.  在 EAC 中，转至“符合性管理”\>“数据丢失防护”。

2.  双击出现在策略列表中的策略之一，或者突出显示一个项目并选择“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在“编辑 DLP 策略”页上，选择“规则”。

4.  若要添加策略提示到现有规则，请突出显示该规则并选择“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。
    
    若要添加可完全自定义的新空白规则，请选择“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")，然后选择“创建新规则”。

5.  在“应用此规则的条件”中，选择“邮件包含敏感信息”。此条件是必需的。

6.  依次选择 ![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")、敏感信息类型、“添加”、“确定”，然后选择“确定”。

7.  在“执行以下操作”框中，选择“使用策略提示通知发件人”及“选择阻止或发送邮件”下拉列表中的一个选项，然后选择“确定”。

8.  如果要添加其他条件或操作，则选择窗口底部的“更多选项”。
    
    > [!NOTE]  
    > 仅可以使用以下条件：
    > <ul>
    > <li><p><strong>SentTo（收件人为）</strong></p></li>
    > <li><p><strong>SentToScope（收件人位于）</strong></p></li>
    > <li><p><strong>From（发件人为）</strong></p></li>
    > <li><p><strong>FromMemberOf（发件人为以下组的成员）</strong></p></li>
    > <li><p><strong>FromScope（发件人位于）</strong></p></li>
    > </ul>
    > 不可以使用下列操作：
    > <ul>
    > <li><p><strong>RejectMessageReasonText（拒绝该邮件并给出说明）</strong></p></li>
    > <li><p><strong>RejectMessageEnhancedStatusCode（拒绝具有以下增强状态代码的邮件）</strong></p></li>
    > <li><p><strong>DeletedMessage（在不通知任何人的情况下删除邮件）</strong></p></li>
    > </ul>


9.  在“选择此规则的模式”列表中，选择是否要强制执行规则。建议首先测试该规则。

10. 选择“保存”完成规则修改并保存更改。

## 您如何知道这有效？

要验证是否成功创建了仅对发件人进行通知的策略提示，可进行以下操作：

1.  在 EAC 中，转至“符合性管理”\>“数据丢失防护”。

2.  选择希望在其中包含一封通知邮件的策略。

3.  选择“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")，然后选择“规则”。

4.  选择希望在其中包含一封通知邮件的特定规则。

5.  确认您的“通知发件人”操作是否出现在规则摘要的下方部分。

## 创建或修改阻止邮件策略提示

该过程会导致向邮件发件人显示策略提示，指示邮件被拒绝，并且必须在修正有问题的条件后方可传递邮件。会向发件人提供一个选项，用于指示其邮件不包含存在问题的条件。这也称为误报替代。如果发件人对此进行了指示，则邮件就可离开发件箱，并且会审核用户的报告。然而，Exchange 将阻止发送该邮件。要配置自定义策略提示文本，请参阅 创建自定义策略提示通知文本。

## 使用 EAC 可配置阻止邮件策略提示

1.  在 EAC 中，转至“符合性管理”\>“数据丢失防护”。

2.  双击出现在策略列表中的策略之一，或者突出显示一个项目并选择“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在“编辑 DLP 策略”页上，选择“规则”。

4.  若要添加策略提示到现有规则，请突出显示该规则并选择“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

5.  若要添加可以完全自定义的新空白规则，请选择“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。

6.  若要添加展示策略提示的操作，请选择“更多选项…”，然后选择“添加操作”按钮。

7.  从下拉列表中选择“通过策略提示通知发件人”，然后选择“阻止邮件”。

8.  选择“确定”，然后选择“保存”以完成规则修改并保存更改。

## 您如何知道这有效？

要验证是否已成功创建拒绝邮件策略提示，请执行以下操作：

1.  在 EAC 中，转至“符合性管理”\>“数据丢失防护”。

2.  选择一次以突出显示您希望在其中包含一封通知邮件的策略。

3.  选择“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")，然后选择“规则”。

4.  选择一次以突出显示您希望在其中包含一封通知邮件的特定规则。

5.  确认您的“通知发件人无法发送该邮件”操作是否出现在规则摘要的下方部分。

## 创建或修改除非覆盖否则阻止的策略提示

策略提示有四个选项，可拒绝或防止邮件离开发件人的发件箱。有关这些选项的详细信息，请参阅[策略提示](technical-overview-of-policy-tips-in-exchange-online-and-exchange-2013.md)。

## 使用 EAC 可配置除非覆盖否则阻止策略提示

1.  在 EAC 中，转至“符合性管理”\>“数据丢失防护”。

2.  两次选择出现在策略列表中的策略之一，或者出显示一个项目并选择“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在“编辑 DLP 策略”页上，选择“规则”。

4.  若要添加策略提示到现有规则，请突出显示该规则并选择“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。
    
    若要添加可完全自定义的新空白规则，请选择“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")，然后选择“更多选项…”。

5.  若要添加可展示策略提示的操作，请选择“添加操作”按钮。

6.  从下拉列表中选择“通过策略提示通知发件人”，然后选择“阻止邮件，但是允许发件人覆盖并发送”。

7.  选择“确定”，然后选择“保存”以完成规则修改并保存更改。

## 您如何知道这有效？

要验证是否已成功创建除非覆盖否则拒绝策略提示，请执行以下操作：

1.  在 EAC 中，转至“符合性管理”\>“数据丢失防护”。

2.  选择一次以突出显示您希望在其中包含一封通知邮件的策略。

3.  选择“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")，然后选择“规则”。

4.  选择一次以突出显示您希望在其中包含一封通知邮件的特定规则。

5.  确认您的“阻止邮件，但是允许发件人覆盖并发送”操作是否出现在规则摘要的下方部分。

## 创建自定义策略提示通知文本

该可选过程将帮助您自定义电子邮件发件人将在其电子邮件程序中看到的策略提示通知文本。如果您进行该操作，除非您还使用将导致通知出现的操作配置了 DLP 策略规则，否则您的自定义策略提示通知文本将不会出现。请记住，即使您不自定义自己的策略提示通知文本，也存在可显示出来的默认系统策略提示通知。有关默认文本的详细信息，请参阅 [策略提示](technical-overview-of-policy-tips-in-exchange-online-and-exchange-2013.md)。

## 使用 EAC 来创建和管理自定义策略提示通知文本

1.  在 EAC 中，转至“符合性管理”\>“数据丢失防护”。

2.  选择“策略提示设置”![策略提示设置](images/JJ619307.54d1813d-3289-4765-a9a3-a7303a5ab3c7(EXCHG.150).gif "策略提示设置")。

3.  若要使用自己自定义的邮件添加新的策略提示，请选择“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。有关可用操作选择的详细信息，请参阅[策略提示](technical-overview-of-policy-tips-in-exchange-online-and-exchange-2013.md)。
    
    若要修改现有策略提示，请突出显示提示并选择“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。
    
    若要删除现有策略提示，请将其突出显示，并选择“删除”![删除图标](images/JJ657511.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "删除图标")，然后确认您的操作。

4.  选择“保存”完成策略提示修改并保存更改。

5.  选择“关闭”完成策略提示的管理并保存更改。

## 使用命令行管理程序来创建自定义策略提示通知文本

以下示例将新建英语策略提示，其将阻止发送邮件。此策略提示的文本更改为以下值：“此邮件似乎包含受限制的内容，因而将不会被传送。”

    New-PolicyTipConfig -Name en\Reject -Value "This message appears to contain restricted content and will not be delivered."

有关 DLP cmdlet 的详细信息，请参阅 [策略和合规性 cmdlet](https://technet.microsoft.com/zh-cn/library/dd298082\(v=exchg.150\))。

## 使用命令行管理程序来修改自定义策略提示通知文本

下面的示例修改现有采用英语的只进行通知的策略提示。该自定义策略提示的文本更改为“不建议在电子邮件中发送银行账户号码”。

    Set-PolicyTipConfig en\NotifyOnly "Sending bank account numbers in email is not recommended."

有关 DLP cmdlet 的详细信息，请参阅 [策略和合规性 cmdlet](https://technet.microsoft.com/zh-cn/library/dd298082\(v=exchg.150\))。

## 您如何知道这有效？

要验证是否已成功创建自定义策略提示文本，请执行以下操作：

1.  在 EAC 中，转至“符合性管理”\>“数据丢失防护”。

2.  选择“策略提示设置”![策略提示设置](images/JJ619307.54d1813d-3289-4765-a9a3-a7303a5ab3c7(EXCHG.150).gif "策略提示设置")。

3.  选择“刷新”![刷新图标](images/Dd353189.85f271ca-32a4-426c-842a-d2172567099d(EXCHG.150).gif "刷新图标")。

4.  确认自己的操作、区域设置和该区域设置的文本出现在列表中。

## 详细信息

[数据丢失预防](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[策略提示](technical-overview-of-policy-tips-in-exchange-online-and-exchange-2013.md)

[邮件流或传输规则](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)Exchange 2013

[Exchange Online 中的邮件流规则（传输规则）](https://technet.microsoft.com/zh-cn/library/jj919238\(v=exchg.150\))Exchange Online

[Exchange 2010 MailTips](https://go.microsoft.com/fwlink/?linkid=265179)

