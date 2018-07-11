---
title: '管理邮件审批并进行故障排除: Exchange 2013 Help'
TOCTitle: 管理邮件审批并进行故障排除
ms:assetid: 860df43f-a05b-4da3-83f1-68d3123a923d
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd298110(v=EXCHG.150)
ms:contentKeyID: 52061523
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 管理邮件审批并进行故障排除

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-03-09_

尝试删除仲裁邮箱时，可能收到以下错误消息：


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>无法删除仲裁邮箱 &lt;<em>邮箱</em>&gt;，因为它正用于启用成员资格限制或审阅的现有收件人的审批工作流。在删除此仲裁邮箱之前，应当禁用这些收件人的审批功能，或为这些收件人指定其他仲裁邮箱。</p></td>
</tr>
</tbody>
</table>


仲裁邮箱可用于处理仲裁收件人和通讯组成员身份审批的审批工作流。可以使用 PowerShell 查找所有配置为使用仲裁邮箱的收件人。确定收件人后，可以配置他们以使用其他仲裁邮箱，或者可以禁用对他们的审阅。

## 在开始之前，您需要知道什么？

  - 估计完成时间：15 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[收件人权限](recipients-permissions-exchange-2013-help.md)主题中的“仲裁”条目。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

## 步骤 1：使用命令行管理程序查找所有使用您正尝试删除的仲裁邮箱的收件人

运行以下命令：

    $AM = Get-Mailbox "<arbitration mailbox>" -Arbitration
    $AMDN = $AM.DistinguishedName
    Get-Recipient -RecipientPreviewFilter {ArbitrationMailbox -eq $AMDN}

例如，要查找所有使用名为 Arbitration Mailbox01 的仲裁邮箱的收件人，请运行下列命令：

    $AM = Get-Mailbox "Arbitration Mailbox01" -Arbitration
    $AMDN = $AM.DistinguishedName
    Get-Recipient -RecipientPreviewFilter {ArbitrationMailbox -eq $AMDN}

> [!NOTE]  
> 仲裁邮箱是使用可分辨名称 (DN) 指定的。如果您知道仲裁邮箱的 DN，可以运行单一命令：<code>Get-Recipient -RecipientPreviewFilter {ArbitrationMailbox -eq &lt;DN&gt;}</code>。<code>Get-Recipient -RecipientPreviewFilter {ArbitrationMailbox -eq &lt;DN&gt;}</code>.


## 步骤 2：使用命令行管理程序指定其他仲裁邮箱或者禁用对收件人的仲裁

要阻止仲裁收件人使用您正尝试删除的仲裁邮箱，您可以指定其他仲裁邮箱，也可以禁用对收件人的审阅。

如果选择为收件人指定其他仲裁邮箱，请运行下列命令：

    Set-<RecipientType> <Identity> -ArbitrationMailbox <different arbitration mailbox>

例如，要重新配置名为 All Employees 的通讯组以使用名为 Arbitration Mailbox02 的仲裁邮箱进行成员身份验证审批，请运行下列命令：

    Set-DistributionGroup "All Employees" -ArbitrationMailbox "Arbitration Mailbox02"

如果选择禁用对收件人的审阅，请运行下列命令：

    Set-<RecipientType> <Identity> -ModerationEanbled $false

例如，要禁用对名为 Human Resources 的邮箱的审阅，请运行下列命令：

    Set-Mailbox "Human Resources" -ModerationEanbled $false

## 您如何知道操作成功？

如果您可以删除仲裁邮箱且未收到说明它正在使用的错误，则此过程是成功的。

遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

