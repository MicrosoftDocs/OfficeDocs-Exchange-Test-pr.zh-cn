---
title: 'Permissions in Exchange hybrid deployments: Exchange 2013 Help'
TOCTitle: Permissions in Exchange hybrid deployments
ms:assetid: 58b46b2c-a6b2-424a-8fc2-0f1fe1ad8e18
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ906433(v=EXCHG.150)
ms:contentKeyID: 51408299
ms.date: 05/05/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Permissions in Exchange hybrid deployments

 

_<strong>适用于：</strong>Exchange Server 2013, Exchange Server 2016_

_<strong>上一次修改主题：</strong>2018-05-02_

The Exchange Online in Office 365 organization is based on Exchange Server and, like on-premises organizations, it also uses Role Based Access Control (RBAC) to control permissions. Administrators are granted permissions using management role groups, and end users are granted permissions using management role assignment policies.

Learn more about permissions in Exchange Online and on-premises Exchange at: [权限](https://technet.microsoft.com/zh-cn/library/dd351175\(v=exchg.150\))

## Administrator permissions

By default, the user that was used to create the Office 365 tenant is made a member of the Organization Management role group in the Exchange Online organization. This user can manage the entire Exchange Online organization, including configuration of organization-level settings and management of Exchange Online recipients.

You can add additional administrators in the Exchange Online organization, depending on the management that needs to take place. For example, you can add additional organization administrators and recipient administrators, enable specialist users to perform compliance tasks such as discovery, configure custom permissions, and more. All Exchange Online permissions management for Office 365 administrators must be performed in the Exchange Online organization using either the Exchange Administration Center (EAC) or remote PowerShell.

> [!IMPORTANT]
> There is no transfer of permissions between the on-premises organization and the Office 365 organization. Permissions that you've defined in the on-premises organization must be re-created in the Office 365 organization.


For more information, see [管理角色组](https://technet.microsoft.com/zh-cn/library/jj657480\(v=exchg.150\)) and [管理角色组成员](https://technet.microsoft.com/zh-cn/library/jj657492\(v=exchg.150\)).

## Delegate mailbox permissions

In on-premises Exchange deployments, users can be granted a variety of permissions to other users' mailboxes. This is called delegated mailbox permissions and it's useful when an administrative assistant needs to manage some part of another users's mailbox; for example, managing an executive's calendar. Exchange hybrid deployments support the use of some, but not all, mailbox permissions between mailboxes located in an on-premises Exchange organization and mailboxes located in Office 365. The following sections detail which permission are, and aren't, supported; additional configuration required to support hybrid mailbox permissions; and how mailbox permissions are synchronized between your on-premises organization and Office 365.

## Mailbox permissions supported in hybrid environments

The following permissions **are** supported:

  - **Full Access** A mailbox on an on-premises Exchange server can be granted the **Full Access** permission to an Office 365 mailbox, and vice versa. For example, an Office 365 mailbox can be granted the **Full Access** permission to an on-premises shared mailbox. Users need to open the mailbox using the Outlook desktop client; cross-premises mailbox permissions aren't supported in Outlook on the web.
    
    > [!NOTE]
    > Users might receive additional credential prompts when they first access a mailbox that’s in the other organization and add it to their Outlook profile.


  - **Send on Behalf of** A mailbox on an on-premises Exchange server can be granted the **Send on Behalf of** permission to an Office 365 mailbox, and vice versa. For example, an Office 365 mailbox can be granted the **Send on Behalf of** permission to an on-premises shared mailbox. Users need to open the mailbox using the Outlook desktop client; cross-premises mailbox permissions aren't supported in Outlook on the web.
    
    Some changes are needed on your Azure Active Directory Connect server for Send on Behalf of permissions to sync between your on-premises Exchange servers and Exchange Online. For details, see Enabling support for hybrid mailbox permissions in Azure Active Directory Connect later in this topic.

  - **Private items** When adding a delegate the option can be configured to allow a user with folder permissions to see private calendar items.

> [!NOTE]
> As of February 2018 the feature to support Full Access and Send on Behalf Of is being rolled out and expected to be complete by the second quarter of 2018.


The following permissions or capabilities **aren't** supported:

  - **Send-As** Lets a user send mail as though it appears to be coming from another user's mailbox.

  - **Auto-mapping** Enables Outlook, when it starts, to automatically open any mailboxes that a user has been granted **Full Access** to.

  - **Folder permissions** Grants access to the contents of a particular folder.

Any mailboxes that receive these permissions from another mailbox need to be moved at the same time as the granting mailbox. If a mailbox receives permissions from multiple mailboxes, that mailbox, and all of the mailboxes granting permissions to it, need to be moved at the same time.

## Configuring your on-premises Exchange servers to support hybrid mailbox permissions

To enable Full Access and Send on Behalf of permissions in a hybrid deployment, additional configuration changes might be necessary depending on the version of Exchange you have installed. The following table shows which versions of Exchange support delegated mailbox permissions in a hybrid deployment with Office 365 and what additional configuration is needed. For steps on how to configure Exchange 2013 and 2010 servers and mailboxes to support ACLs, see [Configure Exchange to support delegated mailbox permissions in a hybrid deployment](configure-exchange-to-support-delegated-mailbox-permissions-in-a-hybrid-deployment-exchange-2013-help.md).


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Exchange version</th>
<th>Prerequisites</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange 2016</p></td>
<td><p>No additional configuration required.</p></td>
</tr>
<tr class="even">
<td><p>Exchange 2013</p></td>
<td><p>Exchange 2013 servers need the following:</p>
<ul>
<li><p>The latest cumulative update (CU), or the immediately previous CU, installed. Exchange 2013 servers running older CUs aren't supported and may not work with delegated mailbox permissions in a hybrid deployment.</p></li>
<li><p>The Exchange organization is configured to allow access control lists (ACLs) to be stamped on mail objects and synchronized with Office 365.</p></li>
<li><p>On-premises remote mailboxes associated with mailboxes moved to Office 365 prior to Exchange 2013 CU10 need to be manually configured to support ACLs. Remote mailboxes, created on servers running Exchange 2013 CU10 or later, and after the Exchange organization is set to allow ACLs, are configured automatically.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Exchange 2010</p></td>
<td><p>Exchange 2010 SP3 servers need the following:</p>
<ul>
<li><p>The latest update rollup (RU), or the immediately previous RU, installed. Exchange 2010 SP3 servers running older RU aren't supported and may not work with delegated mailbox permissions in a hybrid deployment.</p></li>
<li><p>On-premises remote mailboxes associated with Office 365 mailboxes need to be configured to support ACLs. This needs to be done for each on-premises remote mailbox that's associate with an Office 365 mailbox.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Exchange 2007 or earlier</p></td>
<td><p>Not supported.</p></td>
</tr>
</tbody>
</table>


## Enabling support for hybrid mailbox permissions in Azure Active Directory Connect

In addition to configuring your on-premises Exchange servers, you also need to make sure Azure Active Directory Connect (AAD Connect) server is set up to synchronize hybrid mailbox permissions. Here's what you need to do to make sure your AAD Connect server is ready to support these permissions:

  - **Upgrade AAD Connect** AAD Connect needs to be upgraded to at least version 1.1.553.0. You can download the latest version of AAD Connect from [Microsoft Azure Active Directory Connect](http://go.microsoft.com/fwlink/p/?linkid=510956).

  - **Enable Exchange Hybrid in AAD Connect** To synchronize the attributes that enable hybrid mailbox permissions (specifically the Send on Behalf of permission), you need to make sure that the **Exchange Hybrid deployment** configuration option is enabled in AAD Connect. For information about how to run the AAD Connect installation wizard again to update its configuration, check out [Azure AD Connect sync: Running the installation wizard a second time](https://docs.microsoft.com/en-us/azure/active-directory/connect/active-directory-aadconnectsync-installation-wizard)

## How mailbox permissions are synchronized between your on-premises and Office 365 organizations

## End user permissions

As with administrator permissions, end users in Exchange Online can be granted permissions. By default, end users are granted permissions via the default role assignment policy. This policy is applied to every mailbox in the Exchange Online organization. If the permissions granted by default are sufficient, you don't need to change anything.

If you do want to customize end user permissions, you can either modify the existing default role assignment policy, or you can create new assignment policies. If you create multiple assignment policies, you can assign different policies to different groups of mailboxes, enabling you to control permissions granted to each group depending on their requirements. All permissions management for Exchange Online end users must be performed in the Exchange Online organization using either the EAC or remote PowerShell.

Like administrator permissions, end user permissions aren't transferred between the on-premises organization and the Exchange Online organization. Any permissions that you've defined in the on-premises organization must be re-created in the Exchange Online organization.

For more information, see [管理角色分配策略](https://technet.microsoft.com/zh-cn/library/jj657511\(v=exchg.150\)) and [更改邮箱的分配策略](https://technet.microsoft.com/zh-cn/library/dd638076\(v=exchg.150\)).

The following table lists the permissions granted by the default role assignment policies in the Exchange Online organization.

### Default role assignment policy permissions

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Management role</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MyTeamMailboxes</p></td>
<td><p>The <code>MyTeamMailboxes</code> management role enables individual users to create site mailboxes and connect them to Microsoft SharePoint sites.</p></td>
</tr>
<tr class="even">
<td><p>My Marketplace Apps</p></td>
<td><p>The <code>My Marketplace Apps</code> management role enables individual users to view and modify their Microsoft Office marketplace apps.</p></td>
</tr>
<tr class="odd">
<td><p>MyBaseOptions</p></td>
<td><p>The <code>MyBaseOptions</code> management role enables individual users to view and modify the basic configuration of their own mailbox and associated settings.</p></td>
</tr>
<tr class="even">
<td><p>MyContactInformation</p></td>
<td><p>The <code>MyContactInformation</code> management role enables individual users to modify their contact information, including address and phone numbers.</p></td>
</tr>
<tr class="odd">
<td><p>MyDistributionGroupMembership</p></td>
<td><p>The <code>MyDistributionGroupMembership</code> management role enables individual users to view and modify their membership in distribution groups in an organization, provided that those distribution groups allow manipulation of group membership.</p></td>
</tr>
<tr class="even">
<td><p>MyDistributionGroups</p></td>
<td><p>The <code>MyDistributionGroups</code> management role enables individual users to create, modify, and view distribution groups, and to modify, view, remove, and add members to distribution groups they own.</p></td>
</tr>
<tr class="odd">
<td><p>MyMailSubscription</p></td>
<td><p>The <code>MyMailSubscription</code> role enables individual users to view and modify their e-mail subscription settings such as message format and protocol defaults.</p></td>
</tr>
<tr class="even">
<td><p>MyProfileInformation</p></td>
<td><p>The <code>MyProfileInformation</code> management role enables individual users to modify their name.</p></td>
</tr>
<tr class="odd">
<td><p>MyRetentionPolicies</p></td>
<td><p>The <code>MyRetentionPolicies</code> management role enables individual users to view their retention tags, and to view and modify their retention tag settings and defaults.</p></td>
</tr>
<tr class="even">
<td><p>MyTextMessaging</p></td>
<td><p>The <code>MyTextMessaging</code> management role enables individual users to create, view, and modify their text messaging settings.</p></td>
</tr>
<tr class="odd">
<td><p>MyVoiceMail</p></td>
<td><p>The <code>MyVoiceMail</code> management role enables individual users to view and modify their voice mail settings.</p></td>
</tr>
<tr class="even">
<td><p>My ReadWriteMailbox Apps</p></td>
<td><p>The <code>My ReadWriteMailbox Apps</code> management role enables users to install apps with ReadWriteMailbox permissions.</p></td>
</tr>
<tr class="odd">
<td><p>My Custom Apps</p></td>
<td><p>The <code>My Custom Apps</code> management role enables users to view and modify their custom apps.</p></td>
</tr>
</tbody>
</table>

