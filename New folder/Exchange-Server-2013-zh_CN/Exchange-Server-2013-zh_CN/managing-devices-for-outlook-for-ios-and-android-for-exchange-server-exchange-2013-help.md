---
title: '管理适用于 Exchange Server 的 Outlook for iOS 和 Outlook for Android 设备: Exchange 2013 Help'
TOCTitle: 管理适用于 Exchange Server 的 Outlook for iOS 和 Outlook for Android 设备
ms:assetid: 16ce7d24-be74-4466-b126-828a67f69b6e
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Mt465748(v=EXCHG.150)
ms:contentKeyID: 70086926
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 管理适用于 Exchange Server 的 Outlook for iOS 和 Outlook for Android 设备

 

_**适用于：** Exchange Server 2010, Exchange Server 2013_

_**上一次修改主题：** 2018-04-01_

**摘要：** 本文介绍 Exchange Active Sync 如何帮助你在 Exchange 本地组织中使用 Outlook for iOS 和 Outlook for Android 管理移动设备。

Microsoft 建议使用 Exchange ActiveSync 管理用于访问本地环境中的 Exchange 邮箱的移动设备。Exchange ActiveSync 是一种 Microsoft Exchange 同步协议，它允许移动电话访问运行 Microsoft Exchange 的服务器上的组织信息。

