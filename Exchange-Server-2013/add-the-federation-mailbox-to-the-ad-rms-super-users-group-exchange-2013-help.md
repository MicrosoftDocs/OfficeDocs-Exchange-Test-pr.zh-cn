---
title: '将联合身份验证邮箱添加到 AD RMS 超级用户组: Exchange 2013 Help'
TOCTitle: 将联合身份验证邮箱添加到 AD RMS 超级用户组
ms:assetid: 44618df9-54f0-4474-a450-dcba48a02901
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Ee424431(v=EXCHG.150)
ms:contentKeyID: 50490387
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 将联合身份验证邮箱添加到 AD RMS 超级用户组

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2016-12-09_

对于下列 Microsoft Exchange Server 2013信息权限管理 (IRM) 功能以启用，必须添加到您的组织的[Active Directory Rights Management Services (AD RMS)](https://technet.microsoft.com/en-us/library/hh831364.aspx)群集上的超级用户组联盟邮箱 （ Exchange 2013安装程序所创建的系统邮箱）︰

  - Microsoft OfficeOutlook Web App 中的 IRM

  - Exchange ActiveSync 中的 IRM

  - 日记报告解密

  - 传输解密

您可以配置为已启用邮件的通讯组，AD RMS.成员的通讯组中的超级用户组授予所有者从 AD RMS 群集请求许可证时使用许可证。这允许他们解密发布该群集的所有 RMS 保护内容。是否使用现有的通讯组或创建通讯组并将其配置为 AD RMS 中的超级用户组，则建议您将通讯组专门为此目的并配置适当的设置审批、 审核，并监视成员身份的更改。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876845.Caution(EXCHG.150).gif" title="小心" alt="小心" />小心：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在 AD RMS 配置超级用户组允许该组的成员能够解密受 IRM 保护的内容。我们建议您采取有力措施，对控制和监视的组成员身份并启用审核跟踪成员身份的更改。此外可以通过将组配置为受限制的组使用组策略来限制不必要对组成员身份的更改。有关详细信息，请参阅<a href="https://technet.microsoft.com/en-us/library/cc756802(v=ws.10).aspx">受限制的组策略设置</a>。</td>
</tr>
</tbody>
</table>


关于 IRM 的更多管理任务，请参阅[信息权限管理过程](information-rights-management-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：15 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [收件人权限](recipients-permissions-exchange-2013-help.md)主题中的\&quot;通讯组\&quot;条目。

  - 必须在 Active Directory 林中部署一个 AD RMS 群集。

  - 如果超级用户组已配置 AD RMS 群集上，对通讯组成员身份的任何修改可能需要 24 小时刷新由 AD RMS 群集。这是在群集上的组成员身份缓存的结果。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

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

## 步骤 1︰ 使用 Shell 将联盟邮箱添加到通讯组

如果已经创建并配置为 AD RMS 群集中的超级用户组的通讯组，您可以为该组的成员添加Exchange 2013联盟邮箱。如果没有配置超级用户组，必须创建一个通讯组并将联盟邮箱添加为成员。

1.  创建通讯组用作 AD RMS 超级用户组专用。有关详细信息，请参阅[创建和管理通讯组](create-and-manage-distribution-groups-exchange-2013-help.md)。

2.  新建通讯组中添加用户**FederatedEmail.4c1f4d8b-8179-4148-93bf-00a95fa1e042** 。联合身份验证邮箱是系统邮箱，因此 EAC 中不可见。若要将它添加到通讯组，必须使用[Add-DistributionGroupMember](https://technet.microsoft.com/zh-cn/library/bb124340\(v=exchg.150\)) cmdlet 从外壳。
    
    此示例将联合邮箱添加到 ADRMSSuperUsers 通讯组。
    
        Add-DistributionGroupMember ADRMSSuperUsers -Member FederatedEmail.4c1f4d8b-8179-4148-93bf-00a95fa1e042

有关语法和参数的详细信息，请参阅 [Add-DistributionGroupMember](https://technet.microsoft.com/zh-cn/library/bb124340\(v=exchg.150\))。

## 步骤 2︰ 使用 AD RMS 设置超级用户组

AD RMS 群集上执行下列步骤。若要执行此过程时使用的帐户必须是 AD RMS 服务器上本地 AD RMS 企业管理员组的成员。

1.  打开 Active Directory 权限管理服务控制台，并展开 AD RMS 群集。

2.  在控制台树中，展开\&quot;安全策略\&quot;，然后单击\&quot;超级用户\&quot;。

3.  在操作窗格中，单击\&quot;启用超级用户\&quot;。

4.  在结果窗格中，单击\&quot;更改超级用户组\&quot;以打开\&quot;超级用户\&quot;属性表。

5.  在\&quot;超级用户组\&quot;框中，键入在上一过程中创建的通讯组的电子邮件地址，或单击\&quot;浏览\&quot;选择通讯组。

## 您如何知道这有效？

向新的或现有通讯组添加了联盟邮箱之后，使用 [Get-DistributionGroupMember](https://technet.microsoft.com/zh-cn/library/aa996367\(v=exchg.150\)) cmdlet 检查组的成员身份。

有关如何检查通讯组成员身份的示例，请参阅 **Get-DistributionGroupMember** 中的[Examples](https://technet.microsoft.com/zh-cn/aa996367\(exchg.150\)#examples)。

使用 AD RMS 设置超级用户组之后，可以使用以下方法来验证超级用户组配置是否正确。此外，您可以使用[Test-IRMConfiguration](https://technet.microsoft.com/zh-cn/library/dd979798\(v=exchg.150\)) cmdlet 以验证 IRM 功能。

  - 使用 AD RMS 控制台验证是否已将正确的组配置为超级用户组。

  - 在 AD RMS 服务器上运行以下 PowerShell 命令检索该超级用户组。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>在 Windows Server 2008 R2 和更高版本上提供了 ADRMSAdmin PowerShell 模块。</td>
    </tr>
    </tbody>
    </table>
    
        Import-Module ADRMSAdmin
        New-PSDrive -Name MyRmsAdmin -PsProvider AdRmsAdmin -Root https://localhost 
        Get-ItemProperty -Path MyRmsAdmin:\SecurityPolicy\SuperUser

