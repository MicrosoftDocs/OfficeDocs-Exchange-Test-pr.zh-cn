---
title: '为就地电子数据展示搜索创建自定义管理范围: Exchange Online Help'
TOCTitle: 为就地电子数据展示搜索创建自定义管理范围
ms:assetid: 1543aefe-3709-402c-b9cd-c11fe898aad1
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dn741464(v=EXCHG.150)
ms:contentKeyID: 62219858
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 为就地电子数据展示搜索创建自定义管理范围

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2015-01-21_

您可以使用自定义管理范围，允许特定用户或组使用就地电子数据展示来搜索 Exchange 2013 或 Exchange Online 组织中的部分邮箱。例如，您可能希望发现管理员仅搜索特定位置或部门的用户邮箱。您可以通过创建自定义管理作用域来执行此操作。此自定义的管理作用域使用收件人筛选器来控制哪些邮箱可以搜索。收件人筛选器作用域根据收件人类型或其他收件人属性，使用筛选器指向特定收件人。

对于就地电子数据展示，用户邮箱上可以用于为自定义作用域创建收件人筛选器的唯一属性是通讯组成员身份（实际的属性名称为 *MemberOfGroup*）。如果您使用其他属性（如 *CustomAttributeN*、*Department* 或 *PostalCode*），由分配了自定义作用域的角色组成员运行的搜索将失败。

要了解有关管理作用域的详细信息，请参阅：

  - [了解管理角色作用域](understanding-management-role-scopes-exchange-2013-help.md)

  - [了解管理角色作用域筛选器](understanding-management-role-scope-filters-exchange-2013-help.md)

## 在开始之前，您需要知道什么？

  - 估计完成时间：15 分钟

  - 如前所述，您只能使用组成员身份作为收件人筛选器来创建将用于电子数据展示的自定义收件人筛选器作用域。任何其他收件人属性不能用于为电子数据展示搜索创建自定义作用域。请注意，也不能使用动态通讯组中的成员身份。

  - 执行步骤 1 到 3，允许发现管理员导出使用自定义管理作用域的电子数据展示搜索的搜索结果。

  - 如果您的发现管理员不需要预览搜索结果，则可以跳过步骤 4。

  - 如果您的发现管理员不需要复制搜索结果，则可以跳过步骤 5。

## 步骤 1：将用户分为若干通讯组以进行电子数据展示

要搜索组织中的部分邮箱或者缩小发现管理员可以搜索的源邮箱范围，您需要将这部分邮箱分为一个或多个通讯组。当您在步骤 2 中创建自定义管理作用域时，您将这些通讯组用作收件人筛选器来创建自定义管理作用域。这样，发现管理员可以仅搜索属于指定组成员的用户的邮箱。

您可以使用现有通讯组进行电子数据展示，也可以创建新的通讯组。请参阅本主题结尾的详细信息，查看有关如何创建可用于作用域电子数据展示搜索的通讯组的提示。

## 步骤 2：创建自定义管理作用域

现在您将创建一个由通讯组成员身份定义的自定义管理作用域（使用 *MemberOfGroup* 收件人筛选器）。将该作用域应用到用于电子数据展示的角色组时，该角色组的成员可以搜索属于用于创建自定义管理作用域的通讯组成员的用户的邮箱。

此过程使用 Exchange 命令行管理程序命令创建一个名为渥太华用户电子数据展示作用域的自定义作用域。它指定一个名为渥太华用户的通讯组作为自定义作用域的收件人筛选器。

1.  运行此命令获取渥太华用户组的属性，并将属性保存到一个变量，该变量可用于下一个命令。
    
        $DG = Get-DistributionGroup -Identity "Ottawa Users"

2.  运行此命令，根据渥太华用户通讯组的成员身份创建一个自定义管理作用域。
    
        New-ManagementScope "Ottawa Users eDiscovery Scope" -RecipientRestrictionFilter "MemberOfGroup -eq '$($DG.DistinguishedName)'"
    
    通讯组的可分辨名称包含在变量 **$DG** 中，用于为新的管理作用域创建收件人筛选器。

## 步骤 3：创建管理角色组

在此步骤中，您创建一个新的管理角色组并分配您在步骤 2 中创建的自定义作用域。添加合法保留和邮箱搜索角色，以便角色组成员可以执行就地电子数据展示搜索并将邮箱置于就地保留或诉讼保留状态。您还可以向该角色组添加成员，以便他们可以搜索属于在步骤 2 中用于创建自定义作用域的通讯组的成员的邮箱。

在下面的示例中，渥太华用户电子数据展示管理员安全组将作为成员添加到该角色组。您可以使用命令行管理程序或 EAC 执行此步骤。

