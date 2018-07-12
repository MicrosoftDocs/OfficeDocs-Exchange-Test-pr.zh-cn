---
title: '创建电子邮件地址策略: Exchange 2013 Help'
TOCTitle: 创建电子邮件地址策略
ms:assetid: eb2bf42e-2058-4e17-85d5-97546433b40a
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb125137(v=EXCHG.150)
ms:contentKeyID: 50491903
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.OrganizationConfiguration.NewEmailAddressPolicyWizardForm.EmailAddressPolicyIntroductionPage
ms.translationtype: MT
---

# 创建电子邮件地址策略

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2012-12-10_

收件人必须有电子邮件地址，才能发送或接收电子邮件。电子邮件地址策略为收件人（包括用户、联系人和组）生成主电子邮件地址和辅助电子邮件地址，以便收件人可以接收和发送电子邮件。

创建电子邮件地址策略时，可以使用以下电子邮件地址类型：

  - **主 SMTP 电子邮件地址**。\&quot;*固有*\&quot;SMTP 电子邮件地址是为您提供的常用电子邮件地址类型。

  - **自定义 SMTP 电子邮件地址**。如果不希望使用固有 SMTP 电子邮件地址，您可以指定自定义的 SMTP 电子邮件地址。
    
    创建自定义的 SMTP 电子邮件地址时，可以使用下表中的变量为电子邮件地址的本地部分指定备用值。
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>变量</th>
    <th>值</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>%g</p></td>
    <td><p>名</p></td>
    </tr>
    <tr class="even">
    <td><p>%i</p></td>
    <td><p>中间名首字母</p></td>
    </tr>
    <tr class="odd">
    <td><p>%s</p></td>
    <td><p>姓</p></td>
    </tr>
    <tr class="even">
    <td><p>%d</p></td>
    <td><p>显示名称</p></td>
    </tr>
    <tr class="odd">
    <td><p>%m</p></td>
    <td><p>Exchange 别名</p></td>
    </tr>
    <tr class="even">
    <td><p>%<em>x</em>s</p></td>
    <td><p>使用姓的前 <em>x</em> 位字母。例如，如果 <em>x</em> =2，则使用姓的前两个字母。</p></td>
    </tr>
    <tr class="odd">
    <td><p>%<em>x</em>g</p></td>
    <td><p>使用给定名的前 <em>x</em> 位字母。例如，如果 <em>x</em> =2，则使用名的前两个字母。</p></td>
    </tr>
    </tbody>
    </table>


  - **非 SMTP 电子邮件地址**。支持以下类型的非 SMTP 电子邮件地址：
    
      - EX（旧版 DN 代理地址前缀 DisplayName）
    
      - X.500
    
      - X.400
    
      - MSMail
    
      - CcMail
    
      - Lotus Notes
    
      - Novell GroupWise
    
      - Exchange 统一消息代理地址（EUM 代理地址）
    
    > [!important]
    > 在 Exchange 中，所有非 SMTP 电子邮件地址都被视为自定义地址。Exchange 不会为 X.400、GroupWise 或 Lotus Notes 电子邮件地址类型提供唯一的对话框或属性页。如果添加非 SMTP 自定义电子邮件地址，则必须具有相应的动态链接库 (DLL) 文件。如果没有提供相应的 DLL 文件，则无法创建自定义电子邮件地址策略。以下错误将记录到事件查看器中：&amp;quot;在‘i386’计算机上，丢失了 Microsoft Exchange 目录中的‘SADF’地址类型的电子邮件地址描述对象&amp;quot;。


有关如何创建电子邮件地址策略的详细说明，请参阅下列主题：

[创建电子邮件地址策略](create-an-email-address-policy-exchange-2013-help.md)

[通过使用收件人筛选器创建电子邮件地址策略](create-an-email-address-policy-by-using-recipient-filters-exchange-2013-help.md)

## 在开始之前，您需要知道什么？

  - 估计完成时间：5 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [电子邮件地址和通讯簿](email-addresses-and-address-books-exchange-2013-help.md)主题中的\&quot;电子邮件地址策略\&quot;条目。

  - 必须先配置接受的域，然后才能在电子邮件地址策略中使用 SMTP 地址域。若要了解详细信息，请参阅[接受域](accepted-domains-exchange-2013-help.md)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!warning]
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 您想执行什么操作？

## 使用 EAC 创建电子邮件地址策略

1.  导航至\&quot;邮件流\&quot;\>\&quot;电子邮件地址策略\&quot;，然后单击\&quot;添加\&quot;![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。

2.  在\&quot;电子邮件地址策略\&quot;中，完成下列字段：
    
      - **策略名**
    
      - **电子邮件地址的格式**
    
      - **指定将应用此电子邮件地址的收件人类型**

3.  
    
    单击\&quot;**添加规则**\&quot;，进一步限制对其应用此策略的收件人。这会创建 **And** 布尔语句。
    
    > [!CAUTION]
    > 如果应用过多规则，则可能将电子邮件地址策略限制到不包含任何用户的程度。


4.  单击\&quot;预览应用策略的收件人\&quot;来查看将向其应用该策略的收件人。

5.  
    
    单击\&quot;保存\&quot;保存更改并创建策略。

6.  您将收到警告，在更新电子邮件地址策略之前，将不会应用该策略。在创建策略后，选择它，然后在详细信息窗格中，单击\&quot;应用\&quot;。

## 使用命令行管理程序创建电子邮件地址策略

本示例创建一个涵盖东南办事处邮箱用户（其电子邮件地址由他们的姓加上名的前两个字母组成）的电子邮件地址策略。

    New-EmailAddressPolicy -Name "southeast offices" -IncludedRecipients MailboxUsers -ConditionalStateorProvince "Georgia","Alabama","Louisiana" -EnabledEmailAddressTemplates "SMTP:%s%2g@southeast.contoso.com"

有关语法和参数的详细信息，请参阅 [New-EmailAddressPolicy](https://technet.microsoft.com/zh-cn/library/aa996800\(v=exchg.150\))。

