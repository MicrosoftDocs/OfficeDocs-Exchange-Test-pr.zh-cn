---
title: '设置 Outlook Voice Access: Exchange Online Help'
TOCTitle: 设置 Outlook Voice Access
ms:assetid: 5ce8c877-35f3-4e55-a65e-5ca469aeae99
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd298010(v=EXCHG.150)
ms:contentKeyID: 50556580
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 设置 Outlook Voice Access

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2015-03-09_

Microsoft Outlook Voice Access 允许启用了 Exchange 统一消息 (UM) 的用户使用模拟、数字或移动电话访问其邮箱。

Outlook Voice Access 用户（也称为\&quot;订阅者\&quot;）是组织中已启用统一消息的用户。订阅者可使用 Outlook Voice Access 通过电话来访问邮箱，检索电子邮件、语音邮件、个人联系人和日历信息。

**目录**

Outlook Voice Access overview

Outlook Voice Access interfaces

Outlook Voice Access scenarios

Distribution groups and contact groups

Choosing a language

Controlling Outlook Voice Access features

## Outlook Voice Access 概述

在 Microsoft Exchange UM 中，启用了 UM 的用户可以呼叫在 UM 拨号计划中配置的内部或外部电话号码，以访问其邮箱和使用 Outlook Voice Access 菜单系统。使用此菜单，启用了 UM 的用户可以读取电子邮件、收听语音邮件、与其 Outlook 日历交互、访问其个人联系人以及执行各种任务，例如配置其 Outlook Voice Access PIN 和录制语音邮件问候语。

经过身份验证和未经身份验证这两类用户均可拨打 Outlook Voice Access 号码。当未经身份验证的用户拨打 UM 拨号计划上设置的 Outlook Voice Access 号码时，只能对用户执行目录搜索。经过身份验证的用户（即输入其 PIN 的用户）可以执行目录搜索，并登录其邮箱以监听电子邮件、日历项目和语音邮件，以及搜索个人联系人。如果在目录或个人联系人中搜索用户，则在找到用户后，即可将呼叫转移给用户或拨打用户的分机号码。

## Outlook Voice Access 界面

Outlook Voice Access 用户具有两个可用的统一消息用户界面：电话用户界面 (TUI) 和使用自动语音识别 (ASR) 的语音用户界面 (VUI)。

必须先在 UM 拨号计划和 UM 邮箱策略中为用户启用 VUI，然后用户才能在 Outlook Voice Access 中使用 VUI。默认情况下，当您创建拨号计划和 UM 邮箱策略并为用户启用语音邮件之后，该用户即可使用 ASR 或 Outlook Voice Access VUI 导航菜单、邮件或其他选项。但是，即使用户能够使用 VUI，他们仍需使用电话键盘来输入 PIN、导航个人选项和执行目录搜索。下表列出了默认设置。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>UM 组件</th>
<th>默认设置</th>
<th>启用 VUI 访问的 Exchange 命令行管理程序示例</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>UM 拨号计划</p></td>
<td><p>已启用</p></td>
<td><p><code>Set-UMDialPlan -id MyUMDialPlan -AutomaticSpeechRecognitionEnabled  $true</code></p></td>
</tr>
<tr class="even">
<td><p>UM 邮箱策略</p></td>
<td><p>已启用</p></td>
<td><p><code>Set-UMMaiboxPolicy -id MyUMPolicy -AllowAutomaticSpeechRecognition  $true</code></p></td>
</tr>
<tr class="odd">
<td><p>用户的邮箱</p></td>
<td><p>已启用</p></td>
<td><p><code>Set-UMMailbox -id tonysmith -AutomaticSpeechRecognitionEnabled $true</code></p></td>
</tr>
</tbody>
</table>


下一部分列出了许多描述 VUI 功能的方案。

返回顶部

## Outlook Voice Access 方案