## 使用命令行管理程序创建管理角色组

运行此命令，创建一个使用在步骤 2 中创建的自定义作用域的新角色组。该命令还会添加合法保留和邮箱搜索角色，并将渥太华用户电子数据展示管理员安全组添加为新角色组的成员。

    New-RoleGroup "Ottawa Discovery Management" -Roles "Mailbox Search","Legal Hold" -CustomRecipientWriteScope "Ottawa Users eDiscovery Scope" -Members "Ottawa Users eDiscovery Managers"

## 使用 EAC 创建管理角色组

1.  在 EAC 中，转到\&quot;权限\&quot;\>\&quot;管理员角色\&quot;，然后单击\&quot;新建\&quot;![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。

2.  在\&quot;新角色组\&quot;中，提供以下信息：
    
      - **名称** 为新角色组提供一个描述性名称。在此示例中，您使用**渥太华发现管理**。
    
      - **写入作用域**   选择您在步骤 2 中创建的自定义管理作用域。此作用域将应用于新角色组。
    
      - **角色**   单击\&quot;添加\&quot;![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")，将\&quot;合法保留\&quot;和\&quot;邮箱搜索\&quot;角色添加到新角色组。
    
      - **成员**   单击\&quot;添加\&quot;![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")，选择您想添加为新角色组成员的用户、安全组或角色组。在此示例中，\&quot;渥太华用户电子数据展示管理员\&quot;安全组的成员将只能搜索属于\&quot;渥太华用户\&quot;通讯组成员的用户的邮箱。

3.  单击\&quot;保存\&quot;创建角色组。
    
    下面是您完成后\&quot;新角色组\&quot;窗口的外观示例。
    
    ![为自定义范围创建一个新的角色组](images/Dn741464.a6e3419f-d5d9-404f-890d-ad35f499756f(EXCHG.150).gif "为自定义范围创建一个新的角色组")  

## （可选）步骤 4：将发现管理员添加为用于创建自定义管理作用域的通讯组的成员

如果您想让发现管理员预览电子数据展示搜索结果，您只需执行此步骤。

运行此命令，将渥太华用户电子数据展示管理员安全组添加为渥太华用户通讯组的成员。

    Add-DistributionGroupMember -Identity "Ottawa Users" -Member "Ottawa Users eDiscovery Managers"

您还可以使用 EAC 将成员添加到通讯组。有关详细信息，请参阅[创建和管理通讯组](create-and-manage-distribution-groups-exchange-2013-help.md)。

## （可选）步骤 5：将发现邮箱添加为用于创建自定义管理作用域的通讯组的成员

如果您想让发现管理员复制电子数据展示搜索结果，您只需执行此步骤。

运行此命令，将名为渥太华发现邮箱的发现邮箱添加为渥太华用户通讯组的成员。

    Add-DistributionGroupMember -Identity "Ottawa Users" -Member "Ottawa Discovery Mailbox"

> [!NOTE]
> 要打开发现邮箱并查看搜索结果，发现管理员必须分配有发现邮箱的完全访问权限。有关详细信息，请参阅<a href="create-a-discovery-mailbox-exchange-2013-help.md">创建发现邮箱</a>。


## 您如何知道这有效？

下面几种方法可验证您已成功地实现电子数据展示的自定义管理作用域。进行验证时，请确保运行电子数据展示搜索的用户是使用自定义管理作用域的角色组的成员。

  - 创建电子数据展示搜索，选择用于创建作为待搜索邮箱的源的自定义管理作用域的通讯组。应成功搜索所有邮箱。

  - 创建电子数据展示搜索，搜索不属于用于创建自定义管理作用域的通讯组成员的任何用户的邮箱。因为发现管理员只能搜索属于用于创建自定义管理作用域的通讯组成员的用户的邮箱，搜索应该会失败。在这种情况下，将返回错误，例如\&quot;由于当前用户没有访问邮箱的权限，无法搜索邮箱 \<*name of mailbox*\>\&quot;。

  - 创建电子数据展示搜索，搜索不属于用于创建自定义管理作用域的通讯组成员的用户的邮箱。在相同的搜索中包括不是成员的用户的邮箱。搜索应该会部分成功。应该能成功搜索用于创建自定义管理作用域的通讯组的成员的邮箱。搜索不属于组成员的用户的邮箱应该会失败。

## 详细信息

  - 因为通讯组在此示例中用于确定电子数据展示搜索范围，而不用于邮件传递，因此当您创建和配置电子数据展示的通讯组时，请考虑以下事项：
    
      - 创建具有封闭成员身份的通讯组，因此成员只能由组所有者添加到组中或从组中删除。如果您在命令行管理程序中创建组，请使用语法 `MemberJoinRestriction closed` 和 `MemberDepartRestriction closed`。
    
      - 启用组仲裁，以便发送到组的任何邮件将首先发送给可以相应批准或拒绝邮件的组仲裁人。如果您在命令行管理程序中创建组，请使用语法 `ModerationEnabled $true`。如果您使用 EAC，您可以在创建组后启用仲裁。
    
      - 将通讯组从组织的共享通讯簿中隐藏。创建组后使用 EAC 或 **Set-DistributionGroup** cmdlet。如果您使用命令行管理程序，请使用语法 `HiddenFromAddressListsEnabled $true`。
    
    在下面的示例中，第一个命令创建启用封闭成员身份和仲裁的通讯组。第二个命令将组从共享地址簿中隐藏。
    ```
        New-DistributionGroup -Name "Vancouver Users eDiscovery Scope" -Alias VancouverUserseDiscovery -MemberJoinRestriction closed -MemberDepartRestriction closed -ModerationEnabled $true
    ```
    ```
        Set-DistributionGroup "Vancouver Users eDiscovery Scope" -HiddenFromAddressListsEnabled $true
    ```

    有关创建和管理通讯组的详细信息，请参阅[创建和管理通讯组](create-and-manage-distribution-groups-exchange-2013-help.md)。

  - 尽管您只能使用通讯组成员身份作为用于电子数据展示的自定义管理作用域的收件人筛选器，但您可以使用其他收件人属性将用户添加到该通讯组。下面是根据常规用户或邮箱属性，使用 **Get-Mailbox** 和 **Get-Recipient** cmdlet 返回特定用户组的一些示例。
    ```
        Get-Recipient -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'Department -eq "HR"'
    ```
    ```
        Get-Mailbox -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'CustomAttribute15 -eq "VancouverSubsidiary"'
    ```
    ```
        Get-Recipient -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'PostalCode -eq "98052"'
    ```
    ```
        Get-Recipient -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'StateOrProvince -eq "WA"'
    ```
    ```
        Get-Mailbox -RecipientTypeDetails UserMailbox -ResultSize unlimited -OrganizationalUnit "namsr01a002.sdf.exchangelabs.com/Microsoft Exchange Hosted Organizations/contoso.onmicrosoft.com"
    ```

  - 然后您可以使用前一个要点中的示例创建一个变量，此变量可用于 **Add-DistributionGroupMember** cmdlet，以将用户组添加到通讯组。在下面的示例中，第一个命令创建一个变量，此变量包含对于用户帐户中的 *Department* 属性其值为 **Vancouver** 的所有用户邮箱。第二个命令将这些用户添加到温哥华用户通讯组。
    ```
        $members = Get-Recipient -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'Department -eq "Vancouver"'
    ```
    ```
        $members | ForEach {Add-DistributionGroupMember "Ottawa Users" -Member $_.Name}
    ```
    
  - 您可以使用 **Add-RoleGroupMember** cmdlet 将成员添加到用于确定电子数据展示搜索范围的现有角色组。例如，以下命令将用户 admin@ottawa.contoso.com 添加到渥太华发现管理角色组。
    
        Add-RoleGroupMember "Vancouver Discovery Management" -Member paralegal@vancouver.contoso.com
    
    您还可以使用 EAC 将成员添加到角色组。有关详细信息，请参阅[管理角色组成员](manage-role-group-members-exchange-2013-help.md)中的\&quot;将成员添加到角色组\&quot;部分。

  - 在 Exchange Online 中，用于电子数据展示的自定义管理作用域不能用于搜索非活动状态的邮箱。这是因为非活动邮箱不能作为通讯组的成员。例如，假设用户是用于创建电子数据展示的自定义管理作用域的通讯组的成员，然后该用户离开组织，且其邮箱变为非活动状态（将邮箱置于诉讼保留或就地保留状态，然后删除相应的 Office 365 用户帐户），那么结果是将从任何通讯组中删除用户，包括用于创建用于电子数据展示的自定义管理作用域的组的成员。如果发现管理员（他/她是已分配有自定义管理作用域的角色组的成员）尝试搜索非活动状态的邮箱，搜索将失败。若要搜索非活动邮箱，发现管理器必须是发现管理角色组或有权限搜索整个组织的任何角色组的成员。
    
    有关非活动邮箱的详细信息，请参阅 [Exchange Online 中的非活动邮箱](https://technet.microsoft.com/zh-cn/library/dn798632\(v=exchg.150\))。

