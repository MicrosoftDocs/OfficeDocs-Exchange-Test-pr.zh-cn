---
title: '管理邮件流规则: Exchange 2013 Help'
TOCTitle: 管理邮件流规则
ms:assetid: e7a81372-b6d7-4d1f-bc9e-a845a7facac2
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ657505(v=EXCHG.150)
ms:contentKeyID: 50491882
ms.date: 02/08/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 管理邮件流规则

 

_**适用于：** Exchange Online, Exchange Online Protection, Exchange Server 2013_

_**上一次修改主题：** 2016-12-09_

您可以使用邮件流规则（也称为传输规则），针对通过您的组织传递的邮件查找特定条件并对其进行操作。本主题介绍如何创建、复制、启用或禁用、删除或导入或导出规则、调整其顺序，以及如何监视规则使用情况。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>为确保您的规则按预期方式工作，一定要全面测试每个规则以及规则之间的交互。</td>
</tr>
</tbody>
</table>


对本程序使用的方案感兴趣？请参阅以下主题：

  - [组织范围内的免责声明、签名、脚注或标头](organization-wide-disclaimers-signatures-footers-or-headers-exchange-online-help.md)

  - [使用传输规则检查邮件附件](use-transport-rules-to-inspect-message-attachments-exchange-2013-help.md)

  - [常见的附件阻止方案](common-attachment-blocking-scenarios-for-mail-flow-rules-exchange-2013-help.md)

  - [使用邮件流规则根据字词、短语或模式的列表路由电子邮件](use-mail-flow-rules-to-route-email-based-on-a-list-of-words-phrases-or-patterns-exchange-2013-help.md)

  - [常见邮件审批方案](common-message-approval-scenarios-exchange-2013-help.md)

  - [使用邮件流规则以便邮件可以规避待筛选邮件功能](use-mail-flow-rules-so-messages-can-bypass-clutter-exchange-2013-help.md)

  - [配置邮件流规则的最佳做法](best-practices-for-configuring-mail-flow-rules-exchange-2013-help.md)

  - [Use mail flow rules to inspect message attachments in Office 365](https://technet.microsoft.com/zh-cn/library/jj919236\(v=exchg.150\))

  - [使用传输规则来配置大容量电子邮件过滤](https://technet.microsoft.com/zh-cn/library/dn720438\(v=exchg.150\))

  - [为加密或解密电子邮件定义规则](https://go.microsoft.com/fwlink/p/?linkid=402846)

  - [在 Office 365 中创建组织范围内安全发件人或阻止发件人列表](https://technet.microsoft.com/zh-cn/library/dn198251\(v=exchg.150\))

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤时间：5 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[邮件策略和遵从性权限](messaging-policy-and-compliance-permissions-exchange-2013-help.md) (Exchange Server) 中或 [Exchange Online 中的功能权限](https://technet.microsoft.com/zh-cn/library/jj200673\(v=exchg.150\)) 中的“传输规则”条目。

  - 如果将规则列出为“版本 14”，则意味着该规则基于 Exchange Server 2010 邮件流规则格式。所有选项都可用于这些规则。

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

## 创建邮件流规则

您可以通过设置数据丢失防护 (DLP) 策略、创建一个新规则或者复制一个规则来创建邮件流规则。您可以使用 Exchange 管理中心 (EAC) 或 Exchange 命令行管理程序。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>创建或修改邮件流规则后，可能需要花费 30 分钟将新的或已更新的规则应用到电子邮件。</td>
</tr>
</tbody>
</table>


## 使用 DLP 策略创建邮件流规则

每个 DLP 策略都是一个邮件流规则集合。创建 DLP 策略后，您可以使用下面的过程微调规则。

1.  更改 DLP 策略。有关说明，请参阅以下内容：
    
      - [Exchange Server 2013 DLP 过程](dlp-procedures-exchange-2013-help.md)
    
      - [Exchange Online DLP 过程](dlp-procedures-exchange-2013-help.md)

2.  修改由 DLP 策略创建的邮件流规则。请参阅查看或修改传输规则。

## 使用 EAC 创建邮件流规则

EAC 使您能够通过使用模板或复制现有规则来创建邮件流规则，或从头开始创建。

1.  转到“邮件流”\>“规则”。

2.  使用以下某一选项创建规则：
    
      - 要从模板创建规则，请单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")，并选择模板。
    
      - 要复制规则，请选择规则，如何选择“复制”![复制图标](images/JJ657480.ed7f7abf-39d8-4f43-a918-ccb3bff87ef5(EXCHG.150).gif "复制图标")。
    
      - 要从头开始创建新的规则，请单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")，然后选择“创建新的规则”。

3.  在“新规则”对话框中，命名该规则，然后选择用于此规则的条件和操作：
    
    1.  在“在以下情况应用此规则…”中，从可用条件列表中选择所需的条件。
        
          - 有些条件需要您指定值。例如，如果您选择“发件人是…”条件，您必须指定发件人的地址。如果您要添加单词或短语，请注意不能用尾随空格。
        
          - 如果没有列出您所需的条件，或者如果您需要添加例外，请选择“更多选项”。将列出其他的条件和例外。
        
          - 如果您不希望指定条件，但希望将该规则应用至组织中的每个邮件，请选择\[应用于所有邮件\]条件。
    
    2.  在“执行以下操作…”中，从列出的可用操作列表中选择希望规则对符合条件的邮件采取的操作。
        
          - 您需要指定一些操作的值。例如，如果您选择“将要审批的邮件转发给…”条件，将需要在组织中选择一个收件人。
        
          - 如果没有列出您所需的条件，请选择“更多选项”。将列出其他的条件。
    
    3.  指定适用于此规则的规则匹配数据如何显示在[数据丢失防护 (DLP) 报告](https://go.microsoft.com/fwlink/p/?linkid=402768)以及[传输规则报告](https://go.microsoft.com/fwlink/p/?linkid=402769)中。
        
          - 在“使用以下严重性级别审核此规则”下，选择一个级别，用来指定此规则的严重级别。邮件流规则组规则的 Office 365 活动报告按严重性级别进行匹配。严重性级别只是一个筛选器，可方便用户使用这些报告。严重性级别对规则的处理优先级没有任何影响。
            
            <table>
            <thead>
            <tr class="header">
            <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
            </tr>
            </thead>
            <tbody>
            <tr class="odd">
            <td>如果您清除“使用以下严重性级别审核此规则”复选框，则规则匹配不会显示在规则报告中。</td>
            </tr>
            </tbody>
            </table>
    
    4.  设置规则的模式。您可以使用两种测试模式之中的一种来测试该规，而不会影响邮件流。当满足条件时，两种测试模式都可以将某个条目添加到邮件跟踪。
        
          - **强制**   该选项会启用规则，并会立即开始处理邮件。将执行有关此规则的所有操作。
        
          - **带有策略提示的测试**   该选项会启用规则，任何策略提示操作（**使用策略提示通知发件人**）都将被发送出去，但不会执行有关消息传递的操作。为了使用此模式，需开启数据丢失防护 (DLP)。若要了解详细信息，请参阅[策略提示](technical-overview-of-policy-tips-in-exchange-online-and-exchange-2013.md)。
        
          - **不带策略提示的测试**   只有“生成事件报告”操作会被强制执行，而不会执行有关消息传递的操作。

4.  如果您对规则感到满意，请转到第 5 步。如果您想要添加更多条件或操作，或者想要指定例外或设置其他属性，请单击“更多选项”。在单击“更多选项”后，填写以下字段来创建自己的规则：
    
    1.  若要添加更多条件，请单击“添加条件”。如果有多个条件，可通过单击条件旁边的“删除 X”来删除其中任何一个。请注意，如果单击“更多选项”将有更多的条件可供使用。
    
    2.  若要添加更多操作，请单击“添加操作”。如果有多个操作，可通过单击操作旁边的“删除 X”来删除其中任何一个。请注意，如果单击“更多选项”将有更多的操作可供使用。
    
    3.  若要指定例外，请单击“添加例外”，然后使用“除非…”下拉列表选择例外。可通过单击例外旁边的“删除 X”删除规则中的任何例外。
    
    4.  如果您希望该规则在特定日期后生效，请单击“在以下日期激活该规则：”并指定一个日期。请注意，规则仍在该日期之前启用，但不会得到处理。
        
        同样地，您也可以在特定日期停止处理规则。为此，请单击“在以下日期停用该规则：”并指定一个日期。请注意，规则在该日期之后仍处于启用状态，但不会得到处理。
    
    5.  您可以选择避免在该规则处理邮件后应用其他规则。为此，请单击“停止处理其他规则”。如果您选择了此选项，且通过该规则处理邮件，那么不会有任何后续规则处理该邮件。
    
    6.  您可以指定在规则无法完成处理时应该如何处理邮件。默认情况下，规则会遭到忽略，且邮件会得到常规处理，但您也可以选择重新提交邮件进行处理。为此，请选中“当规则无法完成处理时延迟邮件”复选框。
    
    7.  如果规则分析发件人地址，默认情况下它只检查邮件头。不过，您还可以将规则配置为检查 SMTP 邮件信封。若要指定检查内容，请单击下面的“匹配邮件中的发件人地址”值之一：
        
          - **头**   只检查邮件头。
        
          - **信封**   只检查 SMTP 邮件信封。
        
          - **头或信封**   检查邮件头和 SMTP 邮件信封。
    
    8.  您可以在“注释”框中对此规则添加注释。

5.  单击“保存”完成规则创建。

## 使用 Exchange 命令行管理程序 创建邮件流规则

本示例使用 [New-TransportRule](https://technet.microsoft.com/zh-cn/library/bb125138\(v=exchg.150\)) cmdlet 新建了对从组织外部发送到销售部门通讯组的邮件预置“`External message to Sales DG:`”的邮件流规则。

    New-TransportRule -Name "Mark messages from the Internet to Sales DG" -FromScope NotInOrganization -SentTo "Sales Department" -PrependSubject "External message to Sales DG:"

上述过程中使用的规则参数和操作仅用于演示。查看所有的可用邮件流规则条件和操作来确定哪个满足您的需求。

## 您如何知道这有效？

若要验证是否已成功新建邮件流规则，请执行下列操作：

  - 在 EAC 中，确认“规则”列表上是否列出了您创建的新邮件流规则。

  - 在 Exchange 命令行管理程序 中，通过运行以下命令验证是否已成功新建邮件流规则（下面的示例验证了您在上面的 Exchange 命令行管理程序 示例中创建的规则）：
    
        Get-TransportRule "Mark messages from the Internet to Sales DG"

## 查看或修改邮件流规则

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>创建或修改邮件流规则后，可能需要花费 30 分钟将新的或已更新的规则应用到电子邮件。</td>
</tr>
</tbody>
</table>


## 使用 EAC 查看或修改邮件流规则

1.  在 EAC 中，转到“邮件流”\>“规则”。

2.  在您选择列表中的一个规则后，该规则的条件、操作、例外和选择属性将显示在细节窗格中。若要查看特定规则的所有属性，请双击该规则。这将打开规则编辑器窗口，您可以在该窗口中更改规则。有关规则属性的详细信息，请参阅本主题前面的使用 EAC 创建邮件流规则部分。

## 使用 Exchange 命令行管理程序 查看或修改邮件流规则

下面的示例列出了您组织中配置的所有规则：

    Get-TransportRule

若要查看特定邮件流规则的属性，您需要提供该规则的名称或其 GUID。这对于将输出发送到 **Format-List** cmdlet 来格式化属性通常很有帮助。下面的示例将返回名为“**Sender is a member of Marketing**”的邮件流规则的所有属性：

    Get-TransportRule "Sender is a member of marketing" | Format-List

若要修改现有规则的属性，请使用 [Set-TransportRule](https://technet.microsoft.com/zh-cn/library/bb123534\(v=exchg.150\)) cmdlet。通过该 cmdlet，您可以更改与规则相关联的任何属性、条件、操作或例外。下面的示例对规则“发件人是营销成员”添加了例外，以使该规则不应用于用户 Kelly Rollin 发送的邮件：

    Set-TransportRule "Sender is a member of marketing" -ExceptIfFrom "Kelly Rollin"

## 您如何知道这有效？

若要验证是否已成功修改邮件流规则，请执行下列操作：

  - 在 EAC 的规则列表中，在“规则”列表中单击您修改的规则，并查看细节窗格。

  - 在 Exchange 命令行管理程序 中，通过运行以下命令验证是否已成功修改邮件流规则，该命令将列出您修改的属性以及规则的名称（下面的示例验证了您在上面的 Exchange 命令行管理程序 示例中修改的规则）：
    
        Get-TransportRule "Sender is a member of marketing" | Format-List Name,ExceptIfFrom

## 邮件流规则属性

您还可以使用 Set-TransportRule cmdlet 修改组织中的现有传输规则。下面是 EAC 中 不可用的列表属性，您可以进行更改。有关使用 Set-TransportRule cmdlet 进行这些更改的详细信息，请参阅 [Set-TransportRule](https://technet.microsoft.com/zh-cn/library/bb123534\(v=exchg.150\))


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>EAC 中的条件名称</th>
<th>Exchange 命令行管理程序 中的条件名称</th>
<th>属性</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>停止处理规则</strong></p></td>
<td><p><code>StopRuleProcessing </code></p></td>
<td><p><code> Not applicable</code></p></td>
<td><p>使您可以停止处理其他规则</p></td>
</tr>
<tr class="even">
<td><p><strong>标头/信封匹配</strong></p></td>
<td><p><code>SenderAddressLocation </code></p></td>
<td><p>不适用</p></td>
<td><p>使您能够检查 SMTP 邮件信封，确保标头和信封匹配</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p><strong>审核严重性</strong></p></td>
<td><p><code>SetAuditSeverity </code></p></td>
<td><p><code>Not applicable</code></p></td>
<td><p>使您能够选择用于审核的严重性级别</p></td>
</tr>
<tr class="even">
<td><p><strong>规则模式</strong></p></td>
<td><p><code>Mode</code></p></td>
<td><p><code>Not applicable</code></p></td>
<td><p>使您能够设置规则的模式</p></td>
</tr>
</tbody>
</table>


## 设置邮件流规则的优先级

首先处理列表顶部的规则。此规则的“优先级”为 0。

## 使用 EAC 来设置规则的优先级

1.  在 EAC 中，转到“邮件流”\>“规则”。此时，将按照处理顺序来显示这些规则。

2.  选择一个规则，并使用箭头将规则在列表中向上或向下移动。

## 使用 Exchange 命令行管理程序 来设置规则的优先级

下面的示例将“发件人是营销成员”的优先级设置为 2：

    Set-TransportRule "Sender is a member of marketing" priority "2"

## 您如何知道这样可行？

若要验证是否已成功修改邮件流规则，请执行下列操作：

  - 从 EAC 的规则列表中，查看规则的顺序。

  - 在 Exchange 命令行管理程序 中，验证规则的优先级（下面的示例验证了您在上面的 Exchange 命令行管理程序 示例中修改的规则）：
    
        Get-TransportRule * | Format-List Name,Priority

## 启用或禁用邮件流规则

这些规则在创建时启用。您可以禁用邮件流规则。

## 使用 EAC 启用或禁用邮件流规则

1.  在 EAC 中，转到“邮件流”\>“规则”。

2.  若要禁用规则，请清除该规则名称旁边的复选框。

3.  若要启用已禁用的规则，请选中该规则名称旁边的复选框。

## 使用 Exchange 命令行管理程序 启用或禁用邮件流规则

下面的示例禁用了邮件流规则“发件人是营销成员”：

    Disable-TransportRule "Sender is a member of marketing"

下面的示例启用了邮件流规则“发件人是营销成员”：

    Enable-TransportRule "Sender is a member of marketing"

## 您如何知道这有效？

若要验证是否已成功启用或禁用邮件流规则，请执行下列操作：

  - 在 EAC 中，查看“规则”列表中的规则列表，并检查“开”列中的复选框状态。

  - 在 Exchange 命令行管理程序 中，运行以下命令，查看组织中返回的所有规则列表及其状态：
    
        Get-TransportRule | Format-Table Name,State

## 删除邮件流规则

## 使用 EAC 删除邮件流规则

1.  在 EAC 中，转到“邮件流”\>“规则”。

2.  选择要删除的规则，然后单击“删除”![删除图标](images/JJ657511.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "删除图标")。

## 使用 Exchange 命令行管理程序 删除邮件流规则

下面的示例删除了邮件流规则“发件人是营销成员”：

    Remove-TransportRule "Sender is a member of marketing"

## 您如何知道这有效？

若要验证是否已成功删除邮件流规则，请执行下列操作：

  - 在 EAC 中，查看“规则”列表中的规则，并验证您删除的规则是否已不再显示。

  - 在 Exchange 命令行管理程序 中，运行以下命令并确认您删除的规则是否已不再列出：
    
        Get-TransportRule

## 监视规则使用情况

如果您正在使用 Exchange Online 或 Exchange Online Protection，您可以通过使用规则报告来检查每一条规则的匹配次数。为了包含在报告中，必须选中规则的“使用以下严重性级别审核此规则”复选框。可以联机查看报告，或下载所有邮件保护报告的 Excel 版本。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>虽然大部分数据会在 24 小时内出现在报告中，但有些数据可能需要长达 5 天才会出现。</td>
</tr>
</tbody>
</table>


## 使用 Office 365 管理中心生成一个报告规则

1.  在 Office 365 管理中心，选择“报告”。

2.  在“规则”部分，选择“邮件的主要规则匹配项”或“邮件的规则匹配项”。

若要了解详细信息，请参阅[查看邮件保护报告](https://go.microsoft.com/fwlink/p/?linkid=402958)。

## 下载报告的 Excel 版本

1.  在 Office 365 管理中心的报告页面上，选择“邮件保护报告 (Excel)”。

2.  如果是首次使用 Excel 邮件保护报告，会打开一个转到下载页面的选项卡。
    
    1.  选择“下载”来下载适用于 Exchange Online 报告的 Microsoft Office 365 Excel 插件。
    
    2.  打开下载文件。
    
    3.  在“Office 365 安装的邮件保护报告”对话框中，选择“下一步”，接受许可协议中的条款，然后选择“下一步”。
    
    4.  选择您要使用的服务，然后选择“下一步”。
    
    5.  验证先决条件，然后选择“下一步”。
    
    6.  选择“安装”。报告的快捷方式会放置在您的桌面上。

3.  在您的桌面上，选择“Office 365 邮件保护报告”。

4.  在该报告中，选择“规则”选项卡。

## 导入或导出邮件流规则集合

您必须使用 Exchange 命令行管理程序 导入或导出邮件流规则集合。有关如何从 XML 文件导入邮件流规则集合的信息，请参阅 [Import-TransportRuleCollection](https://technet.microsoft.com/zh-cn/library/bb123582\(v=exchg.150\))。有关如何将邮件流规则集合导出到 XML 文件的信息，请参阅 [Export-TransportRuleCollection](https://technet.microsoft.com/zh-cn/library/bb124410\(v=exchg.150\))。

## 需要更多帮助？

适用于 Exchange Online 的资源：

[Exchange Online 中的邮件流规则（传输规则）](https://technet.microsoft.com/zh-cn/library/jj919238\(v=exchg.150\))

[在联机 Exchange 邮件流规则条件和例外 （谓语）](https://technet.microsoft.com/zh-cn/library/jj919235\(v=exchg.150\))

[联机在 Exchange 邮件流规则操作](https://technet.microsoft.com/zh-cn/library/jj919237\(v=exchg.150\))

[传输和收件箱规则限制](https://go.microsoft.com/fwlink/p/?linkid=324584)

适用于 Exchange Online Protection 的资源：

[Exchange Online Protection 中的邮件流规则（传输规则）](https://technet.microsoft.com/zh-cn/library/dn271424\(v=exchg.150\))

[邮件流规则条件和例外 （谓语） 在 Exchange 在线保护](https://technet.microsoft.com/zh-cn/library/jj919234\(v=exchg.150\))

[邮件流规则操作在 Exchange 在线保护](https://technet.microsoft.com/zh-cn/library/jj920117\(v=exchg.150\))

[传输和收件箱规则限制](https://go.microsoft.com/fwlink/p/?linkid=324584)

适用于 Exchange Server 2013 的资源：

[邮件流或传输规则](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)

[传输规则条件（谓词）](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md)

[传输规则操作](mail-flow-rule-actions-in-exchange-2013-exchange-2013-help.md)

