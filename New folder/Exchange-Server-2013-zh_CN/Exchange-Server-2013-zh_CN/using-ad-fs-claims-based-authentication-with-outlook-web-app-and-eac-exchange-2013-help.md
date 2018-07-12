---
title: '对 Outlook Web App 和 EAC 使用 AD FS 基于声明的身份验证: Exchange 2013 Help'
TOCTitle: 对 Outlook Web App 和 EAC 使用 AD FS 基于声明的身份验证
ms:assetid: 919a9bfb-c6df-490a-b2c4-51796b0f0596
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dn635116(v=EXCHG.150)
ms:contentKeyID: 61203678
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 对 Outlook Web App 和 EAC 使用 AD FS 基于声明的身份验证

 

_**适用于：** Exchange Server 2013 SP1_

_**上一次修改主题：** 2017-04-14_

**摘要：** 

对于本地 Exchange 2013 Service Pack 1 (SP1) 部署，安装和配置 Active Directory 联合身份验证服务 (AD FS) 意味着，您现在可以使用 AD FS 基于声明的身份验证方法连接到 Outlook Web App 和 EAC。您可以将 AD FS 和基于声明的身份验证与 Exchange 2013 SP1 集成。使用基于声明的身份验证可代替传统的身份验证方法，包括以下方法：

  - Windows 身份验证

  - 窗体身份验证

  - 摘要式身份验证

  - 基本身份验证

  - Active Directory 客户端证书身份验证

身份验证是确认用户标识的过程。身份验证验证用户是其声明的那个人。基于声明的标识是进行身份验证的另一种方法。基于声明的身份验证将身份验证的管理从应用程序（在本案例中为 Outlook Web App 和 EAC）中删除，从而通过集中化身份验证来简化帐户管理。Outlook Web App 和 EAC 不负责对用户进行身份验证、存储用户帐户和密码、查找用户标识详细信息，或者与其他标识系统集成。集中化身份验证有助于使将来的身份验证方法升级变得更加简单。

> [!NOTE]
> 适用于设备的 OWA 不支持 AD FS 基于声明的身份验证。


AD FS 有多个版本可供使用，如下表所汇总。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Windows Server 版本</th>
<th>安装</th>
<th>AD FS 版本</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Windows Server 2008 R2</p></td>
<td><p><strong>下载并安装</strong> AD FS 2.0（此为附加 Windows 组件）。</p></td>
<td><p>AD FS 2.0</p></td>
</tr>
<tr class="even">
<td><p>Windows Server 2012</p></td>
<td><p>安装<strong>内置</strong> AD FS 服务器角色。</p></td>
<td><p>AD FS 2.1</p></td>
</tr>
<tr class="odd">
<td><p>Windows Server 2012 R2</p></td>
<td><p>安装<strong>内置</strong> AD FS 服务器角色。</p></td>
<td><p>AD FS 3.0</p></td>
</tr>
</tbody>
</table>


此处，您将执行的任务基于包含 AD FS 角色服务的 Windows Server 2012 R2。

**所需步骤概述**

Step 1 - Review the certificate requirements for AD FS

Step 2 - Install and configure Active Directory Federation Services (AD FS)

第 3 步 - 为 Outlook Web App 和 EAC 创建信赖方信任和自定义声明规则

第 4 步 - 安装 Web 应用程序代理角色服务（可选）

第 5 步 - 配置 Web 应用程序代理角色服务（可选）

第 6 步 - 使用 Web 应用程序代理发布 Outlook Web App 和 EAC（可选）

第 7 步 - 将 Exchange 2013 配置为使用 AD FS 身份验证

第 8 步 - 在 OWA 和 ECP 虚拟目录上启用 AD FS 身份验证

第 9 步 - 重启或再循环 Internet Information Services (IIS)

第 10 步 - 为 Outlook Web App 和 EAC 测试 AD FS 声明

Additional information you might want to know

