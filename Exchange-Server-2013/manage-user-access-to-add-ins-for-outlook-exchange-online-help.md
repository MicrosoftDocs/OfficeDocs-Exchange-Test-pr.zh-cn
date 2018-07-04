---
title: '管理用户对 Outlook 的应用程序的访问: Exchange 2013 Help'
TOCTitle: 管理用户对 Outlook 的应用程序的访问
ms:assetid: e5833dec-a23a-439e-ac03-92671817bff8
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ943757(v=EXCHG.150)
ms:contentKeyID: 52061572
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 管理用户对 Outlook 的应用程序的访问

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2018-04-17_

可以使用 EAC 或 Exchange Online PowerShell 管理用户对适用于 Outlook 的外接程序的访问。

  - 使用 Exchange 管理中心 (EAC) 时，可以在组织一级管理用户的基本外接程序访问设置。例如，可以配置为用户启用还是禁用外接程序。还可以指定对于用户来说外接程序是必需还是可选。

  - 使用 Exchange Online PowerShell 时，您不仅可以像使用 EAC 一样管理所有设置，还可以管理其他设置。例如，您可以限制组织内某些用户能否使用应用程序。

有关更多管理任务，请参阅 [适用于 Outlook 的应用程序](add-ins-for-outlook-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：5 分钟。

  - 若要了解如何使用 Windows PowerShell 连接到 Exchange Online，请参阅[连接到 Exchange Online PowerShell](https://go.microsoft.com/fwlink/p/?linkid=396554)。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[收件人权限](recipients-permissions-exchange-2013-help.md) 主题中的“Outlook 的外接程序”条目。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!tip]
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 要执行什么操作？

## 指定外接程序是可用、已启用还是已禁用

## 使用 EAC 指定外接程序是可用、已启用还是已禁用

1.  在 EAC 中，导航到“**组织**”\>“**外接程序**”。

2.  在列表视图中，选择要更改其设置的外接程序，然后单击“**编辑**”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  如果不想让用户使用外接程序，请清除“**允许组织内用户使用该外接程序**”复选框，然后单击“**保存**”。

4.  如果想让用户能够使用外接程序，请选中“**允许组织内用户使用该外接程序**”复选框，然后选择所需的选项。
    
      - “**可选、默认启用**”   如果想要让用户关闭外接程序，可以使用该设置。
    
      - “**可选、默认禁用**”   如果想要让用户打开外接程序，可以使用该设置。
    
      - “**强制、始终启用。用户无法禁用该外接程序**”   如果不想让用户关闭外接程序，可以使用该设置。

5.  单击“保存”。

## 使用 Exchange Online PowerShell 指定外接程序可用、已启用或已禁用

可以使用 Exchange Online PowerShell 指定外接程序可用、已启用或已禁用。

> [!NOTE]
> 运行以下命令，查找组织内安装的所有适用于 Outlook 的外接程序的显示名称和外接程序 ID。


    Get-app -Organizationadd-in | Format-List DisplayName,add-inID

如果想要禁用外接程序并对所有用户隐藏，请运行以下命令。

    Set-app <add-in ID> -Organizationadd-in -Enabled $false

如果想要将外接程序设置为默认启用，但不想让用户能够关闭它，请运行下列命令：

    Set-app <add-in ID> -Organizationadd-in -Enabled $true -DefaultStateForUser Enabled

如果想要将外接程序设置为默认禁用，但不想让用户能够打开它，请运行下列命令：

    Set-app <add-in ID> -Organizationadd-in -Enabled $true -DefaultStateForUser Disabled

如果想要强制要求用户使用外接程序，请运行下列命令：

    Set-app <add-in ID> -Organizationadd-in -Enabled $true -DefaultStateForUser AlwaysEnabled

有关语法和参数的详细信息，请参阅 [Set-App](https://technet.microsoft.com/zh-cn/library/jj218630\(v=exchg.150\))。

## 您如何知道操作成功？

1.  在 EAC 中，导航到“**组织**”\>“**外接程序**”。

2.  查看“用户默认值”和“提供至”列中的值。

或

1.  从 Exchange Online PowerShell 运行 `Get-app -Organizationadd-in | Format-List DisplayName,add-inId,Enabled,Default*`。

2.  查看“DefaultStateForUser”和“Enabled”的值。

## 限制某些用户能否使用应用程序

## 使用 Exchange Online PowerShell 限制某些用户能否使用应用程序

如果只想让营销团队通讯组的成员能够使用 LinkedIn 外接程序，请运行下列命令。

    $a = Get-DistributionGroupMember Marketing

    Set-app <add-in ID for the LinkedIn add-in> -Organizationadd-in -ProvidedTo SpecificUsers -UserList $a.Identity -DefaultStateForUser Enabled}

有关语法和参数的详细信息，请参阅 [Set-App](https://technet.microsoft.com/zh-cn/library/jj218630\(v=exchg.150\))。

## 您如何知道操作成功？

若要验证您是否已成功限制某些用户能否使用应用程序，请执行下列步骤：

1.  从 Exchange Online PowerShell 运行 `Get-app -Organizationadd-in | Format-List DisplayName,add-inId,Enabled,Default*,ProvidedTo,UserList`。

2.  查看“ProvidedTo”的值。

