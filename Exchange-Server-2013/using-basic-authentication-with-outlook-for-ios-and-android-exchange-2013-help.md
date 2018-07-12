---
title: 'Outlook for iOS and Android: Exchange 2013 Help'
TOCTitle: Outlook for iOS and Android
ms:assetid: 3a66817c-30da-4965-a6db-2955b5365b0f
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Mt465744(v=EXCHG.150)
ms:contentKeyID: 70061263
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Outlook for iOS and Android

 

_**适用于：** Exchange Server 2010, Exchange Server 2013_

_**上一次修改主题：** 2018-04-02_

**摘要：**  本文包含体系结构和有关 Outlook iOS 和 Android 在 Exchange 2013 管理员的安全信息部署环境。

IOS 和 Android 的 Outlook 应用程序旨在将组合在一起的电子邮件、 日历、 联系人和其他文件，使您的组织中做更多的用户从他们的移动设备。 本文提供了该应用程序的存储设计和体系结构的概述，以便 Exchange 管理员可以部署和维护 Exchange 组织中的 Outlook iOS 和 Android。

> [!NOTE]  
> <a href="https://support.office.com/zh-cn/article/outlook-for-ios-and-android-help-center-cd84214e-a5ac-4e95-9ea3-e07f78d0cd">Outlook for iOS 和 Android 帮助中心</a>向用户开放，其中包括在特定设备上使用应用的帮助和疑难解答信息。


## Outlook for iOS 和 Outlook for Android 体系结构

Outlook for iOS 和 Outlook for Android 包括安装在移动设备上的前端应用和后端的安全可扩展云服务，称为 *Outlook 服务*。处理 Outlook 服务中的信息将启用增强功能，以及可提升 Outlook 体验、改进性能和稳定性的功能。此体系结构依赖于 Outlook 服务进行密集处理，从而最大限度地减少用户设备所需的资源。

Outlook 服务所能为用户提供的服务示例包括：

  - 重点收件箱分类。

  - 一键单击从邮件列表取消订阅功能。

  - 提高了搜索速度和有效性。

  - 转发和发送大文件时，无需首先将其下载到移动设备。

## 数据缓存

以提高性能、 电子邮件、 日历和每个用户的邮箱中的文件数据的一个子集被缓存在 Outlook 信息服务。此服务当前运行在Microsoft Azure上。我们将移动到 Office 365 的 Outlook 信息服务，并计划让移动很快完成。

利用 Outlook 信息服务中的信息是当前高速缓存在美国或欧洲，这取决于连接的客户端的 IP 地址。我们移动到 Office 365 的 Outlook 信息服务，我们将使用区域性的数据中心战略靠 Office 365 信任中心的原则。Office 365 中的客户所在的国家或地区，服务在初始安装过程中输入客户的管理员，确定该客户的数据的主存储位置。有关详细信息，请参阅[Office 365 信任中心](https://go.microsoft.com/fwlink/p/?linkid=525776)。

## 数据缓存常见问题解答

以下是 Outlook for iOS和 Outlook for Android 中有关数据存储的常见问题解答。

## 在 Outlook 服务中缓存了多少用户邮箱数据？

大约一个月的电子邮件、日历和联系人数据。缓存过程由相应算法确定，该算法决定了邮箱的大小、邮箱内给定文件夹的相对重要性（如默认收件箱文件夹比之用户创建的文件夹），以及用户访问给定文件夹的频率等因素。

Outlook 服务存储附件数据如下：用户请求在 Outlook 中打开电子邮件附件时，该服务将从 Exchange 服务器检索附件，并临时进行存储。此时，附件被传递到用户移动设备上的应用。超过一个月的数据将定期从该服务删除，此时附件只能在 Exchange 服务器上使用。

## 如何从 Outlook 服务中删除我的信息？

从 Outlook 服务中删除信息的方式有三种。

  - 选项 1：为每个已使用适用于 iOS 和 Android 的 Outlook 应用连接到 Office 365 或 Exchange 的用户启动远程擦除。

  - 选项 2：使所有用户删除 Outlook 应用。所有数据将在大约 3-7 天内删除。

  - 选项 3：让每个用户从 Outlook 应用中删除其帐户，然后从其移动设备中删除该应用。若要删除帐户，请用户执行以下步骤：
    
    1.  在 Outlook 应用的\&quot;**设置**\&quot;中，点击\&quot;**帐户设置**\&quot;。
    
    2.  点击\&quot;**选择帐户**\&quot;，然后对所选的帐户点击\&quot;**删除帐户**\&quot;。
    
    3.  点击\&quot;**设备和远程数据**\&quot;。

## 在 Outlook 服务中进行存储时，临时缓存的邮箱数据如何受到保护？

您可以阅读有关如何在[Azure 信任中心](https://azure.microsoft.com/support/trust-center/)当前保护我们的数据。如先前所述，我们正转向从 Azure Office 365。在[Office 365 信任中心](https://go.microsoft.com/fwlink/p/?linkid=525776)介绍了这些服务的安全。