## 在开始之前，我需要知道什么？

  - 至少需要安装单独的 Windows Server 2012 R2 服务器：一个作为使用 Active Directory 域服务 (AD DS) 的域控制器、一个 Exchange 2013 服务器、一个 Web 应用程序代理服务器和一个 Active Directory 联合身份验证服务 (AD FS) 服务器。验证所有更新是否均已安装。

  - 在组织中合适数量的 Windows Server 2012 R2 服务器上安装 AD DS。您还可以使用\&quot;服务器管理器\&quot;\>\&quot;主控板\&quot;中的\&quot;通知\&quot;\&quot;将此服务器提升为域控制器\&quot;。

  - 为组织安装合适数量的客户端访问服务器和邮箱服务器。验证是否已在组织的所有 Exchange 2013 服务器中安装所有更新（包括 SP1）。若要下载 SP1，请参阅 [Exchange 2013 更新](updates-for-exchange-2013-exchange-2013-help.md)。

  - 在服务器上部署 Web 应用程序代理需要本地管理员权限。在部署 Web 应用程序代理之前，必须在组织中运行 Windows Server 2012 R2 的服务器中部署 AD FS。

  - 安装和配置 AD FS 角色并在 Windows Server 2012 R2 中创建信赖方信任和声明规则。为此，需要使用作为 Domain Admins、Enterprise Admins 或本地 Administrators 组成员的用户帐户登录。

  - 参阅[功能权限](feature-permissions-exchange-2013-help.md)，确定 Exchange 2013 所需的权限。

  - 您必须获得权限，才能管理 Outlook Web App。若要了解您需要哪些权限，请参阅[客户端和移动设备权限](clients-and-mobile-devices-permissions-exchange-2013-help.md)主题中的\&quot;Outlook Web App 权限\&quot;条目。

  - 您必须获得权限，才能管理 EAC。若要查看需要什么权限，请参阅 [Exchange 和命令行管理程序基础结构权限](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md)主题中的\&quot;Exchange 管理中心连接性\&quot;条目。

  - 可能只能使用命令行管理程序执行某些过程。若要了解如何在本地 Exchange 组织中打开命令行管理程序，请参阅[打开命令行管理程序](https://technet.microsoft.com/zh-cn/library/dd638134\(v=exchg.150\))。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!tip]
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 步骤 1 – 查看 AD FS 的证书要求

在保护 Exchange 2013 SP1 服务器、Web 客户端（例如 Outlook Web App），以及 EAC、Windows Server 2012 R2 服务器（包括 Active Directory 联合身份验证服务 (AD FS) 服务器和 Web 应用程序代理服务器）之间的通信的过程中，证书扮演了非常重要的角色。证书的要求取决于正在设置的是 AD FS 服务器、AD FS 代理还是 Web 应用程序代理服务器。用于 AD FS 服务的证书（包括 SSL 和令牌签名证书）必须导入到所有 Exchange、AD FS 和 Web 应用程序代理服务器中的信任根证书颁发机构存储中。当您使用 [Set-OrganizationConfig](https://technet.microsoft.com/zh-cn/library/aa997443\(v=exchg.150\)) cmdlet 时，导入的证书的指纹也会在 Exchange 2013 SP1 服务器上使用。

在任何 AD FS 设计中，必须使用各种证书来保护 Internet 中的用户和 AD FS 服务器之间的通信安全。每个联合服务器必须拥有服务通信证书或安全套接字层 (SSL) 证书，以及令牌签名证书，然后 AD FS 服务器、Active Directory 域控制器和 Exchange 2013 服务器才能进行通信和身份验证。根据你的安全和预算要求，认真考虑公共 CA 或企业 CA 将获得你的哪些证书。如果要安装和配置企业根或从属 CA，你可以使用 Active Directory 证书服务 (AD CS)。如果想了解有关 AD CS 的详细信息，请参阅 [Active Directory 证书服务概述](https://go.microsoft.com/fwlink/?linkid=392697)。

尽管 AD FS 不需要 CA 颁发的证书，但 SSL 证书（默认情况下，SSL 证书还被用作服务通信证书）必须受 AD FS 客户端信任。我们建议不要使用自签名证书。联合服务器使用 SSL 证书保护 Web 服务通信，以便实现与 Web 客户端以及与联合服务器代理的 SSL 通信。由于 SSL 证书必须受客户端计算机信任，我们建议您使用由受信任的 CA 签名的证书。您选择的所有证书都必须拥有相应的私钥。从 CA（企业或公共）收到证书后，确保所有证书都被导入到所有服务器中的信任根证书颁发机构存储中。您可以使用\&quot;证书\&quot;MMC 管理单元将证书导入到存储中，或者使用 Active Directory 证书服务分发证书。有一点很重要，如果您导入的证书已过期，您需要手动导入另一个有效证书。

> [!important]
> 如果您使用来自 AD FS 的自签名令牌签名证书，必须将此证书导入到所有 Exchange 2013 服务器中的信任根证书颁发机构存储中。如果未使用自签名令牌签名证书，并且已部署 Web 应用程序代理，则必须更新 Web 应用程序代理配置和所有 AD FS 信赖方信任中的公钥。


设置 Exchange 2013 SP1、AD FS 和 Web 应用程序代理时，请遵循以下证书建议：

  - **邮箱服务器**   邮箱服务器中使用的证书为自签名证书，这些证书是在安装 Exchange 2013 时创建的。由于所有客户端都通过 Exchange 2013 客户端访问服务器连接到 Exchange 2013 邮箱服务器，因此您只需要管理客户端访问服务器中的证书。

  - **客户端访问服务器**   需要用于服务通信的 SSL 证书。如果您的现有 SSL 证书已经包含正用于设置信赖方信任终结点的 FQDN，则无需其他证书。

  - **AD FS**   AD FS 需要两种类型的证书：
    
      - 用于服务通信的 SSL 证书
        
          - 主题名称：** adfs.contoso.com**（AD FS 部署名称）
        
          - 主题备用名称 (SAN)：无
    
      - 令牌签名证书
        
          - 主题名称：** tokensigning.contoso.com**
        
          - 主题备用名称 (SAN)：无
        
        > [!NOTE]
        > 替换 AD FS 中的令牌签名证书时，必须更新所有现有信赖方信任，以使用新的令牌签名证书。


  - **Web 应用程序代理**
    
      - 用于服务通信的 SSL 证书
        
          - 主题名称：** owa.contoso.com**
        
          - 主题备用名称 (SAN)：无
        
        > [!NOTE]
        > 如果您的 Web 应用程序代理外部 URL 与内部 URL 相同，您可以在此重新使用 Exchange 的 SSL 证书。
    
      - AD FS 代理 SSL 证书
        
          - 主题名称：** adfs.contoso.com**（AD FS 部署名称）
        
          - 主题备用名称 (SAN)：无
    
      - 令牌签名证书 - 作为以下步骤的一部分，此证书将从 AD FS 自动复制。如果使用了此证书，它必须受组织中 Exchange 2013 服务器的信任。

请参阅[查看部署 AD FS 的要求](https://go.microsoft.com/fwlink/?linkid=392699)中的证书要求部分，以获取有关证书的详细信息。

> [!NOTE]
> Outlook Web App 和 EAC 仍然需要 SSL 加密证书，即使您已经拥有用于 AD FS 的 SSL 证书。SSL 证书在 OWA 和 ECP 虚拟目录中使用。


## 步骤 2 - 安装和配置 Active Directory 联合身份验证服务 (AD FS)

Windows Server 2012 R2 中的 AD FS 提供了简化的安全联合身份验证和 Web 单一登录 (SSO) 功能。AD FS 引入了联合身份验证服务，该服务支持基于浏览器的 Web SSO、多重和基于声明的身份验证。AD FS 通过使用基于声明的身份验证和访问授权机制维护应用程序的安全，从而简化了对系统和应用程序的访问。

在 Windows Server 2012 R2 上安装 AD FS 的步骤：

1.  打开\&quot;开始\&quot;屏幕中的\&quot;服务器管理器\&quot;或桌面任务栏中的\&quot;服务器管理器\&quot;。单击\&quot;管理\&quot;菜单中的\&quot;添加角色和功能\&quot;。

2.  在\&quot;开始之前\&quot;页中，单击\&quot;下一步\&quot;。

3.  在\&quot;选择安装类型\&quot;页上，单击\&quot;基于角色或基于功能的安装\&quot;，然后单击\&quot;下一步\&quot;。

4.  在\&quot;选择目标服务器\&quot;页上，单击\&quot;从服务器池中选择服务器\&quot;，验证是否已选择本地计算机，然后单击\&quot;下一步\&quot;。

5.  在\&quot;选择服务器角色\&quot;页上，单击\&quot;Active Directory 联合身份验证服务\&quot;，然后单击\&quot;下一步\&quot;。
    
    在\&quot;选择功能\&quot;页上，单击\&quot;下一步\&quot;。已经为您选择了所必需的先决条件或功能。您不需要再选择其他任何功能。

6.  在\&quot;Active Directory 联合身份验证服务(AD FS)\&quot;页上，单击\&quot;下一步\&quot;。

7.  在\&quot;确认安装选择\&quot;页上，选中\&quot;如果需要，自动重新启动目标服务器\&quot;，然后单击\&quot;安装\&quot;。
    
    > [!NOTE]
    > 在安装过程中请勿关闭向导。


安装了所需 AD FS 服务器并生成所需证书后，必须配置 AD FS，然后测试 AD FS 是否能够正常运行。你还可以使用此处的检查表帮助设置和配置 AD FS：[检查表：设置联合服务器](https://go.microsoft.com/fwlink/?linkid=392700)。

配置 Active Directory 联合身份验证服务的步骤：

1.  在\&quot;安装进度\&quot;页上，在\&quot;Active Directory 联合身份验证服务\&quot;下的窗口中，单击\&quot;在此服务器上配置联合身份验证服务\&quot;。Active Directory 联合身份验证服务配置向导将会打开。

2.  在\&quot;欢迎\&quot;页中，单击\&quot;在联合服务器场中创建第一个联合服务器\&quot;，然后单击\&quot;下一步\&quot;。

3.  在\&quot;连接到 AD DS\&quot;页中，为此计算机加入的正确的 Active Directory 域指定拥有域管理员权限的帐户，然后单击\&quot;下一步\&quot;。如果需要选择其他用户，请单击\&quot;更改\&quot;。

4.  在\&quot;指定服务属性\&quot;页上，执行以下操作，然后单击\&quot;下一步\&quot;：
    
      - 导入之前从 AD CS 或公共 CA 获得的 SSL 证书。此证书是必需的服务身份验证证书。浏览到 SSL 证书的位置。有关创建和导入 SSL 证书的详细信息，请参阅[服务器证书](https://go.microsoft.com/fwlink/?linkid=392703)。
    
      - 为联合身份验证服务输入名称 - 例如，键入 **adfs.contoso.com**。
    
      - 若要为联合身份验证服务提供显示名称，键入组织的名称 - 例如 **Contoso, Ltd.**。

5.  在\&quot;指定服务帐户\&quot;页上，选择\&quot;使用现有的域用户帐户或组托管服务帐户\&quot;，然后指定创建域控制器时创建的 GMSA 帐户 (FsGmsa)。包括帐户密码，然后单击\&quot;下一步\&quot;。
    
    > [!NOTE]
    > 全局托管服务帐户 (GMSA) 是配置域控制器时必须创建的帐户。安装和配置 AD FS 时需要 GMSA 帐户。如果尚未创建此帐户，请运行以下 Windows PowerShell 命令。该命令为 contoso.com 域和 AD FS 服务器创建帐户：


6.  运行以下命令。
    
        Add-KdsRootKey -EffectiveTime (Get-Date).AddHours(-10)

7.  本示例创建名为 adfs.contoso.com 的联合身份验证服务名为 FsGmsa 的新 GMSA 帐户。联合身份验证服务名称是客户端可见的值。
    
        New-ADServiceAccount FsGmsa -DNSHostName adfs.contoso.com -ServicePrincipalNames http/adfs.contoso.com

8.  在\&quot;指定配置数据库\&quot;页上，选择\&quot;在此服务器上使用 Windows 内部数据库创建数据库\&quot;，然后单击\&quot;下一步\&quot;。

9.  在\&quot;查看选项\&quot;页上，验证配置选择。还可以选择使用\&quot;查看脚本\&quot;按钮自动进行其他 AD FS 安装。单击\&quot;下一步\&quot;。

10. 在\&quot;先决条件检查\&quot;页上，验证所有的先决条件检查是否都已成功完成，然后单击\&quot;配置\&quot;。

11. 在\&quot;安装进度\&quot;页上，确认所有项目都已正确安装，然后单击\&quot;关闭\&quot;。

12. 在\&quot;结果\&quot;页上，查看结果，检查配置是否成功完成，然后单击\&quot;完成联合身份验证服务部署所需的后续步骤\&quot;。

下面的Windows PowerShell 命令执行相同的操作，为前面的步骤。
```
    Import-Module ADFS
```
```
    Install-AdfsFarm -CertificateThumbprint 0E0C205D252002D535F6D32026B6AB074FB840E7 -FederationServiceDisplayName "Contoso Corporation" -FederationServiceName adfs.contoso.com -GroupServiceAccountIdentifier "contoso\FSgmsa`$"
```

有关详细信息和语法，请参阅 [Install-AdfsFarm](https://go.microsoft.com/fwlink/?linkid=392704)。

验证安装的步骤：在 AD FS 服务器上，打开 Web 浏览器，然后浏览到联合身份验证元数据的 URL - 例如 **https://adfs.contoso.com/federationmetadata/2007-06/federationmetadata.xml**。

## 第 3 步 - 为 Outlook Web App 和 EAC 创建信赖方信任和自定义声明规则

对于所有要通过 Web 应用程序代理发布的应用程序和服务，您必须在 AD FS 服务器上配置信赖方信任。对于包含多个使用单独命名空间的 Active Directory 站点的部署，您必须为每个命名空间添加 Outlook Web App 和 EAC 的信赖方信任。

EAC 使用 ECP 虚拟目录。您可以使用 [Get-EcpVirtualDirectory](https://technet.microsoft.com/zh-cn/library/dd351058\(v=exchg.150\)) 和 [Set-EcpVirtualDirectory](https://technet.microsoft.com/zh-cn/library/dd297991\(v=exchg.150\)) cmdlet 查看或配置 EAC 的设置。若要访问 EAC，必须使用 Web 浏览器并转到 **http://server1.contoso.com/ecp**。

> [!NOTE]
> 在如下示例中，我们特意在 URL 中添加尾部反斜杠 <strong>/</strong>。务必确保 AD FS 信赖方信任与 Exchange 用户 URI 的信赖方信任<strong>是相同的</strong>。这意味着 AD FS 信赖方信任和 Exchange 用户 URI 的信赖方信任在其 URL 中<strong>都有</strong>或<strong>都使用</strong>尾部斜杠。本节中的示例对任何以&amp;quot;owa&amp;quot;或&amp;quot;ecp&amp;quot;结尾的 url，在其尾部后面追加一个 <strong>/</strong>，即变为&amp;quot;/owa/&amp;quot;或&amp;quot;/ecp/&amp;quot;。


对于 Outlook Web App，若要使用 Windows Server 2012 R2 中的 AD FS 管理单元创建信赖方信任，请执行以下操作：

1.  在\&quot;服务器管理器\&quot;中，单击\&quot;工具\&quot;，然后选择\&quot;AD FS 管理\&quot;。

2.  在\&quot;AD FS 管理单元\&quot;中，在\&quot;AD FS\\信任关系\&quot;下，右键单击\&quot;信赖方信任\&quot;，然后单击\&quot;添加信赖方信任\&quot; 以打开\&quot;添加信赖方信任\&quot;向导。

3.  在\&quot;欢迎\&quot;页中，单击\&quot;开始\&quot;。

4.  在\&quot;选择数据源\&quot;页上，单击\&quot;手动输入有关信赖方的数据\&quot;，然后单击\&quot;下一步\&quot;。

5.  在\&quot;指定显示名称\&quot;页上，在\&quot;显示名称\&quot;框中，键入 **Outlook Web App**，然后在\&quot;备注\&quot;下，为此信赖方信任键入描述（例如，**This is a trust for https://mail.contoso.com/owa**），然后单击\&quot;下一步\&quot;。

6.  在\&quot;选择配置文件\&quot;页上，单击\&quot;AD FS 配置文件\&quot;，然后单击\&quot;下一步\&quot;。

7.  在\&quot;配置证书\&quot;页上，单击\&quot;下一步\&quot;。

8.  在\&quot;配置 URL\&quot;页上，单击\&quot;启用对 WS-Federation 被动协议的支持\&quot;，然后在\&quot;信赖方 WS-Federation 被动协议 URL\&quot;下，**type https://mail.contoso.com/owa**，然后单击\&quot;下一步\&quot;。

9.  在\&quot;配置标识符\&quot;页上，为此信赖方指定一个或多个标识符，单击\&quot;添加\&quot;将它们添加到列表，然后单击\&quot;下一步\&quot;。

10. 在\&quot;是否立即配置多重身份验证?\&quot;页上，选择\&quot;为此信赖方信任配置多重身份验证设置\&quot;。

11. 在\&quot;配置多重身份验证\&quot;页上，验证已选择\&quot;我不想现在为此信赖方信任配置多重身份验证设置\&quot;，然后单击\&quot;下一步\&quot;。

12. 在\&quot;选择颁发授权规则\&quot;页上，选择\&quot;允许所有用户访问此信赖方\&quot;，然后单击\&quot;下一步\&quot;。

13. 在\&quot;准备好添加信任\&quot;页上，查看设置，然后单击\&quot;下一步\&quot;，保存信赖方信任信息。

14. 在\&quot;完成\&quot;页上，验证未选择\&quot;关闭向导时打开此信赖方信任的编辑声明规则对话框\&quot;，然后单击\&quot;关闭\&quot;。

若要为 EAC 创建信赖方信任，必须再次执行这些步骤并创建第二个信赖方信任，但是不要在显示名称中加入 **Outlook Web App**，而是输入 **EAC**。对于描述，请输入 **This is a trust for the Exchange Admin Center**，\&quot;信赖方 WS-Federation 被动协议 URL\&quot;为 **https://mail.contoso.com/ecp**。

在基于声明的标识模型中，作为联合身份验证服务的 Active Directory 联合身份验证服务 (AD FS) 的功能是颁发包含一组声明的令牌。声明规则控制有关 AD FS 颁发的声明的决策。声明规则和所有服务器配置数据都存储在 AD FS 配置数据库中。

您必须创建两个声明规则：

  - Active Directory 用户 SID

  - Active Directory UPN

若要添加所需的声明规则，请执行以下操作：

1.  在\&quot;服务器管理器\&quot;中，单击\&quot;工具\&quot;，然后单击\&quot;AD FS 管理\&quot;。

2.  在控制台树中，在\&quot;AD FS\\信任关系\&quot;下，单击\&quot;声明提供程序信任\&quot;或\&quot;信赖方信任\&quot;，然后单击 Outlook Web App 的信赖方信任。

3.  在\&quot;信赖方信任\&quot;窗口中，右键单击 Outlook Web App 信任，然后单击\&quot;编辑声明规则\&quot;。

4.  在\&quot;编辑声明规则\&quot;窗口中，在\&quot;颁发转换规则\&quot;选项卡上，单击\&quot;添加规则\&quot;以启动\&quot;添加转换声明规则向导\&quot;。

5.  在\&quot;选择规则模板\&quot;页面中的\&quot;声明规则模板\&quot;下，选择列表中的\&quot;使用自定义规则发送声明\&quot;，然后单击\&quot;下一步\&quot;。

6.  在\&quot;配置规则\&quot;页中，在\&quot;选择规则类型\&quot;步骤中的\&quot;声明规则名称\&quot;下，为声明规则输入名称。使用声明规则的描述性名称 - 例如，**ActiveDirectoryUserSID**。在\&quot;自定义规则\&quot;下，为此规则输入以下声明规则语言语法：
    
        c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", Issuer == "AD AUTHORITY"] => issue(store = "Active Directory", types = ("http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid"), query = ";objectSID;{0}", param = c.Value);

7.  在\&quot;配置规则\&quot;页上，单击\&quot;完成\&quot;。

8.  在\&quot;编辑声明规则\&quot;窗口中，在\&quot;颁发转换规则\&quot;选项卡上，单击\&quot;添加规则\&quot;以启动\&quot;添加转换声明规则向导\&quot;。

9.  在\&quot;选择规则模板\&quot;页面中的\&quot;声明规则模板\&quot;下，选择列表中的\&quot;使用自定义规则发送声明\&quot;，然后单击\&quot;下一步\&quot;。

10. 在\&quot;配置规则\&quot;页中，在\&quot;选择规则类型\&quot;步骤中的\&quot;声明规则名称\&quot;下，为声明规则输入名称。使用声明规则的描述性名称 - 例如，**ActiveDirectoryUPN**。在\&quot;自定义规则\&quot;下，为此规则输入以下声明规则语言语法：
    
        c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", Issuer == "AD AUTHORITY"] => issue(store = "Active Directory", types = ("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn"), query = ";userPrincipalName;{0}", param = c.Value);

11. 单击\&quot;完成\&quot;。

12. 在\&quot;编辑声明规则\&quot;窗口中，单击\&quot;应用\&quot;，然后单击\&quot;确定\&quot;。

13. 为 EAC 信赖方信任重复执行此程序的第 3-12 步。

您也可以使用 Windows PowerShell 创建信赖方信任和声明规则：

1.  创建两个 .txt 文件，IssuanceAuthorizationRules.txt 和 IssuanceTransformRules.txt。

2.  将它们的内容导入两个变量中。

3.  运行以下两个 cmdlet 以创建信赖方信任。在此示例中，这还将配置声明规则。

**IssuanceAuthorizationRules.txt 包含：** 

    @RuleTemplate = "AllowAllAuthzRule" => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");

**IssuanceTransformRules.txt 包含：** 

    @RuleName = "ActiveDirectoryUserSID" c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", Issuer == "AD AUTHORITY"] => issue(store = "Active Directory", types = ("http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid"), query = ";objectSID;{0}", param = c.Value); 
    
    @RuleName = "ActiveDirectoryUPN" c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", Issuer == "AD AUTHORITY"] => issue(store = "Active Directory", types = ("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn"), query = ";userPrincipalName;{0}", param = c.Value);

**运行以下命令：** 

    [string]$IssuanceAuthorizationRules=Get-Content -Path C:\IssuanceAuthorizationRules.txt
    
    [string]$IssuanceTransformRules=Get-Content -Path c:\IssuanceTransformRules.txt
    
    Add-ADFSRelyingPartyTrust -Name "Outlook Web App" -Enabled $true -Notes "This is a trust for https://mail.contoso.com/owa/" -WSFedEndpoint https://mail.contoso.com/owa/ -Identifier https://mail.contoso.com/owa/ -IssuanceTransformRules $IssuanceTransformRules -IssuanceAuthorizationRules $IssuanceAuthorizationRules
    
    Add-ADFSRelyingPartyTrust -Name "Exchange Admin Center (EAC)" -Enabled $true -Notes "This is a trust for https://mail.contoso.com/ecp/" -WSFedEndpoint https://mail.contoso.com/ecp/ -Identifier https://mail.contoso.com/ecp/ -IssuanceTransformRules $IssuanceTransformRules -IssuanceAuthorizationRules $IssuanceAuthorizationRules

## 第 4 步 - 安装 Web 应用程序代理角色服务（可选）

> [!NOTE]
> 第 4 步、第 5 步和第 6 步均适用于想使用 Web 应用程序代理发布 Exchange OWA 和 ECP，并想让 Web 应用程序代理执行 AD FS 身份验证的用户。不过，使用 Web 应用程序代理发布 Exchange 是可选步骤。因此，如果您没有使用 Web 应用程序代理，但确实想让 Exchange 自行执行 AD FS 身份验证，则可以跳到第 7 步。


Web 应用程序代理是 Windows Server 2012 R2 中的新远程访问角色服务。Web 应用程序代理为公司网络中的 Web 应用程序提供反向代理功能，以允许多种设备上的用户从公司网络外部访问这些应用程序。Web 应用程序代理使用 Active Directory 联合身份验证服务 (AD FS) 对 Web 应用程序的访问进行预先身份验证，并充当 AD FS 代理。尽管 Web 应用程序代理不是必须的，但是当外部客户端可以访问 AD FS 时，我们建议使用此代理。但是，通过 Web 应用程序代理使用 AD FS 身份验证时，不支持 Outlook Web App 中的脱机访问。若要获取有关与 Web 应用程序代理集成的详细信息，请参阅[为发布内部应用程序安装和配置 Web 应用程序代理](https://go.microsoft.com/fwlink/?linkid=392705)

> [!warning]
> 不能在安装了 AD FS 的同一服务器上安装 Web 应用程序代理。


若要部署 Web 应用程序代理，必须在将充当 Web 应用程序代理服务器的服务器上安装包含 Web 应用程序代理角色服务的远程访问服务器角色。安装 Web 应用程序代理角色服务的步骤：

1.  在 Web 应用程序代理服务器中的\&quot;服务器管理器\&quot;中，单击\&quot;管理\&quot;，然后单击\&quot;添加角色和功能\&quot;。

2.  在\&quot;添加角色和功能向导\&quot;中，单击\&quot;下一步\&quot;三次，转到\&quot;服务器角色\&quot;页。

3.  在\&quot;服务器角色\&quot;页上，选择列表中的\&quot;远程访问\&quot;，然后单击\&quot;下一步\&quot;。

4.  在\&quot;功能\&quot;页上，单击\&quot;下一步\&quot;。

5.  在\&quot;远程访问\&quot;页上，阅读信息，然后单击\&quot;下一步\&quot;。

6.  在\&quot;角色服务\&quot;页上，选择\&quot;Web 应用程序代理\&quot;。然后在\&quot;添加角色和功能向导\&quot;窗口中，单击\&quot;添加功能\&quot;，然后单击\&quot;下一步\&quot;。

7.  在\&quot;确认\&quot;窗口中，单击\&quot;安装\&quot;。还可以选中\&quot;如果需要，自动重新启动目标服务器\&quot;。

8.  在\&quot;安装进度\&quot;对话框中，验证安装已成功，然后单击\&quot;关闭\&quot;。

以下 Windows PowerShell cmdlet 执行的任务与以上步骤相同。

    Install-WindowsFeature Web-Application-Proxy -IncludeManagementTools

## 第 5 步 - 配置 Web 应用程序代理角色服务（可选）

必须配置 Web 应用程序代理才能连接到 AD FS 服务器。对所有要部署为 Web 应用程序代理服务器的服务器重复此过程。

配置 Web 应用程序角色服务的步骤：

1.  在 Web 应用程序代理服务器中的\&quot;服务器管理器\&quot;中，单击\&quot;工具\&quot;，然后单击\&quot;远程访问管理\&quot;。

2.  在\&quot;配置\&quot;窗格中，单击\&quot;Web 应用程序代理\&quot;。

3.  在\&quot;远程访问管理\&quot;控制台中间的窗格中，单击\&quot;运行 Web 应用程序代理配置向导\&quot;。

4.  在\&quot;Web 应用程序代理配置向导\&quot;中的\&quot;欢迎\&quot;对话框中，单击\&quot;下一步\&quot;。

5.  在\&quot;联合服务器\&quot;页上，执行以下操作，然后单击\&quot;下一步\&quot;：
    
      - 在\&quot;联合身份验证服务名称\&quot;框中，输入 AD FS 服务器的完全限定的域名 (FQDN) - 例如，**adfs.contoso.com**。
    
      - 在\&quot;用户名\&quot;和\&quot;密码\&quot;框中，键入 AD FS 服务器上本地管理员帐户的凭据。

6.  在\&quot;AD FS 代理证书\&quot;对话框中，在当前已安装在 Web 应用程序代理服务器中的证书列表中，选择 Web 应用程序代理要用来执行 AD FS 代理功能的证书，然后单击\&quot;下一步\&quot;。您在此步骤中选择的证书的主题应该是联合身份验证服务名称 - 例如，**adfs.contoso.com**。

7.  在\&quot;确认\&quot;对话框中查看设置。可以根据需要复制 Windows PowerShell cmdlet，以自动进行其他安装。单击\&quot;配置\&quot;。

8.  在\&quot;结果\&quot;对话框中，验证配置已成功，然后单击\&quot;关闭\&quot;。

以下 Windows PowerShell cmdlet 执行的任务与以上步骤相同。

    Install-WebApplicationProxy -CertificateThumprint 1a2b3c4d5e6f1a2b3c4d5e6f1a2b3c4d5e6f1a2b -FederationServiceName adfs.contoso.com

## 第 6 步 - 使用 Web 应用程序代理发布 Outlook Web App 和 EAC（可选）

在第 3 步中，您为 Outlook Web App 和 EAC 创建了信赖方信任。您现在需要发布这两个应用程序。不过，在发布之前，请先确认您是否已为这两个应用程序创建了信赖方信任，并且是否在 Web 应用程序代理服务器上拥有适用于 Outlook Web App 和 EAC 的证书。对于需要由 Web 应用程序代理发布的所有 AD FS 终结点，您必须在 AD FS 管理控制台中，将终结点设置为**代理已启用**。

使用 Web 应用程序代理，按照步骤发布 Outlook Web App。对于 EAC，重复这些步骤即可。发布 EAC 时，需要更改名称、外部 URL、外部证书和后端 URL。

使用 Web 应用程序代理发布 Outlook Web App 和 EAC 的步骤：

1.  在 Web 应用程序代理服务器上的\&quot;远程访问管理\&quot;控制台中，在\&quot;导航\&quot;窗格中，单击\&quot;Web 应用程序代理\&quot;，然后在\&quot;任务\&quot;窗格中，单击\&quot;发布\&quot;。

2.  在\&quot;发布新应用程序向导\&quot;中的\&quot;欢迎\&quot;页上，单击\&quot;下一步\&quot;。

3.  在\&quot;预身份验证\&quot;页上，单击\&quot;Active Directory 联合身份验证服务(AD FS)\&quot;，然后单击\&quot;下一步\&quot;。

4.  在\&quot;信赖方\&quot;页上，在信赖方列表中，为要发布的应用程序选择信赖方，然后单击\&quot;下一步\&quot;。

5.  在\&quot;发布设置\&quot;页上，执行以下操作，然后单击\&quot;下一步\&quot;：
    
    1.  在\&quot;名称\&quot;框中，为此应用程序输入友好名称。此名称只在\&quot;远程访问管理控制台\&quot;中的已发布应用程序列表中使用。您可以使用 **OWA** 和 **EAC** 作为名称。
    
    2.  在\&quot;外部 URL\&quot;框中，为此应用程序输入外部 URL - 例如，为 Outlook Web App 输入 **https://external.contoso.com/owa**，为 EAC 输入 **https://external.contoso.com/ecp**。
    
    3.  在\&quot;外部证书\&quot;列表中，选择主题名称与外部 URL 的主机名称匹配的证书。
    
    4.  在\&quot;后端服务器 URL\&quot;框中，输入后端服务器的 URL。请注意，此值会在输入外部 URL 时自动输入，并且只有在后端服务器 URL 不同时才需要更改此值 - 例如，对于 Outlook Web App 为 **https://mail.contoso.com/owa**，对于 EAC 为 **https://mail.contoso.com/ecp**。
    
    > [!NOTE]
    > Web 应用程序代理可以翻译 URL 中的主机名，但是不能翻译路径。因此，您可以输入不同的主机名，但是必须输入相同的路径。例如，您可以输入外部 URL <em>https://external.contoso.com/app1/</em> 和后端服务器 URL <em>https://mail.contoso.com/app1/</em>。但是，不能输入外部 URL <em>https://external.contoso.com/app1/</em> 和后服务器 URL <em>https://mail.contoso.com/internal-app1/</em>。


6.  在\&quot;确认\&quot;页上，查看设置，然后单击\&quot;发布\&quot;。您可以复制 Windows PowerShell 命令，以便设置其他已发布应用程序。

7.  在\&quot;结果\&quot;页上，确保应用程序已成功发布，然后单击\&quot;关闭\&quot;。

以下 Windows PowerShell cmdlet 执行的任务与 Outlook Web App 的上述步骤相同。

    Add-WebApplicationProxyApplication -BackendServerUrl 'https://mail.contoso.com/owa/' -ExternalCertificateThumbprint 'E9D5F6CDEA243E6E62090B96EC6DE873AF821983' -ExternalUrl 'https://external.contoso.com/owa/' -Name 'OWA' -ExternalPreAuthentication ADFS -ADFSRelyingPartyName 'Outlook Web App'

以下 Windows PowerShell cmdlet 执行的任务与 EAC 的上述步骤相同。

    Add-WebApplicationProxyApplication -BackendServerUrl 'https://mail.contoso.com/ecp/' -ExternalCertificateThumbprint 'E9D5F6CDEA243E6E62090B96EC6DE873AF821983' -ExternalUrl 'https://external.contoso.com/ecp/' -Name 'EAC' -ExternalPreAuthentication ADFS -ADFSRelyingPartyName 'Exchange Admin Center'

完成这些步骤后，Web 应用程序代理会对 Outlook Web App 和 EAC 客户端执行 AD FS 身份验证，还会代表这两个应用程序代理对 Exchange 的连接。您不需要为 Exchange 本身配置 AD FS 身份验证，因此，请继续执行第 10 步，测试您的配置。

## 第 7 步 - 将 Exchange 2013 配置为使用 AD FS 身份验证

对 AD FS 进行配置以用于对 Exchange 2013 中的 Outlook Web App 和 EAC 进行基于声明的身份验证时，必须为 Exchange 组织启用 AD FS。必须使用 [Set-OrganizationConfig](https://technet.microsoft.com/zh-cn/library/aa997443\(v=exchg.150\)) cmdlet 为您的组织配置 AD FS 设置：

  - 将 AD FS 颁发者设置为 **https://adfs.contoso.com/adfs/ls/**。

  - 将 AD FS URI 设置为 **https://mail.contoso.com/owa/** 和 **https://mail.contoso.com/ecp/**。

  - 通过使用 AD FS 服务器上的Windows PowerShell 并输入`Get-ADFSCertificate -CertificateType "Token-signing"`签名证书指纹的 AD FS 标记中找到。然后，指定您找到的令牌签名证书指纹。如果 AD FS 令牌签名证书已过期，必须通过使用[Set-OrganizationConfig](https://technet.microsoft.com/zh-cn/library/aa997443\(v=exchg.150\)) cmdlet 更新从新 AD FS 令牌签名证书的指纹。

在 Exchange 管理外壳程序中运行下面的命令。

    $uris = @(" https://mail.contoso.com/owa/","https://mail.contoso.com/ecp/")
    Set-OrganizationConfig -AdfsIssuer "https://adfs.contoso.com/adfs/ls/" -AdfsAudienceUris $uris -AdfsSignCertificateThumbprint "88970C64278A15D642934DC2961D9CCA5E28DA6B"

> [!NOTE]
> <em>-AdfsEncryptCertificateThumbprint</em>参数不支持这些方案。


有关详细信息和语法，请参阅 [Set-OrganizationConfig](https://technet.microsoft.com/zh-cn/library/aa997443\(v=exchg.150\)) 和 [Get-ADFSCertificate](https://go.microsoft.com/fwlink/?linkid=392706)。

## 第 8 步 - 在 OWA 和 ECP 虚拟目录上启用 AD FS 身份验证

对于 OWA 和 ECP 虚拟目录，将 AD FS 身份验证启用作为唯一的身份验证方法并禁用所有其他形式的身份验证。

> [!CAUTION]
> 配置 OWA 虚拟目录之前必须配置 ECP 虚拟目录。


通过使用 Exchange 管理外壳配置 ECP 虚拟目录。在 Shell 窗口中，运行下面的命令。

    Get-EcpVirtualDirectory | Set-EcpVirtualDirectory -AdfsAuthentication $true -BasicAuthentication $false -DigestAuthentication $false -FormsAuthentication $false -WindowsAuthentication $false

通过使用 Exchange 管理外壳配置 OWA 虚拟目录。在 Shell 窗口中，运行下面的命令。

    Get-OwaVirtualDirectory | Set-OwaVirtualDirectory -AdfsAuthentication $true -BasicAuthentication $false -DigestAuthentication $false -FormsAuthentication $false -WindowsAuthentication $false -OAuthAuthentication $false

> [!NOTE]
> 前面的 Exchange 管理外壳程序命令组织中每个客户端访问服务器上配置的 OWA 和 ECP 的虚拟目录。如果您不想将这些设置应用于所有客户端访问服务器，使用<em>-Identity</em>参数并指定客户端访问服务器。很可能想要将这些设置应用仅将 Internet 客户端访问服务器在您的组织面临着。


有关详细信息和语法，请参阅 [Get-OwaVirtualDirectory](https://technet.microsoft.com/zh-cn/library/aa998588\(v=exchg.150\)) 和 [Set-OwaVirtualDirectory](https://technet.microsoft.com/zh-cn/library/bb123515\(v=exchg.150\)) 或 [Get-EcpVirtualDirectory](https://technet.microsoft.com/zh-cn/library/dd351058\(v=exchg.150\)) 和 [Set-EcpVirtualDirectory](https://technet.microsoft.com/zh-cn/library/dd297991\(v=exchg.150\))。

## 第 9 步 - 重启或再循环 Internet Information Services (IIS)

完成全部所需步骤（包括对 Exchange 虚拟目录进行更改）后，您需要重新启动 Internet 信息服务。为此，可以使用下列方法之一：

  - 使用 Windows PowerShell：
    
        Restart-Service W3SVC,WAS -noforce

  - 使用命令行：单击\&quot;开始\&quot;，再单击\&quot;运行\&quot;，键入 `IISReset /noforce`，然后单击\&quot;确定\&quot;。

  - 使用 Internet 信息服务 (IIS) 管理器：在\&quot;服务器管理器\&quot;\>\&quot;IIS\&quot;中，单击\&quot;工具\&quot;，然后单击\&quot;Internet 信息服务(IIS)管理器\&quot;。在\&quot;Internet 信息服务(IIS)管理器\&quot;窗口中，在\&quot;管理服务器\&quot;下的操作窗格中，单击\&quot;重新启动\&quot;。

## 第 10 步 - 为 Outlook Web App 和 EAC 测试 AD FS 声明

若要为 Outlook Web App 测试 AD FS 声明，请执行以下操作：

  - 在您的 Web 浏览器中，登录 Outlook Web App（例如，**https://mail.contoso.com/owa**）。

  - 在浏览器窗口中，如果您看到证书错误，只需继续转到 Outlook Web App 网站即可。您应该会重定向到 ADFS 登录页面或 ADFS 凭据提示页面。

  - 键入您的用户名（域/用户）和密码，然后单击\&quot;登录\&quot;。

此时，系统会在窗口中加载 Outlook Web App。

为 EAC 测试 AD FS 声明的步骤：

1.  在 Web 浏览器中，转到 **https://mail.contoso.com/ecp**。

2.  在浏览器窗口中，如果您看到证书错误，只需继续转到 ECP 网站即可。您应该会重定向到 ADFS 登录页面或 ADFS 凭据提示页面。

3.  键入您的用户名（域/用户）和密码，然后单击\&quot;登录\&quot;。

4.  EAC 应该会在窗口中加载。

## 您可能希望了解的其他信息

**多重身份验证**

对于本地 Exchange 2013 SP1 部署，使用声明部署和配置 Active Directory 联合身份验证服务 (AD FS) 2.0 意味着 Exchange 2013 SP1 中的 Outlook Web App 和 EAC 可以支持多重身份验证方法，例如基于证书的身份验证、身份验证或安全令牌，以及指纹身份验证。双重身份验证常常会与其他形式的身份验证混淆。多重身份验证需要使用三个身份验证要素中的两个。这些因素是：

  - 只有用户才知道的信息（例如密码、PIN 或模式）

  - 只有用户才有的东西（例如 ATM 卡、安全令牌、智能卡或移动电话）

  - 只有用户本身才拥有的东西（例如生物特征，指纹）

有关 Windows Server 2012 R2 中多重身份验证的详细信息，请参阅[概述：使用适用于敏感应用程序的附加多重身份验证管理风险](https://go.microsoft.com/fwlink/?linkid=392707)和[操作实例：使用适用于敏感应用程序的附加多重身份验证管理风险](https://go.microsoft.com/fwlink/?linkid=392708)。

在 Windows Server 2012 R2 AD FS 角色服务中，联合身份验证服务充当安全令牌服务，提供用于声明的安全令牌，并为你提供支持多重身份验证的功能。联合身份验证服务根据提供的凭据颁发令牌。在帐户存储验证用户的凭据之后，便会根据信任策略的规则生成用户声明，然后将其添加到颁发给客户端的安全令牌中。有关声明的详细信息，请参阅[了解声明](https://go.microsoft.com/fwlink/?linkid=392709)。

**与其他版本的 Exchange 共存**

如果您的组织中部署有多个版本的 Exchange，也可以对 Outlook Web App 和 EAC 使用 AD FS 身份验证。此方案只支持 Exchange 2010 和 Exchange 2013 部署。只有当所有客户端均要通过 Exchange 2013 服务器进行连接，**且**这些 Exchange 2013 服务器已配置 AD FS 身份验证时，才支持此方案。

在 Exchange 2010 服务器上有邮箱的用户可以通过已配置 AD FS 身份验证的 Exchange 2013 服务器来访问自己的邮箱。对 Exchange 2013 服务器的初始客户端连接使用的是 AD FS 身份验证。不过，对 Exchange 2010 服务器的代理连接使用的是 Kerberos。不支持通过其他任何方式来为 Exchange Server 2010 直接配置 AD FS 身份验证。