以下示例展示如何通过电话使用 Outlook Voice Access：

  - **访问电子邮件**   Outlook Voice Access 用户用电话拨打 Outlook Voice Access 号码，希望访问电子邮件。此时听到语音提示\&quot;欢迎使用，您已连接到 Microsoft Exchange。若要访问邮箱，请输入分机号码。若要与某人联系，请按井号键。\&quot;用户输入邮箱的分机号码之后，将听到语音提示\&quot;请输入您的 PIN 并按井号键。\&quot;用户输入 PIN 之后，语音提示说：\&quot;您有两封新的语音邮件，10 封新的电子邮件，您的下一次会议时间是上午 10:00。请说出语音邮件、电子邮件、日历、个人联系人、目录或个人选项。\&quot;当用户说出\&quot;电子邮件\&quot;时，语音邮件系统将读取用户邮箱中邮件的邮件头、名称、主题、时间和优先级。

  - **访问日历**   Outlook Voice Access 用户用电话拨打 Outlook Voice Access 号码，希望访问日历。此时听到语音提示\&quot;欢迎使用，您已连接到 Microsoft Exchange。若要访问邮箱，请输入分机号码。若要与某人联系，请按井号键。\&quot;用户输入邮箱的分机号码之后，将听到语音提示\&quot;请输入您的 PIN 并按井号键。\&quot;用户输入 PIN 之后，语音提示说：\&quot;您有两封新的语音邮件，10 封新的电子邮件，您的下一次会议时间是上午 10:00。请说出语音邮件、电子邮件、日历、个人联系人、目录或个人选项。\&quot;用户说\&quot;日历\&quot;后，语音邮件系统说：\&quot;好，我应打开哪天？\&quot;用户说\&quot;今天的日历\&quot;。语音邮件系统回答\&quot;正在打开今天的日历\&quot;。语音邮件系统将读出用户当天的每个日历约会。
    
    > [!NOTE]  
    > 如果运行 Microsoft Exchange 统一消息服务的邮箱服务器在用户邮箱中遇到损坏的日历项，将无法读出该项目，但是将使呼叫者返回 Outlook Voice Access 主菜单，并且不再读出当天其他时间可能安排的任何其他会议。


  - **访问语音邮件**   Outlook Voice Access 用户用电话拨打 Outlook Voice Access 号码，希望访问语音邮件。此时听到语音问候语\&quot;欢迎使用，您已连接到 Microsoft Exchange。若要访问邮箱，请输入分机号码。若要与某人联系，请按井号键。\&quot;用户输入邮箱的分机号码之后，将听到语音提示\&quot;请输入您的 PIN 并按井号键。\&quot;用户输入 PIN 之后，语音提示说：\&quot;您有两封新的语音邮件，10 封新的电子邮件，您的下一次会议时间是上午 10:00。请说出语音邮件、电子邮件、日历、个人联系人、目录或个人选项。\&quot;用户说出\&quot;语音邮件\&quot;，语音邮件系统将读取用户邮箱中语音邮件的邮件头、名称、主题、时间和优先级。
    
    > [!NOTE]  
    > 如果启用了语音识别，用户可以使用语音输入访问其启用了 UM 的邮箱。订阅者还可以通过按 0 使用按键（又名&amp;quot;双音多频 (DTMF)&amp;quot;）进行访问。不会为 PIN 输入启用语音识别。


  - **在目录中查找用户**   Outlook Voice Access 用户用电话拨打 Outlook Voice Access 号码，希望通过拼写其电子邮件的别名在目录中查找用户。此时听到语音问候语\&quot;欢迎使用，您已连接到 Microsoft Exchange。若要与某人联系，请按井号键。\&quot;用户按下井号键，然后使用按键输入拼出该人员的 SMTP 地址。
    
    > [!NOTE]  
    > Outlook Voice Access 号码的目录搜索功能不支持语音。用户只能通过使用按键输入来拼出要联系的人员的姓名。
    
    > [!IMPORTANT]  
    > 在某些公司（特别是东亚的公司）中，营业室电话键上可能未显示字母。这样的话，如果不了解键映射的工作原理，几乎就无法运用使用按键接口的读出姓名功能。默认情况下，统一消息使用 E.161 键映射。例如，2=ABC、3=DEF、4=GHI、5=JKL、6=MNO、7=PQRS、8=TUV、9=WXYZ。
    
    在输入字母和数字的组合（例如\&quot;Mike1092\&quot;）时，数字将映射到其自身。为正确输入电子邮件别名\&quot;Mike1092\&quot;，用户必须按数字 64531092。同时，对于 A-Z 和 0-9 以外的字符，不存在对应的电话键。因此，不应输入这些字符。例如，应将电子邮件别名\&quot;jim.wilson\&quot;输入为 546945766。即使要输入的字符有 10 个，用户也只需输入 9 个数字，因为句点 (.) 没有对应的数字。

