---
title: '准备 Active Directory 和域: Exchange 2013 Help'
TOCTitle: 准备 Active Directory 和域
ms:assetid: f895e1ce-d766-4352-ac46-ec959c9954a9
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb125224(v=EXCHG.150)
ms:contentKeyID: 50492014
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 准备 Active Directory 和域

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2016-12-09_

安装 Microsoft Exchange Server 2013 之前，你需要准备 Active Directory 林及其子域。Exchange 需要准备 Active Directory，使其可以存储关于用户邮箱以及组织中 Exchange 服务器的配置的信息。如果您对 Active Directory 林或域不熟悉，请参阅 [Active Directory 域服务概述](https://go.microsoft.com/fwlink/p/?linkid=399226)。

> [!NOTE]  
> 无论是首次在你的环境中安装 Exchange 还是已在运行早期版本的 Exchange Server，都需要为 Exchange 2013 准备 Active Directory。有关 Exchange 2013 添加到 Active Directory 的新架构类和属性（包括由 Service Pack (SP) 和累积更新 (CU) 创建的）的详细信息，可以参阅 <a href="exchange-2013-active-directory-schema-changes-exchange-2013-help.md">Exchange 2013 Active Directory 架构更改</a>。


有多种方法可用于为 Exchange 准备 Active Directory。第一种是让 Exchange 2013 安装程序向导为您代劳。如果您没有大型 Active Directory 部署，且没有负责管理 Active Directory 的单独团队，我们建议您使用向导。您所使用的帐户需为架构管理员和企业管理员安全组的成员。有关如何使用安装程序向导的详细信息，请参阅[使用安装向导安装 Exchange 2013](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md)。

如果您具有大型 Active Directory 部署，或者具有单独的团队来管理 Active Directory，本主题对您很适用。遵循本主题中的步骤可帮助您增强对每个准备阶段以及谁可以执行每个步骤的控制。例如，Exchange 管理员可能没有扩展 Active Directory 架构所需的权限。

在开始之前，您需要知道什么？

1\. 扩展 Active Directory 架构

2\. 准备 Active Directory

3\. 准备 Active Directory 域

您如何知道操作成功？

想了解在为 Exchange 准备 Active Directory 时发生了什么？请查看[安装 Exchange 2013 后 Active Directory 中有哪些变化？](what-changes-in-active-directory-when-exchange-2013-is-installed-exchange-2013-help.md)

## 在开始之前，您需要知道什么？

  - 估计完成时间：10-15 分钟或更长（不包括 Active Directory 复制），取决于组织规模和子域数量。

  - 您用于运行这些步骤的计算机需满足 [Exchange 2013 系统要求](exchange-2013-system-requirements-exchange-2013-help.md)。此外，您的 Active Directory 林需满足 [Exchange 2013 系统要求](exchange-2013-system-requirements-exchange-2013-help.md)中“网络和目录服务器”部分的要求。

  - 如果您的组织具有多个 Active Directory 域，我们建议采用以下做法：
    
      - 在拥有来自每个域的 Active Directory 服务器的情况下，从 Active Directory 站点执行以下步骤。
    
      - 在具有每个域中可写的全局编录服务器的 Active Directory 站点中安装第一台 Exchange 服务器。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 1\. 扩展 Active Directory 架构

让组织为 Exchange 2013 做好准备的第一步是扩展 Active Directory 架构。Exchange 在 Active Directory 中存储了大量信息，但在存储之前，需要添加和更新类、属性及其他项目。如果您想知道在扩展架构时发生了哪些变化，请参阅 [Exchange 2013 Active Directory 架构更改](exchange-2013-active-directory-schema-changes-exchange-2013-help.md)。

扩展架构之前，需要注意以下事项：

  - 您登录所使用的帐户需为架构管理员和企业管理员安全组的成员。

  - 您在其上运行命令以扩展架构的计算机需位于与架构主机相同的 Active Directory 域和站点中。

  - 如果您使用 *DomainController* 参数，请确保使用作为架构主机的域控制器的名称。

  - 为 Exchange 扩展架构的唯一方式是使用本主题中的步骤或使用 Exchange 2013 安装程序。不支持扩展架构的其他方法。

> [!TIP]  
> 如果您没有单独的团队来管理 Active Directory 架构，您可以跳过此步骤，直接转到准备 Active Directory。如果未在步骤 1 中扩展架构，步骤 2 中的命令将为您扩展架构。如果您决定跳过步骤 1，您仍需记住上述信息。


准备好之后，请执行以下操作来扩展您 Active Directory 架构。如果您具有多个 Active Directory 林，请确保登录到正确的林。

1.  确保计算机已准备好运行 Exchange 2013 安装程序。要查看运行安装程序需要什么，请参阅 [Exchange 2013 先决条件](exchange-2013-prerequisites-exchange-2013-help.md)中的 [Active Directory preparation](exchange-2013-prerequisites-exchange-2013-help.md)部分。

2.  打开 Windows 命令提示符窗口，然后转到下载 Exchange 安装文件的位置。

3.  运行以下命令以扩展架构。
    
        Setup.exe /PrepareSchema /IAcceptExchangeServerLicenseTerms

安装程序扩展完架构之后，你需要等待 Active Directory 将更改复制到所有域控制器。如果你想查看复制进展，可以使用 `repadmin` 工具。`Repadmin` 是 Windows Server 2012 R2、Windows Server 2012 和 Windows Server 2008 R2 中 Active Directory 域服务工具功能的一部分。有关如何使用此工具的详细信息，请参阅 [Repadmin](https://go.microsoft.com/fwlink/p/?linkid=257879)。

## 2\. 准备 Active Directory

现在 Active Directory 架构已扩展完毕，您可以为 Exchange 2013 准备 Active Directory 的其他部件。在此设置过程中，Exchange 将在用于存储信息的 Active Directory 中创建容器、对象及其他项目。所有 Exchange 容器、对象、属性等的集合称为 *Exchange 组织*。

为 Exchange 准备 Active Directory 之前，需要注意以下事项：

  - 您登录所使用的帐户需为企业管理员安全组的成员。如果您想使用 *PrepareAD* 命令扩展架构而跳过了步骤 1，您使用的帐户还需为架构管理员安全组的成员。

  - 您在其上运行命令的计算机需位于与架构主机相同的 Active Directory 域和站点中。它还需要联系 TCP 端口 389 上林中的所有域。

  - 等待 Active Directory 将在步骤 1 中所做的所有更改复制到所有域控制器，然后再执行此步骤。

当您运行以下命令为 Exchange 准备 Active Directory 时，您需要指定 Exchange 组织。此名称供 Exchange 在内部使用，用户通常不会看到。Exchange 安装所在的公司的名称通常用作组织名称。所使用的名称不会影响 Exchange 的功能，也不会确定可用的电子邮件地址。您可以将其命名为所需的任何名称，只要记住以下几点：

  - 您可以使用从 A 到 Z 的任何大写或小写字母。

  - 您可以使用数字 0-9。

  - 名称中可以包含空格，只要不出现在名称的开头或结尾。

  - 可以在名称中使用连字符或短划线。

  - 名称最多可为 64 个字符，但不能为空。

  - 名称设置之后则不能更改。

准备好之后，请执行以下操作来为 Exchange 准备 Active Directory。如果您要使用的组织名称包含空格，请为名称加上引号 (")。

1.  打开 Windows 命令提示符窗口，然后转到下载 Exchange 安装文件的位置。

2.  运行以下命令：
    
        Setup.exe /PrepareAD /OrganizationName:"<organization name>" /IAcceptExchangeServerLicenseTerms

安装程序为 Exchange 准备好 Active Directory 之后，ni 需要等待 Active Directory 将更改复制到所有域控制器。如果ni 想查看复制进展，可以使用 `repadmin` 工具。`repadmin` 是 Windows Server 2012 R2、Windows Server 2012 和 Windows Server 2008 R2 中 Active Directory 域服务工具功能的一部分。有关如何使用此工具的详细信息，请参阅 [Repadmin](https://go.microsoft.com/fwlink/p/?linkid=257879)。

## 3\. 准备 Active Directory 域

为 Exchange 准备 Active Directory 的最后一步是准备将安装 Exchange 或启用邮件的用户将位于的每个 Active Directory 域。此步骤创建其他容器和安全组，并设置权限，以便 Exchange 可以访问它们。

如果您的 Active Directory 林中具有多个域，您将有多种选择来进行准备。选择与您希望执行的操作相符的选项。如果您只有一个域，您可以跳过此步骤，因为步骤 2 中的 *PrepareAD* 命令已为您准备域。

## 准备 Active Directory 林中的所有域

要准备所有 Active Directory 域，您可以在运行安装程序时使用 *PrepareAllDomains* 参数。安装程序将为您准备 Active Directory 林中的每个 Exchange 域。

在准备 Active Directory 林中的所有域之前，请牢记以下事项：

  - 您使用的帐户需为企业管理员安全组的成员。

  - 等到 Active Directory 将在步骤 2 中所做的更改复制到所有域控制器。否则在您尝试准备域时可能会出现错误。

准备好之后，执行以下操作为 Exchange 准备 Active Directory 林中所有域。

1.  打开 Windows 命令提示符窗口，然后转到下载 Exchange 安装文件的位置。

2.  运行以下命令：
    
        Setup.exe /PrepareAllDomains /IAcceptExchangeServerLicenseTerms

## 让我选择想要准备的 Active Directory 域

如果您想选择要准备哪些 Active Directory 域，您可以在运行安装程序时使用 *PrepareDomain* 参数。使用 *PrepareDomain* 参数时，您需要包含想要准备的域的完全限定域名 (FQDN)。

在准备 Active Directory 林中的域之前，请牢记以下事项：

  - 您使用的帐户需要具有权限，具体取决于域是何时创建的。
    
      - **域在运行 PrepareAD 之前创建**   如果域是在您运行步骤 2 中的 *PrepareAD* 命令**之前**创建的，您使用的帐户需为您想要准备的域的域管理员组成员。
    
      - **域在运行 PrepareAD 之后创建**   如果域是在您运行步骤 2 中的 *PrepareAD* 命令**之后**创建的，您使用的帐户需为 1) 组织管理角色组的成员，且为 2) 您想要准备的域的域管理员组成员。

  - 等到 Active Directory 将在步骤 2 中所做的更改复制到所有域控制器。否则在您尝试准备域时可能会出现错误。

  - 您需要准备 Exchange 服务器将安装的每个域。您还需要准备任何将包含启用邮件的用户的域，即使这些域不包含任何 Exchange 服务器。

  - 您不需要在运行 *PrepareAD* 命令的域中运行 *PrepareDomain* 命令。*PrepareAD* 命令将自动准备域。

准备好之后，执行以下操作为 Exchange 准备 Active Directory 林中各个域。

1.  打开 Windows 命令提示符窗口，然后转到下载 Exchange 安装文件的位置。

2.  运行以下命令。包含您想准备的域的 FQDN。如果您想准备在其中运行命令的域，则无需包含 FQDN。
    
        Setup.exe /PrepareDomain:<FQDN of the domain you want to prepare> /IAcceptExchangeServerLicenseTerms

3.  为您将安装 Exchange 服务器或启用邮件的用户将位于的每个 Active Directory 域重复这些步骤。

## 您如何知道操作成功？

完成上述所有步骤之后，你可以进行检查，确保一切进行顺利。为此，你可使用一种称为 Active Directory 服务接口编辑器（ADSI 编辑）的工具。ADSI 编辑也是 Windows Server 2012 R2、Windows Server 2012 和 Windows Server 2008 R2 中的 Active Directory 域服务工具功能的一部分。如果你想要了解更多相关信息，请查看 [ADSI 编辑 (adsiedit.msc)](https://go.microsoft.com/fwlink/p/?linkid=294644)。

> [!WARNING]  
> 永远不要更改 ADSI 编辑中的值，除非 Microsoft 支持人员要求您这样做。更改 ADSI 编辑中的值可能会对 Exchange 组织和 Active Directory 造成无法修复的损坏。


在 Exchange 扩展您的 Active Directory 架构并准备 ExchangeActive Directory 后，系统会更新若干个属性，以便显示准备工作已完成。使用以下列表中的信息，确保这些属性的值正确。对于您要安装的 Exchange 2013 版本，每个属性都必须与下表中的值匹配。

  - 在“架构”命名上下文中，验证 **ms-Exch-Schema-Verision-Pt** 上的 **rangeUpper** 属性设置为 Exchange 2013 Active Directory 版本表中为您的 Exchange 2013 版本显示的值。
    
     

  - 在“配置”命名上下文中，验证 CN=\<*your organization*\>,CN=Microsoft Exchange,CN=Services,CN=Configuration,DC=\<*domain*\> 容器中的 **objectVersion** 属性是否设置为 Exchange 2013 Active Directory 版本表中为您的 Exchange 2013 版本显示的值。
    
     

  - 在“默认”命名上下文中，验证 DC=\<**下的“Microsoft Exchange 系统对象”***root domain*容器中的 **objectVersion** 属性是否设置为 Exchange 2013 Active Directory 版本表中 Exchange 2013 版本所显示的值。
    
     

您还可以查看 Exchange 安装程序日志，以验证是否成功完成 Active Directory 准备工作。有关详细信息，请参阅[验证 Exchange 2013 安装](verify-an-exchange-2013-installation-exchange-2013-help.md)。您无法使用[验证 Exchange 2013 安装](verify-an-exchange-2013-installation-exchange-2013-help.md)主题中提到的 **Get-ExchangeServer** cmdlet，除非在 Active Directory 站点中完成至少一个邮箱服务器角色和一个客户端访问服务器角色的安装。

## Exchange 2013 Active Directory 版本

下表向您显示 Active Directory 中的 Exchange 2013 对象，每次您安装 Exchange 2013 的一个新版本时将更新这些对象。您可以将您看到的对象版本与下表中的值进行比较，确认您安装的 Exchange 2013 版本在安装过程中成功更新 Active Directory。


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th> </th>
<th>Exchange 版本</th>
<th>rangeUpper</th>
<th>objectVersion</th>
<th>objectVersion</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>命名上下文</strong></p></td>
<td><p> </p></td>
<td><p>Schema</p></td>
<td><p>Default</p></td>
<td><p>Configuration</p></td>
</tr>
<tr class="even">
<td><p><strong>容器</strong></p></td>
<td><p> </p></td>
<td><p>ms-Exch-Schema-Version-Pt</p></td>
<td><p>Microsoft Exchange 系统对象</p></td>
<td><p>CN=&lt;<em>your organization</em>&gt;、CN=Microsoft Exchange、CN=Services、CN=Configuration、DC=&lt;<em>domain</em>&gt;</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Exchange 2013 CU10 及更高版本</p></td>
<td><p>15312</p></td>
<td><p>13236</p></td>
<td><p>16130</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Exchange 2013 CU9</p></td>
<td><p>15312</p></td>
<td><p>13236</p></td>
<td><p>15965</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Exchange 2013 CU8</p></td>
<td><p>15312</p></td>
<td><p>13236</p></td>
<td><p>15965</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Exchange 2013 CU7</p></td>
<td><p>15312</p></td>
<td><p>13236</p></td>
<td><p>15965</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Exchange 2013 CU6</p></td>
<td><p>15303</p></td>
<td><p>13236</p></td>
<td><p>15965</p></td>
</tr>
<tr class="even">
<td><p> </p></td>
<td><p>Exchange 2013 CU5</p></td>
<td><p>15300</p></td>
<td><p>13236</p></td>
<td><p>15870</p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>Exchange 2013 SP1</p></td>
<td><p>15292</p></td>
<td><p>13236</p></td>
<td><p>15844</p></td>
</tr>
<tr class="even">
<td><p> </p></td>
<td><p>Exchange 2013 CU3</p></td>
<td><p>15283</p></td>
<td><p>13236</p></td>
<td><p>15763</p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>Exchange 2013 CU2</p></td>
<td><p>15281</p></td>
<td><p>13236</p></td>
<td><p>15688</p></td>
</tr>
<tr class="even">
<td><p> </p></td>
<td><p>Exchange 2013 CU1</p></td>
<td><p>15254</p></td>
<td><p>13236</p></td>
<td><p>15614</p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>Exchange 2013 RTM</p></td>
<td><p>15137</p></td>
<td><p>13236</p></td>
<td><p>15449</p></td>
</tr>
</tbody>
</table>

