﻿---
title: '创建通讯组命名策略: Exchange 2013 Help'
TOCTitle: 创建通讯组命名策略
ms:assetid: b2ffb654-345d-4be1-be8e-83d28901373e
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ218693(v=EXCHG.150)
ms:contentKeyID: 50489787
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 创建通讯组命名策略

 

_**适用于：**Exchange Online, Exchange Server 2013_

_**上一次修改主题：**2012-11-01_

使用组命名策略，您可以对您组织中的用户创建的通讯组的名称进行管理并使之标准化。您可以要求在创建通讯组时向其名称中添加特定前缀和后缀，并且可以阻止使用特定词语。这可帮助您尽可能减少在组名称中使用不适当的词语。

组命名策略：

  - 对用户创建的组强制执行一致的命名策略。

  - 在共享通讯簿中标识通讯组。

  - 提出有关组的功能或成员身份的建议。

  - 标识可能成为组成员的用户类型。

  - 标识使用组的地理区域。

  - 阻止在组名称中使用不适当的词语。

组命名策略是如何工作的？当用户创建一个组时，将在“显示名”字段指定一个名称。在创建组之后，Microsoft Exchange 会通过添加在组命名策略中定义的任何前缀或后缀来应用组命名策略。在 Exchange 管理中心 (EAC) 的通讯组列表、共享通讯簿以及电子邮件“收件人:”、“抄送:”和“发件人:”字段中将显示全名。如果用户尝试使用您已阻止的词语，则当他们尝试保存新组时，他们会收到一条错误消息，要求他们删除被阻止的词语，然后重新保存该组。

下面是一些组命名策略的示例。在每个组命名策略中，**\<组名称\>**是创建该组的人员提供的描述性名称。创建组时，Exchange 会将策略定义的前缀和后缀添加到显示名称。

  - 用于单个前缀 (**DG**) 和后缀 (**Users**) 的文本字符串（包含下划线字符）：
    
    **DG\_\<Group Name\>\_Users**

  - 多个前缀（**DG** 和 **Contoso**）和一个后缀（**Users**），使用文本字符串：
    
    **DG\_Contoso\_\<Group Name\>\_Users**

  - 一个用于前缀的特性 (**Department**)：
    
    **Department\_\<Group Name\>**
    
    例如，假定您的学校填充教职工的 Department 特性。下面是心理学系的某个教职工创建的组名称的示例：
    
    **Psychology\_Cognitive201**
    
    在此示例中，下划线字符 (\_) 作为第二个前缀中唯一的文本字符串提供，用于将部门名称与组名称分开。

## 在开始之前，您需要知道什么？

  - 估计完成时间：5 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[收件人权限](recipients-permissions-exchange-2013-help.md)主题中的“通讯组”条目。

  - 组名称的最大长度为 64 个字符。这包括前缀、用户提供的组名称和后缀的组合字符数。

  - 只对用户创建的组应用组命名策略。当您或其他管理员使用 EAC 创建通讯组时，组命名策略将被忽略，并且不会应用于组名称。

  - 创建组名称时不会保留空格。建议您在文本字符串、属性和组名称之间使用下划线字符 (\_) 或一些其他占位符。

  - 创建和编辑通讯组时，可以使用 Windows PowerShell 覆盖组命名策略。有关详细信息，请参阅[重命名策略的通讯组](override-the-distribution-group-naming-policy-exchange-2013-help.md)。

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


## 使用 EAC 创建组命名策略

1.  在 EAC 中，选择“组” \> “更多” \> “配置组命名策略”。

2.  在“组命名策略”下，可以通过在下拉菜单中选择“属性”或“文本”来配置前缀。
    
      - **属性**   选择属性，然后单击“确定”。
    
      - **文本**   键入文本字符串，然后单击“确定”。
    
    请注意，您键入的文本字符串或所选的特性都会显示为超链接。单击超链接可更改文本字符串或特性。

3.  单击“添加”可添加其他前缀。

4.  对于后缀，在下拉菜单中选择“属性”或“文本”，然后配置后缀。

5.  单击“添加”可添加其他后缀。
    
    在添加前缀或后缀之后，请注意，将会显示的组命名策略的预览。

6.  若要从策略中删除前缀或后缀，请单击“删除”![删除](images/JJ218693.37ba42c3-6f0d-42f3-b69b-ff912a99b5b7(EXCHG.150).gif "删除")。

7.  单击“阻止的词语”可添加或删除阻止的词语。
    
      - 若要向列表中添加词语，请键入要阻止的词语，然后单击“添加”![为电子邮件迁移中排除的文件夹添加符号](images/JJ218693.444d5c83-821f-472c-b733-e84308e2531e(EXCHG.150).gif "为电子邮件迁移中排除的文件夹添加符号")。
    
      - 若要从列表中删除词语，请将其选中，然后单击“删除”。
    
      - 若要编辑现有已阻止的词语，请将其选中，然后单击“编辑”。

8.  完成后，单击“Save”。

## 您如何知道这有效？

若要验证是否已成功创建组命名策略，请执行以下操作：

  - 在 EAC 中，选择“组” \> “更多” \> “配置组命名策略”。
    
    在“组命名策略”页面，定义的组命名策略将显示在“策略预览”下方。

  - 在 Windows PowerShell 中，运行以下命令可显示组命名策略：
    
        Get-OrganizationConfig | FL DistributionGroupNamingPolicy

