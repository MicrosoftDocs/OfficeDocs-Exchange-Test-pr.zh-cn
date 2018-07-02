---
title: 'Exchange 2013 部署权限参考: Exchange 2013 Help'
TOCTitle: Exchange 2013 部署权限参考
ms:assetid: b13412d0-0cc4-4c1d-bf31-cae3d3e211a9
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Ee681663(v=EXCHG.150)
ms:contentKeyID: 59636410
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2013 部署权限参考

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2016-12-09_

本主题介绍了安装 Microsoft Exchange Server 2013 组织所需的权限。与管理角色组关联的通用安全组 (USG)，以及其他 Windows 安全组和安全主体，均添加到了各种 Active Directory 对象的访问控制列表 (ACL) 中。ACL 控制每个对象上可执行的操作。通过了解授予给每个角色组、安全组或安全主体的权限，可以确定安装 Exchange 2013 所需的最低权限。

在某些情况下，ACL 不应用于常用的属性 **ntSecurityDescriptor**，而是应用于其他属性，如 **msExchMailboxSecurityDescriptor**。目录服务不能强制实现 Windows 安全描述符中未指定的安全性。大多数情况下，将复制这些 ACL，通过存储服务将 ACL 存储在相应的对象上。不过，只有将这些 ACL 作为原始二进制数据查看的工具。

每个权限表的列包含以下信息：

  - **帐户：** 允许或拒绝权限的安全主体。

  - **ACE 类型：** 访问控制条目 (ACE) 类型。
    
      - **允许 ACE：** “允许 ACE”允许与 ACE 关联的用户或组访问邮件。
    
      - **拒绝 ACE：** “拒绝 ACE”阻止与 ACE 关联的用户或组访问邮件。

  - **继承：** 用于子对象的继承类型。
    
      - “所有”指示权限应用于该对象及其所有子对象。
    
      - “后代”指示权限应用于“针对属性/应用于”行中列出的对象类。
    
      - “无”指示这些权限只应用于该对象。

  - **权限：** 为帐户授予的权限。

  - **针对属性/应用于：** 在某些情况下，权限只应用于给定的属性、属性集或对象类。此处指定了这些受限的权限。

  - **注释：** 如果适用，此列说明需要这些权限的原因并提供有关权限的其他信息。

权限通常按在 Active Directory Service Interfaces (ADSI) Edit (AdsiEdit.msc) 上（在 **View/Edit** 选项卡上 **Advanced** 视图中的 **Security** 属性页）使用的名称在表中列出。ADSI Edit **Security** 属性页上列出很简洁的权限视图。LDP 工具 (Ldp.exe) 直接使用数字值显示访问掩码。安装代码通过预定义的常量引用权限。

下表说明这些值之间的关系。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>ADSI Edit Summary 页</th>
<th>ADSI Edit Advanced 视图，View/Edit 选项卡</th>
<th>应用于给定对象的 ACL 条目</th>
<th>二进制值 （LDP 中的访问掩码）</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>完全控制</p></td>
<td><p>完全控制</p></td>
<td><p><code>WRITE_OWNER | WRITE_DAC | READ_CONTROL | DELETE | ACTRL_DS_CONTROL_ACCESS | ACTRL_DS_LIST_OBJECT | ACTRL_DS_DELETE_TREE | ACTRL_DS_WRITE_PROP | ACTRL_DS_READ_PROP | ACTRL_DS_SELF | ACTRL_DS_LIST | ACTRL_DS_DELETE_CHILD | ACTRL_DS_CREATE_CHILD</code></p></td>
<td><p><code>0x000F01FF</code></p></td>
</tr>
<tr class="even">
<td><p>读取</p></td>
<td><p>列出内容 + 读取所有属性 + 读取权限</p></td>
<td><p><code>ACTRL_DS_LIST | ACTRL_DS_READ_PROP | READ_CONTROL</code></p></td>
<td><p><code>0x00020014</code></p></td>
</tr>
<tr class="odd">
<td><p>写</p></td>
<td><p>写入所有属性 + 所有验证写入</p></td>
<td><p><code>ACTRL_DS_WRITE_PROP | ACTRL_DS_SELF</code></p></td>
<td><p><code>0x00000028</code></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>列出内容</p></td>
<td><p><code>ACTRL_DS_LIST</code></p></td>
<td><p><code>0x00000004</code></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>读取所有属性</p></td>
<td><p><code>ACTRL_DS_READ_PROP</code></p></td>
<td><p><code>0x00000010</code></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>写入所有属性</p></td>
<td><p><code>ACTRL_DS_WRITE_PROP</code></p></td>
<td><p><code>0x00000020</code></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>删除</p></td>
<td><p><code>DELETE</code></p></td>
<td><p><code>0x00010000</code></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>删除子树目录</p></td>
<td><p><code>ACTRL_DS_DELETE_TREE</code></p></td>
<td><p><code>0x00000040</code></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>读取权限</p></td>
<td><p><code>READ_CONTROL</code></p></td>
<td><p><code>0x00020000</code></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>修改权限</p></td>
<td><p><code>WRITE_DAC</code></p></td>
<td><p><code>0x00040000</code></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>修改所有者</p></td>
<td><p><code>WRITE_OWNER</code></p></td>
<td><p><code>0x00080000</code></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>所有验证写入</p></td>
<td><p><code>ACTRL_DS_SELF</code></p></td>
<td><p><code>0x00000008</code></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>所有扩展权限</p></td>
<td><p><code>ACTRL_DS_CONTROL_ACCESS</code></p></td>
<td><p><code>0x00000100</code></p></td>
</tr>
<tr class="even">
<td><p>创建所有子对象</p></td>
<td><p>创建所有子对象</p></td>
<td><p><code>ACTRL_DS_CREATE_CHILD</code></p></td>
<td><p><code>0x00000001</code></p></td>
</tr>
<tr class="odd">
<td><p>删除所有子对象</p></td>
<td><p>删除所有子对象</p></td>
<td><p><code>ACTRL_DS_DELETE_CHILD</code></p></td>
<td><p><code>0x00000002</code></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p></p></td>
<td><p><code>ACTRL_DS_LIST_OBJECT</code></p></td>
<td><p><code>0x00000080</code></p></td>
</tr>
</tbody>
</table>


扩展权限是由各个应用程序指定的自定义权限。这些权限在 ACL 中指定。但是，它们对于 Active Directory 是无意义的。特定的应用程序强制使用任何扩展权限。“Create public folder”和“Create named properties in the information store”就是 Exchange 扩展权限的示例。

