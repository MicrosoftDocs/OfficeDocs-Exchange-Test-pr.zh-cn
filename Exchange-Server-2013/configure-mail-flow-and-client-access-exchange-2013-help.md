---
title: '配置邮件流和客户端访问: Exchange 2013 Help'
TOCTitle: 配置邮件流和客户端访问
ms:assetid: 4acc7f2a-93ce-468c-9ace-d5f7eecbd8d4
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ218640(v=EXCHG.150)
ms:contentKeyID: 50490484
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 配置邮件流和客户端访问

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2016-12-09_

Exchange Server 2013 邮件流和客户端访问的安装后任务，包括如何配置 SSL 证书。

在您的组织中安装 Microsoft Exchange Server 2013 之后，您需要为邮件流和客户端访问配置 Exchange Server 2013。如果未执行这些附加的步骤，您无法将邮件发送到 Internet 和外部客户端（例如 Microsoft Office Outlook），Exchange ActiveSync 设备也无法连接到您的 Exchange 组织。

本主题中的步骤假设执行基本 Exchange 部署，该部署具有一个 Active Directory 站点和一个简单邮件传输协议 (SMTP) 命名空间。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>本主题使用 Ex2013CAS、contoso.com、mail.contoso.com、172.16.10.11 等示例值。请将示例值替换为您组织的服务器名称、FQDN 和 IP 地址。</td>
</tr>
</tbody>
</table>


