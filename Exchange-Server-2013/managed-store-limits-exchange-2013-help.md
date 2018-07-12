---
title: '托管存储限制: Exchange 2013 Help'
TOCTitle: 托管存储限制
ms:assetid: bea9ec15-bfb5-4716-b14e-010e389c9f9e
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Mt741981(v=EXCHG.150)
ms:contentKeyID: 73226015
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 托管存储限制

 

_**上一次修改主题：** 2016-09-15_

**摘要：** 关于托管存储连接限制及其配置方式。

在 MicrosoftExchange Server 2013 中，对 Exchange 托管存储施加了连接和使用限制，以防止单个应用程序或单个用户使用与托管存储之间的所有可用连接。如果允许单个用户或应用程序使用所有连接，则其他用户或应用程序将无法访问托管存储，这可能导致停机。

> [!NOTE]  
> 对于具有管理特权的帐户进行的任何连接，会话限制最大值已增加到 64,000。


## 术语

了解以下术语可帮助你理解本主题中涉及的连接类型。

  - 会话  
    会话表示由服务和客户端应用程序（如 Microsoft Outlook）用于连接到托管存储的连接。服务和客户端可以在特定时间拥有多个会话。术语“*连接*”和“*会话*”可以互换使用。

<!-- end list -->

  - 线程  
    线程表示对托管存储并发执行的请求。例如，如果用户在 Outlook 中打开文件夹，则 Outlook 会代表用户对托管存储执行请求。该请求的执行为单个线程。
    
    在 Exchange Server 2013 中，不再有基于客户端类型的线程限制。相反，对于所有客户端，**每个邮箱数据库**的最大线程数为 50。例外情况是可用性服务，每个用户的最大限制为 16。

返回顶部

## 会话限制

下表列出了与托管存储之间的客户端连接类型以及基于这些连接的限制。如果你要修改会话限制，请参阅紧随该表之后的“配置会话限制”。

以前版本的 Exchange 根据每个服务器的连接数设置与托管存储之间的连接数限制。在 Exchange 2013 中，会话限制根据每个邮箱数据库的连接进行设置。

Exchange 2013 中的连接限制类型如下：

  - **每个进程的最大会话数**   指定 Exchange 服务在一个邮箱数据库上一次可以打开的最大会话数。

  - **每个进程的最大用户会话数**   指定单个用户的特定协议的最大会话数。

以下部分“配置会话限制”介绍如何修改这些限制。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>客户端类型</th>
<th></th>
<th>每个邮箱数据库的最大会话数</th>
<th>每个邮箱数据库的默认用户会话数</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>管理员</p></td>
<td></td>
<td><p>10,000</p></td>
<td><p>不适用</p></td>
</tr>
<tr class="even">
<td><p>可用性服务</p></td>
<td></td>
<td><p>10,000</p></td>
<td><p>16</p></td>
</tr>
<tr class="odd">
<td><p>内容索引</p></td>
<td></td>
<td><p>10,000</p></td>
<td><p>不适用</p></td>
</tr>
<tr class="even">
<td><p>Exchange ActiveSync</p></td>
<td></td>
<td><p>不适用</p></td>
<td><p>16</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Web 服务</p></td>
<td></td>
<td><p>不适用</p></td>
<td><p>16</p></td>
</tr>
<tr class="even">
<td><p>管理</p></td>
<td></td>
<td><p>不适用</p></td>
<td><p>16</p></td>
</tr>
<tr class="odd">
<td><p>中间层上的 MAPI (MoMT)</p></td>
<td></td>
<td><p>不适用</p></td>
<td><p>32</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeMailboxAssistants：事件</p></td>
<td></td>
<td><p>10,000</p></td>
<td><p>不适用</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeMailboxAssistants：计时</p></td>
<td></td>
<td><p>10,000</p></td>
<td><p>不适用</p></td>
</tr>
<tr class="even">
<td><p>MSExchange 远程过程调用</p></td>
<td></td>
<td><p>不适用</p></td>
<td><p>16</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft OfficeOutlook Web App</p></td>
<td></td>
<td><p>不适用</p></td>
<td><p>16</p></td>
</tr>
<tr class="even">
<td><p>POP3 和 IMAP4</p></td>
<td></td>
<td><p>不适用</p></td>
<td><p>16</p></td>
</tr>
<tr class="odd">
<td><p>传输</p></td>
<td></td>
<td><p>10,000</p></td>
<td><p>不适用</p></td>
</tr>
<tr class="even">
<td><p>统一消息</p></td>
<td></td>
<td><p>不适用</p></td>
<td><p>16</p></td>
</tr>
<tr class="odd">
<td><p>其他</p></td>
<td></td>
<td><p>不适用</p></td>
<td><p>16</p></td>
</tr>
</tbody>
</table>


## 配置会话限制

你可以修改默认会话限制。

> [!NOTE]  
> 如果要修改会话限制，则需要在任何数据库可用性组 (DAG) 中的所有邮箱服务器上修改这些限制。如果未在所有服务器上进行相同更改，则结果会不一致。若要提高对客户端访问服务器的会话限制，必须在限制策略中提高 <code>RCAMaxConcurrency</code> 值。有关详细信息，请参阅 <a href="https://technet.microsoft.com/zh-cn/library/dd298094(v=exchg.150)">Set-ThrottlingPolicy</a>。


> [!CAUTION]  
> 未正确编辑注册表可能造成严重问题，也许需要您重新安装操作系统。未正确编辑注册表造成的问题可能无法解决。在编辑注册表之前，请备份所有有价值的数据。


1.  启动注册表编辑器 (regedit)。

