---
title: '管理 DSN 邮件: Exchange 2013 Help'
TOCTitle: 管理 DSN 邮件
ms:assetid: 23c9d844-6fc7-44c9-a308-587338281611
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa996803(v=EXCHG.150)
ms:contentKeyID: 50490077
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
f1_keywords:
- 更改系统邮件
- 更改拒绝邮件
- 更改配额邮件
- 更改 ndr 邮件
ms.translationtype: HT
---

# 管理 DSN 邮件

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2013-02-20_

Microsoft Exchange Server 2013 使用传递状态通知 (DSN) 向邮件发件人提供未送达报告 (NDR) 和其他状态消息。您可以使用内置 DSN，也可以创建自定义 DSN 邮件以满足组织需求。

## 在开始之前，您需要知道什么？

  - 估计完成时间：15 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[邮件流权限](mail-flow-permissions-exchange-2013-help.md)主题中的“DNS”条目。

  - 无法删除随 Exchange 附带的内置 DSN 邮件。要更改内置 DSN 邮件，需要为要自定义的 DSN 代码创建自定义 DSN 邮件。删除自定义 DSN 邮件后，与该邮件关联的 DSN 代码将还原为随 Exchange 附带的内置 DSN 邮件。

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

## 使用命令行管理程序查看内置的和自定义的 DSN 邮件

要查看随 Exchange 2013 附带的所有内置 DSN 邮件的摘要列表，请运行以下命令：

    Get-SystemMessage -Original

要查看组织中的所有自定义 DSN 邮件的摘要列表，请运行以下命令：

    Get-SystemMessage

要查看以英语形式发送给内部发件人的 DSN 代码 5.1.2 自定义 DSN 邮件的详细信息，请运行以下命令：

    Get-SystemMessage En\Internal\5.1.2 | Format-List

## 使用命令行管理程序创建自定义 DSN 邮件

运行以下命令：

    New-SystemMessage -Internal <$true | $false> -Language <Locale> -DSNCode <x.y.z> -Text "<DSN text>"

此示例创建以英语形式发送给内部发件人的 DSN 代码 5.1.2 自定义纯文本 DSN 邮件。

    New-SystemMessage -Internal $true -Language En -DSNCode 5.1.2 -Text "You tried to send a message to a disabled mailbox that's no longer accepting messages. Please contact the Help Desk at extension 123 for assistance."

此示例创建以英语形式发送给外部发件人的 DSN 代码 5.1.2 自定义纯文本 DSN 邮件。

    New-SystemMessage -Internal $false -Language En -DSNCode 5.1.2 -Text "You tried to send a message to a disabled mailbox that's no longer accepting messages. Please contact your System Administrator for more information."

此示例创建以英语形式发送给内部发件人的 DSN 代码 5.1.2 自定义 HTML DSN 邮件。

    New-SystemMessage -DSNCode 5.1.2 -Internal $true -Language En -Text 'You tried to send a message to a <B>disabled</B> mailbox. Please visit <A HREF="http://it.contoso.com">Internal Support</A> or contact &quot;InfoSec&quot; for more information.'

## 您如何知道这有效？

要验证是否已成功创建自定义 DNS 邮件，请执行以下操作：

1.  运行以下命令：
    
        Get-SystemMessge -DSNCode <x.y.z> | Format-List Name,Internal,Text,Language

2.  验证显示的值是否为您配置的值。

3.  发送将生成您配置的自定义 DSN 的测试邮件。

## 使用命令行管理程序更改自定义 DSN 邮件的文本

要更改自定义 DSN 邮件的文本，请运行以下命令：

    Set-SystemMessage <Locale>\<Internal | External>\<DSNcode> -Text "<DSN text>"

此示例更改分配到以英语形式发送给内部发件人的 DSN 代码 5.1.2 自定义 DSN 邮件的文本。

    Set-SystemMessage En\Internal\5.1.2 -Text "The mailbox you tried to send an e-mail message to is disabled and is no longer accepting messages. Please contact the Help Desk at extension 123 for assistance."

## 您如何知道这有效？

要验证是否已成功更改自定义 DNS 邮件的文本，请执行以下操作：

