---
title: 'Configure Exchange to support delegated mailbox permissions in a hybrid deployment: Exchange 2013 Help'
TOCTitle: Configure Exchange to support delegated mailbox permissions in a hybrid deployment
ms:assetid: a2a10cb3-4557-4ff5-8191-c653522f4512
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Mt784505(v=EXCHG.150)
ms:contentKeyID: 74447332
ms.date: 02/01/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configure Exchange to support delegated mailbox permissions in a hybrid deployment

 

_<strong>上一次修改主题：</strong>2018-01-30_

Delegated mailbox permissions enable someone to manage some part of another users's mailbox. A common example of this is an administrative assistant who needs to manage an executive's mailbox and calendar. Hybrid deployments between an on-premises Exchange organization and Office 365 support the **Full Access** and **Send on Behalf of** delegated mailbox permissions. However, depending on the version of Exchange you have installed in your on-premises organization, you might need to perform additional configuration to use delegated mailbox permissions in a hybrid deployment. The following lists the versions of Exchange that support delegated mailbox permissions in a hybrid deployment and whether additional configuration is needed for that version.

  - **Exchange 2016** No additional configuration is required.

  - **Exchange 2013** A supported Exchange 2013 cumulative update (CU) and additional configuration are required.

  - **Exchange 2010** A supported Exchange 2010 update roll (RU) and additional configuration are required.

For more information about the specific requirements to support delegated mailbox permissions in a hybrid deployment, take a look at [Permissions in Exchange hybrid deployments](permissions-in-exchange-hybrid-deployments-exchange-2013-help.md).

The following sections step you through the configuration of Exchange 2013 and Exchange 2010 on-premises deployments to enable support for delegated mailbox permissions. Before you follow these steps, you need to make sure you're on the latest Exchange 2013 CU or Exchange SP3 RU. For more information, see [混合部署先决条件](hybrid-deployment-prerequisites-exchange-2013-help.md).

## Exchange 2013

What you need to do to enable support for delegated mailbox permissions depends on a few factors. If you moved mailboxes to Office 365 and at that time:


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>The following was installed...</th>
<th>And ACLable object synchronization at the organization was...</th>
<th>Then you need to...</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange 2013 CU9 or earlier</p></td>
<td><p>This feature isn't available in Exchange 2013 CU9 and earlier.</p></td>
<td><p>Manually configure each mailbox to support ACLs</p></td>
</tr>
<tr class="even">
<td><p>Exchange 2013 CU10 or later</p></td>
<td><p>Disabled</p></td>
<td><ol>
<li><p>Enable ACLable object synchronization at the organization level</p></li>
<li><p>Manually enable ACLs on each mailbox moved to Office 365 before ACLable object synchronization was enabled at the organization level.</p></li>
</ol>
<p>No additional configuration is needed for mailboxes moved to Office 365 after ACLable object synchronization is enabled at the organization level.</p></td>
</tr>
<tr class="odd">
<td><p>Exchange 2013 CU10 or later</p></td>
<td><p>Enabled</p></td>
<td><p>No additional configuration is needed</p></td>
</tr>
</tbody>
</table>


## Enable ACLable object synchronization

To enable ACLable object synchronization at the organization level, do the following.

1.  Install the latest version of Azure Active Directory Connect (AAD Connect) on all of your AAD Connect servers. This is needed to allow AAD Connect to synchronize the attributes needed to support hybrid permissions. You can download AAD Connect from [Microsoft Azure Active Directory Connect](http://go.microsoft.com/fwlink/p/?linkid=510956).

2.  Open the Exchange Management Shell on a server running the latest available Exchange 2013 CU, or the immediately previous CU.

3.  Run the following command.
    
        Set-OrganizationConfig -ACLableSyncedObjectEnabled $True

After you do this, any mailboxes that you move to Office 365 will be properly configured to support delegated mailbox permissions. If mailboxes were moved to Office 365 prior to you completing these steps, you'll need to manually enable ACLs on those mailboxes using the steps in Enable ACLs on remote mailboxes.

> [!IMPORTANT]
> ACLs aren't enabled on remote mailboxes created in Office 365. If you create a remote mailbox in Office 365, you'll need to follow the steps in the Enable ACLs on remote mailboxes section to enable ACLs on that remote mailbox. To avoid this extra step, we recommend that you create the mailbox on an on-premises Exchange server and then move the mailbox to Office 365.


## Enable ACLs on remote mailboxes

To enable ACLs on mailboxes moved to Office 365 before ACLable object synchronization was enabled at the organization level, do the following.

1.  Open the Exchange Management Shell on a server running the latest available Exchange 2013 CU, or the immediately previous CU.

2.  To enable ACLs on a single mailbox, run the following command.
    
        Get-AdUser <Identity> | Set-AdObject -Replace @{msExchRecipientDisplayType=-1073741818}

3.  To enable ACLs on all mailboxes moved to Office 365, run the following command.
    
        Get-RemoteMailbox | ForEach { Get-AdUser -Identity $_.Guid | Set-ADObject -Replace @{msExchRecipientDisplayType=-1073741818}}

4.  To verify that the mailboxes have been successfully updated, run the following command.
    
        Get-RemoteMailbox | ForEach { Get-AdUser -Identity $_.Guid -Properties msExchRecipientDisplayType | Format-Table -AutoSize DistinguishedName, msExchRecipientDisplayType}

## Exchange 2010

Exchange 2010 SP3 servers support the configuration of ACLs on remote mailboxes, however, this configuration needs to be set manually on each mailbox. Unlike newer versions of Exchange, Exchange 2010 doesn't provide the ability to set this feature at the organization level. You need to follow the steps below on any mailboxes that you've previously moved to Office 365, and on any mailboxes that will be moved from an Exchange 2010 SP3 server to Office 365 in the future.

## Enable ACLs on remote mailboxes

To enable ACLs on mailboxes moved to Office 365, do the following.

1.  Open the Exchange Management Shell on a server running the latest available Exchange 2010 SP3 RU, or the immediately previous RU.

2.  To enable ACLs on a single mailbox, run the following command.
    
        Get-AdUser <Identity> | Set-AdObject -Replace @{msExchRecipientDisplayType=-1073741818}

3.  To enable ACLs on all mailboxes moved to Office 365, run the following command.
    
        Get-RemoteMailbox | ForEach { Get-AdUser -Identity $_.Guid | Set-ADObject -Replace @{msExchRecipientDisplayType=-1073741818}}

4.  To verify that the mailboxes have been successfully updated, run the following command.
    
        Get-RemoteMailbox | ForEach { Get-AdUser -Identity $_.Guid -Properties msExchRecipientDisplayType | Format-Table -AutoSize DistinguishedName, msExchRecipientDisplayType}

