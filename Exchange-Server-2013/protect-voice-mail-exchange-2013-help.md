---
title: '保护语音邮件: Exchange 2013 Help'
TOCTitle: 保护语音邮件
ms:assetid: a88d41d5-2e70-4193-bcd3-dec50dff412b
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd351041(v=EXCHG.150)
ms:contentKeyID: 52061420
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 保护语音邮件

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2016-12-09_

某些旧版专用交换机 (PBX) 和 IP PBX 电话系统允许呼叫者将语音邮件标记为私人，阻止邮件的预期收件人将其转发给其他人。在集成语音邮件系统中，可通过多种方式访问语音邮件，这使得阻止将标记为私人的语音邮件暴露给非预期收听者更加具有挑战性。

统一消息 (UM) 可配置为使用 Active Directory 权限管理服务 (AD RMS) 来保护组织的语音邮件。此功能称为\&quot;受保护的语音邮件\&quot;。

当语音邮件受保护时，不但会阻止收件人转发此邮件，而且 UM 也会确保只有邮件的预期收件人可以访问其内容。可使用 MicrosoftOutlook 2010 或更高版本、Outlook Web App 或 Outlook Voice Access 来访问受保护的语音邮件。

**内容**

Overview of Protected Voice Mail

Overview of Active Directory Rights Management Services

Client support and end-user features

Protected voice mail structure

Composing a Protected Voice Mail message

UM mailbox policies

Text message notifications and Protected Voice Mail

## 受保护的语音邮件的概述

Exchange 2010 统一消息 (UM) 及更高版本附带受保护的语音邮件功能。它可在 UM 邮箱策略中进行配置，还可以使用 Exchange 管理控制台、Exchange 2010 中的命令行管理程序、Exchange 管理中心 (EAC) 或 Exchange 2013 命令行管理程序中的 cmdlet 配置所有受保护的语音邮件设置。

\&quot;受保护的语音邮件\&quot;是通过将信息权限管理 (IRM) 应用到语音邮件而实现的。当语音邮件受 UM 保护时：

  - 用户可以答复受保护的语音邮件。

  - 语音邮件的收件人不能转发该邮件。

  - 用户不能保存语音邮件的副本。

  - 用户不能保存或复制语音邮件的附加音频。

  - 只能由预期收件人打开语音邮件。

呼叫应答语音邮件和人际语音邮件（使用 Outlook Voice Access 发给用户的语音邮件）都可受 UM 保护。但是，保护不适用于以下类型的邮件：

  - 传真邮件。

  - 非语音邮件。例如，电子邮件或会议请求，即使是使用 Outlook Voice Access（语音答复）创建的也是如此。

返回顶部

## Active Directory 权限管理服务概述

AD RMS（Windows Server 2008 及更高版本的一个组件）可用于帮助保护文件，以便只有发件人希望的用户可以查看文件。AD RMS 通过指定用户访问文件所必须具有的权限来保护文件。可以配置权限以允许用户使用权限管理信息打开、修改、打印、转发或执行其他操作。使用 AD RMS 可以在数据分布于网络外部时保护数据。

AD RMS 系统具有服务器和客户端组件，包括以下内容：

  - 安装了 Windows Server 2008 R2 或更高版本且运行 Active Directory 权限管理服务服务器角色的服务器管理证书和许可证。

  - 数据库服务器。

  - AD RMS 客户端。AD RMS 客户端的最新版本作为 Windows 7 和 Windows 8 操作系统的一部分包括在内。

服务器组件由多个在 Microsoft 服务器（如 Windows Server 2008 或更高版本）上运行的 Web 服务组成。客户端组件可以在客户端或服务器操作系统上运行，并且包括使应用程序能够对内容进行加密和解密、检索模板和吊销列表以及从服务器获取许可证和证书的功能。

