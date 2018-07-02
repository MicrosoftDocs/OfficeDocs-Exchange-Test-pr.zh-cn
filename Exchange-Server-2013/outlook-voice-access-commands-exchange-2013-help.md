---
title: 'Outlook Voice Access 命令: Exchange Online Help'
TOCTitle: Outlook Voice Access 命令
ms:assetid: 8fe9247c-695f-47d8-827e-c79d0426854b
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dn205137(v=EXCHG.150)
ms:contentKeyID: 54652246
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Outlook Voice Access 命令

 

_**适用于：**Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：**2015-03-09_

Outlook语音访问允许启用统一邮件 UM 的用户可以访问其邮箱使用模拟、 数字或移动电话。使用位于Outlook语音访问的菜单系统，启用 UM 的用户可以读取电子邮件，收听语音邮件、 Outlook日历与交互、 访问其个人联系人和管理个人选项，配置其Outlook语音访问 PIN 或录制语音邮件等。本主题包含 Outlook Voice Access 命令和用户如何使用它们时通过调用 Outlook Voice Access 数字访问其邮箱的列表。

## Outlook Voice Access 用户界面

由两个用户接口 Outlook Voice Access ︰ 使用电话键盘电话用户界面 (TUI) 和语音用户界面 (VUI) 使用声音命令。用户可以使用Outlook语音访问从外部或内部的电话来访问他们的个人电子邮件、 语音邮件、 联系人和其邮箱中的日历信息访问语音邮件系统。

## 电子邮件和语音邮件命令参考

作为Outlook的语音访问用户，当您拨入到一个 Outlook Voice Access 的编号显示菜单选项使您能够访问您的邮箱，并管理电子邮件和语音邮件。下表列出了可用于管理您的电子邮件和语音邮件的命令。

