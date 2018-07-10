---
title: '电子邮件地址策略: Exchange 2013 Help'
TOCTitle: 电子邮件地址策略
ms:assetid: b63b63bb-6faf-4337-8441-50bc64b49bb8
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb232171(v=EXCHG.150)
ms:contentKeyID: 50491404
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 电子邮件地址策略

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2016-07-21_

收件人（包括用户、资源、联系人和组）是 Active Directory 中任何已启用邮件的对象，Microsoft Exchange 可以向其传递或路由邮件。为了使收件人可以发送或接收电子邮件，收件人必须有电子邮件地址。电子邮件地址策略为收件人生成主电子邮件地址和辅电子邮件地址，以便其可以接收和发送电子邮件。

默认情况下，Exchange 包含适用于所有已启用邮件的用户的电子邮件地址策略。此默认策略将收件人的别名指定为电子邮件地址的本地部分，并使用默认的接受域。电子邮件地址的本地部分是显示在符号 (@) 前面的名称。但是，可以更改电子邮件地址的显示方式。例如，您可以指定地址显示为 *firstname*.*lastname*@contoso.com。

此外，如果要为所有收件人或部分收件人指定其他电子邮件地址，可以修改默认策略或创建其他策略。例如，David Hamilton 的用户邮箱可接收发送到 hdavid@mail.contoso.com 和 hamilton.david@mail.contoso.com 的电子邮件。

是否要查找与电子邮件地址策略相关的管理任务？请参阅[电子邮件地址策略程序](email-address-policy-procedures-exchange-2013-help.md)。

## 收件人策略的行为

Exchange 将策略应用于符合收件人筛选条件的所有收件人：

  - 收件人策略按顺序应用（从最高优先级到最低优先级）。如果在两个或多个策略之间发生冲突，将应用具有最高优先级的策略。默认收件人策略始终具有最低优先级，并在没有其他策略相匹配的情况下应用。
    
    当你创建一个收件人策略，但没有明确指定优先级时，它将添加为最高优先级。如果你指定已与现有策略相关联的优先级，现有的策略和具有较低优先级的所有策略将会向下移动一个级别。将按指定的优先级插入新的策略。
    
    收件人策略功能分为两项功能：电子邮件地址策略和接受域。有关接受域的详细信息，请参阅[接受域](accepted-domains-exchange-2013-help.md)。

  - 运行 Exchange 命令行管理程序中的 **Update-EmailAddressPolicy** cmdlet 时，将使用电子邮件地址策略更新收件人对象。

  - 每次修改和保存收件人对象时，Exchange 强制实施正确应用电子邮件地址条件和设置。修改和保存电子邮件地址策略时，所有相关联的收件人将随着该更改而进行更新。此外，如果修改收件人对象，将重新评估并强制实施该收件人的电子邮件地址策略成员身份。

## 创建电子邮件地址策略

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

