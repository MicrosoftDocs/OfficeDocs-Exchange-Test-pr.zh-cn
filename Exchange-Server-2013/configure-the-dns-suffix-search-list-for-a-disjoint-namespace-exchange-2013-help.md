---
title: '为非连续命名空间配置 DNS 后缀搜索列表: Exchange 2013 Help'
TOCTitle: 为非连续命名空间配置 DNS 后缀搜索列表
ms:assetid: cfa715ac-7b69-47c3-b206-933ec2cf677b
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb847901(v=EXCHG.150)
ms:contentKeyID: 50491585
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 为非连续命名空间配置 DNS 后缀搜索列表

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2016-12-09_

本主题说明如何使用组策略管理控制台 (GPMC) 配置域名系统 (DNS) 后缀搜索列表。在一些 Microsoft Exchange 2013 方案中，如果具有脱节命名空间，则必须配置 DNS 后缀搜索列表以包括多个 DNS 后缀。

## 在开始之前，您需要知道什么？

  - 估计完成时间：10 分钟

  - 若要执行以下步骤，必须为您使用的帐户委派 Domain Admins 组成员身份。

  - 确认您在将要安装 GPMC 的计算机上已经安装了 .NET Framework 3.0。
    
    > [!NOTE]  
    > 可以从 Microsoft 下载中心下载的最新版本的 GPMC 适用于 32 位版本的 Windows Server 2003 和 Windows XP 操作系统，可以在 32 位和 64 位域控制器上远程管理组策略对象。此版本的 GPMC 不包括 64 位版本，且 32 位版本不能在 64 位平台上运行。32 位版本的 Windows Server 2008 和 32 位版本的 Windows Vista 均包括 32 位版本的 GPMC。64 位版本的 Windows Server 2008 和 64 位版本的 Windows Vista 均包括 64 位版本的 GPMC。


  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 使用 GPMC 配置 DNS 后缀搜索列表

1.  在域中的 32 位计算机上，安装带有 Service Pack 1 (SP1) 的 GPMC。有关下载信息，请参阅[带有 Service Pack 1 的组策略管理控制台](https://go.microsoft.com/fwlink/p/?linkid=100126)。
    
    > [!NOTE]  
    > 如果域中包含运行 Windows Server 2008 或 Windows Vista 的计算机，则可以跳过此步骤。


2.  单击“开始”\>“程序”\>“管理工具”\>“组策略管理”。

3.  在“组策略管理”中，展开将在其中应用组策略的林和域。右键单击“组策略对象”，然后单击“新建”。

4.  在“新建 GPO”中，键入策略的名称，然后单击“确定”。

5.  右键单击在步骤 4 中创建的新策略，然后单击“编辑”。

6.  在“组策略管理编辑器”中，依次展开“计算机配置”、“策略”、“管理模板”、“网络”，然后单击“DNS 客户端”。

7.  右键单击“DNS 后缀搜索列表”，单击“所有任务”，然后单击“编辑”。

8.  在“DNS 后缀搜索列表属性”页上，选择“启用”。在“DNS 后缀”框中，键入脱节计算机的主 DNS 后缀、DNS 域名，以及 Exchange 可能与之交互操作的其他服务器（如监视服务器或第三方应用程序的服务器）的任何其他命名空间。单击“确定”。

9.  在“组策略管理”中，展开“组策略对象”，然后选择在步骤 4 中创建的策略。在“作用域”选项卡上，设置策略的作用域以便其仅应用于脱节的计算机。

## 您如何知道这有效？

要验证您是否已成功完成迁移，请执行下列操作：

  - 在安装 Exchange 2013 之后，检查是否可在组织内外发送电子邮件。

## 详细信息

[Windows Server Group Policy](https://go.microsoft.com/fwlink/p/?linkid=100128)（Windows Server 组策略）

[Group Policy](https://go.microsoft.com/fwlink/?linkid=268043)（组策略）

[非连续命名空间应用场景](disjoint-namespace-scenarios-exchange-2013-help.md)

