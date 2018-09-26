---
title: '将 Exchange 配置为接收多个权威域的邮件: Exchange 2013 Help'
TOCTitle: 将 Exchange 配置为接收多个权威域的邮件
ms:assetid: 11801f73-4934-4025-a1c1-3935dada7e9b
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa996314(v=EXCHG.150)
ms:contentKeyID: 51408195
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 将 Exchange 配置为接收多个权威域的邮件

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2016-06-15_

在 Microsoft Exchange Server 2013 中，很容易将多个权威域添加到组织中。但在添加了权威域后，需要确定如何在组织中使用这些权威域。例如：

  - 如果想要在组织中为收件人的新权威域添加一个电子邮件地址，您是希望替换收件人的现有主（答复）地址，还是将这些新电子邮件地址作为代理（辅）地址添加？

  - 您是否希望将新权威域中的电子邮件地址应用于所有收件人和所有收件人类型？或者，您是希望将新电子邮件地址应用于特定收件人类型，还是基于其用户属性的特定收件人（例如，仅财务部门的用户）？

在下列示例方案中，您的 Exchange 组织可能必须接收并处理多个权威 SMTP 域的电子邮件：

  - 正在更改 SMTP 域名，但暂时必须继续接受旧域名的电子邮件，以防客户将电子邮件发送到先前的电子邮件地址。可以将新的电子邮件地址设置为主（答复）地址。这意味着新地址将是收件人发送的所有电子邮件上显示的默认电子邮件地址。可以将旧的电子邮件地址设置为辅地址。这样，收件人将可以继续接收向旧电子邮件地址发送的电子邮件。

  - 希望为组织中的各个业务单位提供不同的电子邮件地址。例如，如果 contoso.com Active Directory 林包含分支机构 Tailspin Toys 和 Fourth Coffee 的子域，您可能希望将 SMTP 域名 contoso.com、tailspintoys.com 和 fourthcoffee.com 分别分配给相应业务单位中的收件人。

  - 提供电子邮件托管服务并且必须接受多个 SMTP 域名的电子邮件。

## 在开始之前，您需要知道什么？

  - 估计完成该任务的时间：30 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [邮件流权限](mail-flow-permissions-exchange-2013-help.md)主题中的\&quot;接受域\&quot;条目以及[收件人权限](recipients-permissions-exchange-2013-help.md)主题中的\&quot;电子邮件地址策略\&quot;条目。

  - 如果您已在外围网络中订阅了边缘传输服务器，请在 Exchange 组织中的邮箱服务器上配置接受的域。在 EdgeSync 同步期间，接受的域配置会复制到边缘传输服务器。有关详细信息，请参阅[边缘订阅](edge-subscriptions-exchange-2013-help.md)。

  - 创建接受域时，可以在地址空间使用通配符 ( \* )，指示 Exchange 组织还接受 SMTP 地址空间的所有子域。例如，若要将 contoso.com 及其所有子域配置为接受域，请输入 **\*.contoso.com** 作为 SMTP 地址空间。但是，如果将在电子邮件地址策略中使用子域名，则每个子域必须具有明确的接受域条目。

  - 每个用于接受来自 Internet 的电子邮件的 SMTP 域都需要公共 DNS MX 记录。每条 MX 记录应解析为接收组织电子邮件的面向 Internet 的服务器。

  - 需要配置发送连接器和接收连接器，以便 Exchange 组织将电子邮件发送到 Internet 以及从 Internet 接收电子邮件。Internet 发送连接器和 Internet 接收连接器的配置由 Exchange 拓扑确定。有关配置连接器的详细信息，请参阅[连接器](connectors-exchange-2013-help.md)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 您该如何做？

## 步骤 1：创建权威域

## 使用 Exchange 管理中心创建权威域

