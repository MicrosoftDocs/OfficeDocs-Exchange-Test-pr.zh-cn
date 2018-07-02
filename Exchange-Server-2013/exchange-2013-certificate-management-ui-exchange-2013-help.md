---
title: 'Exchange 2013 证书管理 UI: Exchange 2013 Help'
TOCTitle: Exchange 2013 证书管理 UI
ms:assetid: 8975848d-07f0-4643-9eac-20aece69945f
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ984582(v=EXCHG.150)
ms:contentKeyID: 52061525
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 2013 证书管理 UI

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2014-04-21_

在 Exchange Server 部署中管理证书是最重要的管理任务之一。确保正确设置和配置证书是为企业提供安全邮件基础结构的关键所在。在 Exchange 2010 中，Exchange 管理控制台 (EMC) 是管理证书的主要方法。在 Exchange 2013 中，Exchange 管理控制台 (EAC)（新的 Exchange 2013 管理用户界面）中提供证书管理功能。在 Exchange 2013 中，重点在于最大程度地减少管理员必须管理的证书数、最大程度地减少管理员必须与证书进行的交互，以及允许从中央位置管理证书。

## 客户端访问服务器证书

Exchange 2013 中的客户端访问服务器是无状态的精简服务器，旨在接受传入客户端连接，并将其代理到正确的邮箱服务器。客户端访问服务器中的 Exchange 证书管理 UI 可帮助您完成各种任务，包括申请新证书和续订已到期或即将到期的证书。

## 了解证书管理 UI

您可以通过在 EAC 中依次选择\&quot;服务器\&quot;和\&quot;证书\&quot;来访问 Exchange 证书管理 UI。通过使用管理 UI，您可以执行以下操作：

  - **创建新证书**   选择\&quot;添加\&quot;![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标") 将启动\&quot;新建 Exchange 证书\&quot;向导。

  - **编辑现有证书**   选择有效证书上的\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标") 将允许您查看证书的属性页。

  - **删除证书**   选中某个证书后选择\&quot;删除\&quot;![删除图标](images/JJ657511.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "删除图标") 将启动删除确认对话框。

  - **执行其他操作**   选择\&quot;更多选项\&quot;![更多选项图标](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "更多选项图标") 将允许您导出或导入证书。如果您要导出证书，该证书必须有效。

## 证书过期

在早期版本的 Microsoft Exchange 中，数字证书即将到期的情况很少见。在 Exchange 2013 中，通知中心会在任何 Exchange 2013 客户端访问服务器上存储的证书即将过期时显示警告。

## 邮箱服务器证书

Exchange 2010 和 Exchange 2013 之间的一个主要区别是，Exchange 2013 邮箱服务器上使用的证书是自签名证书。由于所有客户端都通过 Exchange 2013 客户端访问服务器连接到 Exchange 2013 邮箱服务器，因此您只需要管理客户端访问服务器中的证书。客户端访问服务器会自动信任邮箱服务器上的自签名证书，因此客户端不会接收有关不信任的自签名证书的警告，前提是客户端访问服务器具有来自 Windows 证书颁发机构 (CA) 或受信任第三方的非自签名证书。没有可用于管理邮箱服务器上的自签名证书的工具或 cmdlet。正确安装服务器后，您无需再担心邮箱服务器上的证书。

## 自签名证书过期

默认情况下，安装在 Exchange 2013 邮箱服务器上的自签名证书将在自安装之日起五年后过期。

## 证书 cmdlet

您可以使用以下 cmdlet 来管理 Exchange 客户端访问服务器上的数字证书：

  - Import-ExchangeCertificate   此 cmdlet 用于将证书导入到服务器。您可以导入 CA 签名证书（用于完成待处理证书签名请求 (CSR)）或具有私钥的证书（PKCS \#12 文件，通常具有 .pfx 扩展名，之前与私钥一起从服务器导出）。

  - Remove-ExchangeCertificate   此 cmdlet 用于将证书从服务器删除。

  - Enable-ExchangeCertificate   此 cmdlet 用于向证书分配服务。

  - Get-ExchangeCertificate   此 cmdlet 用于根据各种条件检索 Exchange 证书。

  - New-ExchangeCertificate   此 cmdlet 用于创建新的自签名证书或 CSR。