有关与邮件流、客户端和设备相关的其他管理任务，请参阅[邮件流](mail-flow-exchange-2013-help.md)和[客户端和移动](clients-and-mobile-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成该任务的时间：50 分钟

  - 本主题中的过程需要特定权限。请参阅每个过程，以了解其权限信息。

  - 如果您未在客户端访问服务器上配置安全套接字层 (SSL) 证书，那么当您连接到 Exchange 管理中心 (EAC) 网站时，您可能会收到证书警告。本主题稍后会向您展示如何执行此操作。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>每个组织在 Active Directory 林中都需要至少一台客户端访问服务器和一台邮箱服务器。另外，每个包含邮箱服务器的 Active Directory 站点还必须包含至少一台客户端访问服务器。如果您要分隔服务器角色，我们建议您先安装邮箱服务器角色。</td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。</td>
</tr>
</tbody>
</table>


## 您该如何做？

## 步骤 1：创建“发送”连接器

您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[邮件流权限](mail-flow-permissions-exchange-2013-help.md)主题中的“发送连接器”条目。

您需要在邮箱服务器上创建发送连接器，才能将邮件发送到 Internet。执行以下操作。

1.  浏览至您的客户端访问服务器的 URL，打开 EAC。例如，https://Ex2013CAS/ECP。

2.  在“域名\\用户名”和“密码”中输入用户名和密码，然后单击“登录”。

3.  转到“邮件流”\>“发送连接器”。在“发送连接器”页上，单击“新建”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。

4.  在“新建发送连接器”向导中，指定发送连接器的名称，然后选择“Internet”。单击“下一步”。

5.  请确认“与收件人域关联的 MX 记录”处于选中状态。单击“下一步”。

6.  在“地址空间”下，单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。在“添加域”窗口中，请确保“类型”字段中选择的条目为“SMTP”。在“完全限定域名 (FQDN)”字段中，输入 **\***。单击“保存”。

7.  确保未选择“作用域发送连接器”，然后单击“下一步”。

8.  在“源服务器”下面，单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。在“选择服务器”窗口中，选择一个邮箱服务器。在选择了服务器之后，单击“添加”，然后单击“确定”。

9.  单击“完成”。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>安装 Exchange 2013 之后将创建默认的入站接收连接器。此接收连接器接受来自外部服务器的匿名 SMTP 连接。如果这是您想要的功能，那么您无需完成任何其他配置。如果您要限制与外部服务器的入站连接，请修改客户端访问服务器上的“默认前端 &lt;客户端访问服务器&gt;”接收连接器。</td>
</tr>
</tbody>
</table>


## 您如何知道此步骤有效？

要验证您是否已成功创建出站发送连接器，请执行以下步骤：

1.  在 EAC 中，确认新的发送连接器是否显示在“邮件流”\>“发送连接器”中。

2.  打开 Outlook Web App，并向外部收件人发送一封邮件。如果收件人收到了此邮件，那么您已经成功配置发送连接器。

## 步骤 2：添加其他接受域

您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[邮件流权限](mail-flow-permissions-exchange-2013-help.md)主题中的“接受域”条目。

默认情况下，当您在 Active Directory 林部署了新的 Exchange 2013 组织，Exchange 将使用运行 Setup /PrepareAD 的 Active Directory 域的域名。如果您希望收件人可以接收来自其他域的邮件，以及将邮件发送到其他域，那么您必须将该域添加为接受域。在下一步骤中，还必须将该域添加为默认电子邮件地址策略中的主 SMTP 地址。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>对于您通过它接受 Internet 电子邮件的每个 SMTP 域来说，要求有公用域名系统 (DNS) MX 资源记录。每条 MX 记录应解析为接收组织电子邮件的面向 Internet 的服务器。</td>
</tr>
</tbody>
</table>


1.  浏览至您的客户端访问服务器的 URL，打开 EAC。例如，https://Ex2013CAS/ECP。

2.  在“域名\\用户名”和“密码”中输入用户名和密码，然后单击“登录”。

3.  转到“邮件流”\>“接受域”。在“接受域”页上，单击“新建”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。

4.  在“新建接受域”向导中，指定接受域的名称。

5.  在“接受域”字段中，指定您要添加的 SMTP 收件人域，例如 contoso.com。

6.  选择“权威域”，然后单击“保存”。

## 您如何知道此步骤有效？

验证是否已成功创建了接受域，请执行以下操作：

  - 在 EAC 中，验证新的接受域是否显示在“邮件流”\>“接受域”中。

## 步骤 3：配置默认电子邮件地址策略

您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[电子邮件地址和通讯簿权限](email-address-and-address-book-permissions-exchange-2013-help.md)主题中的“电子邮件地址策略”条目。

如果您在之前步骤中添加了接受域，并且您希望将该域添加到组织中的所有收件人，那么您需要更新默认的电子邮件地址策略。

1.  浏览至您的客户端访问服务器的 URL，打开 EAC。例如，https://Ex2013CAS/ECP。

2.  在“域名\\用户名”和“密码”中输入用户名和密码，然后单击“登录”。

3.  转到“邮件流”\>“电子邮件地址策略”。在“电子邮件地址策略”页中，选择“默认策略”，然后单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

4.  在“默认策略电子邮件地址策略”页中，单击“电子邮件地址格式”。

5.  在“电子邮件地址格式”下面，单击您要更改的 SMTP 地址，然后单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

6.  在“电子邮件地址格式”页面的“电子邮件地址参数”字段中，指定您要应用到 Exchange 组织中所有收件人的 SMTP 收件人域。该域必须与您在之前步骤中添加的接受域相匹配。例如，@contoso.com。单击“保存”。

7.  单击“保存”。

8.  在“默认策略”详细信息窗格中，单击“应用”。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>我们建议您配置与每个用户的主电子邮件地址匹配的用户主体名称 (UPN)。如果您未提供与用户的电子邮件地址匹配的 UPN，那么用户除了提供他们的电子邮件地址之外，还需要手动提供他们的域\用户名或 UPN。如果他们的 UPN 与电子邮件地址相匹配，那么 Outlook Web App、ActiveSync 和 Outlook 会自动将他们的电子邮件地址与 UPN 相匹配。</td>
</tr>
</tbody>
</table>


## 您如何知道此步骤有效？

要验证您是否已成功配置默认电子邮件地址策略，请执行以下操作：

1.  在 EAC 中，转到“收件人”\>“邮箱”。

2.  选择邮箱，然后在收件人详细信息窗格中确认“用户邮箱”字段已设置为*\<别名\>*@*\<新接受域\>*。例如，david@contoso.com。

3.  或者，您可以新建一个邮箱并通过下列操作确认向该邮箱提供具有新接受域的电子邮件地址：
    
    1.  转到“收件人”\>“邮箱”，单击“新建”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")，然后选择“用户邮箱”。
    
    2.  在新建用户邮箱页面，提供新建邮箱所需的信息。单击“保存”。
    
    3.  选择新邮箱，然后在收件人详细信息窗格中确认“用户邮箱”字段已设置为*\<别名\>*@*\<新接受域\>*。例如，david@contoso.com。

## 步骤 4：配置外部 URL

[客户端和移动设备权限](clients-and-mobile-devices-permissions-exchange-2013-help.md)主题中的“*\<服务\>* 虚拟目录设置”条目。

在客户端通过 Internet 连接到新服务器之前，您需要在客户端访问服务器的虚拟目录上配置外部域或 URL，然后配置公共域名服务 (DNS) 记录。以下步骤对每个虚拟目录的外部 URL 配置相同的外部域。如果您要对一个或多个虚拟目录外部 URL 配置不同外部域，那么您需要手动配置外部 URL。有关详细信息，请参阅[虚拟目录管理](virtual-directory-management-exchange-2013-help.md)。

1.  浏览至您的客户端访问服务器的 URL，打开 EAC。例如，https://Ex2013CAS/ECP。

2.  在“域名\\用户名”和“密码”中输入用户名和密码，然后单击“登录”。

3.  转到“服务器”\>“服务器”，选择面向 Internet 的客户端访问服务器的名称，然后单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

4.  单击“Outlook 无处不在”。

5.  在“指定外部主机名”字段中，指定外部可访问的客户端访问服务器的 FQDN。例如，mail.contoso.com。

6.  位于此处时，还要设置客户端访问服务器的可从内部访问的 FQDN。在“指定内部主机名”字段中，插入在上一步中使用的 FQDN。例如，mail.contoso.com。

7.  单击“保存”。

8.  转到“服务器”\>“虚拟目录”，然后单击“配置外部访问域”![配置图标](images/JJ218640.a9c33f23-3d44-44e7-a5d0-8446200c746e(EXCHG.150).gif "配置图标")。

9.  在“选择要与外部 URL 一起使用的客户端访问服务器”下面，单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")

10. 选择您要配置的客户端访问服务器，然后单击“添加”。添加您要配置的所有客户端访问服务器之后，单击“确定”。

11. 在“输入将与外部客户端访问服务器一起使用的域名”中键入要应用的外部域。例如，mail.contoso.com。单击“保存”。
    
    <table>
    <colgroup>
    <col style="width: 100%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>有些组织的 Outlook Web App FQDN 是唯一的，可保护用户免受基础服务器 FQDN 变更的影响。许多组织为 Outlook Web App FQDN 使用 owa.contoso.com 而非 mail.contoso.com。如果要配置唯一的 Outlook Web App FQDN，请在完成上一步后执行以下操作。此检查表假定您已配置唯一的 Outlook Web App FQDN。
    <ol>
    <li><p>选择“owa (默认网站)”，然后单击“编辑”<img src="images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif" title="编辑图标" alt="编辑图标" />。</p></li>
    <li><p>在“外部 URL”中，键入 <strong>https://</strong>，再键入要使用的唯一 Outlook Web App FQDN，然后加上 <strong>/owa</strong>。例如，https://owa.contoso.com/owa。</p></li>
    <li><p>单击“保存”。</p></li>
    <li><p>选择“ecp (默认网站)”，然后单击“编辑”<img src="images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif" title="编辑图标" alt="编辑图标" />。</p></li>
    <li><p>在“外部 URL”中，键入 <strong>https://</strong>，再键入上一步中指定的相同 Outlook Web App FQDN，然后加上 <strong>/ecp</strong>。例如，https://owa.contoso.com/ecp。</p></li>
    <li><p>单击“保存”。</p></li>
    </ol></td>
    </tr>
    </tbody>
    </table>


对客户端访问服务器虚拟目录配置了外部 URL 之后，您需要为自动发现、Outlook Web App 和邮件流配置公共 DNS 记录。公共 DNS 记录应指向面向 Internet 的客户端访问服务器的外部 IP 地址或 FQDN，并且使用您在客户端访问服务器上配置的可从外部访问的 FQDN。以下是建议创建的用于启用邮件流和外部客户端连接的 DNS 记录示例。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>FQDN</th>
<th>DNS 记录类型</th>
<th>值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Contoso.com</p></td>
<td><p>MX</p></td>
<td><p>Mail.contoso.com</p></td>
</tr>
<tr class="even">
<td><p>Mail.contoso.com</p></td>
<td><p>A</p></td>
<td><p>172.16.10.11</p></td>
</tr>
<tr class="odd">
<td><p>Owa.contoso.com</p></td>
<td><p>CNAME</p></td>
<td><p>Mail.contoso.com</p></td>
</tr>
<tr class="even">
<td><p>Autodiscover.contoso.com</p></td>
<td><p>CNAME</p></td>
<td><p>Mail.contoso.com</p></td>
</tr>
</tbody>
</table>


## 您如何知道此步骤有效？

要验证您是否已成功配置客户端访问服务器虚拟目录的外部 URL，请执行以下操作：

1.  在 EAC 中，转到“服务器”\>“虚拟目录”。

2.  在“选择服务器”字段中，选择面向 Internet 的客户端访问服务器。

3.  选择虚拟目录，然后在虚拟目录详细信息窗格中确认“外部 URL”字段中填充了正确的 FQDN 和服务，如下所示：
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>虚拟目录</th>
    <th>外部 URL 值</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><strong>自动发现</strong></p></td>
    <td><p>未显示外部 URL</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>ECP</strong></p></td>
    <td><p>https://owa.contoso.com/ecp</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>EWS</strong></p></td>
    <td><p>https://mail.contoso.com/EWS/Exchange.asmx</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>Microsoft-Server-ActiveSync</strong></p></td>
    <td><p>https://mail.contoso.com/Microsoft-Server-ActiveSync</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>OAB</strong></p></td>
    <td><p>https://mail.contoso.com/OAB</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>OWA</strong></p></td>
    <td><p>https://owa.contoso.com/owa</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>PowerShell</strong></p></td>
    <td><p>http://mail.contoso.com/PowerShell</p></td>
    </tr>
    </tbody>
    </table>


要验证您是否已成功配置公共 DNS 记录，请执行下列操作：

1.  打开命令提示符，运行 `nslookup.exe`。

2.  更改为可以查询公共 DNS 区域的 DNS 服务器。

3.  在 `nslookup` 中查找您创建的每个 FQDN 的记录。验证为每个 FQDN 返回的值是否正确。

4.  在 `nslookup` 中键入 `set type=mx`，然后查找在步骤 1 中添加的接受域。确认返回的值与客户端访问服务器的 FQDN 匹配。

## 步骤 5：配置内部 URL

您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[客户端和移动设备权限](clients-and-mobile-devices-permissions-exchange-2013-help.md)主题中的“*\<服务\>* 虚拟目录设置”条目。

在客户端可以从 Intranet 连接到新服务器之前，您需要在客户端访问服务器的虚拟目录上配置内部域或 URL，然后配置您的专用域名服务 (DNS) 记录。

以下过程让您可以选择用户在 Intranet 和 Internet 上使用相同的 URL 还是不同的 URL 访问您的 Exchange 服务器。您的选择取决于您已准备就绪或要实施的寻址方案。如果您要实施新的寻址方案，我们建议您使用相同的内部和外部 URL。使用相同 URL 可以让用户更加方便地访问您的 Exchange 服务器，因为他们只需记住一个地址。不管您选择的是什么，您都必须确保为您配置的地址空间配置专用 DNS 区域。有关管理 DNS 区域的详细信息，请参阅[管理 DNS 服务器](http://go.microsoft.com/fwlink/p/?linkid=190631)。

有关虚拟目录的内部和外部 URL 的更多信息，请参阅[虚拟目录管理](virtual-directory-management-exchange-2013-help.md)。

## 将内部和外部 URL 配置为相同

1.  打开客户端访问服务器上的 Exchange 命令行管理程序。

2.  将客户端访问服务器的主机名存储在一个变量中，以便在下一步使用。例如，Ex2013CAS。
    
        $HostName = "Ex2013CAS"

3.  在命令行管理程序中运行以下命令，将每个内部 URL 配置为与虚拟目录的外部 URL 相一致。
    
        Set-EcpVirtualDirectory "$HostName\ECP (Default Web Site)" -InternalUrl ((Get-EcpVirtualDirectory "$HostName\ECP (Default Web Site)").ExternalUrl)
        
        Set-WebServicesVirtualDirectory "$HostName\EWS (Default Web Site)" -InternalUrl ((get-WebServicesVirtualDirectory "$HostName\EWS (Default Web Site)").ExternalUrl)
        
        Set-ActiveSyncVirtualDirectory "$HostName\Microsoft-Server-ActiveSync (Default Web Site)" -InternalUrl ((Get-ActiveSyncVirtualDirectory "$HostName\Microsoft-Server-ActiveSync (Default Web Site)").ExternalUrl)
        
        Set-OabVirtualDirectory "$HostName\OAB (Default Web Site)" -InternalUrl ((Get-OabVirtualDirectory "$HostName\OAB (Default Web Site)").ExternalUrl)
        
        Set-OwaVirtualDirectory "$HostName\OWA (Default Web Site)" -InternalUrl ((Get-OwaVirtualDirectory "$HostName\OWA (Default Web Site)").ExternalUrl)
        
        Set-PowerShellVirtualDirectory "$HostName\PowerShell (Default Web Site)" -InternalUrl ((Get-PowerShellVirtualDirectory "$HostName\PowerShell (Default Web Site)").ExternalUrl)

4.  虽然我们在 Shell 中，但是我们还可以配置脱机通讯簿 (OAB)，使自动发现可以选择正确的虚拟目录进行 OAB 分发。运行以下命令以执行此操作。
    
        Get-OfflineAddressBook | Set-OfflineAddressBook -GlobalWebDistributionEnabled $True -VirtualDirectories $Null

对客户端访问服务器虚拟目录配置内部 URL 之后，您需要为 Outlook Web App 和其他连接配置专用 DNS 记录。根据您的配置，您需要将专用 DNS 记录配置为指向内部或外部 IP 地址，或者指向客户端访问服务器的完全限定域名 (FQDN)。以下是建议创建以用于启用内部客户端连接的 DNS 记录示例。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>FQDN</th>
<th>DNS 记录类型</th>
<th>值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Mail.contoso.com</p></td>
<td><p>CNAME</p></td>
<td><p>Ex2013CAS.corp.contoso.com</p></td>
</tr>
<tr class="even">
<td><p>Owa.contoso.com</p></td>
<td><p>CNAME</p></td>
<td><p>Ex2013CAS.corp.contoso.com</p></td>
</tr>
</tbody>
</table>


## 您如何知道此步骤有效？

要验证您是否已成功配置客户端访问服务器虚拟目录的内部 URL，请执行以下操作：

1.  在 EAC 中，转到“服务器”\>“虚拟目录”。

2.  在“选择服务器”字段中，选择面向 Internet 的客户端访问服务器。

3.  选择虚拟目录，然后单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

4.  请确认“内部 URL”字段中填充的是如下所示的正确 FQDN 和服务：
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>虚拟目录</th>
    <th>内部 URL 值</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><strong>自动发现</strong></p></td>
    <td><p>未显示内部 URL</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>ECP</strong></p></td>
    <td><p>https://owa.contoso.com/ecp</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>EWS</strong></p></td>
    <td><p>https://mail.contoso.com/EWS/Exchange.asmx</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>Microsoft-Server-ActiveSync</strong></p></td>
    <td><p>https://mail.contoso.com/Microsoft-Server-ActiveSync</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>OAB</strong></p></td>
    <td><p>https://mail.contoso.com/OAB</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>OWA</strong></p></td>
    <td><p>https://owa.contoso.com/owa</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>PowerShell</strong></p></td>
    <td><p>http://mail.contoso.com/PowerShell</p></td>
    </tr>
    </tbody>
    </table>


要验证您是否已成功配置专用 DNS 记录，请执行下列操作：

1.  打开命令提示符，运行 `nslookup.exe`。

2.  更改为可以查询专用 DNS 区域的 DNS 服务器。

3.  在 `nslookup` 中查找您创建的每个 FQDN 的记录。验证为每个 FQDN 返回的值是否正确。

## 配置不同的内部和外部 URL

1.  浏览至您的客户端访问服务器的 URL，打开 EAC。例如，https://Ex2013CAS/ECP。

2.  转到“服务器”\>“虚拟目录”。

3.  在“选择服务器”字段中，选择面向 Internet 的客户端访问服务器。

4.  选择要更改的虚拟目录，然后单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

5.  在“内部 URL”中，将“https://”和第一个正斜杠“/”之间的主机名替换为您要使用的新的 FQDN。例如，如果要将 EWS 虚拟目录 FQDN 从 Ex2013CAS.corp.contoso.com 更改为 internal.contoso.com，则需要将内部 URL 从 https://Ex2013CAS.corp.contoso.com/ews/exchange.asmx 更改为 https://internal.contoso.com/ews/exchange.asmx。

6.  单击“保存”。

7.  为要更改的每个虚拟目录重复步骤 5 和 6。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>ECP 和 OWA 虚拟目录的内部 URL 必须相同。<br />
    您不能在自动发现虚拟目录上设置内部 URL。</td>
    </tr>
    </tbody>
    </table>


8.  最后，我们需要打开 Shell，然后配置脱机通讯簿 (OAB)，使自动发现可以选择正确的虚拟目录进行 OAB 分发。运行以下命令以执行此操作。
    
        Get-OfflineAddressBook | Set-OfflineAddressBook -GlobalWebDistributionEnabled $True -VirtualDirectories $Null

对客户端访问服务器虚拟目录配置内部 URL 之后，您需要为 Outlook Web App 和其他连接配置专用 DNS 记录。根据您的配置，您需要将专用 DNS 记录配置为指向内部或外部 IP 地址，或者指向客户端访问服务器的 FQDN。以下是建议创建以用于启用内部客户端连接的 DNS 记录示例，前提是您已将虚拟目录内部 URL 配置为使用 internal.contoso.com。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>FQDN</th>
<th>DNS 记录类型</th>
<th>值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>internal.contoso.com</p></td>
<td><p>CNAME</p></td>
<td><p>Ex2013CAS.corp.contoso.com</p></td>
</tr>
</tbody>
</table>


## 您如何知道此步骤有效？

要验证您是否已成功配置客户端访问服务器虚拟目录的内部 URL，请执行以下操作：

1.  在 EAC 中，转到“服务器”\>“虚拟目录”。

2.  在“选择服务器”字段中，选择面向 Internet 的客户端访问服务器。

3.  选择虚拟目录，然后单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

4.  请确认“内部 URL”字段填充了正确的 FQDN。例如，您可能已将内部 URL 设置为使用 internal.contoso.com。
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>虚拟目录</th>
    <th>内部 URL 值</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><strong>自动发现</strong></p></td>
    <td><p>未显示内部 URL</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>ECP</strong></p></td>
    <td><p>https://internal.contoso.com/ecp</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>EWS</strong></p></td>
    <td><p>https://internal.contoso.com/EWS/Exchange.asmx</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>Microsoft-Server-ActiveSync</strong></p></td>
    <td><p>https://internal.contoso.com/Microsoft-Server-ActiveSync</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>OAB</strong></p></td>
    <td><p>https://internal.contoso.com/OAB</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>OWA</strong></p></td>
    <td><p>https://internal.contoso.com/owa</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>PowerShell</strong></p></td>
    <td><p>http://internal.contoso.com/PowerShell</p></td>
    </tr>
    </tbody>
    </table>


要验证您是否已成功配置专用 DNS 记录，请执行下列操作：

1.  打开命令提示符，运行 `nslookup.exe`。

2.  更改为可以查询专用 DNS 区域的 DNS 服务器。

3.  在 `nslookup` 中查找您创建的每个 FQDN 的记录。验证为每个 FQDN 返回的值是否正确。

## 步骤 6：配置 SSL 证书

您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[邮件流权限](mail-flow-permissions-exchange-2013-help.md)主题中的“证书管理”条目。

有些服务，如 Outlook 无处不在 和 Exchange ActiveSync，要求在 Exchange 2013 服务器上配置证书。以下步骤向您展示了如何配置来自第三方证书颁发机构 (CA) 的 SSL 证书：

1.  浏览至您的客户端访问服务器的 URL，打开 EAC。例如，https://Ex2013CAS/ECP。

2.  在“域名\\用户名”和“密码”中输入用户名和密码，然后单击“登录”。

3.  转到“服务器”\>“证书”。在“证书”页面，确保在“选择服务器”字段中选择了客户端访问服务器，然后单击“新建”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。

4.  在“新建 Exchange 证书”向导中，选择“创建从证书颁发机构获取证书的请求”，然后单击“下一步”。

5.  指定此证书的名称，然后单击“下一步”。

6.  如果您要申请通配符证书，请选择“申请通配符证书”，然后在“根域”字段中指定所有子域的根域。如果您不想申请通配符证书，而是要指定要添加到证书的每个域，则将该页留空。单击“下一步”。

7.  单击“浏览”，指定用于存储证书的 Exchange 服务器。您选择的服务器应是面向 Internet 的客户端访问服务器。单击“下一步”。

8.  对于列表中显示的每个服务，验证用户将用来连接到 Exchange 服务器的外部或内部服务器名称是否正确。例如：
    
      - 如果您配置的内部 URL 和外部 URL 相同，“Outlook Web App (从 Internet 访问)”和“Outlook Web App (从 Intranet 访问)”应显示 owa.contoso.com。“OAB (从 Internet 访问)”和“OAB (从 Intranet 访问)”应显示 mail.contoso.com。
    
      - 如果将内部 URL 配置为 internal.contoso.com，“Outlook Web App (从 Internet 访问)”应显示 owa.contoso.com，“Outlook Web App (从 Intranet 访问)”应显示 internal.contoso.com。
    
    这些域将用于创建 SSL 证书申请。单击“下一步”。

9.  添加您要在 SSL 证书中包括的其他任何域。

10. 选择您希望用作证书常用名的域，然后单击“设置为常用名”。例如，contoso.com。单击“下一步”。

11. 提供有关您的组织的信息。此信息将包含在 SSL 证书中。单击“下一步”。

12. 指定用于保存此证书申请的网络位置。单击“完成”。

保存证书申请之后，将此申请提交给您的证书颁发机构 (CA)。该机构可能是内部 CA 或第三方 CA，这取决于您的组织。连接到客户端访问服务器的客户端必须信任您使用的 CA。从 CA 获得证书后，请完成下列步骤：

1.  在 EAC 的“服务器”\>“证书”页面，选择您在之前步骤中创建的证书申请。

2.  在证书申请的详细信息窗格中，单击“状态”下面的“完成”。

3.  在等待完成申请页面，指定 SSL 证书文件的路径，然后单击“确定”。

4.  选择您刚添加的新证书，然后单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

5.  在证书页面上，单击“服务”。

6.  选择您要分配给此证书的服务。至少，您应选择“SMTP”和“IIS”。单击“保存”。

7.  如果您收到警告“是否覆盖现有的默认 SMTP 证书?”，单击“是”。

## 您如何知道此步骤有效？

要验证是否已成功添加新证书，请执行以下操作：

1.  在 EAC 中，转到“服务器”\>“证书”。

2.  选择新证书，然后在证书详细信息窗格中确认以下信息是否准确：
    
      - “状态”显示“有效”
    
      - “已分配给服务”至少显示“IIS”和“SMTP”。

## 您如何知道此任务有效？

要验证您是否已配置邮件流和外部客户端访问，请执行以下操作：

1.  在 Outlook 和/或 Exchange ActiveSync 设备中新建配置文件。确认 Outlook 或移动设备成功创建了新的配置文件。

2.  在 Outlook 或移动设备中向外部收件人发送一封信邮件。确认外部收件人收到此邮件。

3.  在外部收件人邮箱中回复从 Exchange 邮箱发送的此邮件。确认 Exchange 邮箱收到此邮件。

4.  转到 https://owa.contoso.com/owa，并确认不存在任何证书警告。

