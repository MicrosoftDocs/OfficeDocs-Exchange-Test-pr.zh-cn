---
title: '更新地址列表: Exchange 2013 Help'
TOCTitle: 更新地址列表
ms:assetid: 163e7099-cf14-4bb0-a84c-1401e9db670e
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa996375(v=EXCHG.150)
ms:contentKeyID: 50489955
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.OrganizationConfiguration.Mailbox.UpdateAddressListWizardForm.ScheduleWizardPage
ms.translationtype: HT
---

# 更新地址列表

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2012-10-14_

地址列表是收件人和其他 Active Directory 对象的集合。在完成对地址列表筛选规则的编辑后，应用地址列表。若要更新地址列表的成员身份以包含新的收件人并删除那些不再符合筛选条件的收件人，必须应用地址列表。

有关地址列表的更多管理任务，请参阅[地址列表程序](address-list-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：此过程可能需要较长时间才能完成，具体取决于地址列表中的收件人数。

  - 某些地址列表包含数千或数万个收件人，具体取决于组织的大小和添加到地址列表的筛选器。更新地址列表可能会占用大量计算机资源。因此，您可能需要在非高峰期更新地址列表。

  - 如果地址列表包含 3,000 多个收件人，建议使用 Exchange 命令行管理程序更新地址列表。

若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 您想执行什么操作？

## 使用 EAC 更新地址列表

1.  导航到“组织”\>“地址列表”。

2.  在列表视图中，选择要更新的地址列表。

3.  在详细信息窗格中，单击“更新”。

## 使用命令行管理程序更新地址列表

本示例更新地址列表 Washington State。

```powershell
Update-AddressList "Washington State"
```

如果有多个名称相同的地址列表，则必须指定要更新的地址列表的完整路径。例如，如果要更新“北美洲”下的 Sales 地址列表，但在“欧洲”下也有一个 Sales 地址列表，则使用以下命令：

```powershell
Update-AddressList "North America\Sales"
```

有关语法和参数的详细信息，请参阅[Update-AddressList](https://technet.microsoft.com/zh-cn/library/aa997982\(v=exchg.150\))。