1.  在 EAC 中，导航到\&quot;邮件流\&quot;\>\&quot;接受域\&quot;，然后单击\&quot;添加\&quot;![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。

2.  在\&quot;名称\&quot;字段中，输入接受域的显示名称。贵组织的每个接受域必须具有唯一显示名称。这可能与接受域不同。例如，域 contoso.com 可以拥有 Contoso Local Accepted Domain 的显示名称。

3.  在\&quot;接受域\&quot;字段中，指定您的组织为其接受电子邮件的 SMTP 命名空间。例如，contoso.com。

4.  选择\&quot;权威域\&quot;。

5.  单击\&quot;保存\&quot;。

## 使用命令行管理程序创建权威域

若要创建新的权威域，请使用以下语法。

```powershell
    New-AcceptedDomain -Name "<Unique Name>" -DomainName <SMTP domain> -DomainType Authoritative
```

例如，要为域 fourthcoffee.com 创建一个名为\&quot;Fourth Coffee subsidiary\&quot;的新权威域，请运行以下命令：

```powershell
    New-AcceptedDomain -Name "Fourth Coffee subsidiary" -DomainName fourthcoffee.com -DomainType Authoritative
```

## 您如何知道此步骤有效？

若要验证是否已成功创建了权威域，请执行以下操作：

  - 在 EAC 中，导航到\&quot;邮件流\&quot;\>\&quot;接受域\&quot;。验证是否显示创建的接受域，且\&quot;域类型\&quot;的值是否为\&quot;权威\&quot;。

  - 在命令行管理程序中，运行命令 **Get-AcceptedDomain**。验证是否显示创建的域，且 **DomainType** 的值是否为 `Authoritative`。

## 步骤 2：为权威域配置电子邮件地址策略

若要使用创建的权威接受域，需要为权威域配置电子邮件地址策略，以满足方案的目标。例如，您可能需要创建新的电子邮件地址策略，或修改现有策略。可以选择替换某些或所有收件人的主电子邮件地址，也可以选择保留或删除旧的主电子邮件地址。本部分展示了两个示例方案。

## 更改现有主电子邮件地址

若要更改为收件人分配的主（答复）电子邮件地址，并保留旧的主电子邮件地址作为代理（辅）电子邮件地址，请执行下列步骤：

## 使用 EAC 更改现有主电子邮件地址

1.  在 EAC 中，导航到\&quot;邮件流\&quot;\>\&quot;电子邮件地址策略\&quot;。选择要修改的电子邮件地址策略，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

2.  在\&quot;电子邮件地址策略\&quot; 页面上，单击\&quot;电子邮件地址格式\&quot;选项卡。在\&quot;电子邮件地址格式\&quot;部分，单击\&quot;添加\&quot;![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。

3.  在打开的\&quot;电子邮件地址格式\&quot;页面上，进行以下选择：
    
      - **选择接受域**   单击下拉列表，并选择新的权威域。
    
      - 选择\&quot;将此格式作为答复电子邮件地址\&quot;。
    
    完成后，单击\&quot;保存\&quot;。

4.  在\&quot;电子邮件地址策略\&quot;页面上，单击\&quot;保存\&quot;，以保存对策略的更改。

5.  您将收到警告，在更新电子邮件地址策略之前，将不会应用该策略。在创建策略后，选择它，然后在详细信息窗格中，单击\&quot;应用\&quot;。

## 使用命令行管理程序更改现有主电子邮件地址

在命令行管理程序中，使用两个单独的命令：一个命令用于修改现有电子邮件地址策略，另一个命令将更新的电子邮件地址策略应用于组织中的收件人。

若要更改现有主电子邮件地址，并保留旧的主电子邮件地址作为代理地址，请运行以下命令：

```powershell
    Set-EmailAddressPolicy <EmailAddressPolicyIdentity> -EnabledEmailAddressTemplates SMTP:<NewPrimaryEmailAddress>,smtp:<OldPrimaryEmailAddress>
```

例如，假设组织中的电子邮件地址策略使用的电子邮件地址格式为 *useralias*`@contoso.com`。此示例将名为\&quot;Default Policy\&quot;的电子邮件地址策略中的主（答复）地址域更改为 `@fourthcoffee.com`，并保留 `@contoso.com` 域中旧的主答复地址作为代理（辅）地址。

```powershell
    Set-EmailAddressPolicy "Default Policy" -EnabledEmailAddressTemplates SMTP:@fourthcoffee.com,smtp:@contoso.com
```

> [!NOTE]  
> 大写字母形式的 <code>SMTP</code> 限定符指定主（答复）地址。小写字母形式的 <code>smtp</code> 限定符指定代理（辅）地址。


若要将更新的电子邮件地址策略应用于收件人，请使用以下语法。

```powershell
Update-EmailAddressPolicy <EamilAddressPolicyIdentity>
```

例如，若要应用名为\&quot;Default Policy\&quot;的更新电子邮件地址策略，请运行以下命令：

```powershell
Update-EmailAddressPolicy "Default Policy"
```

## 替换已筛选收件人组的现有主电子邮件地址

无法修改要应用到已筛选收件人组的默认电子邮件地址策略。需要创建新的电子邮件地址策略，或修改现有的自定义电子邮件策略。本部分中的示例创建了新的电子邮件地址策略。在本示例中，新接受域中的主（答复）地址将替换指定收件人旧的主地址，且未保留旧的主地址作为代理（辅）电子邮件地址。因此，受到影响的收件人将无法再在其旧的主电子邮件地址中收到电子邮件。

此外，应用于特定用户的电子邮件地址策略的优先级应高于（由较低的整数值表示）其他电子邮件地址策略（包括默认策略），因此，将首先应用特定策略。由于两个策略不能具有相同的优先级值，可能需要先降低组织默认电子邮件地址策略的优先级。

## 使用 EAC 替换已筛选收件人组的现有主电子邮件地址

若要创建其他电子邮件地址来用作已筛选收件人组的主电子邮件地址，请执行下列步骤。

1.  在 EAC 中，导航到\&quot;邮件流\&quot;\>\&quot;电子邮件地址策略\&quot;，然后单击\&quot;添加\&quot;![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。

2.  在\&quot;电子邮件地址策略\&quot;页面上，填写下列字段:
    
    1.  **策略名称**   输入唯一的描述性名称。
    
    2.  **电子邮件地址格式**   单击\&quot;添加\&quot;![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。在打开的\&quot;电子邮件地址格式\&quot;页面上，进行以下选择：
        
          - **选择接受域**   单击下拉列表，并选择新的权威域。
        
          - **电子邮件地址格式**   为组织选择合适的电子邮件地址格式。
        
          - 选择\&quot;将此格式作为答复电子邮件地址\&quot;。
        
        完成后，单击\&quot;保存\&quot;。

3.  **与其他策略一起按此顺序运行此策略**   应用于特定用户的策略优先级通常应高于（用较低的整数值表示）其他电子邮件地址策略（包括默认策略）。

4.  **指定将应用此电子邮件地址的收件人类型**   选择您希望应用电子邮件地址策略的收件人类型。

5.  **创建规则以进一步定义应用此电子邮件地址策略的收件人**   单击\&quot;添加规则\&quot;以限制将应用此策略的收件人。这将创建布尔\&quot;And\&quot;语句。根据需要多次重复此步骤。
    
    > [!CAUTION]  
    > 如果应用过多规则，则可能将电子邮件地址策略限制到不包含任何用户的程度。


6.  单击\&quot;预览应用策略的收件人\&quot;来查看将向其应用该策略的收件人。

7.  单击\&quot;保存\&quot;保存更改并创建策略。

8.  您将收到警告，在更新电子邮件地址策略之前，将不会应用该策略。在创建策略后，选择它，然后在详细信息窗格中，单击\&quot;应用\&quot;。

## 使用命令行管理程序替换已筛选收件人组的现有主电子邮件地址

若要替换已筛选收件人组的主电子邮件地址，请使用以下命令：

```powershell
    New-EmailAddressPolicy -Name <Policy Name> -Priority <Integer> -IncludedRecipients <RecipientTypes> <Conditional Recipient Properties> -EnabledEmailAddressTemplates SMTP:@<NewPrimaryEmailAddress>
```

本示例创建了名为\&quot;Fourth Coffee Recipients\&quot;的电子邮件地址策略，将该策略分配给 Fourth Coffee 部门的邮箱用户，并为该电子邮件地址策略设置了最高优先级，因此将首先应用该策略。请注意，没有为这些收件人保留旧的主电子邮件地址，因此他们无法在旧的主电子邮件地址中接收电子邮件。

```powershell
    New-EmailAddressPolicy -Name "Fourth Coffee Recipients" -Priority 1 -IncludedRecipients MailboxUsers -ConditionalDepartment "Fourth Coffee" -EnabledEmailAddressTemplates SMTP:@fourthcoffee.com
```

若要将新的电子邮件地址策略应用于受到影响的收件人，请运行以下命令：

```powershell
Update-EmailAddressPolicy "Fourth Coffee Recipients"
```

## 您如何知道此步骤有效？

若要验证是否已成功为权威域配置电子邮件地址策略，请执行下列操作之一：

  - 在 EAC 中，导航到\&quot;邮件流\&quot;\>\&quot;电子邮件地址策略\&quot;。验证策略是否已按正确的顺序应用。此外，选择任意新策略或更新策略，然后在详细信息窗格中，验证电子邮件地址、包含的收件人以及策略是否已正确应用。

  - 在 Shell 中，运行命令 **Get-EmailAddressPolicy** 和 `Get-EmailAddressPolicy "<Policy Name>"| Format-List` 检验策略的详细信息。

## 您如何知道此任务有效？

若要验证是否已将 Exchange 配置为接受多个权威域的邮件，请执行以下操作：

1.  从 Exchange 组织外部的邮箱向受到影响的收件人发送测试邮件。验证电子邮件地址是否可成功接受邮件。

2.  从受到影响的收件人邮箱向外部收件人发送测试邮件，并验证邮件的\&quot;发件人\&quot;地址是否正确。

