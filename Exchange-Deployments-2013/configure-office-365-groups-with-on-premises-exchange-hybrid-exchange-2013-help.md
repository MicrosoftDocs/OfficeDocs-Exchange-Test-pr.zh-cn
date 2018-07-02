---
title: '使用本地 Exchange 混合配置 Office 365 组: Exchange 2013 Help'
TOCTitle: 使用本地 Exchange 混合配置 Office 365 组
ms:assetid: 184dfcfe-4b8e-450a-adc6-e647213b9501
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Mt668829(v=EXCHG.150)
ms:contentKeyID: 72513077
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 使用本地 Exchange 混合配置 Office 365 组

 

_<strong>上一次修改主题：</strong>2016-12-06_

了解如何使本地 Exchange 用户在混合部署中使用 Office 365 组。

组是 Office 365 的一项服务，它使团队能够更轻松地进行通信、安排会议以及就文档进行协作。任何组成员都可使用与组共享的所有信息，包括从发送到组的电子邮件到存储在组的 OneDrive for Business 或 SharePoint 库中的文件。如果已在本地 Exchange 组织和 Office 365 之间配置了混合部署，则可按照本主题中的步骤使在 Office 365 中创建的组对本地用户可用。

> [!IMPORTANT]
> 对 Exchange 混合部署中的本地用户使用 Office 365 组是一项新功能。因为是新功能，所以可能会在设置时遇到一些问题。请务必查看本主题结尾的已知问题部分，了解可能遇到的问题的修复方法。


## 先决条件