### 电子邮件和语音邮件命令

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>语音命令</th>
<th>按键命令</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>&amp;quot;播放&amp;quot;</p></td>
<td><p></p></td>
<td><p>播放当前的电子邮件或语音邮件。</p></td>
</tr>
<tr class="even">
<td><p>&amp;quot;下一个&amp;quot;</p></td>
<td><p>#</p></td>
<td><p>阅读下一封电子邮件或语音邮件。</p></td>
</tr>
<tr class="odd">
<td><p>&amp;quot;下一封未读邮件&amp;quot;</p></td>
<td><p>00 后接 ##</p></td>
<td><p>读取下一未读的电子邮件。仅可用于电子邮件。</p></td>
</tr>
<tr class="even">
<td><p>&amp;quot;删除&amp;quot;</p></td>
<td><p>7</p></td>
<td><p>删除当前的电子邮件或语音邮件。</p></td>
</tr>
<tr class="odd">
<td><p>&amp;quot;答复&amp;quot;</p></td>
<td><p>8</p></td>
<td><p>答复发送当前电子邮件或语音邮件的用户。</p></td>
</tr>
<tr class="even">
<td><p>&amp;quot;全部答复&amp;quot;</p></td>
<td><p>00 后接 88</p></td>
<td><p>对当前电子邮件上的所有用户的回复。没有可用的语音邮件选项。</p></td>
</tr>
<tr class="odd">
<td><p>&amp;quot;标记为未读&amp;quot;</p></td>
<td><p>9</p></td>
<td><p>将电子邮件标记为未读。</p></td>
</tr>
<tr class="even">
<td><p>&amp;quot;结束&amp;quot;</p></td>
<td><p>33</p></td>
<td><p>停止阅读并转到当前电子邮件或语音邮件的结尾。</p></td>
</tr>
<tr class="odd">
<td><p>&amp;quot;更多选项&amp;quot;</p></td>
<td><p>00</p></td>
<td><p>打开&amp;quot;更多选项&amp;quot;菜单。</p></td>
</tr>
<tr class="even">
<td><p>&amp;quot;上一封&amp;quot;</p></td>
<td><p>00 后接 11</p></td>
<td><p>阅读上一封电子邮件或语音邮件。</p></td>
</tr>
<tr class="odd">
<td><p>&amp;quot;阅读标题&amp;quot;</p></td>
<td><p></p></td>
<td><p>阅读电子邮件或语音邮件的标题。</p></td>
</tr>
<tr class="even">
<td><p>&amp;quot;呼叫发件人&amp;quot;</p></td>
<td><p>00 后接 2</p></td>
<td><p>呼叫发送当前电子邮件或语音邮件的用户。</p></td>
</tr>
<tr class="odd">
<td><p>&amp;quot;转发&amp;quot;</p></td>
<td><p>00 后接 6</p></td>
<td><p>将当前电子邮件或语音邮件转发给其他的电子邮件收件人或组。</p></td>
</tr>
<tr class="even">
<td><p>&amp;quot;已标记为需后续工作&amp;quot;</p></td>
<td><p>00 后接 44</p></td>
<td><p>将当前电子邮件或语音邮件标记为需后续工作。</p></td>
</tr>
<tr class="odd">
<td><p>&amp;quot;通过名称查找&amp;quot;</p></td>
<td><p></p></td>
<td><p>使用用户名查找用户邮箱中的电子邮件或语音邮件。</p></td>
</tr>
<tr class="even">
<td><p>&amp;quot;删除对话&amp;quot;</p></td>
<td><p>00 后接 77</p></td>
<td><p>删除所有与电子邮件会话相关联的电子邮件。仅可用于电子邮件。</p></td>
</tr>
<tr class="odd">
<td><p>&amp;quot;隐藏对话&amp;quot;</p></td>
<td><p>00 后接 99</p></td>
<td><p>隐藏包含在同一个电子邮件对话内的其他电子邮件。仅可用于电子邮件。</p></td>
</tr>
<tr class="even">
<td><p>&amp;quot;信封信息&amp;quot;</p></td>
<td><p>00 后接 5</p></td>
<td><p>阅读电子邮件或语音邮件的信封信息。</p></td>
</tr>
<tr class="odd">
<td><p>&amp;quot;选择语言&amp;quot;</p></td>
<td><p>00 后接 55</p></td>
<td><p>选择希望在阅读电子邮件或语音邮件时使用的语言。</p></td>
</tr>
<tr class="even">
<td><p>&amp;quot;后退&amp;quot;或&amp;quot;重复&amp;quot;</p></td>
<td><p>1</p></td>
<td><p>倒带或重复当前的电子邮件或语音邮件消息。在播放该消息时，只可用。</p></td>
</tr>
<tr class="odd">
<td><p>&amp;quot;暂停&amp;quot;</p></td>
<td><p>2</p></td>
<td><p>暂停当前的电子邮件或语音邮件消息。在播放该消息时，只可用。</p></td>
</tr>
<tr class="even">
<td><p>&amp;quot;快进&amp;quot;</p></td>
<td><p>3</p></td>
<td><p>快速将转发当前的电子邮件或语音邮件消息。在播放该消息时，只可用。</p></td>
</tr>
<tr class="odd">
<td><p>&amp;quot;减慢&amp;quot;</p></td>
<td><p>4</p></td>
<td><p>播放或更慢读取当前的电子邮件或语音邮件消息。在播放该消息时，只可用。</p></td>
</tr>
<tr class="even">
<td><p>&amp;quot;加快&amp;quot;</p></td>
<td><p>6</p></td>
<td><p>播放或读取的当前电子邮件或语音邮件消息更快。在播放该消息时，只可用。</p></td>
</tr>
<tr class="odd">
<td><p>&amp;quot;上一封&amp;quot;</p></td>
<td><p>11</p></td>
<td><p>从开头开始读取以前的电子邮件。仅可用于电子邮件。</p></td>
</tr>
<tr class="even">
<td><p>&amp;quot;重播&amp;quot;</p></td>
<td><p>00 后接 1</p></td>
<td><p>重播当前的电子邮件或语音邮件。</p></td>
</tr>
<tr class="odd">
<td><p>&amp;quot;重复&amp;quot;</p></td>
<td><p>0</p></td>
<td><p>重复当前的菜单选项。</p></td>
</tr>
<tr class="even">
<td><p>&amp;quot;主菜单&amp;quot;</p></td>
<td><p>*</p></td>
<td><p>退出到主菜单。</p></td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您需要访问电子邮件，在您删除它使用Outlook语音访问后，您可以使用Outlook Web App或Outlook电子邮件回相应的文件夹将从移动到已删除邮件文件夹。不能使用Outlook语音访问来访问已删除邮件文件夹。</td>
</tr>
</tbody>
</table>


## 日历选项命令参考

作为Outlook的语音访问用户，当您拨入到一个 Outlook Voice Access 的编号显示的菜单选项，使您可以访问您的邮箱和管理您的日历。下表列出了可用于管理您的日历的命令。

