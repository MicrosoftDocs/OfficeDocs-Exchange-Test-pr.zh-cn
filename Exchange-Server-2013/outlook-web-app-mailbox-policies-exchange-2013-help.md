---
title: 'Outlook Web App 邮箱策略: Exchange 2013 Help'
TOCTitle: Outlook Web App 邮箱策略
ms:assetid: 213b8b7a-1c29-49ee-8c98-d0364ddf4f9d
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd335142(v=EXCHG.150)
ms:contentKeyID: 50490201
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Outlook Web App 邮箱策略

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2012-10-05_

使用 MicrosoftOutlook Web App 邮箱策略创建组织级别策略可管理对 Outlook Web App 中功能的访问权限。

**目录**

Outlook Web App 邮箱策略

创建或删除 Outlook Web App 邮箱策略

配置 Outlook Web App 邮箱策略

应用 Outlook Web App 邮箱策略

## Outlook Web App 邮箱策略

在 Exchange 2013 中，可以创建多个 Outlook Web App 邮箱策略，并将其应用到单个邮箱。将 Outlook Web App 邮箱策略应用到邮箱后，它将覆盖虚拟目录的设置。

Outlook Web App 功能也可通过配置 Outlook Web App 虚拟目录进行管理。虚拟目录设置将用于任何尚未应用邮箱策略的邮箱。

## 创建或删除 Outlook Web App 邮箱策略

默认的 Outlook Web App 邮箱策略在安装 Exchange 时自动创建。默认情况下，在默认 Outlook Web App 邮箱策略上启用所有选项。可以根据组织需要创建多个 Outlook Web App 邮箱策略。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>默认的 Outlook Web App 邮箱策略不会自动应用到任何邮箱。</td>
</tr>
</tbody>
</table>


有关创建或删除邮箱策略的信息，请参阅[创建 Outlook Web App 邮箱策略](create-an-outlook-web-app-mailbox-policy-exchange-2013-help.md)和[从 Exchange 中删除 Outlook Web App 邮箱策略](remove-an-outlook-web-app-mailbox-policy-from-exchange-exchange-2013-help.md)。

## 配置 Outlook Web App 邮箱策略

默认情况下，默认的 Outlook Web App 邮箱策略会启用所有选项。有关配置 Outlook Web App 邮箱策略的信息，请参阅[查看或配置 Outlook Web 应用程序邮箱策略属性](view-or-configure-outlook-web-app-mailbox-policy-properties-exchange-2013-help.md)。

## 应用 Outlook Web App 邮箱策略

一个邮箱只能应用一个 Outlook Web App 邮箱策略。

如果未对某个邮箱应用 Outlook Web App 邮箱策略，则将应用虚拟目录上定义的设置。

通过使用 Exchange 管理中心 (EAC) 修改现有邮箱或通过使用命令行管理程序和 [Set-CASMailbox](https://technet.microsoft.com/zh-cn/library/bb125264\(v=exchg.150\)) cmdlet 应用邮箱策略，可以将 Outlook Web App 邮箱策略应用到邮箱。有关详细信息，请参阅[向邮箱应用或删除 Outlook Web App 邮箱策略](apply-or-remove-an-outlook-web-app-mailbox-policy-on-a-mailbox-exchange-2013-help.md)。

