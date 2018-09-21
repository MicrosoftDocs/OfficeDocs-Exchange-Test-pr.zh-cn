---
title: '对 RollAlternateServiceAccountCredential.ps1 脚本进行故障排除: Exchange 2013 Help'
TOCTitle: 对 RollAlternateServiceAccountCredential.ps1 脚本进行故障排除
ms:assetid: 2bbf36d3-eb89-4f92-a8de-259a7cb64d62
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Ff808310(v=EXCHG.150)
ms:contentKeyID: 63918694
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 对 RollAlternateServiceAccountCredential.ps1 脚本进行故障排除

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-01-14_

本主题提供有关在使用 RollAlternateServiceAccountPassword.ps1 脚本时可能发生的常见错误的解决方案和信息。

## 无法使用密码更新一个或多个客户端访问服务器

## 问题

如果在脚本中使用参数 *ToEntireForest* 或 *ToArrayMembers*，则在某些情况下可能无法更新一个或多个客户端访问服务器。

## 解决方法

使用 **Get-ClientAccessArray** cmdlet 验证将作为脚本目标的服务器是否全部为必需的服务器，如下面的示例所示。

```powershell
Get-ClientAccessArray | fl members
```

如果无法更新的服务器是客户端访问阵列的成员，而且仍无法正确更新，请重新运行 Exchange 安装程序并再次将客户端访问服务器角色添加到服务器。还可以使用参数 *ToSpecificServers* 将各个服务器指定为目标。

## 某些服务器不响应脚本

## 问题

在某些情况下，服务器可能由于暂时性错误（如错误的网络连接）而无法更新。

## 解决方法

验证有问题的服务器是否具有网络和 Active Directory 连接，然后再次尝试运行脚本。

## 某些阵列成员长时间停止运行

## 问题

如果某个服务器在较长时间内停止运行，但是 **Get-ClientAccessArray** cmdlet 仍确定该服务器为阵列成员，则在使用参数 *ToArrayMembers* 和 *ToEntireForest* 时可能损坏了脚本功能。如果某个服务器具有永久性故障，但尚未从部署中完全删除，则会出现相同问题。

## 解决方法

若要解决此问题，请使用 Exchange 安装程序从部署中删除服务器，或在有人值守模式下运行脚本，直至可以删除服务器。

如果服务器只是短时间停机，您不希望永久删除 Exchange，则可以使用参数 *ToSpecificServers* 调整脚本以针对特定服务器运行，从而只将活动服务器作为目标。或者，可以使用 **Remove-ClientAccessArray** cmdlet 从不响应的服务器的 Active Directory 对象中删除 RPC 客户端访问服务，如下面的示例所示。

```powershell
Remove-RPCClientAccess -Server Server.Contoso.com
```

在删除了 RPC 客户端访问服务之后，[Get-ClientAccessArray](https://technet.microsoft.com/zh-cn/library/dd297976\(v=exchg.150\)) 不会将该服务器作为阵列成员返回，并且脚本不会将其作为目标。在该服务器再次正常运行之后，可以使用 **New-RpcClientAccess** cmdlet 重新添加 RPC 客户端访问服务。在重新添加 RPC 客户端访问服务时，请务必在受影响的服务器上重新启动 Microsoft Exchange 通讯簿服务。

> [!CAUTION]  
> 在从服务器中删除 RPC 客户端访问服务之前，请参阅 <a href="https://technet.microsoft.com/zh-cn/library/dd298151(v=exchg.150)">Remove-RPCClientAccess</a> 主题。


## 详细信息

有关如何将 Kerberos 身份验证与客户端访问服务器阵列或负载平衡解决方案一起使用的详细信息，请参阅以下主题：

  - [为负载平衡的客户端访问服务器配置 Kerberos 身份验证](configuring-kerberos-authentication-for-load-balanced-client-access-servers-exchange-2013-help.md)

  - [在命令行管理程序中使用 RollAlternateserviceAccountCredential.ps1 脚本](using-the-rollalternateserviceaccountcredential-ps1-script-in-the-shell-exchange-2013-help.md)