开始前，请确保完成以下操作：

  - 已为租户购买 Azure Active Directory Premium 许可证。这是在 Azure Active Directory Connect 中启用组写回功能所必需的。

  - 已在 Exchange 本地组织和 Office 365 之间配置混合部署并验证它能够正常运行。有关 Exchange 混合部署的详细信息，请参阅以下内容：
    
      - [Exchange Server 混合部署](exchange-server-hybrid-deployments-exchange-2013-help.md)
    
      - [混合部署先决条件](hybrid-deployment-prerequisites-exchange-2013-help.md)

  - 在 CU1 和较新版本的 Exchange 2016，以及 CU11 和较新版本的 Exchange 2013 中提供了与 Office 365 组集成的安装了受支持 Exchange 版本的本地 Exchange。但是，Exchange 混合需要在本地 Exchange 服务器上安装最新的 Exchange 2013 或 Exchange 2016 累积更新 (CU)。如果不能安装最新的 CU，也可使用当前 CU 的上一发布更新。

  - 配置的单一登录使用 Azure Active Directory Connect (Azure AD Connect)。需要这些信息来允许用户单击“**查看组文件**”或组电子邮件中的云附件链接。
    
    在 Exchange 混合部署中为单一登录配置 Azure AD 连接时，建议使用密码同步。在下列情况下，应仅使用 Active Directory 联合身份验证服务 (AD FS)：你在大型组织中、你有一个复杂的本地 Active Directory 部署（例如，多个 Active Directory 林）、另一个 Microsoft 产品需要 AD FS 与 Office 365 配合使用，或者因为合规性策略无法同步本地网络之外的密码。有关单一登录的详细信息，请参阅[将本地标识与 Azure Active Directory 集成](http://go.microsoft.com/fwlink/p/?linkid=723513)。

## 启用 Azure AD Connect 中的组写回

1.  在 Azure AD Connect 向导中，选择“**自定义同步选项**”，然后单击“**下一步**”。

2.  在“**连接到 Azure AD**”页中，输入你的 Office 365 和本地凭据。单击“**下一步**”。

3.  在“**可选功能**”页上，验证以前配置的选项是否仍处于选中状态。最常选择的选项是“**Exchange 混合**”和“**密码哈希同步**”。

4.  选择“**组写回**”，然后单击“**下一步**”。

5.  在“**写回**”页上，选择 Active Directory 组织单位 (OU) 以存储从 Office 365 同步到本地组织的对象，然后单击“**下一步**”。

6.  在“**准备配置**”页上，单击“**配置**”。

7.  完成向导后，在“**配置完成**”页上单击“**退出**”。

8.  打开 Active Directory 域控制器上的 Active Directory 用户和计算机，然后找到开头为 **AAD\_** 的用户帐户。记下此帐户的名称。

9.  在本地 Exchange 服务器上打开 Exchange 命令行管理程序，并运行以下命令。
    
        $AzureADConnectSWritebackAccount = <AAD_ account name from step 8>
        
        $GroupsOU = <writeback Active Directory OU selected in step 5>
        
        Import-Module "C:\Program Files\Microsoft Azure Active Directory Connect\AdPrep\AdSyncPrep.psm1"
        
        Initialize-ADSyncGroupWriteBack -ADConnectorAccount $AzureADConnectSWritebackAccount -GroupWriteBackContainerDN $GroupsOU

## 配置组域

Office 365 组的主 SMTP 域称为*组域*。默认情况下，组织中默认的接受域会被选作组域。如果想要添加专用组域，可以使用下列步骤添加域。有关 Office 365 组的多域支持的详细信息，请参阅 [Multi-domain support for Office 365 Groups](https://support.office.com/en-us/article/multi-domain-support-for-office-365-groups-admin-help-7cf5655d-e523-4bc3-a93b-3ccebf44a01a)（Office 365 组的多域支持）

1.  将新域添加到 Office 365 组织。如需有关将域添加到 Office 365 的帮助，请参阅 [Add users and domains to Office 365](https://support.office.com/en-us/article/add-users-and-domain-to-office-365-6383f56d-3d09-4dcb-9b41-b5f5a5efd611?ui=zh-cn%26rs=zh-cn%26ad=cn)（将用户和域添加到 Office 365）

2.  使用以下命令，添加该组域作为本地 Exchange 组织中的接受域。需要执行该操作，以使用混合发送连接器将出站邮件传递到 Office 365 中的组域。
    
        New-AcceptedDomain -Name groups.contoso.com -DomainName groups.contoso.com -DomainType InternalRelay

3.  使用 DNS 提供程序创建以下公用 DNS 记录。
    
    
    <table>
    <colgroup>
    <col style="width: 33%" />
    <col style="width: 33%" />
    <col style="width: 33%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th><p>DNS 记录名称</p></th>
    <th><p>DNS 记录类型</p></th>
    <th><p>DNS 记录值</p></th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>groups.contoso.com</p></td>
    <td><p>MX</p></td>
    <td><p>groups-contoso-com.mail.protection.outlook.com</p>
    > [!NOTE]
    > 此 DNS 记录值的格式是 <em>&lt;domain key&gt;</em>.mail.protection.outlook.com。要找出你的域密钥是什么，请参阅<a href="https://support.office.com/zh-cn/article/gather-the-information-you-need-to-create-office-365-dns-records-77f90d4a-dc7f-4f09-8972-c1b03ea85a67?ui=zh-cn%26rs=zh-cn%26ad=cn">收集创建 Office 365 DNS 记录所需的信息</a>。

</td>
    </tr>
    <tr class="even">
    <td><p>autodiscover.groups.contoso.com</p></td>
    <td><p>CNAME</p></td>
    <td><p>autodiscover.outlook.com</p></td>
    </tr>
    </tbody>
    </table>
    
    > [!CAUTION]
	> 如果将组域的 MX DNS 记录设置为本地 Exchange 服务器，则本地 Exchange 组织用户和 Office 365 组用户之间的邮件流将不能正常工作。
    
4.  使用以下命令，将组域添加到由本地 Exchange 组织中的混合配置向导创建的混合发送连接器中。
    
        Set-SendConnector -Identity "Outbound to Office 365" -AddressSpaces "contoso.mail.onmicrosoft.com","groups.contoso.com"
    
    > [!NOTE]
    > 如果未更新发送连接器，或未将组域添加为本地 Exchange 组织中的接受域，则不会将从本地邮箱发送的邮件传递至组，除非将该组配置为接收来自外部发件人的邮件。


## 您如何知道这有效？

若要确保组可以正常使用 Exchange 混合部署，应使用本地邮箱以及已从本地组织移动到 Office 365 的邮箱对其进行测试。使用以下各部分中的步骤执行每个测试。

## 使用本地邮箱进行测试

1.  将本地邮箱添加到 Office 365 组。

2.  将 Office 365 邮箱添加到同一 Office 365 组。

3.  使用 Outlook 网页版登录到 Office 365 邮箱。

4.  使用 Office 365 邮箱向组发送邮件。

5.  使用 Outlook 2016 或 Outlook 网页版打开本地邮箱。

6.  验证邮箱收到包含发送到 Office 365 组的文章的电子邮件。

7.  在同一邮箱中，撰写邮件回复并将其发送到组。

8.  验证邮件可由所有组成员查看。

## 使用移动到 Office 365 的邮箱进行测试

1.  将邮箱从本地 Exchange 组织移动到 Office 365。

2.  向 Office 365 组添加邮箱。

3.  在新的浏览器会话中，登录已移动到 Office 365 的邮箱。

4.  在 Outlook 网页版中，验证该组在左侧导航栏中列出。

5.  向组发送邮件。

6.  验证邮件可由所有组成员查看。

## 已知问题

  - **不会显示移动到 Office 365 的邮箱的组** 在将用户从本地 Exchange 组织移动到 Office 365 时，该组不会显示在 Outlook 或 Outlook 网页版中的左侧导航窗格中。若要解决此问题，将该邮箱从其所属的任何组中删除，并将其重新添加到每个组。

  - **不会在本地 Exchange 全局地址列表 (GAL) 中显示新组** 在 Office 365 中创建新组时，该组不会自动显示在本地 GAL 中。若要解决此问题，在本地 Exchange 服务器上打开 Exchange 命令行管理程序，并运行以下命令。
    
        Update-Recipient "<group name>"

  - **组不接收来自本地用户的邮件** 在以下条件为 true 时，本地用户将无法向 Office 365 组发送邮件。
    
      - 将组域配置为本地 Exchange 组织中的权威域。
    
      - 最近创建了该组，且其信息尚未写回到本地 Active Directory。
    
    当 Azure AD Connect 在 Office 365 和本地组织间执行其下一同步时，该问题将自行解决。每隔三十分钟进行一次 Azure AD Connect 同步。

  - **本地用户不能使用包含在组邮件页脚中的链接** 本地用户不能使用包含在向其发送的每个组邮件的页脚中的“**查看组对话**”或“**取消订阅**”链接。若要取消组订阅，本地用户需要与组管理员联系。

  - **发送到组的辅助 SMTP 地址的邮件传送失败** 向某个组添加多个电子邮件地址时，仅将主 SMTP 地址写回到本地 Active Directory。如果某个本地用户尝试将邮件发送到某个组的辅助 SMTP 地址，则邮件将无法传送。若要避免此问题，请仅在每个组上配置一个 SMTP 地址。

  - **本地用户不能成为某个组的管理员** 本地用户不能直接访问组空间。因此，不能将他们添加为组管理员。

  - **如果启用集中式邮件流，外部邮件传送到组可能失败**如果启用集中式邮件流，外部用户发送给组的邮件将传送失败，即使该组允许来自外部发件人的邮件。

  - **本地用户不能作为一个组发送邮件** 本地用户尝试作为 Office 365 组发送邮件会收到权限拒绝错误，即使他们被授予了以组发送权限。以组发送权限只适合 Exchange Online 邮箱用户。

  - **从 Outlook 的左侧导航窗格中选择一个未打开组邮箱的组** Outlook 使用自动发现 URL 打开组邮箱。如果一个组的主电子邮件地址在一个不指向 Office 365 的自动发现 URL (autodiscover.outlook.com) 的域中，Outlook 将无法打开组的邮箱。若要解决此问题，可以使用指向 Office 365 自动发现 URL 的域中的主地址设置组。可以配置电子邮件地址策略，以将主电子邮件添加至每个指向 Office 365 自动发现 URL 的组邮箱。有关详细信息，请查阅 [Multi-domain support for Office 365 Groups](https://support.office.com/en-us/article/multi-domain-support-for-office-365-groups-admin-help-7cf5655d-e523-4bc3-a93b-3ccebf44a01a)（Office 365 组的多域支持）