### 日历命令

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>语音命令</th>
<th>按键命令</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>&amp;quot;下一个&amp;quot;</p></td>
<td><p>#</p></td>
<td><p>阅读下一个日历约会</p></td>
</tr>
<tr class="even">
<td><p>&amp;quot;下一天&amp;quot;</p></td>
<td><p>##</p></td>
<td><p>打开并阅读下一天的日历约会。</p></td>
</tr>
<tr class="odd">
<td><p>&amp;quot;重复&amp;quot;</p></td>
<td><p>0</p></td>
<td><p>重复可用的菜单选项。或者，如果您使用的 VUI，系统读取的日历约会。</p></td>
</tr>
<tr class="even">
<td><p>&amp;quot;更多选项&amp;quot;</p></td>
<td><p>00</p></td>
<td><p>播放更多日历选项菜单。</p></td>
</tr>
<tr class="odd">
<td><p>&amp;quot;重复&amp;quot;</p></td>
<td><p>1</p></td>
<td><p>再次阅读日历约会。</p></td>
</tr>
<tr class="even">
<td><p>&amp;quot;上一个会议&amp;quot;</p></td>
<td><p>00 后接 11</p></td>
<td><p>打开安排的上一个会议。</p></td>
</tr>
<tr class="odd">
<td><p>&amp;quot;与地点拨打&amp;quot;</p></td>
<td><p>2</p></td>
<td><p>呼叫为会议地点列出的电话号码。</p></td>
</tr>
<tr class="even">
<td><p>&amp;quot;与组织者拨打&amp;quot;</p></td>
<td><p>00 后接 22</p></td>
<td><p>呼叫为会议组织者列出的电话号码。</p></td>
</tr>
<tr class="odd">
<td><p>&amp;quot;我会迟到&amp;quot;</p></td>
<td><p>3</p></td>
<td><p>向所有与会者发送&amp;quot;我会迟到&amp;quot;邮件。</p></td>
</tr>
<tr class="even">
<td><p>&amp;quot;接受&amp;quot;或&amp;quot;暂定接受&amp;quot;</p></td>
<td><p>4</p></td>
<td><p>接受或暂定接受会议请求。</p></td>
</tr>
<tr class="odd">
<td><p>&amp;quot;会议详情&amp;quot;</p></td>
<td><p>5</p></td>
<td><p>阅读或播放当前正在阅读的会议的详情。</p></td>
</tr>
<tr class="even">
<td><p>&amp;quot;与会者详情&amp;quot;</p></td>
<td><p>00 后接 55</p></td>
<td><p>阅读或播放已安排的会议的详情。</p></td>
</tr>
<tr class="odd">
<td><p>&amp;quot;转发&amp;quot;</p></td>
<td><p>00 后接 6</p></td>
<td><p>将会议请求转发给其他用户。</p></td>
</tr>
<tr class="even">
<td><p>&amp;quot;谢绝&amp;quot;或&amp;quot;取消&amp;quot;</p></td>
<td><p>7</p></td>
<td><p>谢绝或取消会议请求。</p></td>
</tr>
<tr class="odd">
<td><p>&amp;quot;清除我的日历&amp;quot;</p></td>
<td><p>00 后接 77</p></td>
<td><p>清除当天特定时段内的日历。</p></td>
</tr>
<tr class="even">
<td><p>&amp;quot;答复&amp;quot;</p></td>
<td><p>00 后接 8</p></td>
<td><p>答复会议组织者。</p></td>
</tr>
<tr class="odd">
<td><p>&amp;quot;全部答复&amp;quot;</p></td>
<td><p>00 后接 88</p></td>
<td><p>答复所有与会者。</p></td>
</tr>
<tr class="even">
<td><p>&amp;quot;重复菜单&amp;quot;</p></td>
<td><p>5 后接 0</p></td>
<td><p>重复可用的菜单选项。</p></td>
</tr>
<tr class="odd">
<td><p>&amp;quot;后退&amp;quot;</p></td>
<td><p>5 后接 1</p></td>
<td><p>后退会议详情。</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>5 后接 11</p></td>
<td><p>返回会议详情的开头。</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>5 后接 2</p></td>
<td><p>暂停和继续播放会议详情。</p></td>
</tr>
<tr class="even">
<td><p>&amp;quot;快进&amp;quot;</p></td>
<td><p>5 后接 3</p></td>
<td><p>在会议详情中快进。</p></td>
</tr>
<tr class="odd">
<td><p>&amp;quot;结束&amp;quot;</p></td>
<td><p>5 后接 33</p></td>
<td><p>跳到会议详情的结尾。</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>5 后接 4</p></td>
<td><p>以更慢的速度播放或阅读会议详情。</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>5 后接 55</p></td>
<td><p>选择将用于阅读会议详情的语言。</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>5 后接 6</p></td>
<td><p>以更快的速度播放或阅读会议详情。</p></td>
</tr>
<tr class="odd">
<td><p>&amp;quot;主菜单&amp;quot;</p></td>
<td><p>*</p></td>
<td><p>退出到主菜单。</p></td>
</tr>
</tbody>
</table>