本文重点介绍运行 Outlook for Android 和 Outlook for iOS 的移动设备的特定 Exchange ActiveSync 功能和方案。[Exchange ActiveSync](exchange-activesync-exchange-2013-help.md) 中提供了有关 Microsoft Exchange 同步协议的完整信息。此外，[Office 博客](https://go.microsoft.com/fwlink/p/?linkid=62392)上的信息详细介绍了密码强制执行和使用 Exchange ActiveSync 与运行 Outlook for iOS 和 Outlook for Android 的设备的其他好处。

## PIN 锁定和设备加密

如果组织的 Exchange ActiveSync 策略要求提供移动设备的密码，以便用户同步电子邮件，则 Outlook 将在设备级别强制实施此策略。根据 Apple 和 Google 提供的可用控件，该操作在 iOS 设备和 Android 设备之间的工作方式不同。

在 iOS 设备上，Outlook 会检查以确保正确设置密码或 PIN。如果未设置密码，Outlook 会提示用户在 iOS 设置中创建密码。在设置密码之前，用户将无法访问 Outlook for iOS。

Outlook for iOS 只能在 iOS 8.0 或更高版本上运行。这些设备随附内置加密，一旦启用密码，Outlook 将使用该加密来加密 Outlook 在 iOS 设备上本地存储的所有数据。因此，具有 PIN 的 iOS 设备将被加密，无论 ActiveSync 策略是否需要此操作。

在 Android 设备上，Outlook 将强制执行屏幕锁定规则。此外，Google 还提供了一些控件，可允许 Outlook for Android 遵守有关密码长度和复杂性的 Exchange 策略，并控制在擦除手机前允许的屏幕解锁尝试次数。Outlook for Android 也会鼓励存储加密（如果未启用），通过逐步演练指导用户完成此过程。

不支持这些密码安全设置的 iOS 和 Android 设备将无法连接到 Exchange 邮箱。

## 通过 Exchange ActiveSync 进行远程擦除

Exchange ActiveSync 使管理员能够远程擦除设备（如设备受到侵害的情况）。使用 Outlook for iOS 和 Outlook for Android，远程擦除可针对 Outlook 应用自身进行，而不是进行完整的设备擦除。

在管理员请求远程擦除命令后，擦除在Outlook 应用下次连接到 Exchange 的几秒钟内发生。Outlook 应用将重置，并且所有 Outlook 电子邮件、日历、联系人和文件数据将从设备以及 Outlook 服务中删除。擦除不会影响 Outlook 之外的任何用户的个人应用和信息。

由于 Outlook for iOS 和 Outlook for Android 在 Exchange 中的用户移动设备下显示为单个移动设备关联，因此远程擦除命令将从运行与该用户关联的Outlook（iPhone、iPad、Android）的所有设备中删除数据并删除同步关系。

> [!NOTE]
> 由于 Outlook for iOS 和 Outlook for Android 依托的云架构，远程设备擦除的结果不会报告给 Exchange。即使擦除成功，状态仍将显示为&amp;quot;<strong>正在挂起</strong>&amp;quot;。这是一个已知的问题，解决方案正在开发中。


## 设备标识符和访问控制

由于 Outlook for iOS 和 Outlook for Android 的基于云的体系结构，Exchange 中每个用户的 Outlook 连接显示为单个移动设备标识符 (ID)。这意味着每个用户的移动设备访问控制应用于与此设备 ID 相关联的所有设备。此实现创建两个不同于传统 Exchange ActiveSync 设备访问控制工作原理的条件。

  - **阻止：** 阻止规则会在所有设备和支持的操作系统上阻止 Outlook。用户无法阻止单个设备或操作系统。

  - **隔离：** 隔离过程基于每个用户进行，而不是基于每个设备。一旦用户将设备从隔离中释放，就可以在任意数量的其他设备上按需安装和配置 Outlook。由于该用户已从隔离中释放，与该用户关联的所有新设备都不会被隔离。

移动设备邮箱策略就位时，将适用于所有关联的设备。因此，如果为特定邮箱强制执行 PIN 锁定，则连接到该邮箱的所有设备都需要 PIN。

> [!NOTE]
> 由于设备 ID 不受任何<em>物理设备</em> ID 约束，设备 ID 可自行更改。出现这种情况时，如果将设备 ID 用于管理用户设备，则会造成意想不到的后果，因为 Exchange 可能会意外地阻止或隔离现有的&amp;quot;允许&amp;quot;设备。因此，我们建议管理员仅基于设备类型或设备模型来设置允许/阻止设备的移动设备策略。


## 使用 Exchange ActiveSync 常见问题解答进行设备管理

以下是有关运行 Outlook for iOS 和 Outlook for Android 的设备的密码、PIN 和加密策略的常见问题解答。

## iOS 上的本机邮件应用程序强制实施有关密码长度和复杂性要求的 Exchange ActiveSync 策略。为什么不选择 Outlook？

Outlook 利用可用于 Microsoft 的第三方应用程序开发人员控件。我们将继续改进此功能，因为 Apple 可以向开发人员提供更多的控件。

## 为什么 Outlook for iOS 和 Outlook for Android 在设备级别而不是应用级别强制执行 PIN？

在评估了 iOS 和 Android 中的可用功能后，Microsoft 认为，在方便性和安全性方面，设备级 PIN 能够为客户提供最佳体验。应用级 PIN 意味着用户必须输入两个不同的 PIN 才能访问电子邮件，这种做法不可取。此外，设备级 PIN 意味着我们可以利用本机设备加密、iOS 上的 TouchID 和 Android上的 Smart Lock 等功能。远程擦除仍然在应用级别实现施，这意味着擦除 Outlook 时，用户的个人应用和数据不会受到影响。

## Outlook 为 Android 支持设备加密吗？

是的 Android 的 Outlook 支持 Exchange 邮箱策略的移动设备通过设备加密。但是，在 Android 7.0 之前, 的可用性和实现这一过程因 Android OS 版本和设备制造商，它允许用户在加密过程中取消。与 Google Android 7.0 引入的更改，Outlook 设置为 Android 现在是能够强制执行加密设备运行 Android 7.0 或更高版本。使用设备运行这些操作系统的用户将不能取消此加密流程。

即使 Android 设备未加密，而且攻击是拥有的设备，前提是已启用的设备的 PIN，将无法访问 Outlook 数据库。这种情况即使有启用 USB 调试和安装 Android SDK。如果攻击试图绕过 PIN 来访问这些信息的设备的根，根进程擦除设备中的所有存储，并删除所有 Outlook 数据。如果该设备未加密且为根用户之前被盗，很可能为攻击者获得访问 Outlook 数据库启用 USB 设备上调试通过，将该设备插入计算机与 Android SDK 安装。