2.  导航到下列注册表子项：
    
    **\\\\HKEY\_LOCAL\_MACHINE \\SYSTEM\\CurrentControlSet\\Services\\MSExchangeIS\\ParametersSystem**。

3.  右键单击“**ParametersSystem**”，指向“**新建**”，然后单击“**DWORD (32 位)值**”。
    
    会在结果窗格中创建新值。

4.  将该注册表项重命名为以下值之一，然后按 Enter：
    
      - **每个用户允许的最大会话数**   此限制指定每个用户允许的最大会话数。
    
      - **每个用户允许的最大服务会话数**   此限制指定每个用户允许的最大服务会话数。
    
      - **每个服务允许的最大 Exchange 会话数**   此限制指定每个服务允许的最大 Exchange 会话数。默认值为 10,000。

5.  右键单击新创建的注册表项，然后单击“**修改**”。

6.  在“**数值数据**”框中，键入要限制此项使用的对象数，然后单击“**确定**”。使用上表可查看默认设置。

返回顶部

## 打开项目限制

打开项目限制是对单个会话中单个邮箱可以打开的项目数施加的限制。但是，用户可以同时打开多个会话。例如，如果某个用户打开了两个会话，则该用户可以打开 1,000 个文件夹。

如果你要修改这些限制，请参阅紧随该表之后的“配置打开项目限制”。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>项目类型</th>
<th>注册表对象类型</th>
<th>每个会话的最大打开项目数</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ACL 视图</p></td>
<td><p>objtACLView</p></td>
<td><p>500</p></td>
</tr>
<tr class="even">
<td><p>附件</p></td>
<td><p>objtAttachment</p></td>
<td><p>500</p></td>
</tr>
<tr class="odd">
<td><p>附件视图</p></td>
<td><p>objtAttachmentView</p></td>
<td><p>500</p></td>
</tr>
<tr class="even">
<td><p>Cstream</p></td>
<td><p>objtCStream</p></td>
<td><p>不适用</p></td>
</tr>
<tr class="odd">
<td><p>文件夹</p></td>
<td><p>objtFolder</p></td>
<td><p>500</p></td>
</tr>
<tr class="even">
<td><p>文件夹视图</p></td>
<td><p>objtFolderView</p></td>
<td><p>500</p></td>
</tr>
<tr class="odd">
<td><p>FX 目标流</p></td>
<td><p>objtFXDstStrm</p></td>
<td><p>500</p></td>
</tr>
<tr class="even">
<td><p>FX 源流</p></td>
<td><p>objtFXSrcStrm</p></td>
<td><p>500</p></td>
</tr>
<tr class="odd">
<td><p>邮件</p></td>
<td><p>objtMessage</p></td>
<td><p>250</p></td>
</tr>
<tr class="even">
<td><p>邮件视图</p></td>
<td><p>objtMessageView</p></td>
<td><p>500</p></td>
</tr>
<tr class="odd">
<td><p>通知</p></td>
<td><p>objtNotify</p></td>
<td><p>500,000</p></td>
</tr>
<tr class="even">
<td><p>规则视图</p></td>
<td><p>objtRulesView</p></td>
<td><p>不适用</p></td>
</tr>
<tr class="odd">
<td><p>流</p></td>
<td><p>objtStream</p></td>
<td><p>250</p></td>
</tr>
</tbody>
</table>


## 配置打开项目限制

你可以限制 MAPI 客户端可以同时使用的最大资源数。

> [!NOTE]  
> 如果要修改打开项目限制，则需要在任何 DAG 和客户端访问阵列中的所有邮箱服务器上修改这些限制。如果未在所有服务器上进行相同更改，则结果会不一致。


> [!CAUTION]  
> 未正确编辑注册表可能造成严重问题，也许需要您重新安装操作系统。未正确编辑注册表造成的问题可能无法解决。在编辑注册表之前，请备份所有有价值的数据。


1.  启动注册表编辑器 (regedit)。

2.  导航到下列注册表子项：
    
    **\\\\HKEY\_LOCAL\_MACHINE \\SYSTEM\\CurrentControlSet\\Services\\MSExchangeIS\\ParametersSystem**

3.  右键单击 **ParametersSystem**，指向“新建”，然后单击“项”。
    
    会在控制台树中创建新注册表项。

4.  将该注册表项重命名为“**MaxObjsPerMapiSession**”，然后按 Enter。

5.  右键单击“**MaxObjsPerMapiSession**”，指向“**新建**”，然后单击“**DWORD (32 位)值**”。
    
    会在结果窗格中创建新值。

6.  将该注册表项重命名为 *\<Object\_type\>*，其中 *\<Object\_type\>* 为所修改的注册表对象类型的名称。例如，若要修改可以打开的邮件数，请使用 *objtMessage*。按 Enter。

7.  右键单击新创建的注册表项，然后单击“**修改**”。

8.  在“**数值数据**”框中，键入要限制此项使用的对象数，然后单击“**确定**”。例如，键入“**350**”可增大对象的值。

9.  重新启动 Microsoft Exchange 信息存储服务。

返回顶部

## 项目大小限制

项目大小限制是对用户邮箱中的项目施加的限制。可通过在 [Set-Mailbox](https://technet.microsoft.com/zh-cn/library/bb123981\(v=exchg.150\)) cmdlet 上使用 *MaxSendSize* 和 *MaxReceiveSize* 参数来进行配置：


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>项目类型</th>
<th>限制</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>邮件（已保存）</p></td>
<td><p>SendLimit、ReceiveLimit 的最大大小</p></td>
</tr>
<tr class="even">
<td><p>邮件（已发送）</p></td>
<td><p>SendLimit 的最大大小</p></td>
</tr>
<tr class="odd">
<td></td>
<td></td>
</tr>
</tbody>
</table>


返回顶部

