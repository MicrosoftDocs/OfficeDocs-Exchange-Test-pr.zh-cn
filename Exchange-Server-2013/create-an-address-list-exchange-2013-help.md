---
title: '创建地址列表: Exchange 2013 Help'
TOCTitle: 创建地址列表
ms:assetid: e86ba1b7-c41c-4050-bc29-13996cf53c59
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb125036(v=EXCHG.150)
ms:contentKeyID: 50491845
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.OrganizationConfiguration.Mailbox.NewAddressListWizardForm.AddressListIntroductionPage
ms.translationtype: MT
---

# 创建地址列表

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2012-10-12_

地址列表是收件人和其他 Active Directory 对象的集合。每个地址列表都可以包含一种或多种类型的对象（如用户、联系人、组、公用文件夹、会议和其他资源）。地址列表还提供了一种在 Active Directory 中对启用邮件对象进行分区的机制，从而满足特定用户组的需求。

有关地址列表的其他管理任务，请参阅[地址列表程序](address-list-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：5 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [电子邮件地址和通讯簿权限](email-address-and-address-book-permissions-exchange-2013-help.md)主题中的\&quot;地址列表\&quot;条目。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 您想执行什么操作？

## 使用 EAC 创建地址列表

1.  导航至\&quot;组织\&quot;\>\&quot;地址列表\&quot;，然后单击\&quot;添加\&quot;![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。

2.  在\&quot;地址列表\&quot;中，键入名称并指定要包含在列表中的收件人类型。

3.  默认情况下，Exchange 创建包含组织中所有成员的地址列表。若要创建唯一自定义地址列表，请单击\&quot;**添加规则**\&quot;。
    
    > [!IMPORTANT]  
    > 如果不添加规则，将创建一个地址列表，其对于其中一个默认地址列表是冗余的。


4.  在列表中，选择筛选选项（例如\&quot;自定义属性 1\&quot;）。

5.  在\&quot;指定词语或短语\&quot;中，键入要作为筛选依据的词或短语，单击\&quot;添加\&quot;![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")，然后单击\&quot;确定\&quot;。
    
    通过重复执行第 4 步，可以继续添加多个短语或单词。筛选器创建的是 **OR** 布尔语句。例如，可创建一个筛选器，将地址列表应用于\&quot;自定义 1\&quot;属性等于\&quot;**俄勒冈州**\&quot;、\&quot;**爱达荷州**\&quot;或\&quot;**华盛顿州**\&quot;的用户。

6.  （可选）再次单击\&quot;**添加规则**\&quot;，添加其他筛选器。其他筛选器创建的是 **And** 布尔语句。添加的筛选器越多，向其应用地址列表的用户就越少。

7.  单击\&quot;预览地址列表包含的收件人\&quot;来查看将向其应用该地址列表的收件人。

8.  单击\&quot;保存\&quot;。

9.  你会看到警告，提示你在更新地址列表之前，无法应用地址列表。某些地址列表可能包含数千或数万个收件人，具体视组织规模以及你在地址列表中添加的筛选器而定。由于更新地址列表可能会影响你的资源，因此不妨在非高峰时段更新地址列表。
    
    有关更新地址列表的详细信息，请参阅[更新地址列表](update-an-address-list-exchange-2013-help.md)。

## 使用命令行管理程序创建地址列表

此示例使用 *RecipientFilter* 参数创建地址列表 MyAddressList，包括作为邮箱用户的收件人，并将 `StateOrProvince` 设置为 `Washington` 或 `Oregon`。

    New-AddressList -Name MyAddressList -RecipientFilter {((RecipientType -eq 'UserMailbox') -and ((StateOrProvince -eq 'Washington') -or (StateOrProvince -eq 'Oregon')))}

此示例使用内置条件在 All Rooms 父容器中创建 Building 34 Meeting Rooms 子地址列表。

    New-AddressList -Name "Building 34 Meeting Rooms" -Container "\All Rooms" -IncludedRecipients Resources -ConditionalCustomAttribute1 "Building 34"

有关语法和参数的详细信息，请参阅 [New-AddressList](https://technet.microsoft.com/zh-cn/library/aa996912\(v=exchg.150\))。