返回顶部

## 通讯组和联系人组

用户可使用 Outlook Voice Access 来发送或转发语音邮件、电子邮件或会议请求。可以向以下任何人发送或转发邮件或会议请求：

  - 个人\&quot;联系人\&quot;文件夹中的人员

  - 组织的共享通讯簿中的人员

  - 已在\&quot;联系人\&quot;文件夹中创建的联系人组

  - 包括在组织的共享通讯簿中的通讯组

可使用 VUI（如果已启用 ASR）或电话键盘上的按键输入来发送邮件或会议请求。也可使用 Outlook Voice Access 来收听有关组的详情，包括组中的成员。

> [!NOTE]  
> 如果用户尝试将邮件发送到不包含任何成员的组（共享通讯簿中的通讯组或个人&amp;quot;联系人&amp;quot;文件夹中的联系人组），语音邮件系统将不会向他们提供用于发送或转发邮件或会议请求的选项。如果尝试将没有成员的组作为通过电话创建的邮件或会议请求的其中一位收件人进行添加，语言邮件系统不会将该组添加到邮件，并且会说&amp;quot;由于联系人似乎没有有效的电子邮件地址，因此无法发送。&amp;quot;


## 选择语言

用户无法更改 Outlook Voice Access 用来与他们进行对话的语言。语音邮件系统将尝试查找并使用与用户登录到 MicrosoftOutlook Web App 时所选择的、或者在 Outlook Web App 中的区域设置上所选择的语言最匹配的语言。如果他们选择的语言不受 Outlook Voice Access 支持，语音邮件系统将使用在提示呼叫者留下语言邮件时所使用的同一语言。

返回顶部

## 控制 Outlook Voice Access 功能

默认情况下，当用户拨号连接到 Outlook Voice Access 时，他们可以使用电话来访问其日历、电子邮件和个人联系人并搜索目录。可以使用命令行管理程序在用户使用 Outlook Voice Access 访问其邮箱时，阻止他们访问这些功能中的一项或多项功能。在 UM 邮箱策略上修改 Outlook Voice Access 功能时，您的更改会影响与此 UM 邮箱策略相关联的所有用户。您也可以禁用单个用户邮箱中的某些功能，而另一些功能仅可在 UM 邮箱策略中禁用，并且在个别邮箱中不可用。

> [!NOTE]  
> 只能使用命令行管理程序为启用 UM 的邮箱或 UM 邮箱策略修改 Outlook Voice Access TUI 设置。


**UM 邮箱策略设置：** 您可以禁止用户访问 UM 邮箱策略上的以下 Outlook Voice Access 功能：

  - 自动语音识别

  - 对语音邮件的无 PIN 访问

  - 对其他邮件的语音响应

  - 对其日历的 TUI 访问

  - 对目录的 TUI 访问

  - 对其电子邮件的 TUI 访问

  - 对其个人联系人的 TUI 访问

**已启用 UM 的邮箱设置**   可以针对用户邮箱禁用用户对以下 Outlook Voice Access 功能的访问：

  - 对日历的 TUI 访问

  - 对电子邮件的 TUI 访问

  - 自动语音识别

您可以阻止用户接收语音邮件，但允许他们保留使用 Outlook Voice Access 访问其邮箱的能力。您可以为用户启用 UM，并使用组织中其他用户当前未使用的分机号码配置用户的邮箱。

返回顶部