1.  运行以下命令：`Get-SystemMessage`.
    
        Set-SystemMessage <Locale>\<Internal | External>\<DSNcode> | Format-List -Text

2.  验证显示的值是否为您配置的值。

## 使用命令行管理程序删除自定义 DSN 邮件

运行以下命令：

    Remove-SystemMessage <Local>\<Internal | External>\<DSNcode>

此示例删除以英语形式发送给内部发件人的 DSN 代码 5.1.2 自定义 DSN 邮件。

    Remove-SystemMessage En\Internal\5.1.2

## 您如何知道这有效？

要验证是否已成功删除自定义 DNS 邮件，请执行以下操作：

1.  运行以下命令：`Get-SystemMessage`.

2.  验证 DSN 的区域设置、内部或外部收件人以及是否未列出您已删除的 DSN 代码。

## 将 DSN 邮件副本转发到 Exchange 收件人邮箱

通过将 DSN 邮件复制到 Exchange 收件人的邮箱，可以指定要监视的一系列 DSN 代码。但是默认情况下，不会向 Exchange 收件人分配邮箱，因此任何发送给 Exchange 收件人的邮件都将被丢弃。要将 DSN 邮件副本发送给 Exchange 收件人邮箱，您需要向 Exchange 收件人分配一个邮箱，然后指定要监视的 DSN 代码。默认情况下，监视以下 DSN 代码：`5.4.8`、`5.4.6`、`5.4.4`、`5.2.4`、`5.2.0` 和 `5.1.4`。

## 步骤 1：使用命令行管理程序将邮箱分配给 Exchange 收件人

要将邮箱分配给 Exchange 收件人，请执行以下步骤：

1.  由于电子邮件的数量可能会很大，请考虑为 Exchange 收件人创建专用邮箱和 Active Directory 用户帐户。有关更多信息，请参阅[创建用户邮箱](create-user-mailboxes-exchange-2013-help.md)。否则，确定要与 Exchange 收件人关联的现有邮箱。

2.  运行以下命令：
    
        Set-OrganizationConfig -MicrosoftExchangeRecipientReplyRecipient <MailboxIdentity>
    
    例如，要将名为“Contoso System Mailbox”的现有邮箱分配给 Exchange 收件人，请运行以下命令：
    
        Set-OrganizationConfig -MicrosoftExchangeRecipientReplyRecipient "Contoso System Mailbox"

## 步骤 2：指定要监视的 DSN 代码

## 使用 EAC 指定 DSN 代码

1.  在 EAC 中，导航到“邮件流”\>“接收连接器”\>“更多选项”![更多选项图标](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "更多选项图标") \>“组织传输设置”\>“传递”。

2.  在“DNS 代码”部分中，使用 *\<x.y.z\>* 格式键入要监视的 DSN 代码，然后单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。选择现有条目并单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标") 修改该条目，或单击“删除”![删除图标](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "删除图标") 删除该条目。完成后，单击“Save”。

## 使用命令行管理程序指定 DSN 代码

要替换现有值，请运行以下命令：

    Set-TransportConfig -GenerateCopyOfDSNFor <x.y.z>,<x.y.z>...

此示例将 Exchange 组织配置为将包含 DSN 代码 5.7.1、5.7.2 和 5.7.3 的所有 DSN 邮件转发到 Exchange 收件人。

    Set-TransportConfig -GenerateCopyOfDSNFor 5.7.1,5.7.2,5.7.3

要在不修改任何现有值的情况下添加或删除条目，请运行以下命令：

    Set-TransportConfig -GenerateCopyOfDSNFor @{Add="<x.y.z>","<x.y.z>"...; Remove="<x.y.z>","<x.y.z>"...}

此示例在转发到 Exchange 收件人的现有 DSN 邮件列表中添加 DSN 代码 5.7.5 并删除 DSN 代码 5.7.1。

    Set-TransportConfig -GenerateCopyOfDSNFor @{Add="5.7.5"; Remove="5.7.1"}

## 您如何知道这有效？

要验证您是否已成功将 DNS 邮件副本配置为发送到 Exchange 收件人的邮箱，请监视与 Exchange 收件人关联的邮箱，并验证 DSN 邮件是否包含您指定的 DSN 代码。

