---
title: '使用 Outlook Web App Web 部件: Exchange 2013 Help'
TOCTitle: 使用 Outlook Web App Web 部件
ms:assetid: 7272e3ab-430c-4d6c-8621-9535236ce463
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Mt574711(v=EXCHG.150)
ms:contentKeyID: 70086928
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 使用 Outlook Web App Web 部件

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-07-31_

可以使用 MicrosoftOfficeOutlook Web App Web 部件指定要打开的邮箱、该邮箱中要打开的文件夹以及要使用的内容视图。

使用 Outlook Web App Web 部件可以直接通过 URL 访问 Outlook Web App 内容。URL 可以在 Web 浏览器中输入，也可以嵌入应用程序。通常不以手动方式创建 Web 部件。而是根据在用户界面 (UI) 中作出的选择以编程方式创建 Web 部件，或直接将其嵌入应用程序（如 SharePoint Server 页）中。然后，UI 后面的代码创建 URL。Outlook Web App Web 部件的一项用途是在 Sharepoint 页上显示用户的收件箱或日历。

> [!NOTE]
> 若要使用 Outlook Web App Web 部件，用户的邮箱和通过 Web 部件打开的邮箱必须位于同一 Active Directory 林中。


## 使用 Outlook Web Access Web 部件的权限

若要使用 Outlook Web App Web 部件，必须至少向你委派对所打开内容的“审阅者”访问权限。如果向应用程序嵌入了要求进行身份验证的 Outlook Web App Web 部件，则必须将身份验证信息与对 Web 部件的请求一起传递。这样做的一种方法是将 Outlook Web App 虚拟目录配置为使用集成 Windows 身份验证。通过集成 Windows 身份验证，已使用 Active Directory 帐户登录的用户不必重新输入其凭据即可使用 Outlook Web App。

## Outlook Web App Web 部件语法

Exchange 2013 中的 Outlook Web App 对 /owa 虚拟目录请求使用 URL 格式。可通过直接向 Web 浏览器中键入 URL 或将 URL 嵌入 Web 应用程序（如 SharePoint Server 页）中，发出这些请求。

可以使用 Outlook Web App Web 部件创建不同复杂程度的 URL。可以使用简单的 Web 部件 URL 打开任意邮箱的收件箱。可以使用更复杂的 Web 部件 URL 指定要打开的邮箱、该邮箱中要打开的文件夹以及要使用的内容视图。

根据网络上采用的安全措施，可能必须配置 Web 部件 URL 的编码。配置编码后，UI 后面的代码将使用 URL 编码的参数创建 URL。URL 编码的参数使用 %20 代替空格，使用 %2f 代替路径分隔符“/”。本主题中的所有示例都使用编码的参数。

下表列出 Web 部件的参数以及如何使用这些参数的示例。

### Web 部件参数及其使用方法

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>URL 参数</th>
<th>说明</th>
<th>值和示例</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>服务器名称和目录（必需）</p></td>
<td><p>Outlook Web App 虚拟目录的 URL。</p></td>
<td><p>此 URL 可以与用户登录到 Outlook Web App 时所使用的 URL 相同，例如：</p>
<p>https://&lt;<em>server name</em>&gt;/owa</p></td>
</tr>
<tr class="even">
<td><p>Exchange 2013 明确的登录邮箱标识（可选）</p></td>
<td><p>与要打开的邮箱关联的任何 SMTP 地址。</p>
<p>如果 URL 缺少此部分，将打开经过身份验证的用户的默认邮箱。</p>
<p>如果未指定任何其他参数，默认行为将是打开收件箱。</p></td>
<td><p>若要打开 SMTP 地址为 tsmith@fourthcoffee.com 的邮箱，请使用以下 URL：</p>
<p>https://&lt;<em>server name</em>&gt;/owa/tsmith@fourthcoffee.com</p></td>
</tr>
<tr class="odd">
<td><p>cmd（如果指定的参数不是明确的登录邮箱标识，则是必需的）</p></td>
<td><p>?cmd=contents 显示通过参数指定的 Outlook Web App Web 部件，而不是显示整个 Outlook Web App 用户界面。</p></td>
<td><p>如果未指定邮箱，则 cmd 参数跟在登录地址后面，如下所示：</p>
<p>https://&lt;<em>server name</em>&gt;/owa/?cmd=contents</p>
<p>如果指定了邮箱，则 cmd 参数跟在明确的邮箱标识后面，如下所示：</p>
<p>https://&lt;<em>server name</em>&gt;/owa/&lt;<em>SMTP address</em>&gt;/?cmd=contents</p>
<p>如果未指定任何其他参数，默认行为将是打开收件箱。</p></td>
</tr>
<tr class="even">
<td><p>exsvurl</p></td>
<td><p>使用 LiveID 身份验证时必须包含此参数</p>
<p>如果不存在“exsvurl = 1”，则在 LiveID 身份验证期间将放弃所有参数。此参数仅适用于 Office 365 邮箱。</p></td>
<td><p>https://&lt;server name&gt;/owa/?cmd=contents&amp;exsvurl=1</p></td>
</tr>
<tr class="odd">
<td><p>fpath（可选）</p></td>
<td><p>可能必须使用 URL 编码编写此部分 URL，以便可以通过防火墙。</p>
<p>使用 URL 编码时，空格变为 %20，路径分隔符 (/) 变为 %2f。</p>
<p>文件夹层次结构应从邮箱根目录开始。</p>
<p>此文件夹路径可以指向普通文件夹或搜索文件夹。</p></td>
<td><p>若要打开收件箱中的子文件夹 Projects，请使用以下 URL：</p>
<p>https://&lt;<em>server name</em>&gt;/owa/?cmd=contents&amp;fpath= inbox%2fprojects</p></td>
</tr>
<tr class="even">
<td><p>module（可选）</p></td>
<td><p>可以使用此参数指定默认文件夹中的任意一个，而不必了解本地化名称。</p></td>
<td><p>module 参数的值不区分大小写，并且包含下列值：</p>
<ul>
<li><p>Inbox</p></li>
<li><p>Calendar</p></li>
<li><p>Teammailbox</p></li>
</ul>
<p>若要打开邮箱的日历（与本地化无关），请使用以下 URL：</p>
<p>https://&lt;<em>server name</em>&gt;/owa/?cmd=contents&amp;module=calendar</p></td>
</tr>
<tr class="odd">
<td><p>view（可选）</p></td>
<td><p>此参数指定文件夹要显示的视图。</p>
<p>没有此参数时的默认视图如下：</p>
<ul>
<li><p>Calendar   每日</p></li>
<li><p>Messages   邮件</p></li>
</ul>

