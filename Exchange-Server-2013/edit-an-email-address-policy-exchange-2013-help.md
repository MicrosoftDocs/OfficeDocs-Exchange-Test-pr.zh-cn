---
title: '编辑电子邮件地址策略: Exchange 2013 Help'
TOCTitle: 编辑电子邮件地址策略
ms:assetid: cc8b36a0-95f4-43e9-bc64-87646d2e14e4
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb124580(v=EXCHG.150)
ms:contentKeyID: 50491559
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.OrganizationConfiguration.EditEmailAddressPolicyWizardForm.EmailAddressPolicyIntroductionPage
ms.translationtype: HT
---

# 编辑电子邮件地址策略

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2012-12-10_

电子邮件地址策略为您的收件人（包括用户、联系人和组）生成主电子邮件地址和辅电子邮件地址，以便接收人可以接收和发送电子邮件。

有关电子邮件地址策略的其他管理任务，请参阅 [电子邮件地址策略程序](email-address-policy-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：5 分钟。

  - 如果电子邮件地址策略是通过命令行管理程序创建的，将无法使用 Exchange 管理中心 (EAC) 来编辑该电子邮件地址策略。

  - 如果电子邮件地址策略是使用收件人筛选器创建的，则必须使用命令行管理程序来编辑电子邮件地址策略。有关详细信息，请参阅[通过使用收件人筛选器创建电子邮件地址策略](create-an-email-address-policy-by-using-recipient-filters-exchange-2013-help.md)。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[电子邮件地址和通讯簿](email-addresses-and-address-books-exchange-2013-help.md)主题中的“电子邮件地址策略”条目。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!WARNING]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 您想执行什么操作？

## 使用 EAC 更改向其应用策略的收件人

1.  导航到“邮件流” \> “电子邮件地址策略”。

2.  在此列表视图中，选择您要更改的电子邮件地址策略，然后单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  
    
    在“电子邮件地址策略”中，单击“应用至”并修改设置。

## 使用 EAC 更改电子邮件地址策略的优先级

对于同一电子邮件帐户，用户可以有多个代理电子邮件地址（例如，ayla@exchange.mail.contoso.com 或 ayla@contoso.com）。然后可以按优先级使用这些电子邮件地址。以下面的情形为例：您有两个电子邮件地址策略，可向其分配优先级 1 和 2。如果您创建另一个策略，将对其自动分配优先级 3。但是，如果有两个策略，并将其中一个的优先级指定为 1，那么在另一个策略创建后将向其分配默认优先级 2。在这种情况下，您创建的下一个策略在默认情况下将成为优先级为 2 的策略。上一个优先级为 2 的策略将分配优先级 3。

1.  导航到“邮件流” \> “电子邮件地址策略”。

2.  选择要更改其优先级的电子邮件地址策略，然后单击“提高优先级”![向上键图标](images/JJ150576.1732c727-328b-4a1a-b84d-6d7252c7dcab(EXCHG.150).gif "向上键图标") 或“降低优先级”![向下键图标](images/JJ150576.ef5ca57d-a033-457b-bd92-6361877c33d0(EXCHG.150).gif "向下键图标")。

## 使用命令行管理程序编辑电子邮件地址策略

本示例编辑当前包含 Georgia、Alabama 和 Louisiana 的收件人的 South East Offices 电子邮件地址策略，使其同时包含 Texas 的收件人。

    Set-EmailAddressPolicy -Identity "South East Offices" -ConditionalStateorProvince "Georgia","Alabama","Louisiana","Texas"

> [!NOTE]  
> 虽然已经将电子邮件地址策略应用到 Georgia、Alabama、和 Louisiana 中的收件人，但必须将它们包含在参数中，因为参数会覆盖值；参数不会将值附加到现有值。


有关语法和参数的详细信息，请参阅 [Set-EmailAddressPolicy](https://technet.microsoft.com/zh-cn/library/bb124517\(v=exchg.150\))。

