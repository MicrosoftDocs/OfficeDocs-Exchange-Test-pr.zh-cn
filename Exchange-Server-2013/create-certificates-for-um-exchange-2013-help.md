---
title: '创建 UM 证书: Exchange 2013 Help'
TOCTitle: 创建 UM 证书
ms:assetid: 66807ee7-3d3f-482d-a3ac-d4e9baca3271
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dn205141(v=EXCHG.150)
ms:contentKeyID: 54652287
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 创建 UM 证书

 

_**适用于：** Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2013-04-29_

您可以使用 EAC 中的“新建 Exchange 证书”向导或命令行管理程序来创建自签名证书或内部公钥基础结构 (PKI) 证书请求。对于统一消息 (UM)，您可以针对 Microsoft Exchange 统一消息服务和 Microsoft Exchange 统一消息呼叫路由器服务使用这些证书之一。您可以针对这两项服务使用同一证书，或每个服务使用不同的证书。此外，对于 UM 服务，您也可以购买并导入第三方商业证书。如果您在使用 UM 自签名证书，您可能需要将客户端访问和邮箱服务器的名称加入主题备用名称 (SAN) 中。

在默认情况下，安装 Exchange Server 2013 时，会创建两个自签名证书：** Microsoft Exchange Server 身份验证证书**和 **Microsoft Exchange**。**Microsoft Exchange** 自签名证书可由 UM 用于加密数据，但您必须为 UM 和 UM 呼叫路由器服务分配该证书。在将证书分配给统一消息服务之后，您可以复制该证书并将其导入 VoIP 网关、IP PBX 和启用 SIP 的 PBX。但是，您需要为统一消息专门创建另一个证书，而不是使用默认的自签名证书。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876845.Caution(EXCHG.150).gif" title="小心" alt="小心" />小心：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>将 UM 与 Microsoft Lync Server 集成时，自签名证书不可使用。</td>
</tr>
</tbody>
</table>


有关管理统一消息证书的更多管理任务，请参阅[部署证书的 UM 过程](deploying-certificates-for-um-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：5 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[Exchange 和命令行管理程序基础结构权限](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md)主题中的“证书管理”条目和 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md) 主题中的“UM 服务”条目。还必须使用该计算机上本地 Administrators 组的成员帐户进行登录。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.</td>
</tr>
</tbody>
</table>


## 您想执行什么操作？

## 使用 EAC 创建 UM 证书请求

1.  在 EAC 中，导航至“服务器”\>“证书”，然后单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。

2.  在“新建 Exchange 证书”页面上，选择“创建从证书颁发机构获取证书的请求”，然后单击“下一步”。

3.  为证书输入一个友好名称，然后单击“下一步”。

4.  如果您不需要通配符证书，单击“下一步”。如果您需要通配符证书，选择“申请通配符证书。通配符证书用于凭借单个证书保护根域下的所有子域”，输入根域名称，然后单击“下一步”。

5.  在“在此服务器上存储证书请求”下，单击“浏览”以转至要存储文件的位置。可以在 Exchange 组织中的任一客户端访问或邮箱服务器上存储证书请求。选择位置，单击“确定”，然后单击“下一步”。

6.  如果已发出通配符证书请求，请跳到步骤 9。

7.  如果还未发出通配符证书请求，您需要指定要包含在证书中的域。如果想要编辑域，单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")，然后单击“下一步”。

8.  在“根据您的选择，下列域将包含在您的证书中。您可以在此处添加其他域或进行更改”下，您可以添加、编辑、移除或检查“域”下所列的域名。然后，单击“下一步”。

9.  在“指定有关组织的信息。这是证书颁发机构的要求”下，输入以下信息：
    
      - **组织名称**
    
      - **部门名称**
    
      - **市/位置**
    
      - **省/市/自治区**
    
      - **国家/地区名称**   对于该选项，使用下拉列表选择国家或地区。

10. 在“将证书请求保存至下列文件”下，输入证书文件名称，然后单击“完成”。

## 使用命令行管理程序创建 UM 证书请求

此示例针对名为 `MyMailboxServer` 的邮箱服务器新建了一个 Exchange 证书请求，其友好名称为 `CertUM`。

    New-ExchangeCertificate -FriendlyName 'CertUM' -GenerateRequest -PrivateKeyExportable $true -KeySize '2048' -DomainName '*.northwindtraders.com' -SubjectName 'C=US,S=wa,L=redmond,O=northwindtraders,OU=servers,CN= northwindtraders.com' -Server 'MyMailboxServer'

## 使用 EAC 创建 UM 自签名证书

1.  在 EAC 中，导航至“服务器”\>“证书”，然后单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。

2.  在“新建 Exchange 证书”页面，选择“创建自签名证书”，然后选择“下一步”。

3.  为证书输入一个友好名称，然后选择“下一步”。

4.  单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")选择要应用此证书的 Exchange 服务器，然后选择“下一步”。

5.  指定您想包含在证书中的域，然后选择“下一步”。如果想为服务添加一个域，则单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

6.  验证所包含的域是否正确，然后选择“完成”。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>使用 EAC 创建自签名证书时，系统不会提示您为证书启用相应服务。在证书创建完成之后，您可以使用 EAC 或命令行管理程序中的 <strong>Enable-ExchangeCertificate</strong> cmdlet 启用 Exchange 服务。有关如何为 UM 服务分配证书的详细信息，请参阅<a href="assign-a-certificate-to-the-um-and-um-call-router-services-exchange-2013-help.md">将证书分配给该 UM 和 UM 呼叫路由器服务</a>。</td>
</tr>
</tbody>
</table>


## 使用命令行管理程序创建 UM 自签名证书

此示例针对名为 `MyMailboxServer` 的邮箱服务器新建了一个 Exchange 自签名证书，其友好名称为 `UMCert`。

    New-ExchangeCertificate -Services 'UM, UMCallRouter' -DomainName '*.northwindtraders.com' -FriendlyName 'UMSelfSigned' -SubjectName 'C=US,S=WA,L=Redmond,O=Northwindtraders,OU=Servers,CN= Northwindtraders.com' -PrivateKeyExportable $true

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>使用 <em>Services</em> 参数指定要启用的服务时，系统会提醒您分配这些服务。在此示例中，系统会提示您为 UM 和统一消息呼叫路由器服务启用证书。有关如何为服务启用证书的详细信息，请参阅<a href="assign-a-certificate-to-the-um-and-um-call-router-services-exchange-2013-help.md">将证书分配给该 UM 和 UM 呼叫路由器服务</a>。</td>
</tr>
</tbody>
</table>

