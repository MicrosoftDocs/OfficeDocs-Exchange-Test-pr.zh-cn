---
title: '在 Outlook 中查看反垃圾邮件标记: Exchange 2013 Help'
TOCTitle: 在 Outlook 中查看反垃圾邮件标记
ms:assetid: cddb5dbf-ad1e-471c-9fc8-28ddcf7ec1d0
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb124595(v=EXCHG.150)
ms:contentKeyID: 50491708
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 在 Outlook 中查看反垃圾邮件标记

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2012-10-03_

你可使用 Microsoft Outlook 来查看 Microsoft Exchange 应用至电子邮件的反垃圾邮件标记。当邮件通过对来自 Internet 的入站邮件进行筛选的反垃圾邮件代理时，反垃圾邮件标记通过对邮件应用诊断元数据或标记（如发件人特定的信息、问题验证结果和内容筛选结果），帮助你诊断与垃圾邮件相关的问题。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤的时间：15 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [邮件流权限](mail-flow-permissions-exchange-2013-help.md)主题中的\&quot;邮箱访问\&quot;条目。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 您想执行什么操作？

## 使用 Outlook 2010 或 Outlook 2013 查看反垃圾邮件标记

1.  在客户端计算机上的 Outlook 2010 或 Outlook 2013 中，在\&quot;邮件\&quot;视图中双击某个邮件将其打开。

2.  在功能区的\&quot;标记\&quot;部分中，单击\&quot;选项\&quot;图标可显示邮件的\&quot;属性\&quot;对话框。

3.  在\&quot;属性\&quot;对话框的\&quot;Internet 邮件头\&quot;部分中，使用滚动条查看如下面示例中所示的反垃圾邮件标记。
    
    ```powershell
        X-MS-Exchange-Organization-PCL:7
        X-MS-Exchange-Organization-SCL:6
        X-MS-Exchange-Organization-Antispam-Report: DV:3.1.3924.1409;SID:SenderIDStatus Fail;PCL:PhishingLevel SUSPICIOUS;CW:CustomList;PP:Presolved;TIME:TimeBasedFeatures
    ```    
## 使用 Outlook 2007 查看反垃圾邮件标记

1.  在客户端计算机上的 Outlook 2007 中，在\&quot;邮件\&quot;视图中双击某个邮件将其打开。

2.  在\&quot;邮件\&quot;选项卡上的\&quot;选项\&quot;组中，单击\&quot;邮件选项\&quot;。

3.  在\&quot;邮件选项\&quot;对话框的\&quot;Internet 邮件头\&quot;部分中，使用滚动条可查看如下面示例中所示的反垃圾邮件标记。
    
    ```powershell
        X-MS-Exchange-Organization-PCL:7
        X-MS-Exchange-Organization-SCL:6
        X-MS-Exchange-Organization-Antispam-Report: DV:3.1.3924.1409;SID:SenderIDStatus Fail;PCL:PhishingLevel SUSPICIOUS;CW:CustomList;PP:Presolved;TIME:TimeBasedFeatures
    ```    
