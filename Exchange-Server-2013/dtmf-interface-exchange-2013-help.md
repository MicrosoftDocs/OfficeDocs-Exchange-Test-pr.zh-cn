---
title: 'DTMF 接口: Exchange Online Help'
TOCTitle: DTMF 接口
ms:assetid: 2c7c9d8a-ed12-4dcf-a5b7-3cea0e785e49
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa996919(v=EXCHG.150)
ms:contentKeyID: 54652236
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# DTMF 接口

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2016-12-09_

在统一消息 (UM) 中，呼叫方可以使用双音多频 (DTMF)（也称为按键）和语音输入与系统进行交互。呼叫方可以使用的方法取决于 UM 拨号计划和自动助理的配置方式。

通过 DTMF 界面，呼叫方可以在拨打拨号计划中配置的 Outlook Voice Access 号码或拨打自动助理中配置的电话号码时，使用电话软键盘定位用户并导航 UM 语音邮件菜单系统。本主题讨论了 DTMF 界面，以及呼叫方如何使用 DTMF 界面定位用户并导航 UM 语音邮件菜单系统。

**目录**

DTMF overview

UM dial plans and dial by name

DTMF maps

DTMF maps for users who aren't enabled for Unified Messaging

DTMF maps for users who are enabled for Unified Messaging

For more information

## DTMF 概述

DTMF 要求呼叫方在电话软键盘上按下与统一消息菜单选项对应的按键，或者利用按键上的字母拼写并输入用户名或电子邮件别名。呼叫方可能会使用 DTMF 的原因在于其未启用自动语音识别 (ASR) 或者试图使用语音命令但失败。在上述任意一种情况下，呼叫方都会使用 DTMF 输入来导航菜单和搜索用户。

默认情况下，在 UM 中，DTMF 输入用于拨号计划，并且是 UM 自动助理的默认呼叫方界面。

呼叫方可以将 DTMF 输入用于：

  - 拨号计划拨入访问（使用 Outlook Voice Access）。

  - 拨号计划目录查找和搜索以定位用户。

  - 未启用语音的自动助理。

  - 已启用语音且配置或未配置 DTMF 回退自动助理的自动助理。

  - DTMF 回退自动助理（未启用语音）。

## UM 拨号计划和按名字拨叫

创建 UM 拨号计划时，您可以配置呼叫方在搜索用户或希望与用户联系时用来查找姓名的主要和辅助输入方法。这些设置位于拨号计划的\&quot;设置\&quot;页面，名为\&quot;用于搜索姓名的主要方法\&quot;和\&quot;用于搜索姓名的辅助方法\&quot;。用于搜索姓名的主要和辅助方法的可用选项如下：

  - 姓 名

  - 名 姓

  - SMTP 地址

此外，\&quot;无\&quot;是用于搜索姓名的辅助方法的可用选项。

默认情况下，\&quot;姓氏 名字\&quot;被选为用于搜索姓名的主要方法，而\&quot;SMTP 地址\&quot;被选为用于搜索姓名的辅助方法。因此，当呼叫方拨入 UM 拨号计划上配置的 Outlook Voice Access 号码时，会听到拨号计划的欢迎消息，比如话务员会说\&quot;欢迎使用 Contoso Outlook Voice Access。若要访问邮箱，请输入分机号码。若要与某人联系，请按井号键。\&quot;在呼叫方按井号键之后，系统会答复\&quot;请拼写您要呼叫的人员的姓名，姓在前，或者拼写其电子邮件别名，按井号键两次。\&quot;在这种情况下，系统随后会提示呼叫方先输入用户的姓，然后再输入用户的名（即\&quot;姓氏 名字\&quot;），或者拼写不包括域名的电子邮件别名，具体取决于拨号计划的配置方式。例如，如果用户的电子邮件别名是 tsmith@contoso.com，则呼叫方应输入 tsmith。

如果由于默认设置无法满足您的需求而要更改此配置，可以将其更改为让呼叫方先输入用户的电子邮件别名，或者先输入用户的名，然后再输入用户的姓。在这种情况下，您要将\&quot;SMTP 地址\&quot;设置配置为\&quot;用于搜索姓名的主要方法\&quot;，并将\&quot;名字 姓氏\&quot;设置配置为\&quot;用于搜索姓名的辅助方法\&quot;。按名字拨叫方法设置也适用于与拨号计划相关联的所有 UM 自动助理。若要让呼叫方能够使用 DTMF 输入或电话软键盘上的按键输入用户名，组织目录中必须存在 DTMF 映射及相应的用户值。

有关如何在 UM 拨号计划中更改按名字拨叫主要和辅助方法的详细信息，请参阅[配置 Outlook Voice Access 用户搜索的主要方式](configure-the-primary-way-for-outlook-voice-access-users-to-search-exchange-2013-help.md)和[配置 Outlook Voice Access 用户搜索的辅助方式](configure-the-secondary-way-for-outlook-voice-access-users-to-search-exchange-2013-help.md)。

返回顶部

## DTMF 映射

在 Exchange 组织中，名为 **msExchUMDtmfMap** 的属性与目录中创建的每个用户相关联。统一消息使用该属性将用户的名、姓和电子邮件别名映射到一组数。这种映射也称为 DTMF 映射。借助 DTMF 映射，呼叫方可以在电话软键盘上输入与用户名或电子邮件别名的字母相对应的数字。该属性包含为用户创建 DTMF 映射时所需的值，其映射依据分别为用户名和姓、用户姓和名以及用户的电子邮件别名。

