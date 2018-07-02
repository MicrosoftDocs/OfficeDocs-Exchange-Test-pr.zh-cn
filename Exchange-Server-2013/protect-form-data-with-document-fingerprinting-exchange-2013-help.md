---
title: '使用文档指纹保护表单数据: Exchange Online Help'
TOCTitle: 使用文档指纹保护表单数据
ms:assetid: 110c839b-7693-42f6-aa5d-58ce64f4c357
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dn635175(v=EXCHG.150)
ms:contentKeyID: 61203671
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 使用文档指纹保护表单数据

 

_**适用于：**Exchange Online, Exchange Server 2013_

_**上一次修改主题：**2014-09-11_

如果贵组织使用表单收集敏感信息，用户可能会尝试将这些表单通过电子邮件发送给外部联系人，这就构成了安全风险。Exchange 中的数据丢失防护 (DLP) 可以帮助您通过[文档指纹](overview-of-document-fingerprinting-in-exchange.md)检测此风险，以保护这些敏感信息。要使用文档指纹，只需上载一个空白表单，例如知识产权文档、政府表单或组织内使用的其他标准表单。然后将生成的文档指纹添加到 DLP 策略或传输规则。方法如下：

> [!VIDEO https://www.microsoft.com/zh-cn/videoplayer/embed/0f803e16-397a-4b83-8a85-06cd4264aaca]

## 使用 EAC 创建文档指纹

![EAC 中文档指纹的路径已突出显示](images/Dn635175.e8562ea7-40ba-4feb-adde-2e81f029fcda(EXCHG.150).png "EAC 中文档指纹的路径已突出显示")

1.  在 Exchange 管理中心 (EAC) 中，转至\&quot;合规性管理\&quot;\>\&quot;数据丢失防护\&quot;。

2.  单击\&quot;管理文档指纹\&quot;。

3.  在文档指纹页面，单击\&quot;新建\&quot;![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")创建新的文档指纹。

4.  为文档指纹提供\&quot;名称\&quot;和\&quot;说明\&quot;。（您选择的名称将出现在敏感信息类型列表中。）

5.  要上载表单，请单击\&quot;添加\&quot;![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。

6.  选择表单，然后单击\&quot;打开\&quot;。（确保您上载的文件包含文本、未受密码保护，且是传输规则中支持的文件类型之一。有关受支持的文件类型的列表，请参阅[Use mail flow rules to inspect message attachments in Office 365](https://technet.microsoft.com/zh-cn/library/jj919236\(v=exchg.150\))。否则，您尝试创建指纹时将收到错误。）对要添加到此文档指纹的文档列表中的任何其他文件重复此操作。稍后您也可以向此文档指纹添加文件或从中删除文件。

7.  单击\&quot;保存\&quot;。

文档指纹现在是敏感信息类型的一部分，您可以通过\&quot;邮件包含敏感信息…\&quot;条件将其添加到 DLP 策略或传输规则。

![\&quot;Apply this rule if\&quot;条件已突出显示](images/Dn635175.9355a513-a790-48eb-a61b-575ba2ecdfa6(EXCHG.150).png "&quot;Apply this rule if&quot;条件已突出显示")

有关将规则添加到 DLP 策略的详细信息，请参阅[管理 DLP 策略](manage-dlp-policies-exchange-2013-help.md)的\&quot;更改 DLP 策略\&quot;部分。有关修改传输规则的详细信息，请参阅[将敏感信息规则与传输规则集成](integrating-sensitive-information-rules-with-transport-rules-exchange-2013-help.md)。如果您想创建新规则，请参阅[从模板创建 DLP 策略](how-to-new-dlp-data-loss-prevention-policy-template.md)。

## 使用 Shell 创建基于文档指纹的分类规则包

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>尽管您可以在 Shell 中创建和修改分类规则包，但您会发现在 EAC 中创建文档指纹更简单一点。我们建议您先在 EAC 中尝试，然后再在 Shell 中尝试执行此过程。</td>
</tr>
</tbody>
</table>


DLP 使用分类规则包检测邮件中的敏感内容。要创建基于文档指纹的分类规则包，请使用 **New-Fingerprint** 和 **New-DataClassification** cmdlet。由于 **New-Fingerprint** 的结果不会在数据分类规则以外存储，因此请始终在相同 PowerShell 会话中运行 **New-Fingerprint** 和 **New-DataClassification** 或 **Set-DataClassification**。以下示例基于文件 C:\\My Documents\\Contoso Employee Template.docx 创建新的文档指纹。由于新的指纹存储为变量，因此可以在相同 PowerShell 会话中使用 **New-DataClassification** cmdlet。

    $Employee_Template = Get-Content "C:\My Documents\Contoso Employee Template.docx" -Encoding byte
    $Employee_Fingerprint = New-Fingerprint -FileData $Employee_Template -Description "Contoso Employee Template"

现在，我们可以一起创建名为\&quot;Contoso Employee Confidential\&quot;的新数据分类规则，该规则使用文件 C:\\My Documents\\Contoso Customer Information Form.docx 的文档指纹。

    $Employee_Template = Get-Content "C:\My Documents\Contoso Customer Information Form.docx" -Encoding byte
    $Customer_Fingerprint = New-Fingerprint -FileData $Customer_Form -Description "Contoso Customer Information Form"
    New-DataClassification -Name "Contoso Customer Confidential" -Fingerprints $Customer_Fingerprint -Description "Message contains Contoso customer information." 

现在您可以使用 **Get-DataClassification** cmdlet 查找所有 DLP 数据分类规则包。在本示例中，\&quot;Contoso Customer Confidential\&quot;是数据分类规则包列表的一部分。

最后，将\&quot;Contoso Customer Confidential\&quot;数据分类规则包添加到 DLP 策略。

    New-TransportRule -Name "Notify :External Recipient Contoso confidential" -NotifySender NotifyOnly -Mode Enforce -SentToScope NotInOrganization -MessageContainsDataClassification @{Name=" Contoso Customer Confidential"}

DLP 代理现在可以检测匹配 Contoso Customer Form.docx 文档指纹的文档。

有关语法和参数的信息，请参阅 [New-Fingerprint](https://technet.microsoft.com/zh-cn/library/dn584142\(v=exchg.150\))、[New-DataClassification](https://technet.microsoft.com/zh-cn/library/dn584139\(v=exchg.150\))、[Set-DataClassification](https://technet.microsoft.com/zh-cn/library/dn584141\(v=exchg.150\)) 和 [Get-DataClassification](https://technet.microsoft.com/zh-cn/library/jj215720\(v=exchg.150\))。

## 详细信息

[文档指纹](overview-of-document-fingerprinting-in-exchange.md)

[管理 DLP 策略](manage-dlp-policies-exchange-2013-help.md)

[将敏感信息规则与传输规则集成](integrating-sensitive-information-rules-with-transport-rules-exchange-2013-help.md)

