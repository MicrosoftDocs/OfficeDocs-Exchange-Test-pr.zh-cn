---
title: '在边缘传输服务器上导入地址重写条目: Exchange 2013 Help'
TOCTitle: 在边缘传输服务器上导入地址重写条目
ms:assetid: bd0942c6-9c66-4b4c-b9bc-2f5f783def76
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb331966(v=EXCHG.150)
ms:contentKeyID: 61060579
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 在边缘传输服务器上导入地址重写条目

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-03-09_

使用逗号分隔值 (CSV) 文件可以批量创建地址重写信息或将其导入边缘传输服务器。以下列表描述了需要您执行此操作的常见情况：

  - 您要用边缘传输服务器替换地址重写解决方案。

  - 您与第三方解决方案提供商达成协议，需要您重写他们的电子邮件地址。

  - 您收购其他组织，需要临时重写已收购组织中的电子邮件地址。

可以使用任何文本编辑器（如 Notepad）或应用程序（如 Microsoft Excel）创建 CSV 文件。按照本主题中的描述对文件进行格式化并保存为 .csv 文件。

CSV 文件的第一行（或*标题行*）列出了参数的名称。每个参数都用逗号分隔开。下表介绍了必需以及可选的参数。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>参数</th>
<th>必需还是可选</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Name</em></p></td>
<td><p>必需</p></td>
<td><p>地址重写条目的唯一的描述性名称。</p></td>
</tr>
<tr class="even">
<td><p><em>InternalAddress</em></p></td>
<td><p>必需</p></td>
<td><p>要更改的地址。可以使用下列值：</p>
<ul>
<li><p>单个电子邮件地址 (chris@contoso.com)</p></li>
<li><p>单个域或子域（contoso.com 或 sales.contoso.com）</p></li>
<li><p>域和所有子域 (*.contoso.com)</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><em>ExternalAddress</em></p></td>
<td><p>必需</p></td>
<td><p>您需要的最终电子邮件地址。可以使用下列值：</p>
<ul>
<li><p>单个电子邮件地址（如果您为 <em>InternalAddress</em> 指定了单个电子邮件地址）</p></li>
<li><p>单个域或子域（针对 <em>InternalAddress</em> 的其他所有值）</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><em>ExceptionList</em></p></td>
<td><p>可选</p></td>
<td><p>仅在您要重写某个域和所有子域 (*.contoso.com) 中的电子邮件地址时可用。指定您要从地址重写中排除的一个或多个子域。将值置于双引号内，并用逗号分隔开多个值。例如，<code>&quot;marketing.contoso.com&quot;</code> 或 <code>&quot;marketing.contoso.com,legal.contoso.com&quot;</code>。</p></td>
</tr>
<tr class="odd">
<td><p><em>OutboundOnly</em></p></td>
<td><p>可选</p></td>
<td><p><code>False</code> 意味着重写入站和出站邮件上的地址。<code>True</code> 意味着仅重写出站邮件上的地址，而且需要手动将重写电子邮件地址配置为受影响收件人的代理地址。</p>
<p>默认值为 <code>False</code>。但是，如果 <em>InternalAddress</em> 包含通配符 (*.contoso.com)，那么您必须将值设置为 <code>True</code>。</p>
<p>CSV 文件中的 <em>OutboundOnly</em> 参数值为 <code>True</code> 或 <code>False</code>，而非 <code>$True</code> 或 <code>$False</code>。</p></td>
</tr>
</tbody>
</table>


标题行下面的各行代表单个地址重写条目。每行中的值的顺序必须与标题行中的参数名的顺序相同。每个值都用逗号分隔开。

## 在开始之前，您需要知道什么？

  - 估计完成该任务的时间：30 分钟

  - 请务必了解地址重写的后果影响。例如，重写电子邮件地址在您的 Exchange 组织中必须是独一无二的，而且您可能需要为受影响收件人配置代理地址。有关详细信息，请参阅 [边缘传输服务器上的地址重写](address-rewriting-on-edge-transport-servers-exchange-2013-help.md)和[在边缘传输服务器上管理地址重写](manage-address-rewriting-on-edge-transport-servers-exchange-2013-help.md)。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [邮件流权限](mail-flow-permissions-exchange-2013-help.md)主题中的\&quot;地址重写代理\&quot;条目。

  - 如果有多个边缘传输服务器，建议您使用本主题中的步骤将地址重写条目导入一个边缘传输服务器，然后将该边缘传输服务器的配置克隆到组织中的其他边缘传输服务器上。有关如何克隆边缘传输服务器的详细信息，请参阅[边缘传输服务器克隆配置](edge-transport-server-cloned-configuration-exchange-2013-help.md)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!tip]
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 您该如何做？

## 步骤 1：创建 CSV 文件

创建 CSV 文件后，请考虑以下事项：

  - 如果为 CSV 文件中的可选参数指定了值，每一行在该列中必须包含值。如果要创建多个地址重写条目，且其中的一些条目含有可选参数，一些不含有，则需要将这些地址重写条目划分到两个单独的 CSV 文件中，并分开导入每个 CSV 文件。

  - 如果 CSV 文件包含非 ASCII 字符，请务必使用 UTF-8 或其他 Unicode 编码保存 CSV 文件。根据应用程序的不同，如果计算机的系统区域设置与 CSV 文件中使用的语言相匹配，则使用 UTF-8 或其他 Unicode 编码保存 CSV 文件可能会更容易。

以下示例说明如何填充包含可选的 *ExceptionList* 和 *OutboundOnly* 参数的 CSV 文件：

    Name,InternalAddress,ExternalAddress,ExceptionList,OutboundOnly
    "Wingtip UK",*.wingtiptoys.co.uk,tailspintoys.com,"legal.wingtiptoys.co.uk,finance.wingtiptoys.co.uk,support.wingtiptoys.co.uk",True
    "Wingtip USA",*.wingtiptoys.com,tailspintoys.com,"legal.wingtiptoys.com,finance.wingtiptoys.com,support.wingtiptoys.com,corp.wingtiptoys.com",True
    "Wingtip Canada",*.wingtiptoys.ca,tailspintoys.com,"legal.wingtiptoys.ca,finance.wingtiptoys.ca,support.wingtiptoys.ca",True

## 步骤 2：导入 CSV 文件

若要导入 CSV 文件，请使用以下语法：

    Import-Csv <FileNameAndPath> | ForEach {New-AddressRewriteEntry -Name $_.Name -InternalAddress $_.InternalAddress -ExternalAddress $_.ExternalAddress -OutboundOnly ([Bool]::Parse($_.OutboundOnly)) -ExceptionList $_.ExceptionList}

此示例导入 C:\\My Documents\\ImportAddressRewriteEntries.csv 中的地址重写条目。

    Import-Csv "C:\My Documents\ImportAddressRewriteEntries.csv" | ForEach {New-AddressRewriteEntry -Name $_.Name -InternalAddress $_.InternalAddress -ExternalAddress $_.ExternalAddress -OutboundOnly ([Bool]::Parse($_.OutboundOnly)) -ExceptionList $_.ExceptionList}

## 您如何知道此步骤有效？

若要验证是否成功导入 CSV 文件中的地址重写条目，请执行以下操作：

1.  若要查看所有地址重写条目，请运行命令 `Get-AddressRewriteEntry`。

2.  若要查看有关特定地址重写条目的详细信息，请运行命令 `Get-AddressRewriteEntry <AddressRewriteIdentity> | Format-List`