下表介绍了已启用 UM 的用户（用户名为 Tony Smith，电子邮件别名为 tsmith@contoso.com）的 **msExchUMDtmfMap** 属性的 DTMF 映射值，这些值将存储在 Active Directory 中。

**已启用 UM 的用户（用户名为 Tony Smith）的已存储 DTMF 值**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>目录条目</th>
<th>用户名</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li><p>firstNameLastName:866976484</p></li>
</ul></td>
<td><p>tonysmith</p></td>
</tr>
<tr class="even">
<td><ul>
<li><p>lastNameFirstName:764848669</p></li>
</ul></td>
<td><p>smithtony</p></td>
</tr>
<tr class="odd">
<td><ul>
<li><p>emailAddress:876484</p></li>
</ul></td>
<td><p>tsmith</p></td>
</tr>
</tbody>
</table>


用户名和电子邮件别名可能包含其他非字母数字字符，例如逗号、连字符、下划线或句号。用户的 DTMF 映射中不能使用这些字符。例如，如果 Tony Smith 的电子邮件别名是 tony-smith@contoso.com，那么 DTMF 映射值为 866976484，其中不包括连字符。但是，如果用户的电子邮件别名包含一个或多个数字（例如 tonysmith123@contoso.com），则所创建的 DTMF 映射中会使用这些数字。tonysmith123 的 DTMF 映射是 866976484123。

只有当用户的 DTMF 映射存在时，呼叫方才能输入用户名或电子邮件别名。但是，并非所有用户都有与用户帐户相关联的 DTMF 映射。

返回顶部

## 未启用统一消息的用户的 DTMF 映射

默认情况下，用户（包括已启用邮箱的用户）未启用统一消息。**msExchUMDtmfMap** 属性填充有为未启用 UM 的用户进行 DTMF 映射所需的值。默认情况下，在为所有用户创建邮箱时也会创建以下 DTMF 映射：

1.  emailAddress

2.  firstNameLastName

3.  lastNameFirstName

如果用户没有为自己的帐户定义 DTMF 映射值，则呼叫方在从 UM 自动助理菜单按下电话按键或执行目录搜索时将无法与用户联系。此外，已启用 UM 的用户无法向没有 DTMF 映射的用户发送邮件或转移呼叫，除非他们可以使用自动语音识别 (ASR)。若要让呼叫方使用电话软键盘转移呼叫或与未启用 UM 的用户联系，您必须为这些用户的 DTMF 映射创建必要的值。可以使用带有 *-CreateDtmfMap* 参数的 **Set-User** cmdlet 来创建和更新单个用户的 DTMF 映射；如果用户名在 DTMF 映射创建后发生变化，也可以使用上述命令更新该用户的 DTMF 映射。还可以选择使用此 cmdlet 创建 Exchange 命令行管理程序脚本，从而更新多个用户的 DTMF 映射值。

有关 **Set-User** cmdlet 的详细信息，请参阅 [Set-User](https://technet.microsoft.com/zh-cn/library/aa998221\(v=exchg.150\))。

返回顶部

## 已启用统一消息的用户的 DTMF 映射

默认情况下，为用户启用统一消息时，就会为他们创建 DTMF 映射。这样，可以将来自以下对象的呼叫转移给已启用 UM 的用户：外部呼叫方、未启用 UM 的用户以及其他使用电话软键盘拼写用户名或电子邮件别名的已启用 UM 的用户。

在您为已启用 UM 的用户创建 DTMF 映射值后，呼叫方便可使用目录搜索功能。当呼叫方使用电话软键盘进行如下操作时，就会用到目录搜索功能：

  - 拨入 Outlook Voice Access 号码时，需要确定或搜索用户。

  - 拨入 UM 自动助理时，需要将呼叫定位或转移给已启用 UM 的用户。

有关如何为用户启用统一消息的详细信息，请参阅[为用户启用语音邮件](enable-a-user-for-voice-mail-exchange-2013-help.md)。

有时，为用户启用 UM 后，用户的名、姓或电子邮件别名会发生变化。用户的 DTMF 映射值不会自动更新。如果呼叫方输入新的用户名或电子邮件别名，但用户的 DTMF 映射还没有更新以反映用户名或电子邮件别名的变化，那么呼叫方将无法在目录中定位用户，无法向用户发送邮件，也无法将呼叫转移给用户。如果在为用户启用 UM 后必须更新用户的 DTMF 映射，可以使用带有 *-CreateDtmfMap* 参数的 **Set-User** cmdlet。如果希望为多个已启用 UM 的用户更新 DTMF 映射，也可以使用此 cmdlet 创建 Exchange 命令行管理程序脚本。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876845.Caution(EXCHG.150).gif" title="小心" alt="小心" />小心：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>我们建议您不要使用 ADSI 编辑器等工具手动更改用户的 DTMF 值，因为这可能会导致配置不一致或其他错误。建议您仅使用 <strong>Set-UMService</strong> 或 <strong>Set-User</strong> cmdlet 创建或更新用户的 DTMF 映射。</td>
</tr>
</tbody>
</table>


## 详细信息

[Adsiedit 概述](https://go.microsoft.com/fwlink/p/?linkid=73175)

