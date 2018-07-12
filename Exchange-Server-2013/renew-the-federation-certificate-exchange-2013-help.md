---
title: '续订联合身份验证证书: Exchange 2013 Help'
TOCTitle: 续订联合身份验证证书
ms:assetid: 0f390713-3058-44d0-9c07-3c982616e790
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Mt779252(v=EXCHG.150)
ms:contentKeyID: 74429169
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 续订联合身份验证证书

 

_**上一次修改主题：** 2017-02-28_

本主题介绍如何更新在联合身份验证信任中使用的自签名联合身份验证证书：

  - 如果联合身份验证证书尚未过期，请按照更新工作联合身份验证证书部分中的步骤执行操作。

  - 如果联合身份验证证书已经过期，请按照替换过期的联合身份验证证书部分中的步骤执行操作。

有关联合身份验证信任和联合身份验证的详细信息，请参阅[联盟](federation-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：10 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[Exchange 和命令行管理程序基础结构权限](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md)主题中的“联合身份验证和证书”条目。

  - 本主题中的过程使用 Exchange 命令行管理程序。若要了解如何在本地 Exchange 组织中打开 Exchange 命令行管理程序，请参阅[打开命令行管理程序](https://technet.microsoft.com/zh-cn/library/dd638134\(v=exchg.150\))。

  - 若要查看现有联合身份验证证书是否已过期，请在 Exchange 命令行管理程序中运行以下命令：
    
        Get-ExchangeCertificate -Thumbprint (Get-FederationTrust).OrgCertificate.Thumbprint | Format-Table -Auto Thumbprint,NotAfter

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!WARNING]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 更新工作联合身份验证证书

如果联合身份验证证书尚未过期，可以使用新的联合身份验证证书更新现有的联合身份验证信任。

## 步骤 1：创建新的联合身份验证证书

在 Exchange 命令行管理程序中运行以下命令来创建一个新的联合身份验证证书：

    $SKI = [System.Guid]::NewGuid().ToString("N"); New-ExchangeCertificate -DomainName 'Federation' -FriendlyName "Exchange Delegation Federation" -Services Federation -SubjectKeyIdentifier $SKI -PrivateKeyExportable $true

有关语法和参数的详细信息，请参阅 [New-ExchangeCertificate](https://technet.microsoft.com/zh-cn/library/aa998327\(v=exchg.150\))。

命令输出包含新证书的指纹值。在剩余步骤中将需要此值，可以直接从 Exchange 命令行管理程序 窗口复制该值：

1.  右键单击 Exchange 命令行管理程序窗口中的任意位置，然后选择出现在对话框中的“**标记**”。

2.  选择指纹值，然后按 ENTER 键。

对于本主题中的其他过程，我们将使用联合身份验证证书的指纹值：`6A99CED2E4F2B5BE96C5D17D662D217EF58B8F73`。证书的指纹值将会不同。

## 步骤 2：将新的证书配置为联合身份验证证书

若要使用 Exchange 命令行管理程序将新的证书配置为联合身份验证证书，请使用以下语法：

    Set-FederationTrust -Identity "Microsoft Federation Gateway" -Thumbprint <Thumbprint> -RefreshMetaData

本示例使用步骤 1 中的证书指纹值 `6A99CED2E4F2B5BE96C5D17D662D217EF58B8F73`。

    Set-FederationTrust -Identity "Microsoft Federation Gateway" -Thumbprint 6A99CED2E4F2B5BE96C5D17D662D217EF58B8F73 -RefreshMetaData

有关语法和参数的详细信息，请参阅 [Set-FederationTrust](https://technet.microsoft.com/zh-cn/library/dd298034\(v=exchg.150\))。

**注意：** 命令输出包含一条警告消息，提示你需要更新 DNS 中域所有权 TXT 记录的证明。你将在下一步中执行此操作。

## 步骤 3：更新外部 DNS 中域所有权 TXT 记录的联合身份验证证明

现在可以安全地执行此步骤，因为仅在激活期间检查域所有权 TXT 记录的证明（步骤 5）。但是，更新 TXT 记录后，在继续下一步骤之前，需要等待更新的 TXT 记录进行传播（取决于生存期或 DNS 记录的 TTL 值）。

1.  通过在 Exchange 命令行管理程序中运行以下命令来查找所需的 TXT 记录需要的值：
    
        Get-FederatedDomainProof -DomainName <Domain> | Format-List Thumbprint,Proof
    
    例如，如果联盟域为 contoso.com，则运行以下命令：
    
        Get-FederatedDomainProof -DomainName contoso.com | Format-List Thumbprint,Proof
    
    命令输出如下所示：
    
    `Thumbprint : <new certificate thumbprint>`（例如，`6A99CED2E4F2B5BE96C5D17D662D217EF58B8F73`）
    
    `Proof      : <new hash text>`（例如，`znMfbkgSbOQSsWFdsW+gm3to0nZSdE3zbcPPHGVAqdgsLFGsCPuLHiyVbKoPmgyZKX90NH2g1PbCZH0YTQF6oA==`）
    
    `Thumbprint : <old certificate thumbprint>`（例如，`CC9BC204BB4DC60D06FC1F10F3C373DC785DA2A5`）
    
    `Proof      : <old hash text>`（例如，`m4gZX7OLr9iOWYJMVjEklQpoSkPb5hSbcFjD7Q3/vsqmdJ2Z+HcSt7j5pzBKFmEW2s27JYr3xsK2POzAI/8Ffw==`）
    
    请注意，命令输出返回域所有权两个记录证明的信息：一个用于新证书，一个用于当前正在替换的证书。可以通过指纹值，以及在外部（公用）DNS 中域所有权 TXT 记录的当前证明中配置的哈希文本值进行分辨。

2.  更新外部 DNS 中域所有权 TXT 记录的联合身份验证证明。说明将根据 DNS 提供程序而异，但你可以编辑当前的 TXT 记录，将当前的哈希文本值替换为新的哈希文本值。有关详细信息，请参阅 [Office 365 的外部域名系统记录](https://go.microsoft.com/fwlink/p/?linkid=265522)中的 Exchange Online 部分。

## 步骤 4：验证是否对所有 Exchange 服务器分发新的联合身份验证证书

Exchange 将新的联合身份验证证书自动分发到所有服务器，但我们需要在继续前验证分发。

若要使用 Exchange 命令行管理程序来验证新的联合身份验证证书的分发，请运行以下命令：

    $Servers = Get-ExchangeServer; $Servers | foreach {Get-ExchangeCertificate -Server $_ | Where {$_.Services -match 'Federation'}} | Format-List Identity,Thumbprint,Services,Subject

**注意：** 在 Exchange 2010 中，**Test-FederationCertificate** cmdlet 的输出包含服务器名称。Exchange 2013 或更高版本的 cmdlet 的输出不包含服务器名称。

## 步骤 5：激活新的联合身份验证证书

若要使用 Exchange 命令行管理程序 来激活新的联合身份验证证书，请运行以下命令：

    Set-FederationTrust -Identity "Microsoft Federation Gateway" -PublishFederationCertificate

有关语法和参数的详细信息，请参阅 [Set-FederationTrust](https://technet.microsoft.com/zh-cn/library/dd298034\(v=exchg.150\))。

**注意：** 命令输出包含一条警告消息，提示你需要更新 DNS 中域所有权 TXT 记录的证明（已在步骤 3 中执行此操作）。

## 您如何知道这有效？

要验证是否已成功使用新的联合身份验证证书更新现有的联合身份验证信任，请使用下列步骤：

  - 在 Exchange 命令行管理程序中，运行以下命令来验证是否已使用新的证书：
    
        Get-FederationTrust | Format-List *priv*
    
      - **OrgPrivCertificate** 属性应包含新的联合身份验证证书的指纹。
    
      - **OrgPrevPrivCertificate** 属性应包含旧的（已替换）联合身份验证证书的指纹。

  - 在 Exchange 命令行管理程序中，将 *\<user's email address\>* 替换为组织中用户的电子邮件地址，并运行以下命令来验证联合身份验证信任是否有效：
    
        Test-FederationTrust -UserIdentity <user's email address>

## 替换已过期的联合身份验证证书

如果联合身份验证证书已过期，则需要从联合身份验证信任中删除所有联盟域，然后删除并重新创建联合身份验证信任。

1.  如果有多个联盟域，则需要标识主共享域，以便可以最终删除它。若要使用 Exchange 命令行管理程序来标识主共享域和所有联盟域，请运行以下命令：
    
        Get-FederatedOrganizationIdentifier | Format-List AccountNamespace,Domains
    
    **AccountNamespace** 属性的值包含 `FYDIBOHF25SPDLT<primary shared domain>` 格式的主共享域。例如，在值 `FYDIBOHF25SPDLT.contoso.com` 中，contoso.com 是主共享域。

2.  通过在 Exchange 命令行管理程序中运行以下命令删除不是主共享域的每个联盟域：
    
        Remove-FederatedDomain -DomainName <domain> -Force

3.  删除所有其他联盟域后，在 Exchange 命令行管理程序中运行以下命令，删除主共享域：
    
        Remove-FederatedDomain -DomainName <domain> -Force

4.  在 Exchange 命令行管理程序中运行以下命令，删除联合身份验证信任：
    
        Remove-FederationTrust "Microsoft Federation Gateway"

5.  重新创建联合身份验证信任。有关说明，请参阅[创建联合身份验证信任](https://technet.microsoft.com/zh-cn/library/dd335198\(v=exchg.150\))。