通过使用 AD RMS 和 AD RMS 客户端，可以通过保护信息通过保持永久的使用策略的信息，而不考虑移动位置增加组织的安全策略。可以使用 AD RMS 可以帮助防止敏感信息，如财务报表、 产品规格、 客户数据和机密电子邮件和语音邮件 — 落入有意或无意地错误。有关详细信息，请参阅[AD RMS 概述](https://go.microsoft.com/fwlink/p/?linkid=199436)。

在 Exchange UM 中，可使用信息权限管理 (IRM) 功能对邮件和附件应用持久保护。

使用 IRM 功能以及受保护的语音邮件，组织和用户可以控制收件人用于访问电子邮件和语音邮件的权限。IRM 还可用于限制某些收件人操作，例如向其他收件人转发邮件、打印邮件或附件，或者通过复制和粘贴提取邮件或附件内容。

## IRM 要求

您可以在 Exchange 实现 IRM 之前，您必须首先部署并配置 AD RMS 基础结构。有关详细信息，请参阅[Active Directory Rights Management Services](https://go.microsoft.com/fwlink/p/?linkid=199439)。若要实现 IRM 支持保护语音邮件在 Exchange 组织中，部署必须满足以下要求。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>服务器</th>
<th>要求</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>AD RMS 群集</p></td>
<td><ul>
<li><p>Windows Server 2008 R2 Standard 或 Enterprise SP1，或 Windows Server 2012 Standard 或 Datacenter。有关系统要求的详细信息，请参阅 <a href="exchange-2013-system-requirements-exchange-2013-help.md">Exchange 2013 系统要求</a>.</p></li>
<li><p><strong>服务连接点 (SCP)</strong>   Exchange 2013 和可感知 AD RMS 的应用程序使用在 Active Directory 中注册的 SCP 发现 AD RMS 群集和 URL。AD RMS 允许您在 AD RMS 安装程序中注册 SCP。如果用于安装 AD RMS 的帐户不是 Enterprise Admins 安全组成员，则可在安装之后执行 SCP 注册。一个 Active Directory 林中的 AD RMS 仅有一个 SCP。</p></li>
<li><p><strong>权限</strong>   必须为 Exchange 服务器组中的服务器或各个 Exchange 服务器分配对 AD RMS 服务器证书管道的读取和执行权限。AD RMS 服务器上的默认路径为 \inetpub\wwwroot\_wmcs\certification\ServerCertification.asmx。</p></li>
<li><p><strong>AD RMS 超级用户</strong>   若要启用传输解密、日记报告解密、Outlook Web App 中的 IRM 和 Exchange 搜索的 IRM，必须将联合传递邮箱（由 Exchange 安装程序创建的系统邮箱）添加到 AD RMS 群集上的 AD RMS 超级用户组。有关详细信息，请参阅<a href="add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md">将联合身份验证邮箱添加到 AD RMS 超级用户组</a>。</p></li>
</ul></td>
</tr>
</tbody>
</table>


## 配置和测试 IRM

必须使用命令行管理程序配置 IRM 功能。若要配置各项 IRM 功能，请使用 [Set-IRMConfiguration](https://technet.microsoft.com/zh-cn/library/dd979792\(v=exchg.150\)) cmdlet。有关如何配置 IRM 功能的详细信息，请参阅[信息权限管理过程](information-rights-management-procedures-exchange-2013-help.md)。

设置 Exchange 服务器之后，可使用 [Test-IRMConfiguration](https://technet.microsoft.com/zh-cn/library/dd979798\(v=exchg.150\)) cmdlet 执行 IRM 部署的端到端测试。此 cmdlet 验证组织的 IRM 配置且应在启用受保护的语音邮件之前运行。**Test-IRMConfiguration** cmdlet 将执行以下测试：

  - 检查 Exchange 组织的 IRM 配置。

  - 检查 AD RMS 服务器的版本和修补程序信息。

  - 验证是否可以通过检索权限帐户证书和客户端许可方证书 (CLC) 为 RMS 激活 Exchange 服务器。

  - 从 AD RMS 服务器获取 AD RMS 权限策略模板。

  - 验证指定的发件人是否可以发送受 IRM 保护的邮件。

  - 检索指定收件人的超级用户使用许可证。

  - 获取指定收件人的预许可证。

返回顶部

## 客户端支持和最终用户功能

用于收听受保护的语音邮件的电子邮件客户端软件必须支持 IRM 并且知道如何读取受 UM 保护的语音邮件。支持的电子邮件客户端包括 MicrosoftOutlook 2010 或更高版本、Outlook Web App 和 Outlook Voice Access。下表包含电子邮件客户端列表及其是否受支持的信息。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>电子邮件客户端</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook</p></td>
<td><ul>
<li><p>Outlook 2010 及更高版本支持受保护的语音邮件。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Outlook Web App</p></td>
<td><ul>
<li><p>Exchange 2010 或更高版本中的 Outlook Web App 支持受保护的语音邮件。早期版本的 Outlook Web App（也称为 Outlook Web Access）不支持受保护的语音邮件。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Outlook Voice Access</p></td>
<td><ul>
<li><p>Exchange 2010 及更高版本中的 Outlook Voice Access 支持受保护的语音邮件。Exchange 2007 中包含的 Outlook Voice Access 不支持受保护的语音邮件。</p></li>
<li><p>用户邮箱必须驻留在 Exchange 2010 或更高版本的邮箱服务器上。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Windows Mobile 或 Windows Phone</p></td>
<td><ul>
<li><p>Windows Mobile 不支持受保护的语音邮件。但是，Windows Phone 7 和 Windows Phone 8 支持受保护的语音邮件。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Exchange ActiveSync</p></td>
<td><ul>
<li><p>Exchange 2010 SP1 及更高版本中支持受保护的语音邮件。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>其他电子邮件客户端</p></td>
<td><ul>
<li><p>不支持受保护的语音邮件。</p></li>
</ul></td>
</tr>
</tbody>
</table>


返回顶部

## 受保护的语音邮件结构

实际上每个受保护的语音邮件包括两封邮件。第一封邮件是未加密的外部邮件。它包含名为 message.rpmsg 的附件。此附件包含受 IRM 保护的语音邮件和内部权限管理控制数据。权限管理控制数据包括内容密钥和权限信息，其中权限信息用于指定可以对语音邮件进行访问的用户以及访问方式。

受保护的语音邮件显示在\&quot;语音邮件\&quot;搜索文件夹的用户收件箱中。用户可以使用嵌入的音频播放器收听语音邮件，如同收听普通语音邮件一样，只是\&quot;转发\&quot;按钮将被禁用，并且在邮件顶部将显示一则注意事项，说明此邮件受到保护且不能转发的。

对于不支持受保护的语音邮件的电子邮件客户端，将显示外部邮件的正文。客户端软件不支持受保护的语音邮件时，管理员可以使用 UM 邮箱策略加入文本。可通过配置 UM 邮箱策略来自定义包括在电子邮件中的默认文本。例如，可以配置 UM 邮箱策略，以使用如下自定义文本：*\&quot;您无法打开此语音邮件，因为它受到保护。若要查看或收听此语音邮件，请在 https://mail.contoso.com 中登录邮箱或者拨打 +1 (425) 555-1234 呼叫 Outlook Voice Access。\&quot;*。

返回顶部

## 撰写受保护的语音邮件

可以在以下两种情况下创建受保护的语音邮件：

  - **呼叫应答**   呼叫者呼叫已启用 UM 的用户时会发生呼叫应答，但是用户无法应答此呼叫或者将其直接转发到语音邮件。在呼叫应答方案中，语音邮件系统将在呼叫者录制语音邮件之后播放一系列语音提示。
    
    然后，呼叫者可以从其他邮件选项中进行选择，包括按井号 (\#) 键将语音邮件标记为私人的选项。如果呼叫者按 \# 键，则他们可以按照 UM 提供的说明将邮件标记为私人、从私人语音邮件中删除私人标记或者将语音邮件的重要性标记为\&quot;高\&quot;。下图显示了呼叫者在为用户留下私人语音邮件时可以使用的菜单选项。
    
    > [!NOTE]  
    > 对于呼叫应答呼叫，UM 会使用邮件预期收件人 UM 邮箱策略上的受保护的语音邮件设置，因为呼叫者未经过身份验证。
    
    **创建使用呼叫应答的受保护的语音邮件**
    
    ![使用呼叫应答创建受保护的语音邮件](images/Dd351041.4e9f50bf-5066-4d0a-b3eb-0515a2fc4560(EXCHG.150).jpg "使用呼叫应答创建受保护的语音邮件")  

  - **Outlook Voice Access**   通过 Outlook Voice Access，已启用 UM 的用户可使用模拟、数字或移动电话（通过拨打其 Outlook Voice Access 号码）访问各自的邮箱。有两种统一消息用户界面可供已启用 UM 的用户使用：电话用户界面 (TUI) 和语音用户界面 (VUI)。
    
    Outlook Voice Access 用户可以在目录中搜索联系人并向其发送语音邮件。如果已经为已启用 UM 的收件人启用了受保护的语音邮件，则呼叫者可以在录制邮件之后将其标记为私人。或者，管理员可以配置 UM 邮箱策略，以确保经过身份验证的用户发送的所有语音邮件都受 UM 保护。
    
    > [!NOTE]  
    > 如果呼叫者经过身份验证，则将应用链接到该呼叫者的 UM 邮箱策略上的受保护的语音邮件设置，而不管语音邮件的预期收件人的 UM 邮箱策略设置如何。
    
    **创建使用语音用户界面的受保护的语音邮件**
    
    ![使用语音界面创建受保护的语音邮件](images/Dd351041.6b425ee4-5171-4a63-961f-bdbc6c79e1be(EXCHG.150).jpg "使用语音界面创建受保护的语音邮件")  
    
    **创建使用电话用户界面的受保护的语音邮件**
    
    ![使用按键输入创建受保护的语音邮件](images/Dd351041.dd58fd38-c4c3-437c-adc1-497deb3c8a9f(EXCHG.150).jpg "使用按键输入创建受保护的语音邮件")  

返回顶部

## UM 邮箱策略

可以创建统一消息邮箱策略，以对已启用 UM 的邮箱集合应用一组常用的 UM 策略设置，例如 PIN 策略设置、拨号限制和受保护的语音邮件设置。有关 UM 邮箱策略的详细信息，请参阅[管理 UM 邮箱策略](manage-a-um-mailbox-policy-exchange-2013-help.md)。

可以使用 EAC 或命令行管理程序中的 **Set-UMMailboxPolicy** cmdlet 配置受保护的语音邮件选项。下表列出了可以为受保护的语音邮件配置的设置。

**受保护的语音邮件设置**


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>命令行管理程序参数</th>
<th>是否为 EAC 中的可用设置？</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>ProtectAuthenticatedVoiceMail</em></p></td>
<td><p>是</p></td>
<td><p><em>ProtectAuthenticatedVoiceMail</em> 参数指定已启用 UM 的用户在使用 Outlook Voice Access 访问其邮箱时是否可以发送受保护的语音邮件。默认设置是 <code>None</code>。这意味着撰写语音邮件时不会实施保护，并且呼叫者不会有用于将语音邮件标记为&amp;quot;私人&amp;quot;的选项。如果将此值设置为 <code>Private</code>，则只有呼叫者标记为&amp;quot;私人&amp;quot;的邮件会受到保护。如果将此值设置为 <code>All</code>，则每个语音邮件都会受到保护，而不管呼叫者选择的选项如何。</p></td>
</tr>
<tr class="even">
<td><p><em>ProtectUnauthenticatedVoiceMail</em></p></td>
<td><p>是</p></td>
<td><p><em>ProtectUnauthenticatedVoiceMail</em> 参数指定邮箱服务器（这些服务器应答与 UM 邮箱策略相关联且已启用 UM 的用户的呼叫）是否创建受保护的语音邮件。将邮件从 UM 自动助理发送到已启用 UM 的用户时，也会应用此设置。默认设置是 <code>None</code>。这意味着不会对语音邮件实施保护，并且不会向呼叫者提供用于将邮件标记为&amp;quot;私人&amp;quot;的选项。如果将此值设置为 <code>Private</code>，则只有呼叫者标记为&amp;quot;私人&amp;quot;的邮件会受到保护。如果将此值设置为 <code>All</code>，则每个语音邮件都会受到保护，而不管呼叫者是否已将邮件标记为&amp;quot;私人&amp;quot;。</p></td>
</tr>
<tr class="odd">
<td><p><em>ProtectedVoiceMailText</em></p></td>
<td><p>是</p></td>
<td><p><em>ProtectedVoiceMailText</em> 参数指定要包括在受保护的语音邮件的外部邮件正文中的文本。此文本将显示在所有不支持受保护的语音邮件的电子邮件客户端应用程序中。请注意，此属性设置为 <code>Null</code> 或者为空时，UM 始终会提供一封默认邮件。</p></td>
</tr>
<tr class="even">
<td><p><em>RequireProtectedPlayOnPhone</em></p></td>
<td><p>是</p></td>
<td><p><em>RequireProtectedPlayOnPhone</em> 参数指定是否强制与 UM 邮箱策略相关联的用户通过电话（使用&amp;quot;在电话上播放&amp;quot;）收听受保护的语音邮件。默认值是 <code>$false.</code>。当此值设置为 <code>$true</code> 时，Outlook 或 Outlook Web App 中受保护的语音邮件窗体上的音频媒体播放器将显示为禁用。请注意，总是可访问语音邮件的预览文本。用户无法使用任何媒体播放器软件播放音频文件或使用嵌入的媒体播放器收听语音邮件。</p></td>
</tr>
<tr class="odd">
<td><p><em>AllowVoiceResponseToOtherMessageTypes</em></p></td>
<td><p>是</p></td>
<td><p><em>AllowVoiceResponseToOtherMessageTypes</em> 参数指定经过 Outlook Voice Access 的身份验证从而可以访问其电子邮件的用户是否能够撰写对电子邮件和会议请求的语音回复。</p></td>
</tr>
</tbody>
</table>


有关如何管理受保护的语音邮件设置的详细信息，请参阅[受保护的语音邮件过程](https://docs.microsoft.com/zh-cn/exchange/voice-mail-unified-messaging/set-up-client-voice-mail-features/protected-voice-mail-procedures)或 [Set-UMMailboxPolicy](https://technet.microsoft.com/zh-cn/library/bb124903\(v=exchg.150\))。

返回顶部

## 短信通知和受保护的语音邮件

将其 UM 帐户配置为收到语音邮件时向其移动电话发送短信通知（也称为 SMS 通知）的用户也会收到音频转录（语音邮件预览）文本，该文本是短信正文的一部分。但是，对于受保护的语音邮件，这表示可能会出现安全问题，因为语音邮件的内容应始终受到保护。

当 UM 为受到保护的语音邮件创建短信通知时，会检查语音邮件是否标记为\&quot;私人\&quot;。如果是，则不会向发送到移动电话的短信中添加转录音频文本。而是将以下文本包括在短信中：\&quot;请使用 Outlook Voice Access 访问此受保护的语音邮件。\&quot;

返回顶部