> [!NOTE]
> 默认视图的字符串将自动采用 URL 编码。

<p>视图的默认排序是在 Outlook Web App 客户端打开文件夹时文件夹的排序方式。</p>
<p>标识视图的字符串未本地化，并且不区分大小写。</p></td>
<td><p>可用视图根据文件夹类型的不同而有所不同。</p>
<p>日历视图：</p>
<ul>
<li><p>Daily 每日日历视图</p></li>
<li><p>Weekly 每周日历视图</p></li>
<li><p>Monthly 每月日历视图</p></li>
</ul>
<p>邮件视图：</p>
<ul>
<li><p>Messages 邮件视图，采用默认排序</p></li>
<li><p>By%20Sender 邮件视图，按发件人排序（以“a”开头的发件人姓名排在前面）</p></li>
<li><p>By%20Subject 邮件视图，按主题排序（以“a”开头的主题排在前面）</p></li>
<li><p>By%20Conversation%20Topic 会话视图，在精简版本的 Outlook Web App 中不可用</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>d, m, y（可选）</p></td>
<td><p>指定应显示日历的日期。这些参数可以按任意顺序输入，可以单独使用，也可以一起使用。</p>
<p>如果未指定其中的任何参数，默认值为当前日、月和年的值。例如，如果当前日期为 2016 年 5 月 3 日，并且将月的值指定为“9”（代表九月），显示的日期将为 September 3, 2016。</p></td>
<td><p>数据参数的有效值如下：</p>
<p>d=[1-31]</p>
<p>m=[1-12]</p>
<p>y=[四位数年份]</p>
<p>若要将日历打开至日期 2016 年 5 月 3 日，请使用以下网址：https://&lt;<em>server name</em>&gt;/owa/?cmd=content&amp;fpath=calendar&amp;view=daily&amp;d=3&amp;m=5&amp;y=2016</p></td>
</tr>
<tr class="odd">
<td><p>part（可选）</p></td>
<td><p>指定 Outlook Web App 应显示更小的 Web 部件。</p></td>
<td><p>使用 Web 部件访问 Outlook Web App 内容时，显示的 UI 将小于整个 Outlook Web App UI。part 参数可以进一步减小 UI。以下 URL 示例以最小的 Web 部件格式显示任务列表：</p>
<p>https://&lt;<em>server name</em>&gt;/owa/?cmd=contents&amp;part=1</p>
<p>部件参数不适用于日历模块。</p></td>
</tr>
<tr class="even">
<td><p>FolderList</p></td>
<td><p>此 part 参数包括用户用于在子文件夹之间进行切换的文件夹列表控件。此操作仅适用于电子邮件文件夹。</p></td>
<td><p>https://&lt;server name&gt;/owa/?cmd=contents&amp;folderlist=1</p></td>
</tr>
</tbody>
</table>


## 手动输入 Outlook Web App Web 部件

也可以在 Web 浏览器中手动输入 Outlook Web App Web 部件。例如，用户可以使用 Outlook Web App Web 部件 URL 打开另一个用户的日历。

以下示例显示如何直接访问常见的 Outlook Web App 视图：

  - **收件箱：**  https://*\<server name\>*/owa/?cmd=contents\&module=inbox

  - **日历（今天）：** https://*\<server name\>*/owa/?cmd=contents\&module=calendar\&exsvurl=1

  - **日历（每周）：**  https://*\<server name\>*/owa/?cmd=contents\&module=calendar\&view=weekly\&exsvurl=1

  - **日历（每月）：**  https://*\<server name\>*/owa/?cmd=contents\&module=calendar\&view=monthly\&exsvurl=1

## 详细信息

  - [自定义 Outlook Web App 的登录页、语言选择页和错误页](customize-the-outlook-web-app-sign-in-language-selection-and-error-pages-exchange-2013-help.md)

  - [为 Outlook Web App 创建主题](create-a-theme-for-outlook-web-app-exchange-2013-help.md)

