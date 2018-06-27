---
title: 'UM 语言、提示和问候语: Exchange 2013 Help'
TOCTitle: UM 语言、提示和问候语
ms:assetid: d48df962-9669-420b-838f-44bfe1012e2f
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb124728(v=EXCHG.150)
ms:contentKeyID: 50491735
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# UM 语言、提示和问候语

 

_**适用于：**Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：**2016-12-09_

可以安装并配置语言包，以便在统一消息 (UM) 环境中支持多种语言。

UM 语言包允许呼叫者和 Outlook Voice Access 用户能够用多种语言与语音邮件系统交互。在邮箱服务器上新安装一种语言后，呼叫者和 Outlook Voice Access 用户可以使用该语言收听电子邮件以及与语音邮件系统交互。

有几个关键组件需要依赖 UM 语言包，以使用户和呼叫者能以多种语言与统一消息进行有效的交互。每个 UM 语言包都包含特定语言的语音合成 (TTS) 引擎、预先录制的提示以及对自动语音识别 (ASR) 和语音邮件预览的支持。本主题介绍 UM 语言包，使用 UM 语言包的 UM 组件，以及如何使用安装后的 UM 语言包配置 UM 拨号计划和 UM 自动助理以使用其他语言。

Exchange 统一消息语言包既特定于版本又特定于平台。在 Exchange Server 2007 及更高版本中，提供多个版本的 UM 语言包，包括 Exchange 2007 RTM 版、Exchange 2007 SP1、SP2 和 SP3、Exchange Server 2010 RTM 版、Exchange 2010 SP1 和 SP2 以及 Exchange 2013。对于其中某些版本，可同时支持 32 位和 64 位下载，但对其他版本而言，仅支持 64 位下载。

在邮箱服务器上安装版本和平台均正确的 UM 语言包尤为重要。如果邮箱服务器正在运行早期版本的 Exchange，或设计为支持 32 位平台，请不要在该服务器上安装 UM 语言包。

**目录**

UM 语言包概述

UM 语言组件和功能

语音邮件预览

统一消息语言

统一消息语言包

UM 拨号计划语言

UM 自动助理语言

客户端语言选择过程

## UM 语言包概述

通过统一消息语言包，邮箱服务器可以用另外的语言与呼叫者通信，并在呼叫者使用 ASR 或转录语音邮件时识别其他语言。UM 语言包中包含：

  - 采用 UM 语言包的语言预先录制的提示。例如，“After the tone, please record your message.When you’ve finished recording, hang up, or press the \# key for more options.”

  - 采用 UM 语言包的语言的语法文件，供邮箱服务器用来在目录中查找给定用户的名称。

  - 语音合成 (TTS) 转换，以便呼叫者用 UM 语言包的语言读取内容（电子邮件、日历、联系人信息等）。

  - 对自动语音识别的支持，这使呼叫者可以用 UM 语言包的语言通过语音用户界面 (VUI) 与 UM 交互。

  - 对语音邮件预览的支持，这使用户可以从支持的电子邮件客户端（例如 Outlook 或 Outlook Web App）中用特定语言读取转录的语音邮件。

UM 语言包中包含特定语言的预先录制的提示、TTS 转换支持，在某些情况下还包含 ASR 支持。在多语言环境中，可能必须安装额外的 UM 语言包，因为有些呼叫者喜欢使用其他语言的提示，或者会接收多种语言的电子邮件。若要支持邮箱服务器朗读包含多种语言的电子邮件的功能，必须安装多个 UM 语言包，因为必须指示 TTS 转换系统根据要朗读的邮件文本来选择语言。如果尚未安装统一消息语言包，如果将电子邮件读回给用户，电子邮件将不合逻辑或不清楚。安装相应的语言包可让 TTS 引擎通过使用正确语言对 Outlook Voice Access 用户读出电子邮件和日历项目，并且还提供特定语言的预先记录的提示以用于统一消息。在有些情况下，它们还可以提供 ASR 支持。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>TTS 引擎将文本转换为语音，但是不会将语音转换为文本。启用 UM 的用户可以将包含语音文件附件的电子邮件发送给其他用户。但是，不能创建基于文本的电子邮件并发送给其他用户。</td>
</tr>
</tbody>
</table>


安装语言包时，安装程序将执行下列操作：