## 查找联系人命令参考

作为Outlook的语音访问用户，当您拨入到一个 Outlook Voice Access 的编号显示的菜单选项，使您能够访问您的邮箱、 更改个人选项，或者调用或向联系人发送一条消息。如果您选择使用您的声音，默认情况下处于选中状态，然后选择联系人菜单选项，语音邮件系统可以使用电话键盘导航查找联系人选项。您还可以通过使用电话键盘在目录或联系人中查找用户。下表列出了可用于管理您的联系人或用户搜索的命令。

### 联系人命令

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>语音命令</th>
<th>按键命令</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>&amp;quot;目录&amp;quot;</p></td>
<td><p>00</p></td>
<td><p>搜索目录中的某个用户。</p></td>
</tr>
<tr class="even">
<td><p>&amp;quot;播放详情&amp;quot;</p></td>
<td><p>1</p></td>
<td><p>播放个人联系人的详情，例如为个人联系人列出的电话号码。</p></td>
</tr>
<tr class="odd">
<td><p>&amp;quot;发送邮件&amp;quot;</p></td>
<td><p>3</p></td>
<td><p>向所选的个人联系人发送邮件。</p></td>
</tr>
<tr class="even">
<td><p>&amp;quot;查找另一位联系人&amp;quot;</p></td>
<td><p>4</p></td>
<td><p>查找另一位个人联系人。</p></td>
</tr>
<tr class="odd">
<td><p>&amp;quot;拨打手机号码&amp;quot;</p></td>
<td><p>2 后接 1</p></td>
<td><p>拨打为个人联系人列出的移动电话号码。</p></td>
</tr>
<tr class="even">
<td><p>&amp;quot;拨打办公室电话&amp;quot;</p></td>
<td><p>2 后接 2</p></td>
<td><p>拨打为个人联系人列出的业务电话号码或办公室电话号码。</p></td>
</tr>
<tr class="odd">
<td><p>&amp;quot;拨打家庭电话&amp;quot;</p></td>
<td><p>2 后接 3</p></td>
<td><p>拨打为个人联系人列出的家庭电话号码。</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>##</p></td>
<td><p>如果使用目录搜索功能，可以输入用户在目录中的电子邮件别名或名称。</p></td>
</tr>
<tr class="odd">
<td><p>&amp;quot;主菜单&amp;quot;</p></td>
<td><p>*</p></td>
<td><p>退出到主菜单。</p></td>
</tr>
</tbody>
</table>


## 个人选项命令参考

作为Outlook的语音访问用户，当您拨入到一个 Outlook Voice Access 的编号显示的菜单选项，使您可以访问您的邮箱和管理您的个人选项。使用Outlook语音访问个人选项配置时，您只能使用电话键盘来导航菜单。使用语音来导航菜单不是可用于配置个人选项。下表列出了可用于管理您的个人选项的命令。

### 个人选项命令

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>语音命令</th>
<th>按键命令</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p></p></td>
<td><p>1</p></td>
<td><p>开启或关闭电话的外出问候语。</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>2</p></td>
<td><p>录制个人语音邮件问候语或外出语音邮件问候语。</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>3</p></td>
<td><p>更改用于 Outlook Voice Access 的 PIN。</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>4</p></td>
<td><p>使用 VUI 或按键界面启动。</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>5</p></td>
<td><p>设置要使用的本地时区。</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>6</p></td>
<td><p>选择 12 小时或 24 小时时间格式。</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>*</p></td>
<td><p>返回主菜单。</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>0</p></td>
<td><p>重复可用的菜单选项。</p></td>
</tr>
</tbody>
</table>


## 详细信息

[设置 Outlook Voice Access](setting-up-outlook-voice-access-exchange-2013-help.md)

[设置客户端语音邮件功能](set-up-client-voice-mail-features-exchange-2013-help.md)

