---
title: '为收件人配置自定义邮件提示: Exchange 2013 Help'
TOCTitle: 为收件人配置自定义邮件提示
ms:assetid: df8ee7ae-2486-4890-b057-cda87b4cb1ec
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd638199(v=EXCHG.150)
ms:contentKeyID: 52061427
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 为收件人配置自定义邮件提示

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2014-06-01_

*邮件提示*是用户在一边撰写电子邮件一边执行下列操作之一时在 Outlook Web App 和 Microsoft Outlook 2010 或更高版本的信息栏中看到的信息性消息：

  - 添加收件人

  - 添加附件

  - 答复或全部答复

  - 从“草稿”文件夹中打开已添加收件人地址的邮件

除了可以使用内置邮件提示之外，您还可以创建适用于所有类型的收件人的自定义邮件提示。有关内置邮件提示的详细信息，请参阅[MailTips](mailtips-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：10 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[邮件流权限](mail-flow-permissions-exchange-2013-help.md)主题中的“邮件提示”条目。

  - 您可以在 Exchange 管理中心 (EAC) 或命令行管理程序中配置主要的邮件提示。不过，您只能在命令行管理程序中配置其他邮件提示转换。

  - 当您向收件人添加邮件提示时，会发生两件事：
    
      - HTML 标记会自动添加到文本中。例如，如果您输入以下文本：`This mailbox is not monitored`，那么邮件提示会自动变为：`<html><body>This mailbox is not monitored</body></html>`。不支持邮件提示中的其他 HTML 标记。
    
      - 此文本会作为默认值自动添加到收件人的 *MailTipTranslations* 属性中。如果您修改邮件提示文本，那么默认值会在 *MailTipTranslations* 属性中自动更新。

  - 邮件提示的长度不得超过 175 个显示字符。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 要执行什么操作？

## 配置收件人的邮件提示

## 使用 EAC 配置收件人的邮件提示

1.  在 EAC 中，导航到“收件人”。

2.  根据收件人类型，选择下列收件人选项卡之一：
    
      - **邮箱**
    
      - **组**
    
      - **资源**
    
      - **联系人**
    
      - **已共享**

3.  在收件人选项卡上，选择要修改的收件人，然后单击“修改”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

4.  在显示的收件人属性页面上，单击“邮件提示”。

5.  输入邮件提示的文本。完成后，单击“保存”。

## 使用命令行管理程序配置收件人的邮件提示

若要配置收件人的邮件提示，请使用下列语法：

    Set-<RecipientType> <RecipientIdentity> -MailTip "<MailTip text>"

*\<RecipientType\>* 可以指定任何类型的收件人。例如，`Mailbox`、`MailUser`、`MailContact`、`DistributionGroup` 或 `DynamicDistributionGroup`。

例如，假设您拥有一个名为“技术支持”的邮箱，以供用户提交支持请求，且承诺的响应时间为两个小时。若要配置一个用于说明此情况的自定义邮件提示，请运行以下命令：

    Set-Mailbox "Help Desk" -MailTip "A Help Desk representative will contact you within 2 hours."

## 使用命令行管理程序配置语言不同的其他邮件提示

若要配置其他邮件提示转换，但不影响现有的邮件提示文本或其他现有的邮件提示转换，请使用下列语法：

    Set-<RecipientType> -MailTipTranslations @{Add="<culture1>:<localized text 1>","<culture2>:<localized text 2>"...; Remove="<culture1>:<localized text 1>","<culture2>:<localized text 2>"...}

*\<culture\>* 是一个与语言相关联的有效 ISO 639 双字母区域性代码。

例如，假设名为“通知”的邮箱当前拥有以下邮件提示：“该邮箱未受监视。”若要添加西班牙语翻译，请运行以下命令：

    Set-Mailbox -MailTipTranslations @{Add="ES:Esta caja no se supervisa."}

## 您如何知道操作成功？

若要验证是否成功配置了收件人的邮件提示，请执行下列操作：

1.  在 Outlook Web App 或 Outlook 2010 或更高版本中，撰写已添加收件人地址的电子邮件，但不要发送。

2.  验证信息栏中是否显示邮件提示。

3.  如果您配置了其他邮件提示转换，在语言设置与邮件提示转换的语言一致的 Outlook Web App 中撰写邮件，以验证结果。

