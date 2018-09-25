---
title: '管理员审核日志结构: Exchange 2013 Help'
TOCTitle: 管理员审核日志结构
ms:assetid: 87e259c9-c884-4d53-bd78-d13f2300d73e
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Ff459251(v=EXCHG.150)
ms:contentKeyID: 50556611
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 管理员审核日志结构

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-03-09_

管理员审核日志包含关于 Exchange 命令行管理程序中已经运行的以及由 Exchange 管理中心 (EAC) 运行的所有 cmdlet 和参数的记录。在 EAC 中运行管理员审核日志报告或者在命令行管理程序中运行 **New-AdminAuditLogSearch** cmdlet 时，会按需创建管理员审核日志。有关审核日志的详细信息，请参阅[管理员审核日志记录](administrator-audit-logging-exchange-2013-help.md)。

审核日志是 XML 文件，并且可以包含多个审核日志条目。下表描述了每个 XML 标记及其关联特性。

是否正在寻找与管理员审核日志相关的管理任务？请参阅[管理管理员审核日志记录](manage-administrator-audit-logging-exchange-2013-help.md)。

### 审核日志 XML 标记和特性

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>元素</th>
<th>属性</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>&lt;?xml version=&quot;1.0&quot; encoding=&quot;utf-8&quot;?&gt;</code></p>
<p></p></td>
<td><p><code>N/A</code></p></td>
<td><p>这是 XML 文档声明标记。每个审核日志 XML 文件中都包括此声明标记，该标记包含 XML 版本号和字符型编码值。</p></td>
</tr>
<tr class="even">
<td><p><code>SearchResults</code></p></td>
<td><p><code>N/A</code></p></td>
<td><p>此标记包含 XML 文件中的所有审核日志条目。<code>Event</code> 标记是此标记的子级。</p>
<p>每个 XML 文件只有一个 <code>SearchResults</code> 标记。</p></td>
</tr>
<tr class="odd">
<td><p><code>Event</code></p></td>
<td><p></p></td>
<td><p>此标记包含单个 cmdlet 的审核日志条目。此标记包含 <code>Caller</code>、<code>Cmdlet</code>、<code>ObjectModified</code>、<code>RunDate</code>、<code>Succeeded</code>、<code>Error</code> 和 <code>OriginatingServer</code> 特性。<code>CmdletParameters</code> 和 <code>ModifiedProperties</code> 标记是此标记的子级。</p>
<p>每个审核日志条目有一个 <code>Event</code> 标记。</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p><code>Caller</code></p></td>
<td><p>此特性包含在 <code>Cmdlet</code> 属性中运行 cmdlet 的用户的用户帐户。</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p><code>Cmdlet</code></p></td>
<td><p>此特性包含用户在 <code>Caller</code> 属性中运行的 cmdlet 的名称。</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p><code>ObjectModified</code></p></td>
<td><p>此特性包含由在 <code>Cmdlet</code> 属性中指定的 cmdlet 修改的对象。<code>ModifiedProperties</code> 标记显示修改了此对象的哪些属性。</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p><code>RunDate</code></p></td>
<td><p>此特性包含运行 <code>Cmdlet</code> 属性中的 cmdlet 时的日期和时间。</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p><code>Succeeded</code></p></td>
<td><p>此特性说明 <code>Cmdlet</code> 属性中的 cmdlet 是否成功运行。值为 <code>True</code> 或 <code>False</code>。</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p><code>Error</code></p></td>
<td><p>此特性包含 <code>Cmdlet</code> 属性中的 cmdlet 没有成功完成时生成的错误信息。如果没有出现错误，值将被设置为 <code>None</code>。</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p><code>OriginatingServer</code></p></td>
<td><p>此特性包含运行 <code>Cmdlet</code> 属性中指定的 cmdlet 的服务器。</p></td>
</tr>
<tr class="odd">
<td><p><code>CmdletParameters</code></p></td>
<td><p><code>N/A</code></p></td>
<td><p>此标记包含运行 cmdlet 时指定的所有参数。<code>Parameter</code> 标记是此标记的子级。</p>
<p>每个 <code>Event</code> 标记有一个 <code>CmdletParameters</code> 标记。</p></td>
</tr>
<tr class="even">
<td><p><code>Parameter</code></p></td>
<td><p></p></td>
<td><p>此标记包含运行 cmdlet 时指定的单个参数。此标记包含 <code>Name</code> 和 <code>Value</code> 特性。</p>
<p>每个 <code>CmdletParameters</code> 标记可以有多个 <code>Parameter</code> 标记。</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p><code>Name</code></p></td>
<td><p>此特性包含运行 cmdlet 时指定的参数的名称。</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p><code>Value</code></p></td>
<td><p>此特性包含为 <code>Name</code> 属性中指定的参数提供的值。</p></td>
</tr>
<tr class="odd">
<td><p><code>ModifiedProperties</code></p></td>
<td><p><code>N/A</code></p></td>
<td><p>此标记包含由运行的 cmdlet 修改的所有属性。<code>Property</code> 标记是此标记的子级。</p>
<p>每个 <code>Event</code> 标记有一个 <code>ModifiedProperties</code> 标记。</p>

