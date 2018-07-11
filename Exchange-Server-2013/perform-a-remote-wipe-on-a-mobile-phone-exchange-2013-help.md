---
title: '对移动电话执行远程擦除: Exchange 2013 Help'
TOCTitle: 对移动电话执行远程擦除
ms:assetid: 67ba838e-031d-4a98-b277-170683b6f520
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa998614(v=EXCHG.150)
ms:contentKeyID: 52061369
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 对移动电话执行远程擦除

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2013-02-06_

您的用户每天都随身携带着敏感的公司信息。如果他们中有人丢失了自己的手机，公司数据就可能会落入其他人手中。如果您的用户中有人丢失了自己的手机，您可以使用 Exchange 管理中心 (EAC) 或 Exchange 命令行管理程序擦除手机中所有的公司及用户信息。

> [!NOTE]  
> 本主题还提供有关如何使用 MicrosoftOutlook Web App 对电话执行远程擦除的说明。用户必须登录 Outlook Web App 才能执行远程擦除。


## 在开始之前，您需要知道什么？

  - 估计完成时间：5 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[客户端和移动设备权限](clients-and-mobile-devices-permissions-exchange-2013-help.md)主题中的“移动设备”条目。

  - 此过程可以清除手机上的所有数据，包括安装的应用程序、照片以及个人信息。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 使用 EAC 擦除用户电话

您可以使用 EAC 擦除用户电话中的数据或取消尚未完成的远程擦除操作。

1.  在 EAC 中，导航到“收件人”\>“邮箱”。

2.  选择用户，在“移动设备”下，选择“查看详细信息”。

3.  在“移动设备详细信息”页面上，选择丢失的移动设备，然后选择“擦除数据”。

4.  选择“保存”。

## 使用命令行管理程序擦除用户电话

您可以使用命令行管理程序中的 **Clear-MobileDevice** cmdlet 对用户电话执行擦除。

下列命令可以擦除名为 WM\_TonySmith 的设备，然后向 admin@contoso.com 发送确认邮件。

    Clear-MobileDevice -Identity WM_TonySmith -NotificationEmailAddresses "admin@contoso.com"

## 使用 Outlook Web App 擦除用户电话

您的用户可以使用 Outlook Web App 擦除自己的电话。

1.  在 Outlook Web App 中，选择“设置”\>“电话”\>“移动设备”。

2.  选择手机。

3.  单击或点击“擦除设备”图标。

## 您如何知道操作成功？

有几个方法可以验证远程擦除操作是否已完成。

  - 运行 **Clear-MobileDevice** cmdlet 并配置 *–NotificationEmailAddresses* 参数。当远程擦除完成之后，系统会向所提供的电子邮件地址发送一封邮件。

  - 在 EAC 中，检查移动设备的状态。该状态会从“擦除挂起”变为“擦除成功”。

  - 在 Outlook Web App 中，检查移动设备的状态。该状态会从“擦除挂起”变为“擦除成功”。

