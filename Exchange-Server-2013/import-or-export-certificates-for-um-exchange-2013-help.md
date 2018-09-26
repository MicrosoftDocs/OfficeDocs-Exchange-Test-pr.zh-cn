---
title: '导入或导出证书为 UM: Exchange 2013 Help'
TOCTitle: 导入或导出证书为 UM
ms:assetid: ee688c33-2e08-47e7-95fc-04ba10238341
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dn205143(v=EXCHG.150)
ms:contentKeyID: 54652305
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 导入或导出证书为 UM

 

_**适用于：** Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2013-12-18_

您可以使用 EAC 或命令行管理程序来导入或导出自签名的内部公钥基础结构 (PKI) 或第三方商业证书。对于统一消息 (UM)，可以使用这些 Microsoft Exchange 统一消息服务和 Microsoft Exchange 统一消息呼叫路由器服务的证书之一。您可以对两种服务使用同样的证书，或对每个服务使用不同的证书。

在您需要进行以下操作时导入 Exchange 的证书可能很有用：

  - 导入一个导出到文件中的证书。

  - 导入一个由内部证书颁发机构生成的 PKI 证书文件。

  - 导入一个第三方商业证书。

在您需要进行以下操作时导出当地 Exchange 服务器上证书存储中现有的证书可能很有用：

  - 导出它使其能够导入到另一个 Exchange 服务器。

  - 导出它使其可以导入到 VoIP 网关、IP PBX 或启用 SIP 的 PBX。

  - 导出证书以便可以备份证书及其密钥。

有关管理与统一消息证书相关的其他管理任务，请参阅[部署证书的 UM 过程](deploying-certificates-for-um-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：5 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [Exchange 和命令行管理程序基础结构权限](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md)主题中的\&quot;证书管理\&quot;条目和[统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 服务\&quot;条目。还必须使用该计算机上本地 Administrators 组的成员帐户进行登录。

  - 导出一个证书之前，使用 **Get-ExchangeCertificate** cmdlet 验证证书上的 *PrivateKeyExportable* 属性设置为 `$true`。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 使用 EAC 导出证书

1.  在 EAC 中，单击\&quot;服务器\&quot;\>\&quot;证书\&quot;\>\&quot;更多选项\&quot;![更多选项图标](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "更多选项图标")，再单击\&quot;导出 Exchange 证书\&quot;。

2.  在\&quot;导出 Exchange 证书\&quot;页面上，在\&quot;要导出到的文件\&quot;框中，输入证书文件的名称。

3.  在\&quot;密码\&quot;框中，输入您想用来保护密钥的密码，再单击\&quot;确定\&quot;。

## 使用命令行管理程序导出证书

该示例在提示您输入用户名和密码后，将 Thumbprint A36DE2B9B62980A717EBD0C3052F5F0B08FBFFCC 的证书导出到一个文件中。

```powershell
    $file = Export-ExchangeCertificate -Thumbprint A36DE2B9B62980A717EBD0C3052F5F0B08FBFFCC -BinaryEncoded:$true -Password (Get-Credential).password
```

本示例执行以下操作：

1.  使用 **Get-ExchangeCertificate** cmdlet 来查找想要导出的证书。

2.  使用 **Export-ExchangeCertificate** cmdlet 来设置证书密码。

3.  输入用户名和密码后将证书输出至一个文件中。

<!-- end list -->
```powershell
$file = Get-ExchangeCertificate -DomainName umcorp.northwindtraders.com | Export-ExchangeCertificate -BinaryEncoded:$true -Password (Get-Credential).password
```

```powershell
Set-Content -Path "d:\umcerts\selfsigned.pfx" -Value $file.FileData =Encoding Byte
```
  
  
## 使用 EAC 导入证书

1.  在 EAC 中，单击\&quot;服务器\&quot;\>\&quot;证书\&quot;\>\&quot;更多选项\&quot;![更多选项图标](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "更多选项图标")，再单击\&quot;导入 Exchange 证书\&quot;。

2.  在\&quot;导入 Exchange 证书\&quot;页面上，在\&quot;要从中导入文件的位置\&quot;框中，输入文件共享路径和证书文件名称。如果证书有密码保护，在\&quot;密码\&quot;框中输入密码，然后单击\&quot;下一步\&quot;。

3.  单击\&quot;添加\&quot;![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")，选择想要应用证书的服务器，然后单击\&quot;确定\&quot;。如果想要将服务器从列表视图中删除，单击\&quot;删除\&quot;![删除图标](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "删除图标")，然后单击\&quot;完成\&quot;。

## 使用命令行管理程序导入证书

本示例在您输入用户名和密码后将证书从 d:\\certificates\\exchange\\SelfSignedUMCert.pfx 证书文件导入。

```powershell
    Import-ExchangeCertificate -FileData ([Byte[]]$(Get-Content -Path d:\certificates\exchange\SelfSignedUMCert.pfx -Encoding Byte -ReadCount 0)) -Password:(Get-Credential).password
```