1.  复制将用于配置 UM 拨号计划和自动助理的语言提示。

2.  允许 TTS 引擎在 Outlook Voice Access 用户访问其收件箱时朗读邮件。

3.  针对安装的语言，为启用语音的 UM 拨号计划和自动助理启用 ASR。

4.  用其他语言为客户端启用语音邮件预览。

从 Exchange Server 2013 UM 语言包下载 UM 语言包后，可以使用 **Setup.exe** 命令或运行 *\<UMLanguagePack\>*.exe 安装程序来添加 UM 语言包。但是，必须使用 Setup.exe 命令以删除 UM 语言包。不存在可用于在邮箱服务器中添加或删除语言的 Exchange 命令行管理程序 cmdlet。有关如何安装 UM 语言包的详细信息，请参阅[安装 UM 语言包](install-a-um-language-pack-exchange-2013-help.md)。有关如何删除 UM 语言包的详细信息，请参阅[删除 UM 语言包](remove-a-um-language-pack-exchange-2013-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>默认情况下，当您安装邮箱服务器时，会安装“美国英语”(en-US) 语言包。它无法删除，除非您从计算机中删除邮箱服务器。</td>
</tr>
</tbody>
</table>


返回顶部

下表列出了当前可用的统一消息语言包。此外，还列出了每个 UM 语言包的安装文件名以及 UM 语言的区域性 ID。

### UM 语言包安装文件名和区域性 ID

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
<th>语言</th>
<th>国家/地区</th>
<th>区域性 ID</th>
<th>安装文件名</th>
<th>可用性</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>加泰罗尼亚语</p></td>
<td><p>西班牙</p></td>
<td><p>ca-ES</p></td>
<td><p>UMLanguagePack.ca-ES</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">可进行下载</a></p></td>
</tr>
<tr class="even">
<td><p>中文（香港）</p></td>
<td><p>中国</p></td>
<td><p>zh-HK</p></td>
<td><p>UMLanguagePack.zh-HK</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">可进行下载</a></p></td>
</tr>
<tr class="odd">
<td><p>中文（简体）</p></td>
<td><p>中国</p></td>
<td><p>zh-CHS</p></td>
<td><p>UMLanguagePack.zh-CN</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">可进行下载</a></p></td>
</tr>
<tr class="even">
<td><p>中文（繁体）</p></td>
<td><p>中国台湾</p></td>
<td><p>zh-TW</p></td>
<td><p>UMLanguagePack.zh-TW</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">可进行下载</a></p></td>
</tr>
<tr class="odd">
<td><p>丹麦语</p></td>
<td><p>丹麦</p></td>
<td><p>da-DK</p></td>
<td><p>UMLanguagePack.da-DK</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">可进行下载</a></p></td>
</tr>
<tr class="even">
<td><p>荷兰语</p></td>
<td><p>荷兰</p></td>
<td><p>nl-NL</p></td>
<td><p>UMLanguagePack.nl-NL</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">可进行下载</a></p></td>
</tr>
<tr class="odd">
<td><p>英语</p></td>
<td><p>澳大利亚</p></td>
<td><p>en-AU</p></td>
<td><p>UMLanguagePack.en-AU</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">可进行下载</a></p></td>
</tr>
<tr class="even">
<td><p>英语</p></td>
<td><p>加拿大</p></td>
<td><p>en-CA</p></td>
<td><p>UMLanguagePack.en-CA</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">可进行下载</a></p></td>
</tr>
<tr class="odd">
<td><p>英语</p></td>
<td><p>印度</p></td>
<td><p>en-IN</p></td>
<td><p>UMLanguagePack.en-IN</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">可进行下载</a></p></td>
</tr>
<tr class="even">
<td><p>英语</p></td>
<td><p>英国</p></td>
<td><p>en-GB</p></td>
<td><p>UMLanguagePack.en-GB</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">可进行下载</a></p></td>
</tr>
<tr class="odd">
<td><p>英语</p></td>
<td><p>美国</p></td>
<td><p>en-US</p></td>
<td><p>包括邮箱服务器的安装</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">可进行下载</a></p></td>
</tr>
<tr class="even">
<td><p>芬兰语</p></td>
<td><p>芬兰</p></td>
<td><p>fi-Fl</p></td>
<td><p>UMLanguagePack.fi-Fl</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">可进行下载</a></p></td>
</tr>
<tr class="odd">
<td><p>法语</p></td>
<td><p>加拿大</p></td>
<td><p>fr-CA</p></td>
<td><p>UMLanguagePack.fr-CA</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">可进行下载</a></p></td>
</tr>
<tr class="even">
<td><p>法语</p></td>
<td><p>法国</p></td>
<td><p>fr-FR</p></td>
<td><p>UMLanguagePack.fr-FR</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">可进行下载</a></p></td>
</tr>
<tr class="odd">
<td><p>德语</p></td>
<td><p>德国</p></td>
<td><p>de-DE</p></td>
<td><p>UMLanguagePack.de-DE</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">可进行下载</a></p></td>
</tr>
<tr class="even">
<td><p>意大利语</p></td>
<td><p>意大利</p></td>
<td><p>it-IT</p></td>
<td><p>UMLanguagePack.it-IT</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">可进行下载</a></p></td>
</tr>
<tr class="odd">
<td><p>日语</p></td>
<td><p>日本</p></td>
<td><p>ja-JP</p></td>
<td><p>UMLanguagePack.ja-JP</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">可进行下载</a></p></td>
</tr>
<tr class="even">
<td><p>朝鲜语</p></td>
<td><p>朝鲜语</p></td>
<td><p>ko-KR</p></td>
<td><p>UMLanguagePack.ko-KR</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">可进行下载</a></p></td>
</tr>
<tr class="odd">
<td><p>挪威语（博克马尔）</p></td>
<td><p>挪威</p></td>
<td><p>nb-NO</p></td>
<td><p>UMLanguagePack.nb-NO</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">可进行下载</a></p></td>
</tr>
<tr class="even">
<td><p>波兰语</p></td>
<td><p>波兰</p></td>
<td><p>pl-PL</p></td>
<td><p>UMLanguagePack.pl-PL</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">可进行下载</a></p></td>
</tr>
<tr class="odd">
<td><p>葡萄牙语</p></td>
<td><p>巴西</p></td>
<td><p>pt-BR</p></td>
<td><p>UMLanguagePack.pt-BR</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">可进行下载</a></p></td>
</tr>
<tr class="even">
<td><p>葡萄牙语</p></td>
<td><p>葡萄牙</p></td>
<td><p>pt-PT</p></td>
<td><p>UMLanguagePack.pt-PT</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">可进行下载</a></p></td>
</tr>
<tr class="odd">
<td><p>俄语</p></td>
<td><p>俄罗斯</p></td>
<td><p>ru-RU</p></td>
<td><p>UMLanguagePack.ru-RU</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">可进行下载</a></p></td>
</tr>
<tr class="even">
<td><p>西班牙语</p></td>
<td><p>西班牙</p></td>
<td><p>es-ES</p></td>
<td><p>UMLanguagePack.es-ES</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">可进行下载</a></p></td>
</tr>
<tr class="odd">
<td><p>西班牙语</p></td>
<td><p>墨西哥</p></td>
<td><p>es-MX</p></td>
<td><p>UMLanguagePack.es-MX</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">可进行下载</a></p></td>
</tr>
<tr class="even">
<td><p>瑞典语</p></td>
<td><p>瑞典</p></td>
<td><p>sv-SE</p></td>
<td><p>UMLanguagePack.sv-SE</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">可进行下载</a></p></td>
</tr>
</tbody>
</table>


返回顶部

## UM 语言组件和功能

统一消息中有几个关键组件和功能，用户和呼叫者可使用它们与多语言语音邮件系统交互。若要使这些组件和功能正常使用，并使呼叫者能用多种语言与系统交互，则必须在邮箱服务器上正确安装 UM 语言包。

## 预先录制的提示

安装邮箱服务器角色时，同时安装了一组默认的音频提示文件。这些音频文件包含 Outlook Voice Access 菜单、语音邮件问候语以及 Exchange 统一消息使用的数字的录音。这些音频文件由邮箱服务器向传入的内部和外部呼叫者播放。许多音频文件为默认提示，为电话用户界面 (TUI) 和 Outlook Voice Access 的用户提供在 TUI 和语音用户界面 (VUI) 中移动所需的信息。提示位于 \<*程序文件*\>\\Microsoft\\Exchange Server\\V15\\UnifiedMessaging\\Prompts\\\<语言\>。不应替换或更改邮箱服务器用于帮助呼叫者浏览菜单的提示。

安装新的 UM 语言包时，也会安装该语言预先录制的提示。安装了 UM 语言包后，UM 拨号计划和自动助理就可以使用为该语言预先录制的提示了。

## TTS 语言

统一消息需要使用语音合成 (TTS) 引擎。TTS 功能由 Microsoft Speech Server 服务提供。TTS 引擎可读取书写的文本，并将其转换成呼叫者听得到的语音输出。TTS 引擎可读取并转换用户邮箱中的以下项目：

  - 电子邮件和语音邮件正文、主题和名称

  - 日历项目正文、主题、位置和名称

  - 私人联系人姓名

  - 用户的默认语音邮件问候语

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>用户录制了个性化语音邮件问候语后，就不再使用 TTS 版本的语音问候语了。</td>
</tr>
</tbody>
</table>


## 自动语音识别

除了 TTS，ASR 支持也包含在统一消息中。ASR 功能由 Microsoft Speech Server 服务提供。ASR 让呼叫者可以使用语音命令浏览菜单，并与其个人邮箱中的项目（包括邮件、私人联系人和日历）交互。每个语言包都包含 ASR 支持。

返回顶部

## 语音邮件预览

此外，UM 语言包还提供对语音邮件预览的支持，这使用户可以通过从支持的电子邮件客户端（例如 Outlook 或 Outlook Web App）中读取转录邮件快速筛选其语音邮件。

当呼叫者为启用 UM 的用户留下语音邮件时，语音邮件文件和转录的语音邮件将放入发送到该用户邮箱的语音邮件正文。

所有 UM 语言包都是可以下载的单个文件。这些语言包包括预先录制的提示、语法文件、语音合成 (TTS) 转换和 ASR。但是，并不是所有 UM 语言包都支持“语音邮件预览”。

以下 UM 语言包包含对所有组件和功能的支持，其中包括“语音邮件预览”：

  - 英语（美国）- (en-US)

  - 英语（加拿大）(en-CA)

  - 法语（法国）- (fr-FR)

  - 意大利语 - (it-IT)

  - 波兰语 (pl-PL)

  - 葡萄牙语（葡萄牙）(pt-PT)

  - 西班牙语（西班牙）(es-ES)

默认情况下，如果安装了受支持的 UM 语言包，则在安装邮箱服务器后，该服务器会向启用 UM 的用户发送语音邮件预览。

有许多统一消息语音邮件预览合作伙伴可以为“语音邮件预览”功能提供增强型的转录支持。这些合作伙伴雇用用户来更正使用自动语音识别 (ASR) 创建的语音邮件转录。各个语音邮件预览合作伙伴均必须符合一系列需要认证的要求，才能与统一消息进行交互操作。

如果发现向用户发送的语音邮件预览不够准确，则可以联系在[面向统一消息的 Microsoft Pinpoint](https://go.microsoft.com/fwlink/p/?linkid=261951) 页面中列出的某个已认证语音邮件预览合作伙伴，然后通过支付额外的费用来注册这些语音邮件预览。

可以从 [Microsoft 下载中心](https://go.microsoft.com/fwlink/p/?linkid=266542)下载 UM 语言包。有关详细信息，请参阅[安装 UM 语言包](install-a-um-language-pack-exchange-2013-help.md)。

## 统一消息语言

若要使呼叫者能够使用统一消息中的多语言功能，必须首先安装 UM 语言包。然后，可以选择配置其他 UM 组件。

  - 在您的组织中的邮箱服务器上安装 UM 语言包。

  - 如果需要，为 UM 拨号计划配置默认语言。这样，与 UM 拨号计划关联的 Outlook Voice Access 用户就可在访问其邮箱时使用该新语言了。但是用户仍可在 Outlook Web App 选项中配置其语言设置。

  - 如果需要在自动助理上启用多种语言，可在 UM 自动助理上配置语言设置。默认情况下，UM 自动助理使用 UM 拨号计划语言。但是，您可以更改此设置，允许未经身份验证的呼叫者连接到您的组织，并用在 UM 自动助理中指定的语言浏览自动助理菜单。

## 统一消息语言包

使用 Setup.com 在邮箱服务器上安装 UM 语言包。在安装新语言包后，与该语言包关联的语言将添加到您可以使用的可用语言列表中。您可查看已使用 Exchange 命令行管理程序中的 [Get-UMService](https://technet.microsoft.com/zh-cn/library/jj552407\(v=exchg.150\)) cmdlet 安装的语言。

安装 UM 语言包时，会复制 TTS 引擎使用的文件和所选语言预先录制的提示，并使它们可供连接到语音邮件系统的用户使用。可以从 [Microsoft 下载中心](https://go.microsoft.com/fwlink/p/?linkid=266542)下载 UM 语言包。有关详细信息，请参阅[安装 UM 语言包](install-a-um-language-pack-exchange-2013-help.md)。

## UM 拨号计划语言

创建的每个 UM 拨号计划都包含默认语言设置。由于统一消息可能必须使用 TTS 转换或在 Outlook Voice Access 用户访问其邮箱时为其播放标准音频提示，因此需要 UM 拨号计划语言设置。您不必选择默认拨号计划语言。

首次安装 Exchange 时，美国英语将是默认语言，并且是拨号计划的唯一可用语言选项。在邮箱服务器上安装 UM 语言包后，当您配置拨号计划的默认语言时，与该语言包关联的语言将被列为可用选项。

默认语言对呼叫者很重要。Outlook Voice Access 用户呼入到语音邮件系统时，使用的语言取决于 Outlook Web App 中的语言设置（用户首次登录邮箱时设置）。统一消息将 Outlook Web App 中设置的语言与用户关联到的拨号计划上的可用语言列表进行比较。如果没有适用的匹配，将会使用默认 UM 拨号计划语言。例如，如果您有仅包含来自法国的用户的拨号计划，则可能希望将拨号计划上的默认语言设置更改为法语。

## UM 自动助理语言

默认情况下，由于 UM 自动助理在创建时就与 UM 拨号计划关联，因此 UM 自动助理使用关联的 UM 拨号计划的默认语言设置。但是，创建 UM 自动助理后，可以更改此设置。

由于统一消息可能必须使用 TTS 转换，或为呼叫者播放标准的音频提示，因此需要 UM 自动助理语言设置。统一消息不检查自动助理自定义提示的语言与自动助理的语言设置是否匹配。但是，最好确保自动助理的语言设置与自定义提示的语言匹配。否则，呼叫者可能会听到系统从一种语言转换到另一种语言。

如果需要对呼叫者使用多个不同的特定语言自动助理，则能够更改 UM 自动助理设置也很有用。

## 客户端语言选择过程

通过 UM 语言包，呼叫者和 Outlook Voice Access 用户能够用多种语言与统一消息系统交互。在邮箱服务器上新安装一种语言包后，呼叫者和 Outlook Voice Access 用户就能够听到电子邮件并与语音邮件系统交互，Outlook Web App 用户和使用 Outlook 2010 或更高版本的用户可以使用“语音邮件预览”以特定语言查看语音邮件的转录。

若要支持某个特定语言，必须在每个邮箱服务器上安装该语言的 UM 客户端语言包。

在有些情况下，如果没有安装某个特定语言的 UM 语言包，并且该语言包不可用，则可使用客户端后备语言。有些语言有可供使用的后备 UM 客户端语言，但其他语言则没有。如果没有为某个特定语言安装 UM 语言包，并且该语言没有可用的后备语言，则将使用 en-US（美国英语）。

下表包括了邮箱服务器上未安装特定 UM 语言包时使用的客户端语言和后备语言列表。

### UM 的客户端后备语言

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>语言</th>
<th>国家/地区</th>
<th>区域性 ID</th>
<th>选择的第一种语言（如果已安装）</th>
<th>选择的第二种语言（如果已安装）</th>
<th>选择的第三种语言（如果已安装）</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>加泰罗尼亚语</p></td>
<td><p>西班牙</p></td>
<td><p>ca-ES</p></td>
<td><p>ca-ES</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>中文（香港）</p></td>
<td><p>中国</p></td>
<td><p>zh-HK</p></td>
<td><p>zh-HK</p></td>
<td><p>zh-CN</p></td>
<td><p>zh-TW</p></td>
</tr>
<tr class="odd">
<td><p>中文（简体）</p></td>
<td><p>中国</p></td>
<td><p>zh-CN</p></td>
<td><p>zh-CN</p></td>
<td><p>zh-HK</p></td>
<td><p>zh-TW</p></td>
</tr>
<tr class="even">
<td><p>中文（繁体）</p></td>
<td><p>中国台湾</p></td>
<td><p>zh-TW</p></td>
<td><p>zh-TW</p></td>
<td><p>zh-HK</p></td>
<td><p>zh-CN</p></td>
</tr>
<tr class="odd">
<td><p>丹麦语</p></td>
<td><p>丹麦</p></td>
<td><p>da-DK</p></td>
<td><p>da-DK</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>荷兰语</p></td>
<td><p>荷兰</p></td>
<td><p>nl-NL</p></td>
<td><p>nl-NL</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>英语</p></td>
<td><p>澳大利亚</p></td>
<td><p>en-AU</p></td>
<td><p>en-AU</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>英语</p></td>
<td><p>加拿大</p></td>
<td><p>en-CA</p></td>
<td><p>en-CA</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>英语</p></td>
<td><p>印度</p></td>
<td><p>en-IN</p></td>
<td><p>en-IN</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>英语</p></td>
<td><p>英国</p></td>
<td><p>en-GB</p></td>
<td><p>en-GB</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>英语</p></td>
<td><p>美国</p></td>
<td><p>en-US</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>芬兰语</p></td>
<td><p>芬兰</p></td>
<td><p>fi-FL</p></td>
<td><p>fi-FL</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>法语</p></td>
<td><p>加拿大</p></td>
<td><p>fr-CA</p></td>
<td><p>fr-CA</p></td>
<td><p>fr-FR</p></td>
<td><p>en-US</p></td>
</tr>
<tr class="even">
<td><p>法语</p></td>
<td><p>法国</p></td>
<td><p>fr-FR</p></td>
<td><p>fr-FR</p></td>
<td><p>fr-CA</p></td>
<td><p>en-US</p></td>
</tr>
<tr class="odd">
<td><p>德语</p></td>
<td><p>德国</p></td>
<td><p>de-DE</p></td>
<td><p>de-DE</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>意大利语</p></td>
<td><p>意大利</p></td>
<td><p>it-IT</p></td>
<td><p>it-IT</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>日语</p></td>
<td><p>日本</p></td>
<td><p>ja-JP</p></td>
<td><p>ja-JP</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>韩语</p></td>
<td><p>韩国</p></td>
<td><p>ko-KR</p></td>
<td><p>ko-KR</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>挪威语（博克马尔）</p></td>
<td><p>挪威</p></td>
<td><p>nb-NO</p></td>
<td><p>nb-NO</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>波兰语</p></td>
<td><p>波兰</p></td>
<td><p>pl-PL</p></td>
<td><p>pl-PL</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>葡萄牙语</p></td>
<td><p>巴西</p></td>
<td><p>pt-BR</p></td>
<td><p>pt-BR</p></td>
<td><p>pt-PT</p></td>
<td><p>en-US</p></td>
</tr>
<tr class="even">
<td><p>葡萄牙语</p></td>
<td><p>葡萄牙</p></td>
<td><p>pt-PT</p></td>
<td><p>pt-PT</p></td>
<td><p>pt-BR</p></td>
<td><p>en-US</p></td>
</tr>
<tr class="odd">
<td><p>俄语</p></td>
<td><p>俄罗斯</p></td>
<td><p>ru-RU</p></td>
<td><p>ru-RU</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>西班牙语</p></td>
<td><p>西班牙</p></td>
<td><p>es-ES</p></td>
<td><p>es-ES</p></td>
<td><p>es-MX</p></td>
<td><p>en-US</p></td>
</tr>
<tr class="odd">
<td><p>西班牙语</p></td>
<td><p>墨西哥</p></td>
<td><p>es-MX</p></td>
<td><p>es-MX</p></td>
<td><p>es-ES</p></td>
<td><p>en-US</p></td>
</tr>
<tr class="even">
<td><p>瑞典语</p></td>
<td><p>瑞典</p></td>
<td><p>sv-SE</p></td>
<td><p>sv-SE</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


返回顶部