> [!IMPORTANT]  
> 仅当 <strong>Set-AdminAuditLogConfig</strong> cmdlet 上的 <em>LogLevel</em> 参数设置 <code>Verbose</code> 时，才会填充此标记。

</td>
</tr>
<tr class="even">
<td><p><code>Property</code></p></td>
<td><p></p></td>
<td><p>此标记包含运行 cmdlet 时指定的单个属性。此标记包含 <code>Name</code>、<code>OldValue</code> 和 <code>NewValue</code> 特性。</p>
<p>每个 <code>ModifiedProperties</code> 标记可以有多个 <code>Property</code> 标记。</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p><code>Name</code></p></td>
<td><p>此特性包含运行 cmdlet 时修改的属性的名称。</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p><code>OldValue</code></p></td>
<td><p>此特性包含 <code>Name</code> 特性在更改之前指定的属性所包含的值。</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p><code>NewValue</code></p></td>
<td><p>此特性包含 <code>Name</code> 特性中的属性更改后的值。</p></td>
</tr>
</tbody>
</table>


## 示例审核日志条目

以下是典型审核日志条目的示例。根据日志条目中的信息，我们知道发生了以下事件：

  - 2012 年 10 月 18 日下午 3:48 太平洋夏令时 (UTC-7)，用户 `Administrator` 运行了 cmdlet **Set-Mailbox**。

  - 运行 **Set-Mailbox** cmdlet 时提供了以下两个参数：
    
      - *Identity* 值为`david`
    
      - *ProhibitSendReceiveQuota* 值为`10GB`

  - 修改了对象 `david` 中的以下两个属性：
    
    > [!NOTE]  
    > 在此示例中，因为 <code>Set-AdminAuditLogConfig</code> cmdlet 上的 <em>LogLevel</em> 参数设置为 <code>Verbose</code>，因此将修改后的属性保存到了审核日志中。
    
      - *ProhibitSendReceiveQuota*，其新值为 `10GB`，替换了旧值 `35GB`

  - 操作没有发生任何错误，成功完成。

<!-- end list -->

```xml
    <?xml version="1.0" encoding="utf-8"?>
    <SearchResults>
    
      <Event Caller="corp.e15a.contoso.com/Users/Administrator" Cmdlet="Set-Mailbox" ObjectModified="corp.e15a.contoso.com/Users/david" RunDate="2012-10-18T15:48:15-07:00" Succeeded="true" Error="None" OriginatingServer="WIN8MBX (15.00.0516.032)">
        <CmdletParameters>
          <Parameter Name="Identity" Value="david" />
          <Parameter Name="ProhibitSendReceiveQuota" Value="10 GB (10,737,418,240 bytes)" />
        </CmdletParameters>
        <ModifiedProperties>
          <Property Name="ProhibitSendReceiveQuota" OldValue="35 GB (37,580,963,840 bytes)" NewValue="10 GB (10,737,418,240 bytes)" />
        </ModifiedProperties>
      </Event>
    </SearchResults>
```    

