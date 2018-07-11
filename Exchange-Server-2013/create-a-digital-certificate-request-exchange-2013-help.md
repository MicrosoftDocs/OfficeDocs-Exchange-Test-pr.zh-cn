---
title: '创建数字证书请求: Exchange 2013 Help'
TOCTitle: 创建数字证书请求
ms:assetid: efb00de7-070b-46bf-a2fc-00d07ae085c1
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb125165(v=EXCHG.150)
ms:contentKeyID: 52061563
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 创建数字证书请求

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2013-02-21_

在 Exchange Server 2013 中，您可以使用 EAC 或 Shell 来管理证书。EAC 包括新的证书管理用户界面。通过这个新的 UI，可以创建新的证书，编辑现有的证书或删除证书。

## 在开始之前，您需要知道什么？

  - 估计完成时间：证书颁发机构响应所需时间超过 10 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [客户端和移动设备权限](clients-and-mobile-devices-permissions-exchange-2013-help.md)主题中的\&quot;客户端访问服务器安全\&quot;条目。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 使用 EAC 创建新的证书请求

1.  在 EAC 中，导航到\&quot;服务器\&quot;\>\&quot;证书\&quot;。

2.  在\&quot;选择服务器\&quot;列表中，选择想要创建证书的服务器，然后单击\&quot;添加\&quot;![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。

3.  在\&quot;新建 Exchange 证书\&quot;向导中，选择\&quot;创建从证书颁发机构获取证书的请求\&quot;或\&quot;创建自签名证书\&quot;，然后选择\&quot;下一步\&quot;。

4.  为证书输入一个友好名称，并选择\&quot;下一步\&quot;。

5.  如果您不选择自签名证书而是想要一个通配符证书，选择标记为\&quot;申请通配符证书\&quot;的框，输入根域，例如 \*.contoso.com，然后选择\&quot;下一步\&quot;。如果选择自签名的证书，跳过这一步。

6.  选择您想要应用此证书的服务器，然后选择\&quot;下一步\&quot;。

7.  指定想要包含在证书中的域，然后选择\&quot;下一步\&quot;。

8.  验证包含的域正确无误。如果选择自签名的证书，选择\&quot;完成\&quot;。否则选择\&quot;下一步\&quot;。

9.  键入组织名称、部门名称、城市或地区、州或省以及国家或地区，然后选择\&quot;下一步\&quot;。

10. 输入保存证书请求的位置并选择\&quot;完成\&quot;。

如果不选择自签名证书，将需要发送证书请求文件至证书颁发机构以供其处理。

## 使用命令行管理程序创建新的证书请求

运行下列命令。
  ```
    $reqfile = New-ExchangeCertificate -GenerateRequest -SubjectName "C=US,o=Contoso,cn=contosotocert" -DomainName "contoso.com" -PrivateKeyExportable $true
  ```
  ```
    $reqfile | out-file c:\certreq.txt
  ```
  
## 您如何知道操作成功？

如果创建自签名证书，新创建的证书将会出现在证书管理 UI 中。如果从证书颁发机构创建一个证书请求，则证书请求文件将会在您指定的位置中。将该文件发送至证书颁发机构。

