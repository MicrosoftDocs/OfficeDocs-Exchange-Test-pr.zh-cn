---
title: '为邮箱配置电子邮件转发: Exchange 2013 Help'
TOCTitle: 为邮箱配置电子邮件转发
ms:assetid: c7a7afaf-577e-49d6-8cee-bb4c4a5d570b
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd351134(v=EXCHG.150)
ms:contentKeyID: 50556656
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 为邮箱配置电子邮件转发

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2016-12-09_

利用电子邮件转发可以将邮箱设置为将发送给该邮箱的电子邮件转发给你的组织内部或外部的其他用户邮箱。

> [!important]
> 如果你使用的是 Office 365 企业版，则应按照以下文章中的说明配置电子邮件转发：<a href="https://go.microsoft.com/fwlink/p/?linkid=834774">Office 365 管理中心：在 Office 365 中配置电子邮件转发</a>


如果组织使用的是本地 Exchange 或混合 Exchange 环境，则你应使用本地 Exchange 管理中心 (EAC) 创建和管理共享邮箱。

## 使用 Exchange 管理中心 配置邮件转发

您可以使用 Exchange 管理中心 (EAC)，将电子邮件设置为转发给一个内部收件人、一个外部收件人（使用邮件联系人）或多个收件人（使用通讯组）。

您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[收件人权限](recipients-permissions-exchange-2013-help.md)主题中的“收件人设置权限”条目。

1.  在 EAC 中，导航到“收件人”\>“邮箱”。

2.  在用户邮箱列表中，单击或点击要为其配置邮件转发的邮箱，然后单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在邮箱属性页上，单击“邮箱功能”。

4.  在“邮件流”下，选择“查看详细信息”以查看或更改用于转发电子邮件的设置。
    
    在此页面上，可以设置用户向其发送邮件的收件人最大数量。对于内部部署 Exchange 组织，收件人数目不受限制。对于 Exchange 在线组织，限制是 500 个收件人。

5.  选中“启用转发”复选框，然后单击或点击“浏览”。

6.  在“选择收件人”页面，选择您要向其转发所有电子邮件的用户。如果您想让收件人和转发的电子邮件地址都收到发送出去的电子邮件的副本，请选中“将邮件同时传递到转发地址和邮箱”复选框。单击或点击“确定”，然后单击或点击“保存”。

如果您要将邮件转发到组织外部的地址，该怎么办？或者，将邮件转发给多个收件人，该怎么办？您仍然可以执行此操作！

  - **外部地址**创建邮件联系人，然后，在上述步骤中，在“选择收件人”页上选择邮件联系人。需要了解如何创建邮件联系人？请查看[管理邮件联系人](manage-mail-contacts-exchange-2013-help.md)。

  - **多个收件人**创建通讯组，向其添加收件人，然后在上述步骤中，在“选择收件人”页上选择邮件联系人。需要了解如何创建邮件联系人？请查看[创建和管理通讯组](create-and-manage-distribution-groups-exchange-2013-help.md)。

## 您如何知道这有效？

若要验证是否成功配置了邮件转发，请执行以下操作之一：

1.  在 EAC 中，转到“收件人”\>“邮箱”。

2.  在用户邮箱列表中，单击或点击已为其配置电子邮件转发的邮箱，然后单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在邮箱属性页面上，单击或点击“邮箱功能”。

4.  在“邮件流”下，单击或点击“查看详细信息”以查看邮件转发设置。

## 其他信息

本主题适用于管理员。如果你要将自己的电子邮件转发给其他收件人，请查看以下主题：

  - [将电子邮件转发到其他电子邮件帐户](https://go.microsoft.com/fwlink/p/?linkid=510866)

  - [使用规则管理电子邮件](https://go.microsoft.com/fwlink/p/?linkid=510869)

若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

