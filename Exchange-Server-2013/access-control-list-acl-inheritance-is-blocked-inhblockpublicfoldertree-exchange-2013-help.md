---
title: '访问控制列表 (ACL) 继承已锁定 (_InhBlockPublicFolderTree): Exchange 2013 Help'
TOCTitle: 访问控制列表 (ACL) 继承已锁定 (_InhBlockPublicFolderTree)
ms:assetid: e3b89c8a-d6f8-4864-8bf0-35a78ce87cc4
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/ms.exch.setupreadiness.inhblockpublicfoldertree(v=EXCHG.150)
ms:contentKeyID: 50491860
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 访问控制列表 (ACL) 继承已锁定 (\_InhBlockPublicFolderTree)

 

_**适用于：** Exchange Server_

_**上一次修改主题：** 2015-03-09_

此主题中的内容尚未针对 Microsoft Exchange Server 2013 进行更新。虽然尚未更新，但仍可能适用于 Exchange 2013。如果您仍需要帮助，请查看下面的社区资源。

遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

因为所需的权限无法传播，所以 Microsoft Exchange Server 2007 或 Exchange Server 2010 安装程序无法继续进行。

Exchange 安装程序要求对下列 Exchange 对象启用权限继承：

  - Exchange 组织对象

  - Exchange 管理组对象

  - Exchange 服务器容器对象

  - Exchange 地址列表对象

  - Exchange 公用文件夹对象

  - Exchange 公用文件夹树对象

启用对这些对象权限的继承失败可能会导致邮件流问题、存储装入问题和其他服务中断问题。

若要解决此问题，请确保已为该对象启用\&quot;允许权限传播到此对象和子对象\&quot;设置，再重新运行 Exchange Server 2007 或 Exchange 2010安装程序。


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>使用 Exchange Server 2003 Exchange 系统管理器重新启用 Exchange 配置对象的权限继承的步骤</p></td>
</tr>
<tr class="even">
<td><ol>
<li><p>通过设置注册表参数，启用 Exchange 系统管理器的对象属性框的&amp;quot;安全&amp;quot;选项卡。</p>
<ol>
<li><p>启动注册表编辑器 (Regedt32.exe)。</p></li>
<li><p>找到注册表中的下列项：</p>
<p><strong>HKEY_CURRENT_USER\Software\Microsoft\Exchange\EXAdmin</strong></p></li>
<li><p>在&amp;quot;编辑&amp;quot;菜单上，单击&amp;quot;新建&amp;quot;，然后添加下列注册表值：</p>
<p><strong>值的名称</strong>︰ ShowSecurityPage</p>
<p><strong>数据类型</strong>︰ REG_DWORD</p>
<p><strong>基数</strong>︰ 二进制</p>
<p><strong>值</strong>︰ 1</p></li>
<li><p>退出注册表编辑器。</p></li>
</ol>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>默认情况下，此配置对象属性框的&amp;quot;安全&amp;quot;选项卡未启用。</td>
</tr>
</tbody>
</table>

</li>
<li><p>打开 Exchange 系统管理器，找到有问题的对象，右键单击该对象，并选择&amp;quot;属性&amp;quot;。</p></li>
<li><p>选择&amp;quot;安全&amp;quot;选项卡，再单击&amp;quot;高级&amp;quot;。</p></li>
<li><p>选择&amp;quot;允许可继承的权限从父对象传送到此对象和子对象&amp;quot;以重新启用权限继承。</p></li>
<li><p>重新启动 Exchange Server。</p></li>
</ol></td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Dd876845.Caution(EXCHG.150).gif" title="小心" alt="小心" />小心：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果不正确地修改 Active Directory 对象的属性，使用 ADSI 编辑，LDP 工具，或者另一个 LDAP 版本 3 客户端时，可能会导致严重的问题。这些问题可能要求您重新安装 Microsoft Windows Server™ 2003年和 / 或 Exchange Server。修改 Active Directory 对象属性需要您自担风险。</td>
</tr>
</tbody>
</table>



<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>使用 Exchange Server 2007 或 Exchange Server 2010 的 ADSIEdit 重新启用 Exchange 配置对象的权限继承的步骤</p></td>
</tr>
<tr class="even">
<td><ol>
<li><p>安装 ADSI Edit。</p></li>
<li><p>启动 ADSI 编辑。单击<strong>开始</strong>，单击<strong>运行</strong>，请在文本框中，键入<strong>adsiedit.msc</strong> ，然后单击确定。</p></li>
<li><p>导航到有问题的对象，右键单击对象，并选择&amp;quot;属性&amp;quot;。</p></li>
<li><p>选择&amp;quot;安全&amp;quot;选项卡，再单击&amp;quot;高级&amp;quot;。</p></li>
<li><p>选择&amp;quot;允许可继承的权限从父对象传送到此对象和子对象&amp;quot;以重新启用权限继承。</p></li>
<li><p>选择&amp;quot;确定&amp;quot;两次应用更改。</p></li>
<li><p>等待 Active Directory 复制，按照 Microsoft 知识库文章 232072&amp;quot;在 Active Directory 直接复制合作伙伴间启动复制&amp;quot;(<a href="http://go.microsoft.com/fwlink/?linkid=3052%26kbid=232072" class="uri">http://go.microsoft.com/fwlink/?linkid=3052&amp;kbid=232072</a>)（英文）中的指示传播更改或强制 Active Directory 复制。</p></li>
</ol></td>
</tr>
</tbody>
</table>