有关在安装 Microsoft Exchange Server 2010 期间设置的权限的信息，请参阅 [Exchange 2010 部署权限参考](https://go.microsoft.com/fwlink/p/?linkid=402924)。

## 准备 Active Directory 权限

本节中的权限表说明在执行 `Setup /PrepareAD` 命令时设置的权限。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>本节中描述的权限是当您使用共享权限模型部署 Exchange 2013 时配置的默认权限。如果您已经使用 Active Directory 拆分权限模型部署了Exchange 2013，默认权限将有所不同。有关使用 Active Directory 拆分权限以及共享和拆分权限模型时的默认权限更改的详细信息，请参阅<a href="understanding-split-permissions-exchange-2013-help.md">了解拆分权限</a>中的 <a href="understanding-split-permissions-exchange-2013-help.md">Active Directory split permissions</a>。如果您在安装 Exchange 时不选择使用 Active Directory 拆分权限，Exchange 将使用共享权限。</td>
</tr>
</tbody>
</table>


## Microsoft Exchange 容器权限

下表说明为配置分区中的 Microsoft Exchange 容器设置的权限。

### 对象的可分辨名称：CN=Microsoft Exchange、CN=Services、CN=Configuration、DC=\<domain\>

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
<th>帐户</th>
<th>ACE 类型</th>
<th>继承</th>
<th>权限</th>
<th>针对属性/应用于</th>
<th>注释</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>安装 帐户</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>完全控制</p></td>
<td><p></p></td>
<td><p>此帐户用于运行 <code>/PrepareAD</code>。</p></td>
</tr>
<tr class="even">
<td><p>组织管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>完全控制</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange 受信任子系统</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>完全控制</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>阅读</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>经过身份验证的用户</p></td>
<td><p>允许 ACE</p></td>
<td><p>无</p></td>
<td><p>读取属性</p>
<p>列出内容</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange 受信任子系统</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>修改权限</p></td>
<td><p>msExchSmtpRceiveConnector</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>公用文件夹管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>阅读</p>
<p>列出对象</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>委派安装</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>阅读</p>
<p>列出对象</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## Microsoft Exchange 自动发现容器权限

下表说明了在配置分区中的 Microsoft Exchange 自动发现容器上设置的权限。

### 对象的可分辨名称：CN=Microsoft Exchange Autodiscover、CN=Services、CN=Configuration、DC=\<domain\>

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
<th>帐户</th>
<th>ACE 类型</th>
<th>继承</th>
<th>权限</th>
<th>针对属性/应用于</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>阅读</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## Microsoft Exchange 组织容器权限

本节中的权限表说明了在配置分区中的 Microsoft Exchange 组织及子容器上设置的权限。

### 对象的可分辨名称：CN=\<organization\>、CN=Microsoft Exchange、CN=Services、CN=Configuration、DC=\<domain\>

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
<th>帐户</th>
<th>ACE 类型</th>
<th>继承</th>
<th>权限</th>
<th>针对属性/应用于</th>
<th>注释</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Enterprise Admins</p>
<p>根 Domain Admins</p>
<p>安装 帐户</p>
<p>组织管理</p></td>
<td><p>拒绝 ACE</p></td>
<td><p>全部</p></td>
<td><p>代理发送</p>
<p>代理接收</p></td>
<td><p></p></td>
<td><p>不允许 Windows 管理员打开邮箱。</p></td>
</tr>
<tr class="even">
<td><p>Enterprise Admins</p>
<p>Schema Admins</p>
<p>根 Domain Admins</p>
<p>安装 帐户</p>
<p>组织管理</p></td>
<td><p>拒绝 ACE</p></td>
<td><p>全部</p></td>
<td><p>Exchange Web 服务模拟</p>
<p>Exchange Web 服务令牌序列化</p></td>
<td><p></p></td>
<td><p>扩展权限</p></td>
</tr>
<tr class="odd">
<td><p>Enterprise Admins</p>
<p>Schema Admins</p>
<p>根 Domain Admins</p>
<p>安装 帐户</p></td>
<td><p>拒绝 ACE</p></td>
<td><p>全部</p></td>
<td><p>存储传输访问</p>
<p>存储约束委派</p>
<p>存储读取访问</p>
<p>存储读写访问</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>本地系统</p></td>
<td><p>允许</p></td>
<td><p>全部</p></td>
<td><p>所有扩展权限</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>经过身份验证的用户</p></td>
<td><p>拒绝 ACE</p></td>
<td><p>后代</p></td>
<td><p>读取属性</p></td>
<td><p><code>msExchAvailabilityUserPassword / msExchAvailabilityAddressSpace</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>经过身份验证的用户</p></td>
<td><p>允许</p></td>
<td><p>无</p></td>
<td><p>阅读</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>组织管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>读取权限</p>
<p>列出内容</p>
<p>读取属性</p>
<p>列出对象</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>公用文件夹管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>读取权限</p>
<p>列出内容</p>
<p>读取属性</p>
<p>列出对象</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>NT Authority\Network Service</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>阅读</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>托管可用性服务器</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>读取权限</p>
<p>列出内容</p>
<p>读取属性</p>
<p>列出对象</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>所有扩展权限</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>groupType</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>msExchOwningServer</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>msExchMailboxSecurityDescriptor</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>msExchUMServerWritableFlags</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>msExchDatabaseCreated</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>msExchUserCulture</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>msExchMobileMailboxFlags</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>siteFolderGUID</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>siteFolderServer</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>msExchEDBOffline</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>userCertificate</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>msExchUMDtmfMap</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>msExchBlockedSendersHash</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>Personal Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>Public Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>Exchange Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>msExchPatchMDB</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>publicDelegates</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>msExchUMSpokenName</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>msExchUMPinChecksum</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>legacyExchangeDN</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>msExchSafeSendersHash</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>thumbnailPhoto</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>组织管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>创建顶级公用文件夹</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>公用文件夹管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>创建顶级公用文件夹</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>组织管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>查看信息存储状态</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>公用文件夹管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>查看信息存储状态</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>组织管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>管理信息存储</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>公用文件夹管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>管理信息存储</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>组织管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>在信息存储中创建命名属性</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>公用文件夹管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>在信息存储中创建命名属性</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>组织管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>修改公用文件夹 ACL</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>公用文件夹管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>修改公用文件夹 ACL</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>组织管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>修改公用文件夹配额</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>公用文件夹管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>修改公用文件夹配额</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>组织管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>修改公用文件夹管理 ACL</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>公用文件夹管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>修改公用文件夹管理 ACL</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>组织管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>修改公用文件夹到期日期</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>公用文件夹管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>修改公用文件夹到期日期</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>组织管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>修改公用文件夹副本列表</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>公用文件夹管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>修改公用文件夹副本列表</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>组织管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>修改公用文件夹已删除邮件的保留时间</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>公用文件夹管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>修改公用文件夹已删除邮件的保留时间</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>组织管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>创建公用文件夹</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>公用文件夹管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>创建公用文件夹</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>公用文件夹管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>已启用邮件的公用文件夹</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>每个人</p>
<p>NT Authority\Anonymous Logon</p>
<p></p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>在信息存储中创建命名属性</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>每个人</p>
<p>NT Authority\Anonymous Logon</p>
<p></p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>创建公用文件夹</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>每个人</p>
<p>NT Authority\Anonymous Logon</p>
<p></p></td>
<td><p>允许 ACE</p></td>
<td><p>后代</p></td>
<td><p>读取权限</p>
<p>列出内容</p>
<p>读取属性</p>
<p>列出对象</p></td>
<td><p><code>/ msExchPrivateMDB</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>每个人</p>
<p>NT Authority\Anonymous Logon</p>
<p></p></td>
<td><p>允许 ACE</p></td>
<td><p>后代</p></td>
<td><p>读取权限</p>
<p>列出内容</p>
<p>读取属性</p>
<p>列出对象</p></td>
<td><p><code>/ msExchPublicMDB</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>后代</p></td>
<td><p>读取权限</p>
<p>列出内容</p>
<p>读取属性</p>
<p>列出对象</p></td>
<td><p><code>/ siteAddressing</code></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### 对象的可分辨名称：CN=All Address Lists、CN=Address Lists Container、CN=\<organization\>

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
<th>帐户</th>
<th>ACE 类型</th>
<th>继承</th>
<th>权限</th>
<th>针对属性/应用于</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>经过身份验证的用户</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>列出内容</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>组织管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>msExchLastAppliedRecipientFilter</code></p>
<p><code>msExchRecipientFilterFlags</code></p></td>
</tr>
<tr class="odd">
<td><p>公用文件夹管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>msExchLastAppliedRecipientFilter</code></p>
<p><code>msExchRecipientFilterFlags</code></p></td>
</tr>
</tbody>
</table>


### 对象的可分辨名称：CN=Offline Address Lists、CN=Address Lists Container、CN=\<organization\>

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
<th>帐户</th>
<th>ACE 类型</th>
<th>继承</th>
<th>权限</th>
<th>针对属性/应用于</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>经过身份验证的用户</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>Download Offline Address Book</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### 对象的可分辨名称：CN=Addressing、CN=\<organization\>

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
<th>帐户</th>
<th>ACE 类型</th>
<th>继承</th>
<th>权限</th>
<th>针对属性/应用于</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>经过身份验证的用户</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>阅读</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### 对象的可分辨名称：CN=Recipient Policies、CN=\<organization\>

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
<th>帐户</th>
<th>ACE 类型</th>
<th>继承</th>
<th>权限</th>
<th>针对属性/应用于</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>组织管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>msExchLastAppliedRecipientFilter</code></p>
<p><code>msExchRecipientFilterFlags</code></p></td>
</tr>
<tr class="even">
<td><p>公用文件夹管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>msExchLastAppliedRecipientFilter</code></p>
<p><code>msExchRecipientFilterFlags</code></p></td>
</tr>
</tbody>
</table>


## 配置分区容器权限

本节中的权限表说明通过 `Setup /PrepareAD` 命令为配置分区中的各个容器设置的权限。

### 对象的可分辨名称：CN=Sites、CN=Configuration、DC=\<domain\>

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
<th>帐户</th>
<th>ACE 类型</th>
<th>继承</th>
<th>权限</th>
<th>针对属性/应用于</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>组织管理</p>
<p>Exchange 受信任子系统</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>msExchVersion / site</code></p></td>
</tr>
<tr class="even">
<td><p>组织管理</p>
<p>Exchange 受信任子系统</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>msExchVersion / site-link</code></p></td>
</tr>
<tr class="odd">
<td><p>组织管理</p>
<p>Exchange 受信任子系统</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>msExchPartnerId / site</code></p></td>
</tr>
<tr class="even">
<td><p>组织管理</p>
<p>Exchange 受信任子系统</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>msExchMinorPartnerId / site</code></p></td>
</tr>
<tr class="odd">
<td><p>组织管理</p>
<p>Exchange 受信任子系统</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>msExchResponsibleforSites / site</code></p></td>
</tr>
<tr class="even">
<td><p>组织管理</p>
<p>Exchange 受信任子系统</p></td>
<td><p>允许 ACE</p></td>
<td><p></p></td>
<td><p>写入属性</p></td>
<td><p><code>msExchTransportSiteFlags / site</code></p></td>
</tr>
<tr class="odd">
<td><p>组织管理</p>
<p>Exchange 受信任子系统</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>msExchCost / site-link</code></p></td>
</tr>
<tr class="even">
<td><p>组织管理</p>
<p>Exchange 受信任子系统</p>
<p>本地系统</p>
<p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>后代</p></td>
<td><p>读取权限</p>
<p>列出内容</p>
<p>读取属性</p>
<p>列出对象</p></td>
<td><p><code>/ msExchEdgeSyncEHFConnector</code></p></td>
</tr>
<tr class="odd">
<td><p>组织管理</p>
<p>Exchange 受信任子系统</p>
<p>本地系统</p>
<p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>后代</p></td>
<td><p>读取权限</p>
<p>列出内容</p>
<p>读取属性</p>
<p>列出对象</p></td>
<td><p><code>/ msExchEdgeSyncMservConnector</code></p></td>
</tr>
<tr class="even">
<td><p>组织管理</p>
<p>Exchange 受信任子系统</p></td>
<td><p>允许 ACE</p></td>
<td><p>子代</p></td>
<td><p>创建子项</p>
<p>删除子项</p>
<p>删除目录树</p></td>
<td><p><code>msExchEdgeSyncServiceConfig / site</code></p></td>
</tr>
<tr class="odd">
<td><p>组织管理</p>
<p>Exchange 受信任子系统</p>
<p>本地系统</p>
<p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>后代</p></td>
<td><p>读取权限</p>
<p>列出内容</p>
<p>读取属性</p>
<p>列出对象</p></td>
<td><p><code>/ msExchEdgeSyncServiceConfig</code></p></td>
</tr>
<tr class="even">
<td><p>组织管理</p>
<p>Exchange 受信任子系统</p></td>
<td><p>允许 ACE</p></td>
<td><p>子代</p></td>
<td><p>创建子项</p>
<p>删除子项</p>
<p>删除目录树</p></td>
<td><p><code>msExchEdgeSyncMservConnector / msExchEdgeSyncServiceConfig</code></p></td>
</tr>
<tr class="odd">
<td><p>组织管理</p>
<p>Exchange 受信任子系统</p></td>
<td><p>允许 ACE</p></td>
<td><p>子代</p></td>
<td><p>创建子项</p>
<p>删除子项</p>
<p>删除目录树</p></td>
<td><p><code>msExchEdgeSyncEHFConnector / msExchEdgeSyncServiceConfig</code></p></td>
</tr>
</tbody>
</table>


### 对象的可分辨名称：CN=Deleted Objects、CN=Configuration、DC=\<domain\>

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
<th>帐户</th>
<th>ACE 类型</th>
<th>继承</th>
<th>权限</th>
<th>针对属性/应用于</th>
<th>注释</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>列出内容</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>组织管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>阅读</p>
<p>列出对象</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>安装 帐户</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>读取权限</p>
<p>写入权限</p>
<p>列出内容</p>
<p>读取属性</p>
<p>列出对象</p></td>
<td><p></p></td>
<td><p>这是用于运行 <code>/PrepareAD</code> 的帐户。</p></td>
</tr>
<tr class="even">
<td><p>Exchange 受信任子系统</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>阅读</p>
<p>列出对象</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>网络服务</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>列出内容</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## Exchange 管理组权限

`Setup /PrepareAD` 命令还为组织中的管理组配置下列权限。

### 对象的可分辨名称：CN=\<admin group\>、CN=Administrative Groups、CN=\<organization\>

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
<th>帐户</th>
<th>ACE 类型</th>
<th>继承</th>
<th>权限</th>
<th>针对属性/应用于</th>
<th>注释</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>组织管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>后代</p></td>
<td><p>访问收件人更新服务</p></td>
<td><p><code>msExchExchangeServer</code></p></td>
<td><p>允许 Exchange 收件人管理员使用代理地址信息标记收件人。</p></td>
</tr>
<tr class="even">
<td><p>本地系统</p></td>
<td><p>允许 ACE</p></td>
<td><p>后代</p></td>
<td><p>访问收件人更新服务</p></td>
<td><p><code>msExchExchangeServer</code></p></td>
<td><p>允许服务器使用代理地址信息标记收件人。</p></td>
</tr>
<tr class="odd">
<td><p>公用文件夹管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>后代</p></td>
<td><p>访问收件人更新服务</p></td>
<td><p><code>msExchExchangeServer</code></p></td>
<td><p>允许 Exchange 公用文件夹管理员使用代理地址信息标记收件人。</p></td>
</tr>
</tbody>
</table>


### 对象的可分辨名称：CN=Advanced Security Settings、CN=\<admin group\>、CN=Administrative Groups、CN=\<organization\>

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
<th>帐户</th>
<th>ACE 类型</th>
<th>继承</th>
<th>权限</th>
<th>针对属性/应用于</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>经过身份验证的用户</p></td>
<td><p>允许 ACE</p></td>
<td><p>无</p></td>
<td><p>列出内容</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### 对象的可分辨名称：CN=Encryption、CN=Advanced Security Settings、CN=\<admin group\>、CN=Administrative Groups、CN=\<organization\>

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
<th>帐户</th>
<th>ACE 类型</th>
<th>继承</th>
<th>权限</th>
<th>针对属性/应用于</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>经过身份验证的用户</p></td>
<td><p>允许 ACE</p></td>
<td><p>无</p></td>
<td><p>读取属性</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### 对象的可分辨名称：CN=Arrays、CN=\<admin group\>、CN=Administrative Groups、CN=\<organization\>

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
<th>帐户</th>
<th>ACE 类型</th>
<th>继承</th>
<th>权限</th>
<th>针对属性/应用于</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>经过身份验证的用户</p></td>
<td><p>允许 ACE</p></td>
<td><p>无</p></td>
<td><p>列出内容</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### 对象的可分辨名称：CN=Database Availability Groups、CN=\<admin group\>、CN=Administrative Groups、CN=\<organization\>

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
<th>帐户</th>
<th>ACE 类型</th>
<th>继承</th>
<th>权限</th>
<th>针对属性/应用于</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>经过身份验证的用户</p></td>
<td><p>允许 ACE</p></td>
<td><p>无</p></td>
<td><p>列出内容</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### 对象的可分辨名称：CN=Databases、CN=\<admin group\>、CN=Administrative Groups、CN=\<organization\>

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
<th>帐户</th>
<th>ACE 类型</th>
<th>继承</th>
<th>权限</th>
<th>针对属性/应用于</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>经过身份验证的用户</p></td>
<td><p>允许 ACE</p></td>
<td><p>无</p></td>
<td><p>列出内容</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### 对象的可分辨名称：CN=Servers、CN=\<admin group\>、CN=Administrative Groups、CN=\<organization\>

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
<th>帐户</th>
<th>ACE 类型</th>
<th>继承</th>
<th>权限</th>
<th>针对属性/应用于</th>
<th>注释</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>拒绝 ACE</p></td>
<td><p>全部</p></td>
<td><p>代理接收</p></td>
<td><p></p></td>
<td><p>不允许 Exchange Servers 打开邮箱。</p></td>
</tr>
<tr class="even">
<td><p>经过身份验证的用户</p></td>
<td><p>允许 ACE</p></td>
<td><p>无</p></td>
<td><p>列出内容</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## Microsoft Exchange 安全组容器权限

本节中的权限表说明了为在根域分区中的 Microsoft Exchange 安全组容器上设置的权限。

### 对象的可分辨名称：OU=Microsoft Exchange Security Groups、DC=\<root domain\>

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
<th>帐户</th>
<th>ACE 类型</th>
<th>继承</th>
<th>权限</th>
<th>针对属性/应用于</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>组织管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>完全控制</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange 受信任子系统</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>创建子项</p></td>
<td><p><code>/ Group</code></p></td>
</tr>
<tr class="odd">
<td><p>Exchange 受信任子系统</p></td>
<td><p>允许 ACE</p></td>
<td><p>后代</p></td>
<td><p>删除</p></td>
<td><p><code>/ group</code></p></td>
</tr>
<tr class="even">
<td><p>Exchange 受信任子系统</p></td>
<td><p>允许 ACE</p></td>
<td><p>后代</p></td>
<td><p>写入属性</p></td>
<td><p><code>Member / group</code></p></td>
</tr>
</tbody>
</table>


### 对象的可分辨名称：CN=Organization Management、OU=Microsoft Exchange Security Groups、DC=\<root domain\>

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
<th>帐户</th>
<th>ACE 类型</th>
<th>继承</th>
<th>权限</th>
<th>针对属性/应用于</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>组织管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>完全控制</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### 对象的可分辨名称：CN=Public Folder Management、OU=Microsoft Exchange Security Groups、DC=\<root domain\>

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
<th>帐户</th>
<th>ACE 类型</th>
<th>继承</th>
<th>权限</th>
<th>针对属性/应用于</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>组织管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>完全控制</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### 对象的可分辨名称：CN=ExchangeLegacyInterop、OU=Microsoft Exchange Security Groups、DC=\<root domain\>

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
<th>帐户</th>
<th>ACE 类型</th>
<th>继承</th>
<th>权限</th>
<th>针对属性/应用于</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>组织管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>完全控制</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### 对象的可分辨名称：CN=Exchange Servers、OU=Microsoft Exchange Security Groups、DC=\<root domain\>

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
<th>帐户</th>
<th>ACE 类型</th>
<th>继承</th>
<th>权限</th>
<th>针对属性/应用于</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>组织管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>完全控制</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Root Domain Administrators</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>读取成员</p>
<p>写入成员</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Child Domain Administrators</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>读取成员</p>
<p>写入成员</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## 准备域

下列各表说明在执行 `Setup /PrepareDomain` 命令时设置的权限。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>本节中描述的权限是当您使用共享权限模型部署 Exchange 2013 时配置的默认权限。如果您已经使用 Active Directory 拆分权限模型部署了Exchange 2013，默认权限将有所不同。有关使用 Active Directory 拆分权限以及共享和拆分权限模型时的默认权限更改的详细信息，请参阅<a href="understanding-split-permissions-exchange-2013-help.md">了解拆分权限</a>中的 <a href="understanding-split-permissions-exchange-2013-help.md">Active Directory split permissions</a>。如果您在安装 Exchange 时不选择使用 Active Directory 拆分权限，Exchange 将使用共享权限。</td>
</tr>
</tbody>
</table>


### 对象的可分辨名称：DC=\<domain\>

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
<th>帐户</th>
<th>ACE 类型</th>
<th>继承</th>
<th>权限</th>
<th>针对属性/应用于</th>
<th>注释</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>经过身份验证的用户</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>读取属性</p></td>
<td><p><code>Exchange Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>NT AUTHORITY\NETWORK</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>读取属性</p></td>
<td><p><code>Exchange Personal Information</code></p></td>
<td><p>向传输服务授予读取权限。</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>groupType</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>msExchMailboxSecurityDescriptor</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>msExchUMServerWritableFlags</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>读取属性</p></td>
<td><p><code>Exchange Personal Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>读取属性</p></td>
<td><p><code>Exchange Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>msExchUserCultulre</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>读取属性</p></td>
<td><p><code>memberOf</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>读取属性</p></td>
<td><p><code>garbageCollPeriod</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>读取属性</p></td>
<td><p><code>userAccountControl</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>读取属性</p></td>
<td><p><code>canonicalName</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>复制同步</p></td>
<td><p></p></td>
<td><p>扩展权限</p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>创建子项</p>
<p>删除子项</p>
<p>列出子项</p></td>
<td><p><code>msExchActiveSyncDevices / User</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>创建子项</p>
<p>删除子项</p>
<p>列出子项</p></td>
<td><p><code>msExchActiveSyncDevices / inetOrgPerson</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>msExchSafeSendersHash</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>msExchPublicDelegates</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>msExchMobileMailboxFlags</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>msExchSafeRecipientsHash</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>userCertificate</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>msExchUMDtmfMap</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>msExchBlockedSendersHash</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>msExchUMSpokenName</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>msExchUMPinChecksum</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>thumbnailPhoto</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>组织管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>阅读</p>
<p>列出对象</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>组织管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>Exchange Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>组织管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>garbageCollPeriod</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>组织管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>legacyExchangeDN</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>组织管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>msExchPublicDelegates</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>组织管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>textEncodedORAddress</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>组织管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>proxyAddresses</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>组织管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>mail</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>组织管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>displayNamePrintable</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>组织管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>showInAddressBook</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>组织管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>Exchange Personal Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>组织管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>完全控制</p></td>
<td><p><code>/ msExchDynamicDistributionList</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>组织管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>adminDisplayName</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>组织管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>displayName</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange 受信任子系统</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>阅读</p>
<p>列出对象</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange 受信任子系统</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>displayName</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange 受信任子系统</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>Public Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange 受信任子系统</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>msExchPublicDelegates</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange 受信任子系统</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>adminDisplayName</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange 受信任子系统</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>完全控制</p></td>
<td><p><code>/ msExchDynamicDistributionList</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange 受信任子系统</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>Exchange Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange 受信任子系统</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>Exchange Personal Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange 受信任子系统</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>garbageCollPeriod</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange 受信任子系统</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>textEncodedORAddress</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange 受信任子系统</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>showInAddressBook</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange 受信任子系统</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>legacyExchangeDN</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange 受信任子系统</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>Personal Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange 受信任子系统</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>proxyAddresses</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange 受信任子系统</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>displayNamePrintable</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange 受信任子系统</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>mail</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Windows 权限</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>pwdLastSet</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Windows 权限</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入 DACL</p></td>
<td><p><code>/ user</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Windows 权限</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入 DACL</p>
<p></p></td>
<td><p><code>/ inetOrgPerson</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Windows 权限</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>删除目录树</p></td>
<td><p><code>/ user</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Windows 权限</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>删除目录树</p>
<p></p></td>
<td><p><code>/ inetOrgPerson</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Windows 权限</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>sAMAccountName</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Windows 权限</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>创建子项</p>
<p>删除</p></td>
<td><p><code>/ contact</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Windows 权限</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>创建子项</p>
<p>删除</p></td>
<td><p><code>/ inetOrgPerson</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Windows 权限</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>创建子项</p>
<p>删除</p></td>
<td><p><code>/ user</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Windows 权限</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>创建子项</p>
<p>删除</p></td>
<td><p><code>/ organizationUnit</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Windows 权限</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>创建子项</p>
<p>删除</p></td>
<td><p><code>/ group</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Windows 权限</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>创建子项</p>
<p>删除子项</p></td>
<td><p><code>/ computer</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Windows 权限</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>Member</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Windows 权限</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>wwwHomePage</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Windows 权限</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>countryCode</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Windows 权限</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>userAccountControl</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Windows 权限</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>managedBy</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Windows 权限</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>在下一次登录时重置密码</p></td>
<td><p></p></td>
<td><p>扩展权限</p></td>
</tr>
<tr class="even">
<td><p>Exchange Windows 权限</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>更改密码</p></td>
<td><p><code> / user</code></p></td>
<td><p>扩展权限</p></td>
</tr>
<tr class="odd">
<td><p>委派安装</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>读取属性</p></td>
<td><p><code>User Account Restrictions</code></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### 对象的可分辨名称：CN=AdminSDHolder、CN=System、DC=\<domain\>

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
<th>帐户</th>
<th>ACE 类型</th>
<th>继承</th>
<th>权限</th>
<th>针对属性/应用于</th>
<th>注释</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>经过身份验证的用户</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>读取属性</p></td>
<td><p><code>Exchange Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>NT AUTHORITY\NETWORK</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>读取属性</p></td>
<td><p><code>Exchange Personal Information</code></p></td>
<td><p>向传输服务授予读取权限。</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>groupType</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>msExchMailboxSecurityDescriptor</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>msExchUMServerWritableFlags</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>读取属性</p></td>
<td><p><code>Exchange Personal Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>读取属性</p></td>
<td><p><code>Exchange Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>msExchUserCultulre</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>读取属性</p></td>
<td><p><code>memberOf</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>读取属性</p></td>
<td><p><code>garbageCollPeriod</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>读取属性</p></td>
<td><p><code>userAccountControl</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>读取属性</p></td>
<td><p><code>canonicalName</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>复制同步</p></td>
<td><p></p></td>
<td><p>扩展权限</p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>创建子项</p>
<p>删除子项</p>
<p>列出子项</p></td>
<td><p><code>msExchActiveSyncDevices / User</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>创建子项</p>
<p>删除子项</p>
<p>列出子项</p></td>
<td><p><code>msExchActiveSyncDevices / inetOrgPerson</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>msExchSafeSendersHash</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>msExchPublicDelegates</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>msExchMobileMailboxFlags</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>msExchSafeRecipientsHash</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>userCertificate</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>msExchUMDtmfMap</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>msExchBlockedSendersHash</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>msExchUMSpokenName</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>msExchUMPinChecksum</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>thumbnailPhoto</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>组织管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>阅读</p>
<p>列出对象</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>组织管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>Exchange Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>组织管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>garbageCollPeriod</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>组织管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>legacyExchangeDN</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>组织管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>msExchPublicDelegates</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>组织管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>textEncodedORAddress</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>组织管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>proxyAddresses</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>组织管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>mail</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>组织管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>displayNamePrintable</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>组织管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>showInAddressBook</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>组织管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>Exchange Personal Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>组织管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>完全控制</p></td>
<td><p><code>/ msExchDynamicDistributionList</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>组织管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>adminDisplayName</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>组织管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>displayName</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange 受信任子系统</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>阅读</p>
<p>列出对象</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange 受信任子系统</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>displayName</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange 受信任子系统</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>Public Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange 受信任子系统</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>msExchPublicDelegates</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange 受信任子系统</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>adminDisplayName</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange 受信任子系统</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>完全控制</p></td>
<td><p><code>/ msExchDynamicDistributionList</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange 受信任子系统</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>Exchange Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange 受信任子系统</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>Exchange Personal Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange 受信任子系统</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>garbageCollPeriod</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange 受信任子系统</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>textEncodedORAddress</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange 受信任子系统</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>showInAddressBook</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange 受信任子系统</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>legacyExchangeDN</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange 受信任子系统</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>Personal Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange 受信任子系统</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>proxyAddresses</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange 受信任子系统</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>displayNamePrintable</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange 受信任子系统</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>mail</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Windows 权限</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>pwdLastSet</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Windows 权限</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>sAMAccountName</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Windows 权限</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>Member</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Windows 权限</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>wwwHomePage</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Windows 权限</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>countryCode</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Windows 权限</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>userAccountControl</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Windows 权限</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p><code>managedBy</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>委派安装</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>读取属性</p></td>
<td><p><code>User Account Restrictions</code></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### 对象的可分辨名称：CN=Deleted Objects、DC=\<domain\>

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
<th>帐户</th>
<th>ACE 类型</th>
<th>继承</th>
<th>权限</th>
<th>针对属性/应用于</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>列出内容</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### 对象的可分辨名称：CN=Microsoft Exchange System Objects、DC=\<domain\>

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
<th>帐户</th>
<th>ACE 类型</th>
<th>继承</th>
<th>权限</th>
<th>针对属性/应用于</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>NT AUTHORITY\NETWORK</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>读取属性</p>
<p>列出内容</p>
<p>读取权限</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>经过身份验证的用户</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>读取权限</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>经过身份验证的用户</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>读取属性</p></td>
<td><p><code>garbageCollPeriod</code></p></td>
</tr>
<tr class="even">
<td><p>经过身份验证的用户</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>读取属性</p></td>
<td><p><code>adminDisplayName</code></p></td>
</tr>
<tr class="odd">
<td><p>经过身份验证的用户</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>读取属性</p></td>
<td><p><code>modifyTimeStamp</code></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>拒绝 ACE</p></td>
<td><p>全部</p></td>
<td><p>删除目录树</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>读取权限</p>
<p>列出内容</p>
<p>读取属性删除树</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>创建子项</p>
<p></p></td>
<td><p><code>/ msExchSystemMailbox</code></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>创建子项</p>
<p>删除子项</p></td>
<td><p><code>/ publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>创建子项</p>
<p></p></td>
<td><p><code>/ user</code></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>删除子项</p>
<p></p></td>
<td><p><code>/ msExchSystemMailbox</code></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>删除子项</p>
<p></p></td>
<td><p><code>/ user</code></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>后代</p></td>
<td><p>写入属性</p></td>
<td><p><code>/ publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>后代</p></td>
<td><p>写入属性</p></td>
<td><p><code>/ msExchSystemMailbox</code></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>后代</p></td>
<td><p>写入属性</p></td>
<td><p><code>/ user</code></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>后代</p></td>
<td><p>更改密码</p>
<p>在下一次登录时重置密码</p></td>
<td><p><code>/ user</code></p></td>
</tr>
<tr class="odd">
<td><p>组织管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>读取权限</p>
<p>列出内容</p>
<p>读取属性</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>组织管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>后代</p></td>
<td><p>写入属性</p></td>
<td><p><code>/ msExchSystemMailbox</code></p></td>
</tr>
<tr class="odd">
<td><p>组织管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>创建子项</p>
<p>删除子项</p></td>
<td><p><code>/ msExchSystemMailbox</code></p></td>
</tr>
<tr class="even">
<td><p>组织管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>后代</p></td>
<td><p>写入属性</p></td>
<td><p><code>/ user</code></p></td>
</tr>
<tr class="odd">
<td><p>组织管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>创建子项</p>
<p>删除子项</p></td>
<td><p><code>/ user</code></p></td>
</tr>
<tr class="even">
<td><p>组织管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>后代</p></td>
<td><p>读取属性</p>
<p>写入属性</p></td>
<td><p><code>mail / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>组织管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>后代</p></td>
<td><p>读取属性</p>
<p>写入属性</p></td>
<td><p><code>displayNamePrintable / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>组织管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>后代</p></td>
<td><p>读取属性</p>
<p>写入属性</p></td>
<td><p><code>displayName / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>组织管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>后代</p></td>
<td><p>读取属性</p>
<p>写入属性</p></td>
<td><p><code>textEncodedORAddress / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>组织管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>后代</p></td>
<td><p>读取属性</p>
<p>写入属性</p></td>
<td><p><code>proxyAddresses / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>组织管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>后代</p></td>
<td><p>读取属性</p>
<p>写入属性</p></td>
<td><p><code>cn / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>组织管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>后代</p></td>
<td><p>读取属性</p>
<p>写入属性</p></td>
<td><p><code>showInAddressBook / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>组织管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>后代</p></td>
<td><p>读取属性</p>
<p>写入属性</p></td>
<td><p><code>Exchange Information / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>组织管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>后代</p></td>
<td><p>读取属性</p>
<p>写入属性</p></td>
<td><p>LegacyExchangeDN / publicFolder</p></td>
</tr>
<tr class="odd">
<td><p>组织管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>后代</p></td>
<td><p>读取属性</p>
<p>写入属性</p></td>
<td><p><code>Exchange Personal Information / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>组织管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>后代</p></td>
<td><p>读取属性</p>
<p>写入属性</p></td>
<td><p><code>msDSPhoneticDisplayName / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>组织管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>后代</p></td>
<td><p>读取属性</p>
<p>写入属性</p></td>
<td><p><code>msExchPFContacts / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>组织管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>后代</p></td>
<td><p>读取属性</p>
<p>写入属性</p></td>
<td><p><code>garbageCollPeriod / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>组织管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>后代</p></td>
<td><p>读取属性</p>
<p>写入属性</p></td>
<td><p><code>name / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>组织管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>后代</p></td>
<td><p>读取属性</p>
<p>写入属性</p></td>
<td><p><code>msExchPublicDelegates / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>公用文件夹管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>读取权限</p>
<p>列出内容</p>
<p>读取属性</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>公用文件夹管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>后代</p></td>
<td><p>读取属性</p>
<p>写入属性</p></td>
<td><p><code>mail / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>公用文件夹管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>后代</p></td>
<td><p>读取属性</p>
<p>写入属性</p></td>
<td><p><code>displayNamePrintable / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>公用文件夹管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>后代</p></td>
<td><p>读取属性</p>
<p>写入属性</p></td>
<td><p><code>displayName / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>公用文件夹管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>后代</p></td>
<td><p>读取属性</p>
<p>写入属性</p></td>
<td><p><code>textEncodedORAddress / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>公用文件夹管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>后代</p></td>
<td><p>读取属性</p>
<p>写入属性</p></td>
<td><p><code>proxyAddresses / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>公用文件夹管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>后代</p></td>
<td><p>读取属性</p>
<p>写入属性</p></td>
<td><p><code>cn / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>公用文件夹管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>后代</p></td>
<td><p>读取属性</p>
<p>写入属性</p></td>
<td><p><code>showInAddressBook / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>公用文件夹管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>后代</p></td>
<td><p>读取属性</p>
<p>写入属性</p></td>
<td><p><code>Exchange Information / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>公用文件夹管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>后代</p></td>
<td><p>读取属性</p>
<p>写入属性</p></td>
<td><p><code>legacyExchangeDN / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>公用文件夹管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>后代</p></td>
<td><p>读取属性</p>
<p>写入属性</p></td>
<td><p><code>Exchange Personal Information / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>公用文件夹管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>后代</p></td>
<td><p>读取属性</p>
<p>写入属性</p></td>
<td><p><code>msDSPhoneticDisplayName / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>公用文件夹管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>后代</p></td>
<td><p>读取属性</p>
<p>写入属性</p></td>
<td><p><code>msExchPFContacts / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>公用文件夹管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>后代</p></td>
<td><p>读取属性</p>
<p>写入属性</p></td>
<td><p><code>garbageCollPeriod / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>公用文件夹管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>后代</p></td>
<td><p>读取属性</p>
<p>写入属性</p></td>
<td><p><code>name / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>公用文件夹管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>后代</p></td>
<td><p>读取属性</p>
<p>写入属性</p></td>
<td><p><code>msExchPublicDelegates / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Exchange 受信任子系统</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>读取权限</p>
<p>列出内容</p>
<p>读取属性</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange 受信任子系统</p></td>
<td><p>允许 ACE</p></td>
<td><p>后代</p></td>
<td><p>读取属性</p>
<p>写入属性</p></td>
<td><p><code>mail / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Exchange 受信任子系统</p></td>
<td><p>允许 ACE</p></td>
<td><p>后代</p></td>
<td><p>读取属性</p>
<p>写入属性</p></td>
<td><p><code>displayNamePrintable / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Exchange 受信任子系统</p></td>
<td><p>允许 ACE</p></td>
<td><p>后代</p></td>
<td><p>读取属性</p>
<p>写入属性</p></td>
<td><p><code>displayName / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Exchange 受信任子系统</p></td>
<td><p>允许 ACE</p></td>
<td><p>后代</p></td>
<td><p>读取属性</p>
<p>写入属性</p></td>
<td><p><code>textEncodedORAddress / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Exchange 受信任子系统</p></td>
<td><p>允许 ACE</p></td>
<td><p>后代</p></td>
<td><p>读取属性</p>
<p>写入属性</p></td>
<td><p><code>proxyAddresses / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Exchange 受信任子系统</p></td>
<td><p>允许 ACE</p></td>
<td><p>后代</p></td>
<td><p>读取属性</p>
<p>写入属性</p></td>
<td><p><code>cn / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Exchange 受信任子系统</p></td>
<td><p>允许 ACE</p></td>
<td><p>后代</p></td>
<td><p>读取属性</p>
<p>写入属性</p></td>
<td><p><code>showInAddressBook / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Exchange 受信任子系统</p></td>
<td><p>允许 ACE</p></td>
<td><p>后代</p></td>
<td><p>读取属性</p>
<p>写入属性</p></td>
<td><p><code>Exchange Information / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Exchange 受信任子系统</p></td>
<td><p>允许 ACE</p></td>
<td><p>后代</p></td>
<td><p>读取属性</p>
<p>写入属性</p></td>
<td><p><code>legacyExchangeDN / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Exchange 受信任子系统</p></td>
<td><p>允许 ACE</p></td>
<td><p>后代</p></td>
<td><p>读取属性</p>
<p>写入属性</p></td>
<td><p><code>Exchange Personal Information / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Exchange 受信任子系统</p></td>
<td><p>允许 ACE</p></td>
<td><p>后代</p></td>
<td><p>读取属性</p>
<p>写入属性</p></td>
<td><p><code>msDSPhoneticDisplayName / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Exchange 受信任子系统</p></td>
<td><p>允许 ACE</p></td>
<td><p>后代</p></td>
<td><p>读取属性</p>
<p>写入属性</p></td>
<td><p><code>msExchPFContacts / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Exchange 受信任子系统</p></td>
<td><p>允许 ACE</p></td>
<td><p>后代</p></td>
<td><p>读取属性</p>
<p>写入属性</p></td>
<td><p><code>garbageCollPeriod / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Exchange 受信任子系统</p></td>
<td><p>允许 ACE</p></td>
<td><p>后代</p></td>
<td><p>读取属性</p>
<p>写入属性</p></td>
<td><p><code>name / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Exchange 受信任子系统</p></td>
<td><p>允许 ACE</p></td>
<td><p>后代</p></td>
<td><p>读取属性</p>
<p>写入属性</p></td>
<td><p><code>msExchPublicDelegates / publicFolder</code></p></td>
</tr>
</tbody>
</table>


### 对象的可分辨名称：CN=Exchange Install Domain Servers、CN=Microsoft Exchange System Objects、DC=\<domain\>

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
<th>帐户</th>
<th>ACE 类型</th>
<th>继承</th>
<th>权限</th>
<th>针对属性/应用于</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>组织管理</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>完全控制</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## 服务器角色安装

在安装客户端访问服务器角色和邮箱服务器角色期间，安装程序会将 Organization Management USG 添加到本地计算机上的管理员安全组中，以便名为 Organization Management 的管理角色组的成员可以管理服务器。

下面的权限表说明了在安装客户端访问服务器角色或邮箱服务器角色时设置的权限。

### 对象的可分辨名称：CN=\<server\>、CN=Servers、CN=\<admin group\>、CN=Administrative Groups、CN=\<organization\>

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
<th>帐户</th>
<th>ACE 类型</th>
<th>继承</th>
<th>权限</th>
<th>针对属性/应用于</th>
<th>注释</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MACHINE$</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>读取权限</p>
<p>列出内容</p>
<p>读取属性</p>
<p>列出对象</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>MACHINE$</p></td>
<td><p>允许 ACE</p></td>
<td><p>无</p></td>
<td><p>写入属性</p></td>
<td><p><code>msExchServerSite</code></p>
<p><code>msExchEdgeSyncCredential</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>存储传输访问</p>
<p>存储约束委派</p>
<p>存储读取仅访问</p>
<p>存储读写访问权限</p></td>
<td><p></p></td>
<td><p>扩展权限</p></td>
</tr>
<tr class="even">
<td><p>NT AUTHORITY\NETWORK</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>Exchange Web 服务令牌序列化</p></td>
<td><p></p></td>
<td><p>扩展权限</p>
<p>仅对邮箱服务器角色对象授予。</p></td>
</tr>
<tr class="odd">
<td><p>NT AUTHORITY\NETWORK</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>读取权限</p>
<p>列出内容</p>
<p>读取属性</p>
<p>列出对象</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>本地系统</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>读取权限</p>
<p>列出内容</p>
<p>读取属性</p>
<p>列出对象</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>委派安装</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>完全控制</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>委派安装</p></td>
<td><p>拒绝 ACE</p></td>
<td><p>全部</p></td>
<td><p>创建子项</p>
<p>删除子项</p></td>
<td><p><code>/ msExchPublicMDB</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>经过身份验证的用户</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>读取属性</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>委派安装</p></td>
<td><p>拒绝 ACE</p></td>
<td><p>全部</p></td>
<td><p>代理接收</p>
<p>代理发送</p></td>
<td><p></p></td>
<td><p>扩展权限</p></td>
</tr>
</tbody>
</table>


## 数据库可用性组

本节中的权限表说明针对数据库可用性组及其成员设置的权限。

### 对象的可分辨名称：CN=\<DAGName\>、CN=Database Availability Groups、CN=\<admin group\>、CN=Administrative Groups、CN=\<organization\>

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
<th>帐户</th>
<th>ACE 类型</th>
<th>继承</th>
<th>权限</th>
<th>针对属性/应用于</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>经过身份验证的用户</p></td>
<td><p>允许 ACE</p></td>
<td><p>无</p></td>
<td><p>读取属性</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## 边缘传输

如果安装边缘传输服务器并与 Exchange 组织建立边缘订阅，在组织中实例化该边缘传输服务器时，将设置以下权限表中的权限。

### 对象的可分辨名称：CN=\<server\>、CN=Servers、CN=\<admin group\>、CN=Administrative Groups、CN=\<organization\>

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
<th>帐户</th>
<th>ACE 类型</th>
<th>继承</th>
<th>权限</th>
<th>针对属性/应用于</th>
<th>注释</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>写入属性</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>经过身份验证的用户</p></td>
<td><p>允许 ACE</p></td>
<td><p>无</p></td>
<td><p>读取属性</p></td>
<td><p></p></td>
<td><p>ACE 是在 <code>msExchExchangeServer</code> 类对象 <code>defaultSecurityDescriptor</code> 的架构中定义的</p></td>
</tr>
</tbody>
</table>


## 邮箱服务器安装

安装第一个邮箱服务器期间，会创建以下容器（如果不存在的话）。以下权限表说明所应用的权限。

### 对象的可分辨名称：CN=Availability Configuration、CN=\<organization\>

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
<th>帐户</th>
<th>ACE 类型</th>
<th>继承</th>
<th>权限</th>
<th>针对属性/应用于</th>
<th>注释</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>后代</p></td>
<td><p>读取属性</p></td>
<td><p><code>msExchAvailabilityUserPassword / msExchAvailabilityAddressSpaceObjects</code></p></td>
<td><p>扩展权限</p></td>
</tr>
</tbody>
</table>


### 对象的可分辨名称：CN=Default \<Server\>、CN=SMTP Receive Connectors、CN=Protocols、CN=\<Server\>、CN=Servers、CN=\<admin group\>、CN=\<organization\>

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
<th>帐户</th>
<th>ACE 类型</th>
<th>继承</th>
<th>权限</th>
<th>针对属性/应用于</th>
<th>注释</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>拒绝 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受林头</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>拒绝 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受组织头</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受任何发件人</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受任何发件人</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受任何发件人</p></td>
<td><p></p></td>
<td><p>这是邮箱服务器的已知安全标识符 (SID)。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受任何发件人</p></td>
<td><p></p></td>
<td><p>这是边缘传输服务器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受任何发件人</p></td>
<td><p></p></td>
<td><p>这是外部安全服务器的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受 EXCH50</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受 EXCH50</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受 EXCH50</p></td>
<td><p></p></td>
<td><p>这是邮箱服务器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受 EXCH50</p></td>
<td><p></p></td>
<td><p>这是边缘传输服务器的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受 EXCH50</p></td>
<td><p></p></td>
<td><p>这是外部安全服务器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>将邮件提交到任何收件人</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>将邮件提交到任何收件人</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>将邮件提交到任何收件人</p></td>
<td><p></p></td>
<td><p>这是邮箱服务器的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>将邮件提交到任何收件人</p></td>
<td><p></p></td>
<td><p>这是边缘传输服务器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>将邮件提交到任何收件人</p></td>
<td><p></p></td>
<td><p>这是外部安全服务器的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受 XShadow</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受 XShadow</p></td>
<td><p></p></td>
<td><p>这是边缘传输服务器的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受路由头</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受路由头</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受路由头</p></td>
<td><p></p></td>
<td><p>这是邮箱服务器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受路由头</p></td>
<td><p></p></td>
<td><p>这是边缘传输服务器的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受路由头</p></td>
<td><p></p></td>
<td><p>这是外部安全服务器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受 XSessionParams</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受 XSessionParams</p></td>
<td><p></p></td>
<td><p>这是邮箱服务器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受 XSessionParams</p></td>
<td><p></p></td>
<td><p>这是邮箱服务器的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受林头</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受林头</p></td>
<td><p></p></td>
<td><p>这是邮箱服务器的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受林头</p></td>
<td><p></p></td>
<td><p>这是边缘传输服务器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受 xAttr</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受 xAttr</p></td>
<td><p></p></td>
<td><p>这是邮箱服务器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受 xAttr</p></td>
<td><p></p></td>
<td><p>这是边缘传输服务器的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受 XProxyFrom</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受林 XProxyFrom</p></td>
<td><p></p></td>
<td><p>这是邮箱服务器的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受林 XProxyFrom</p></td>
<td><p></p></td>
<td><p>这是边缘传输服务器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受 XSysProbe</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受林 XSysProbe</p></td>
<td><p></p></td>
<td><p>这是邮箱服务器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受林 XSysProbe</p></td>
<td><p></p></td>
<td><p>这是边缘传输服务器的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>发送 XMessageContext 扩展属性</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>发送 XMessageContext 扩展属性</p></td>
<td><p></p></td>
<td><p>这是邮箱服务器的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>发送 XMessageContext 扩展属性</p></td>
<td><p></p></td>
<td><p>这是边缘传输服务器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>发送 XMessageContext 快速索引</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>发送 XMessageContext 快速索引</p></td>
<td><p></p></td>
<td><p>这是邮箱服务器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>发送 XMessageContext 快速索引</p></td>
<td><p></p></td>
<td><p>这是边缘传输服务器的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>发送 XMessageContext AD 收件人缓存</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>发送 XMessageContext AD 收件人缓存</p></td>
<td><p></p></td>
<td><p>这是邮箱服务器的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>发送 XMessageContext AD 收件人缓存</p></td>
<td><p></p></td>
<td><p>这是边缘传输服务器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受身份验证标志</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受身份验证标志</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受身份验证标志</p></td>
<td><p></p></td>
<td><p>这是邮箱服务器的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受身份验证标志</p></td>
<td><p></p></td>
<td><p>这是边缘传输服务器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受身份验证标志</p></td>
<td><p></p></td>
<td><p>这是外部安全服务器的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>绕过反垃圾邮件检查</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>绕过反垃圾邮件检查</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>绕过反垃圾邮件检查</p></td>
<td><p></p></td>
<td><p>这是邮箱服务器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>绕过反垃圾邮件检查</p></td>
<td><p></p></td>
<td><p>这是边缘传输服务器的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>绕过反垃圾邮件检查</p></td>
<td><p></p></td>
<td><p>这是外部安全服务器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>绕过邮件大小限制</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>绕过邮件大小限制</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>绕过邮件大小限制</p></td>
<td><p></p></td>
<td><p>这是邮箱服务器的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>绕过邮件大小限制</p></td>
<td><p></p></td>
<td><p>这是边缘传输服务器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>绕过邮件大小限制</p></td>
<td><p></p></td>
<td><p>这是外部安全服务器的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受组织头</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受组织头</p></td>
<td><p></p></td>
<td><p>这是邮箱服务器的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受组织头</p></td>
<td><p></p></td>
<td><p>这是边缘传输服务器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>将邮件提交到服务器</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>将邮件提交到服务器</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>将邮件提交到服务器</p></td>
<td><p></p></td>
<td><p>这是邮箱服务器的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>将邮件提交到服务器</p></td>
<td><p></p></td>
<td><p>这是边缘传输服务器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>将邮件提交到服务器</p></td>
<td><p></p></td>
<td><p>这是外部安全服务器的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受权威域发件人</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受权威域发件人</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受权威域发件人</p></td>
<td><p></p></td>
<td><p>这是邮箱服务器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受权威域发件人</p></td>
<td><p></p></td>
<td><p>这是边缘传输服务器的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受权威域发件人</p></td>
<td><p></p></td>
<td><p>这是外部安全服务器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>经过身份验证的用户</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>将邮件提交到任何收件人</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>经过身份验证的用户</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受路由头</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>经过身份验证的用户</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>绕过反垃圾邮件检查</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>经过身份验证的用户</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>将邮件提交到服务器</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### 对象的可分辨名称：CN=Client \<Server\>、CN=SMTP Receive Connectors、CN=Protocols、CN=\<Server\>、CN=Servers、CN=\<admin group\>、CN=\<organization\>

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
<th>帐户</th>
<th>ACE 类型</th>
<th>继承</th>
<th>权限</th>
<th>针对属性/应用于</th>
<th>注释</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>经过身份验证的用户</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>将邮件提交到任何收件人</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>经过身份验证的用户</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受路由头</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>经过身份验证的用户</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>绕过反垃圾邮件检查</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>经过身份验证的用户</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>将邮件提交到服务器</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受 XSessionParams</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受 XSessionParams</p></td>
<td><p></p></td>
<td><p>这是邮箱服务器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受 XSessionParams</p></td>
<td><p></p></td>
<td><p>这是邮箱服务器的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受任何发件人</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受任何发件人</p></td>
<td><p></p></td>
<td><p>这是邮箱服务器的已知安全标识符 (SID)。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受任何发件人</p></td>
<td><p></p></td>
<td><p>这是边缘传输服务器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受任何发件人</p></td>
<td><p></p></td>
<td><p>这是外部安全服务器的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受 Exch50</p></td>
<td><p></p></td>
<td><p>这是邮箱服务器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受 Exch50</p></td>
<td><p></p></td>
<td><p>这是边缘传输服务器的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受 Exch50</p></td>
<td><p></p></td>
<td><p>这是外部安全服务器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受 Exch50</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>将邮件提交到任何收件人</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>将邮件提交到任何收件人</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>将邮件提交到任何收件人</p></td>
<td><p></p></td>
<td><p>这是邮箱服务器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>将邮件提交到任何收件人</p></td>
<td><p></p></td>
<td><p>这是边缘传输服务器的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>将邮件提交到任何收件人</p></td>
<td><p></p></td>
<td><p>这是外部安全服务器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受 XShadow</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受 XShadow</p></td>
<td><p></p></td>
<td><p>这是边缘传输服务器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受路由头</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受路由头</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受路由头</p></td>
<td><p></p></td>
<td><p>这是邮箱服务器的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受路由头</p></td>
<td><p></p></td>
<td><p>这是边缘传输服务器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受路由头</p></td>
<td><p></p></td>
<td><p>这是外部安全服务器的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受林头</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受林头</p></td>
<td><p></p></td>
<td><p>这是邮箱服务器的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受林头</p></td>
<td><p></p></td>
<td><p>这是边缘传输服务器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受 xAttr</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受 xAttr</p></td>
<td><p></p></td>
<td><p>这是邮箱服务器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受 xAttr</p></td>
<td><p></p></td>
<td><p>这是边缘传输服务器的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受 XProxyFrom</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受林 XProxyFrom</p></td>
<td><p></p></td>
<td><p>这是邮箱服务器的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受林 XProxyFrom</p></td>
<td><p></p></td>
<td><p>这是边缘传输服务器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受身份验证标志</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受身份验证标志</p></td>
<td><p></p></td>
<td><p>这是邮箱服务器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受身份验证标志</p></td>
<td><p></p></td>
<td><p>这是边缘传输服务器的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受身份验证标志</p></td>
<td><p></p></td>
<td><p>这是外部安全服务器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受 XSysProbe</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受林 XSysProbe</p></td>
<td><p></p></td>
<td><p>这是邮箱服务器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受林 XSysProbe</p></td>
<td><p></p></td>
<td><p>这是边缘传输服务器的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受身份验证标志</p></td>
<td><p></p></td>
<td><p>这是外部安全服务器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>绕过反垃圾邮件检查</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>绕过反垃圾邮件检查</p></td>
<td><p></p></td>
<td><p>这是邮箱服务器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>绕过反垃圾邮件检查</p></td>
<td><p></p></td>
<td><p>这是边缘传输服务器的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>绕过反垃圾邮件检查</p></td>
<td><p></p></td>
<td><p>这是外部安全服务器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>发送 XMessageContext 扩展属性</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>发送 XMessageContext 扩展属性</p></td>
<td><p></p></td>
<td><p>这是邮箱服务器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>发送 XMessageContext 扩展属性</p></td>
<td><p></p></td>
<td><p>这是边缘传输服务器的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>发送 XMessageContext 快速索引</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>发送 XMessageContext 快速索引</p></td>
<td><p></p></td>
<td><p>这是邮箱服务器的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>发送 XMessageContext 快速索引</p></td>
<td><p></p></td>
<td><p>这是边缘传输服务器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>绕过邮件大小限制</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>绕过邮件大小限制</p></td>
<td><p></p></td>
<td><p>这是邮箱服务器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>绕过邮件大小限制</p></td>
<td><p></p></td>
<td><p>这是边缘传输服务器的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>绕过邮件大小限制</p></td>
<td><p></p></td>
<td><p>这是外部安全服务器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受组织头</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受组织头</p></td>
<td><p></p></td>
<td><p>这是邮箱服务器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受组织头</p></td>
<td><p></p></td>
<td><p>这是边缘传输服务器的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>发送 XMessageContext AD 收件人缓存</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>发送 XMessageContext AD 收件人缓存</p></td>
<td><p></p></td>
<td><p>这是邮箱服务器的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>发送 XMessageContext AD 收件人缓存</p></td>
<td><p></p></td>
<td><p>这是边缘传输服务器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>将邮件提交到服务器</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>将邮件提交到服务器</p></td>
<td><p></p></td>
<td><p>这是邮箱服务器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>将邮件提交到服务器</p></td>
<td><p></p></td>
<td><p>这是边缘传输服务器的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>将邮件提交到服务器</p></td>
<td><p></p></td>
<td><p>这是外部安全服务器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受权威域发件人</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受权威域发件人</p></td>
<td><p></p></td>
<td><p>这是邮箱服务器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受权威域发件人</p></td>
<td><p></p></td>
<td><p>这是边缘传输服务器的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受权威域发件人</p></td>
<td><p></p></td>
<td><p>这是外部安全服务器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## 创建 SMTP 发送连接器

下表说明在创建发送连接器时设置的权限。

### 对象的可分辨名称：CN=\<Connector Name\>、CN=Connections、CN=\<routing group\>、CN=Routing Groups、CN=\<admin group\>、CN=\<organization\>

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
<th>帐户</th>
<th>ACE 类型</th>
<th>继承</th>
<th>权限</th>
<th>针对属性/应用于</th>
<th>注释</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>NT AUTHORITY\ANONYMOUS LOGON</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>发送路由头</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>发送组织头</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>发送组织头</p></td>
<td><p></p></td>
<td><p>这是邮箱服务器的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>发送组织头</p></td>
<td><p></p></td>
<td><p>这是边缘传输服务器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>发送林头</p></td>
<td><p></p></td>
<td><p>这是邮箱服务器的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>发送林头</p></td>
<td><p></p></td>
<td><p>这是邮箱服务器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>发送林头</p></td>
<td><p></p></td>
<td><p>这是边缘传输服务器的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>发送 XShadow</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>发送 XShadow</p></td>
<td><p></p></td>
<td><p>这是邮箱服务器的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>发送 XShadow</p></td>
<td><p></p></td>
<td><p>这是边缘传输服务器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>发送路由头</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-10</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>发送路由头</p></td>
<td><p></p></td>
<td><p>这是伙伴服务器已知的 SID。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>发送路由头</p></td>
<td><p></p></td>
<td><p>这是邮箱服务器的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>发送路由头</p></td>
<td><p></p></td>
<td><p>这是边缘传输服务器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>发送路由头</p></td>
<td><p></p></td>
<td><p>这是外部安全服务器的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-24</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>发送路由头</p></td>
<td><p></p></td>
<td><p>这是旧版 Exchange 服务器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>发送 Exch50</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>发送 Exch50</p></td>
<td><p></p></td>
<td><p>这是邮箱服务器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>发送 Exch50</p></td>
<td><p></p></td>
<td><p>这是边缘传输服务器的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>发送 Exch50</p></td>
<td><p></p></td>
<td><p>这是外部安全服务器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-24</p></td>
<td><p>允许 ACE</p></td>
<td><p>全部</p></td>
<td><p>发送 Exch50</p></td>
<td><p></p></td>
<td><p>这是旧版 Exchange 服务器的已知 SID。</p></td>
</tr>
</tbody>
</table>

