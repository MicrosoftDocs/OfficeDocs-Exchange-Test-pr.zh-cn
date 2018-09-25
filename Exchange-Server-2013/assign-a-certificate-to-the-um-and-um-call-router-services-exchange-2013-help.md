---
title: '将证书分配给该 UM 和 UM 呼叫路由器服务: Exchange 2013 Help'
TOCTitle: 将证书分配给该 UM 和 UM 呼叫路由器服务
ms:assetid: 8a900e5f-9779-4213-92d7-ec157b15fbc5
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dn205140(v=EXCHG.150)
ms:contentKeyID: 54652284
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 将证书分配给该 UM 和 UM 呼叫路由器服务

 

_**适用于：** Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2013-04-29_

您可以使用 EAC 或外壳指定自签名的内部公钥基础结构 (PKI) 或第三方特定的 Exchange 服务的商业证书。当您使用**New-ExchangeCertificate** cmdlet 将证书分配给 Exchange 服务使用*Services*参数时，系统会提示您将证书分配给 Exchange 服务。如果您使用 EAC 创建证书，新交换证书向导不会提示您将证书分配给 Exchange 服务。您需要编辑的证书并将证书分配通过选择您想要将其分配给哪些的服务。

不同的服务有不同的证书要求。例如，有些服务可能只需要服务器名称的证书**主题名称**或者**主题备用名称**框中，其他服务可能需要完全合格的域名称 (FQDN)。请确保该证书名称可以支持所需的启用对服务的使用。

> [!CAUTION]  
> 将统一消息 (UM) 与 Microsoft Lync Server 集成时，不能使用自签名证书。


有关与管理统一消息的证书相关的更多管理任务，请参阅[部署证书的 UM 过程](deploying-certificates-for-um-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：5 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [Exchange 和命令行管理程序基础结构权限](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md)主题中的\&quot;证书管理\&quot;条目和[统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 服务\&quot;条目。还必须使用该计算机上本地 Administrators 组的成员帐户进行登录。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 使用 EAC 向统一消息和 UM 呼叫路由器服务分配证书

1.  在 EAC 中，导航到\&quot;服务器\&quot;\>\&quot;证书\&quot;。

2.  在列表视图中，选择要向统一消息和 UM 呼叫路由器服务分配的证书，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在\&quot;*\<证书名称\>*\&quot;页上，选择\&quot;服务\&quot;，然后选择\&quot;UM\&quot;和\&quot;UM 呼叫路由器\&quot;。

4.  单击\&quot;保存\&quot;。

## 使用命令行管理程序向统一消息和 UM 呼叫路由器服务分配证书

此示例向统一消息和 UM 呼叫路由器服务分配证书。

  ```powershell
    Enable-ExchangeCertificate -Thumbprint 5113ae0233a72fccb75b1d0198628675333d010e -Services 'UM, UMCallRouter'
  ```
