---
title: '配置外部邮局主管地址: Exchange 2013 Help'
TOCTitle: 配置外部邮局主管地址
ms:assetid: 6b0c8675-3238-462d-8973-b52305fb90d2
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb430765(v=EXCHG.150)
ms:contentKeyID: 52061515
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 配置外部邮局主管地址

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2016-12-09_

外部邮局主管地址用作发送给 Microsoft Exchange Server 2013 组织外部的邮件发件人的系统生成的邮件和通知的发件人。外部发件人是在组织中未配置为接受域的域中拥有电子邮件地址的任何发件人。

默认情况下，外部邮局主管地址设置的值为空。此默认值会导致你的 Exchange 组织出现以下行为：

  - 对于所有邮箱服务器和已订阅的边缘传输服务器，外部邮局主管地址为 postmaster@\<*默认接受域*\>。

  - 对于所有未订阅的边缘传输服务器，外部邮局主管地址为 postmaster@\<*Edge Transport server FQDN*\>。

## 在开始之前，您需要知道什么？

  - 估计完成时间：15 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[邮件流权限](mail-flow-permissions-exchange-2013-help.md)主题中的“传输配置”条目。

  - 在配置自定义外部邮局主管地址时，该值将应用于 Exchange 组织中的所有 Exchange 2013 邮箱服务器和 Exchange 2010 集线器传输服务器。但是，该值不会复制到边缘传输服务器上。如果为外部邮局主管地址指定了自定义值，则需要在任何边缘传输服务器上手动配置外部邮局主管地址。

  - 如果你的组织中拥有任何 Exchange 2007 集线器传输服务器或边缘传输服务器，需要使用 **Set-TransportServer** cmdlet 在每个服务器上配置自定义外部邮局主管地址。有关详细信息，请参阅[管理外部邮局主管地址](https://go.microsoft.com/fwlink/?linkid=279922)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

## 您想执行什么操作？

## 使用 EAC 配置外部邮局主管地址

1.  在 EAC 中，导航到“邮件流”\>“接收连接器”\>“更多选项”![更多选项图标](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "更多选项图标")\>“组织传输设置”\>“传递”选项卡。

2.  在“**外部邮局主管地址**”字段中，输入 SMTP 电子邮件地址，如 `postmaster@contoso.com`。如果要将外部邮局主管地址恢复为默认值，请删除任何现有值，使该字段留空。

3.  完成时，请单击“保存”。

## 使用命令行管理程序配置外部邮局主管地址

若要配置外部邮局主管地址，可使用下列语法。

    Set-TransportConfig -ExternalPostmasterAddress <postmaster address>

例如，若要将外部邮局主管地址设置为 `postmaster@contoso.com` 值，请运行以下命令

    Set-TransportConfig -ExternalPostmasterAddress postmaster@contoso.com

若要将外部邮局主管地址返回至默认值，可运行下列命令：

    Set-TransportConfig -ExternalPostmasterAddress $null

## 您如何知道操作成功？

要验证您是否已成功配置外部邮局主管地址，可执行以下操作：

1.  在邮箱服务器上运行下列命令，以验证该外部邮局主管地址值：
    
        Get-TransportConfig | Format-List ExternalPostmasterAddress

2.  从外部电子邮件帐户向你的 Exchange 组织发送将生成传递状态通知 (DSN) 的邮件。例如，你可以将传输规则配置为从包含特定关键字的发件人发送邮件的未送达报告 (NDR)。验证 DSN 中该发件人的电子邮件地址是否与你指定的值匹配。

遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

