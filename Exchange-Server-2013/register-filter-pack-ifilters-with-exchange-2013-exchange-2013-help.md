---
title: '向 Exchange 2013 注册 Filter Pack IFilter: Exchange 2013 Help'
TOCTitle: 向 Exchange 2013 注册 Filter Pack IFilter
ms:assetid: 0338980f-3a64-49d3-bc3c-bf6f10f88cb4
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ837174(v=EXCHG.150)
ms:contentKeyID: 50556517
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 向 Exchange 2013 注册 Filter Pack IFilter

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2016-12-09_

具有附件扫描条件的传输规则在分析附件内容时可执行文本提取。Exchange 2013 可在本机扫描最常用的附件类型。通过在 Exchange 2013 中注册 IFilter，可以包含其他附件类型。此主题介绍了如何注册 Microsoft 和第三方提供商发布的 IFilter。

在为特定的文件类型注册 IFilter 后，具有附件处理条件的传输规则将能够扫描到这些附件。结果是，这些文件类型不再会触发 *AttachmentIsUnsupported* 条件。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876845.Caution(EXCHG.150).gif" title="小心" alt="小心" />小心：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>本主题中列出的过程包括修改 Exchange 服务器上的注册表。未正确编辑注册表可能造成严重问题，也许需要您重新安装操作系统。未正确编辑注册表造成的问题可能无法解决。在编辑注册表之前，请备份所有有价值的数据。<br />
这些过程还会要求您在邮箱服务器上停止，然后再重新启动 Microsoft Exchange 传输服务。</td>
</tr>
</tbody>
</table>


