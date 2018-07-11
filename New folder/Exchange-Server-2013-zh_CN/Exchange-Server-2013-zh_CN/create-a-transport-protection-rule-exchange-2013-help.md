---
title: '创建传输保护规则: Exchange 2013 Help'
TOCTitle: 创建传输保护规则
ms:assetid: 3a857185-ee16-4ee7-9e57-8be95f7e753a
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd302432(v=EXCHG.150)
ms:contentKeyID: 50490334
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 创建传输保护规则

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2016-12-09_

可以使用传输保护规则（基于属性，如发件人、收件人、邮件主题和内容）对邮件应用永久权限保护。

> [!CAUTION]
> 在生产环境中创建传输规则之前，我们建议创建一个测试环境并进行全面测试。本主题中创建传输规则的示例。可以通过使用适当的传输规则谓词和根据您的需求的值创建传输规则。


有关信息权限管理 (IRM) 的其他管理任务，请参阅[信息权限管理过程](information-rights-management-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：2-5 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [邮件策略和遵从性权限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主题中的\&quot;传输规则\&quot;条目。

  - 运行[Active Directory Rights Management Services (AD RMS)](https://technet.microsoft.com/en-us/library/hh831364.aspx)的服务器必须可以在您的组织中，并包含现有 RMS 模板。

  - 如果配置传输保护规则来保护消息使用 IRM，您也可以使用日志记录，请考虑启用日志报告解密，使日志记录代理保存该邮件的未加密的副本日志报告中。若要了解详细信息，请参阅[日记报告解密](journal-report-decryption-exchange-2013-help.md)。

  - 在创建传输保护规则，如果因为 AD RMS 服务器不可用，不能将规则应用于邮件后，将通过对邮箱服务器上的传输服务的排队消息。根据这些消息的信息量，可能在邮箱服务器上占用额外的磁盘空间。Exchange将尝试对 IRM 保护邮件三次。之后这些尝试，如果 AD RMS 服务器不可访问或消息不能为受 IRM 保护的未送达报告 (NDR) 发送给发件人。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!tip]
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 您想执行什么操作？

## 使用 EAC 创建传输保护规则

1.  导航到\&quot;邮件流\&quot;\>\&quot;规则\&quot;。

2.  在列表视图中，单击\&quot;新建\&quot;![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。

3.  在\&quot;新建规则\&quot;中，先单击\&quot;更多选项\&quot;，然后填写下列字段：
    
      - **名称** 键入传输规则的名称。
    
      - **如果，应用该规则**  选择一个条件并输入所需的任何值的情况。若要添加更多条件，请单击**添加条件**。
        
        > [!important]
        > 如果不选择任何条件，创建传输保护规则时，Exchange 2013 与组织中的传输服务的服务器处理的所有消息都是受 IRM 保护。IRM 保护所有邮件都需要更多的资源。因此，我们建议相应地规划您的邮箱服务器和部署 AD RMS。
    
      - **执行以下操作**   选择\&quot;将权限保护应用于邮件\&quot;，然后使用\&quot;选择 RMS 模板\&quot;对话框选择一个模板。
    
      - **除非**   （可选）单击\&quot;添加例外\&quot;为规则指定一个例外。

4.  单击\&quot;保存\&quot;创建传输规则。

## 使用命令行管理程序创建传输保护规则

  - 若要创建传输保护规则，必须在 AD RMS 部署现有 RMS 模板。本示例检索来自 AD RMS 群集可用的模板。
    
        Get-RMSTemplate | format-list
    
    有关语法和参数的详细信息，请参阅 [Get-RMSTemplate](https://technet.microsoft.com/zh-cn/library/dd297960\(v=exchg.150\))。

  - 本示例创建传输保护规则保护 BusinessCriticalProject。包含"关键业务"与**不要转发**模板的主题字段中的短语规则 IRM 保护消息。
    
    > [!NOTE]
    > 在此示例中使用<code>SubjectContainsWords</code>谓词。可以使用传输规则谓词的任意组合以形成条件和例外的规则。有关可用的谓词的信息，请参阅<a href="mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md">传输规则条件（谓词）</a>。
    
        New-TransportRule -Name "Protect-BusinessCriticalProject" -SubjectContainsWords "Business Critical" -ApplyRightsProtectionTemplate "Do Not Forward"
    
    有关语法和参数的详细信息，请参阅 [New-TransportRule](https://technet.microsoft.com/zh-cn/library/bb125138\(v=exchg.150\))。

## 您如何知道这有效？

要验证您是否已成功创建了传输保护规则，请执行以下操作之一：

  - 使用 EAC 验证是否已创建此规则，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标") 查看此规则的属性。

  - 使用[Get-TransportRule](https://technet.microsoft.com/zh-cn/library/aa998585\(v=exchg.150\)) cmdlet 来检索该规则。有关如何检索规则的示例，请参阅**Get-TransportRule**中的[示例](https://technet.microsoft.com/zh-cn/aa998585\(exchg.150\)#examples)。

  - 使用 Outlook、Outlook Web App 或移动设备发送一封符合规则条件的测试邮件，然后检查收件人收到的邮件是否受 IRM 保护。

