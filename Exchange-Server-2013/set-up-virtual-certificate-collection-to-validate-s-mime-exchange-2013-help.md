---
title: '设置虚拟证书集合以验证 S/MIME: Exchange 2013 Help'
TOCTitle: 设置虚拟证书集合以验证 S/MIME
ms:assetid: 04a616e6-197c-490c-ae8c-c8d5f0f0b3dd
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dn626155(v=EXCHG.150)
ms:contentKeyID: 61212703
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 设置虚拟证书集合以验证 S/MIME

 

_**适用于：**Exchange Online, Exchange Server 2013_

_**上一次修改主题：**2016-12-09_

作为租户管理员，您将需要配置用于验证 S/MIME 证书的虚拟证书集合。虚拟证书集合设置为具有 SST 文件名扩展名的证书存储文件类型。SST 文件包含验证 S/MIME 证书时使用的所有根证书和中间证书。

## 创建并保存 SST

只能使用命令行管理程序执行此过程。若要了解如何在本地 Exchange 组织中打开 Exchange 命令行管理程序，请参阅[打开命令行管理程序](https://technet.microsoft.com/zh-cn/library/dd638134\(v=exchg.150\))。若要了解如何使用 Windows PowerShell 连接到 Exchange Online，请参阅[连接到 Exchange Online PowerShell](https://go.microsoft.com/fwlink/p/?linkid=396554)。

作为管理员，您可以创建此 SST 文件，方法是使用 `Export-Certificate` cmdlet 从受信任的计算机导出证书并将类型指定为 SST。有关 `Export-Certificate` cmdlet 的详细信息，请参阅 [Export-Certificate](https://technet.microsoft.com/zh-cn/library/hh848628.aspx) 参考主题。

生成 SST 文件后，使用 `Set-Smimeconfig` cmdlet 将其保存在虚拟证书存储中，方法是使用 *-SMIMECertificateIssuingCA* 参数。例如：`Set-SmimeConfig -SMIMECertificateIssuingCA (Get-Content filename.sst -Encoding Byte)`

## 确保证书有效

Exchange 2013 SP1 首先检查 SST 文件并验证证书。如果验证失败，它将检查本地计算机证书存储以验证证书。此行为是 Exchange 2013 SP1 的新增功能，与 Exchange 的以前版本不同。在 Exchange Online 中，仅使用 SST 进行验证。

## 详细信息

[邮件签名和加密的 S/MIME](s-mime-for-message-signing-and-encryption-exchange-2013-help.md)

[Get-SmimeConfig](https://technet.microsoft.com/zh-cn/library/dn554257\(v=exchg.150\))