有关与传输规则相关的其他管理任务，请参阅[管理邮件流规则](manage-mail-flow-rules-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤时间：每台服务器 5 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[Exchange 和命令行管理程序基础结构权限](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md)主题中的“Exchange Server 配置设置”条目。

  - 您必须在安装了 Exchange 2013 邮箱服务器角色的服务器上执行以下步骤。如果您在执行这些步骤之后添加了其他邮箱服务器，则必须在新设置的服务器上再次执行这些步骤。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。</td>
</tr>
</tbody>
</table>


## 您想执行什么操作？

## 注册 Microsoft Office 2010 Filter Pack

默认情况下，Exchange 传输规则不支持以下 Office 文件类型：

  - Office OneNote

  - Office Publisher

如果要支持这些文件，必须部署 Microsoft Office 2010 Filter Pack。此 Filter Pack 在 Exchange 2013 安装期间不会被部署，也不是部署的先决条件。

## 部署 Microsoft Office 2010 Filter Pack

部署 Office 2010 Filter Pack 分为两个主要步骤：

  - 下载和安装可在 Windows（搜索）中注册 IFilter 的 Filter Pack。

  - 修改注册表，以便也可在 Exchange 2013 中注册 IFilter。 这将允许 Exchange 支持附件文件格式扫描。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>必须在组织中的所有邮箱服务器上执行此步骤。</td>
</tr>
</tbody>
</table>


1.  从 [Microsoft 下载中心](https://go.microsoft.com/fwlink/?linkid=191548)下载并保存 Microsoft Office 2010 Filter Pack (`FilterPack64bit.exe`)。

2.  在邮箱服务器上运行 `FilterPack64bit.exe` 文件，然后按照说明完成此安装。

3.  启动“注册表编辑器”，找到以下注册表子项：
    
        HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v15\HubTransportRole\CLSID

4.  在“CLSID” 下，为 OneNote 文件添加一个子项，操作如下：
    
    1.  右键单击“CLSID”，指向“新建” ，然后单击“项”。
    
    2.  将新项的名称更改为 `{B8D12492-CE0F-40AD-83EA-099A03D493F1}`。
    
    3.  单击刚创建的项，然后将“(默认)”值设置为安装 Office 2010 Filter Pack 所在的位置。默认情况下，该 Filter Pack 安装在 `C:\Program Files\Common Files\Microsoft Shared\Filters\ONIFilter.dll` 中。
    
    4.  右键单击“{B8D12492-CE0F-40AD-83EA-099A03D493F1}”，指向“新建”，然后单击“字符串值”。
    
    5.  将新字符串值命名为 `ThreadingModel`，然后将其设置为 `Both`。

5.  在“CLSID”下，为 Publisher 文件添加一个子项，操作如下：
    
    1.  右键单击“CLSID”，指向“新建”，然后单击“项”。
    
    2.  将新项的名称更改为 `{A7FD8AC9-7ABF-46FC-B70B-6A5E5EC9859A}`。
    
    3.  单击刚创建的项，然后将“(默认)”值设置为安装 Office 2010 Filter Pack 所在的位置。默认情况下，该 Filter Pack 安装在 `C:\Program Files\Common Files\Microsoft Shared\Filters\PUBFILT.dll` 中。
    
    4.  右键单击“{A7FD8AC9-7ABF-46FC-B70B-6A5E5EC9859A}”，指向“新建”，然后单击“字符串值”。
    
    5.  将新字符串值命名为 `ThreadingModel`，然后将其设置为 `Both`。

6.  找到以下注册表项：
    
        HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v15\HubTransportRole\filters

7.  在“筛选器”下，为 .one 扩展名添加一个子项，操作如下：
    
    1.  右键单击“筛选器”，指向“新建”，然后单击“项”。
    
    2.  将新项的名称更改为 `.one`。
    
    3.  单击刚创建的项，然后将“(默认)”值设置为 `{B8D12492-CE0F-40AD-83EA-099A03D493F1}`。

8.  在“筛选器”下，为 .pub 扩展名添加一个子项，操作如下：
    
    1.  右键单击“筛选器”，指向“新建”，然后单击“项”。
    
    2.  将新项的名称更改为 `.pub`。
    
    3.  单击刚创建的项，然后将“(默认)”值设置为 `{A7FD8AC9-7ABF-46FC-B70B-6A5E5EC9859A}`。

9.  关闭注册表编辑器。

10. 在您的邮箱服务器上，按指定的顺序停止然后再重新启动以下服务：
    
    1.  停止 Microsoft Exchange 传输服务。
    
    2.  停止 Microsoft 筛选管理服务。
    
    3.  启动 Microsoft 筛选管理服务。
    
    4.  启动 Microsoft Exchange 传输服务。

## 您如何知道这有效？

要验证您是否成功注册了 Microsoft Office 2010 Filter Pack IFilter，请执行以下操作：

1.  使用以下属性创建传输规则。有关如何创建传输规则的详细说明，请参阅[管理邮件流规则](manage-mail-flow-rules-exchange-2013-help.md)。
    
      - 发件人是您的邮箱。
    
      - 任何附件的内容都包含“Testing IFilters”。
    
      - 生成事件报告，并将其发送到您的邮箱。

2.  创建包含短语“Testing IFilters”的 OneNote 文件，将其附加到新的电子邮件中，然后将其发送给自己。

3.  验证您是否收到您刚创建的规则的传输规则事件报告。这能确认规则引擎可以分析 OneNote 文件的内容。

4.  针对 Publisher 文件重复步骤 2 和 3 。

## 注册第三方 IFilter 以支持其他文件格式

您可以通过注册其他第三方 IFilter 来扩展其他文件类型的附加扫描功能。可以通过在每个邮箱服务器上安装和注册文件类型的 IFilter，添加其他文件支持功能。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Microsoft 没有通过传输规则测试第三方 IFilter，因此，我们建议您在测试环境中部署和测试任何第三方 IFilter，然后再部署到您的生产环境中。</td>
</tr>
</tbody>
</table>


## 部署 Adobe PDF IFilter

此过程介绍了如何部署 [Adobe PDF IFilter](https://www.adobe.com/support/downloads/detail.jsp?ftpid=4025) 以支持在传输规则中处理 PDF 附件。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>默认情况下，Exchange 2013 支持在传输规则中扫描 PDF 文件。此处所用的 PDF 示例的目的是说明如何使用第三方 IFilter 扩展其他文件类型的支持。</td>
</tr>
</tbody>
</table>


1.  下载 [Adobe PDF IFilter](https://www.adobe.com/support/downloads/detail.jsp?ftpid=4025)，然后按照安装说明进行操作。

2.  启动“注册表编辑器”，找到以下子项：
    
        HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v15\HubTransportRole\CLSID

3.  在“CLSID”下，为 PDF 文件添加一个子项，操作如下：
    
    1.  右键单击“CLSID”，指向“新建”，然后单击“项”。
    
    2.  将新项的名称更改为 `{E8978DA6-047F-4E3D-9C78-CDBE46041603}`。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>每个 IFilter 都具有一个唯一的类 ID (CLSID)。您可以在您要注册的 IFilter 的安装文档中或通过在注册表的 <code>HKEY_CLASSES_ROOT\CLSID</code> 项下搜索文件扩展名找到此 CLSID。</td>
        </tr>
        </tbody>
        </table>
    
    3.  单击刚创建的项，然后将“(默认)”值设置为安装 PDF IFilter 所在的位置。默认情况下，PDF IFilter 安装在 `C:\Program Files\Adobe\Adobe PDF IFilter 9 for 64-bit platforms\bin\PDFFilter.dll` 中。

4.  找到以下注册表项：
    
        HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v15\HubTransportRole\filters

5.  在“筛选器”下，为 .pdf 扩展名添加一个子项，操作如下：
    
    1.  右键单击“筛选器”，指向“新建”，然后单击“项”。
    
    2.  将新项的名称更改为 `.pdf`。
    
    3.  单击刚创建的项，然后将“(默认)”值设置为 `{E8978DA6-047F-4E3D-9C78-CDBE46041603}`。

6.  关闭注册表编辑器。

7.  在您的邮箱服务器上，按指定的顺序停止然后再重新启动以下服务：
    
    1.  停止 Microsoft Exchange 传输服务。
    
    2.  停止 Microsoft 筛选管理服务。
    
    3.  启动 Microsoft 筛选管理服务。
    
    4.  启动 Microsoft Exchange 传输服务。

## 您如何知道这有效？

通过本主题前面的 您如何知道这有效？ 部分中所列出的相同步骤，使用 Adobe PDF 文件替换 Publisher 文件。

## 详细信息

[使用传输规则检查邮件附件](use-transport-rules-to-inspect-message-attachments-exchange-2013-help.md)

[邮件流或传输规则](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)

[传输规则条件（谓词）](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md)

[传输规则操作](mail-flow-rule-actions-in-exchange-2013-exchange-2013-help.md)

