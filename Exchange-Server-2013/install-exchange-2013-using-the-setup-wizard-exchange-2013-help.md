---
title: '使用安装向导安装 Exchange 2013: Exchange 2013 Help'
TOCTitle: 使用安装向导安装 Exchange 2013
ms:assetid: da690d47-3384-4430-a69e-0cd4d3bf80a7
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb124778(v=EXCHG.150)
ms:contentKeyID: 50491664
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.ExSetupUI.SetupWizardForm.IntroductionPage
ms.translationtype: HT
---

# 使用安装向导安装 Exchange 2013

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2014-06-19_

本主题介绍如何使用 Microsoft Exchange Server 2013 安装向导将 Exchange 2013 邮箱和客户端访问角色安装在计算机上。有关规划和部署 Exchange 2013 的详细信息，请参阅[规划和部署](planning-and-deployment-for-exchange-2013-installation-instructions.md)。

如果您想将 Exchange 2013 边缘传输角色安装在计算机上，请参阅[使用安装向导安装 Exchange 2013 边缘传输角色](install-the-exchange-2013-edge-transport-role-using-the-setup-wizard-exchange-2013-help.md)。边缘传输角色不能安装在与邮箱或客户端访问服务器角色相同的计算机上。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>你是否曾听说过 Exchange Server 部署助理？它是一款免费的联机工具，它将询问您一些问题并专门为您创建自定义部署检查表，以帮助您在组织中快速部署 Exchange 2013。若您想要了解关于它的详细信息，请转到 <a href="exchange-server-deployment-assistant-exchange-2013-help.md">Exchange Server 部署助理</a>。</td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在运行 Exchange 2013 的计算机上安装了任意服务器角色之后，不能再使用 Exchange 2013 安装向导为该计算机添加其他服务器角色。如果希望为计算机添加其他服务器角色，则必须使用“控制面板”中的“添加或删除程序”或在命令提示符窗口中使用 Setup.exe。</td>
</tr>
</tbody>
</table>


有关安装之后要完成的任务的信息，请参阅 [Exchange 2013 安装后任务](exchange-2013-post-installation-tasks-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：60 分钟

  - 确保在安装 Exchange 2013 之前阅读了发行说明。有关详细信息，请参阅[Exchange 2013 发行说明](release-notes-for-exchange-2013-exchange-2013-help.md)。

  - 每个组织在 Active Directory 林中都需要至少一台客户端访问服务器和一台邮箱服务器。另外，每个包含邮箱服务器的 Active Directory 站点还必须包含至少一台客户端访问服务器。如果您要分隔服务器角色，我们建议您先安装邮箱服务器角色。

  - 安装了 Exchange 2013 的计算机必须使用受支持的操作系统（如 Windows Server 2008 R2 Service Pack 1 (SP1) 或 Windows Server 2012），具有足够的磁盘空间，是 Active Directory 域的成员，并且满足其他要求。有关系统要求的信息，请参阅 [Exchange 2013 系统要求](exchange-2013-system-requirements-exchange-2013-help.md)。

  - 要运行 Exchange 2013 安装，您必须安装 Microsoft .NET Framework 4.5、Windows Management Framework 3.0 以及所需的其他软件。若要了解所有服务器角色的先决条件，请参阅 [Exchange 2013 先决条件](exchange-2013-prerequisites-exchange-2013-help.md)。

  - 如果未提前准备 Active Directory 架构，则必须确保您使用的帐户已委派有 Schema Admins 组的成员身份。如果要在组织中安装第一台 Exchange 2013 服务器，您使用的帐户必须拥有 Enterprise Admins 组成员身份。如果已经准备好架构，但不是要在组织中安装第一台 Exchange 2013 服务器，则您使用的帐户必须是 Exchange 2013 组织管理角色组的成员。
    
    作为委派安装角色组成员的管理员可以部署“组织管理”管理角色组成员之前已经设置过的 Exchange 2013 服务器。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876845.Caution(EXCHG.150).gif" title="小心" alt="小心" />小心：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在服务器上安装 Exchange 之后，不得更改服务器名称。不支持在安装了 Exchange 服务器角色之后重命名服务器。</td>
</tr>
</tbody>
</table>


## 安装 Exchange Server 2013

如果要在组织中安装第一台 Exchange 2013 服务器，并且尚未执行 Active Directory 准备步骤，则您使用的帐户必须拥有企业管理员组成员身份。如果您之前没有准备 Active Directory 架构，则帐户也必须拥有 Schema Admins 组成员身份。有关为 Exchange 2013 准备 Active Directory 的信息，请参阅[准备 Active Directory 和域](prepare-active-directory-and-domains-exchange-2013-help.md)。如果您已经执行了架构和 Active Directory 准备步骤，则您使用的帐户必须是“委派安装”管理角色组或“组织管理”角色组的成员。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>若要下载 Exchange 2013 的最新版本，请参阅 <a href="updates-for-exchange-2013-exchange-2013-help.md">Exchange 2013 更新</a>。</td>
</tr>
</tbody>
</table>


1.  登录到要安装 Exchange 2013 的计算机。

2.  导航到 Exchange 2013 安装文件的网络位置。

3.  通过双击 `Setup.exe` 启动 Exchange 2013 安装程序
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果启用了用户访问控制 (UAC)，则必须右键单击 <code>Setup.exe</code> 并选择“以管理员身份运行”。</td>
    </tr>
    </tbody>
    </table>


4.  在“检查更新？”页面，选择是否希望安装程序连接到 Internet 并下载 Exchange 2013 的产品和安全更新。如果您选择“连接到 Internet 并检查更新”，安装程序将下载更新，并在应用这些更新后继续。如果您选择“现在不检查更新”，您可在随后手动下载和安装更新。我们建议您现在下载并安装更新。单击“下一步”继续。

5.  
    
    “简介”页开始将 Exchange 安装到组织中的过程。它将引导您完成安装。这里列出几个有助于部署的链接。我们建议您在继续安装之前访问这些链接。单击“下一步”继续。

6.  
    
    在“许可协议”页上，查看软件许可条款。如果同意这些条款，请选择“我接受许可协议中的条款”，然后单击“下一步”。

7.  
    
    在“推荐设置”页面上，选择是否要使用建议设置。如果选择“使用建议设置”，Exchange 将自动将错误报告和有关您的计算机硬件以及如何使用 Exchange 的信息发送至 Microsoft。如果选择“不使用建议设置”，这些设置将保持禁用，但是可在设置完成后随时启用它们。有关这些设置以及如何使用发送至 Microsoft 的信息的详细信息，请单击 **?**。

8.  
    
    在“服务器角色选择”页上，选择是否要在该计算机上安装“邮箱角色”、“客户端访问角色”、这两个角色或仅“管理工具”。如果选择不在此安装期间安装其他服务器角色，可以稍后再添加它们。组织必须至少装有一个邮箱角色和至少一个客户端访问服务器角色。它们可以安装在同一台计算机或不同计算机上。如果安装任何服务器角色，将自动安装管理工具。
    
    选择“自动安装要安装 Exchange Server 所需的 Windows Server 角色和功能”让安装向导安装必需的 Windows 组件。您可能需要重新启动计算机以完成一些 Windows 功能的安装。如果不选择该选项，您必须手动安装 Windows 功能。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>此选项仅安装 Exchange 所需的 Windows 功能。您必须手动安装其他必备组件。有关详细信息，请参阅<a href="exchange-2013-prerequisites-exchange-2013-help.md">Exchange 2013 先决条件</a>。</td>
    </tr>
    </tbody>
    </table>
    
    单击“下一步”继续。

9.  在“安装空间和位置”页上，或者接受默认安全位置，或者单击“浏览”选择新位置。确保您要安装 Exchange 的位置有足够磁盘空间。单击“下一步”继续。

10. 
    
    如果这是组织中的第一台 Exchange 服务器，请在“Exchange 组织”页中键入 Exchange 组织的名称。Exchange 组织名称只能包含下列字符：
    
      - A 到 Z
    
      - a 到 z
    
      - 0 到 9
    
      - 空格（不可用于开头或结尾）
    
      - 连字符或短横线
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>组织名称包含的字符不能超过 64 个。组织名称不能为空。</td>
        </tr>
        </tbody>
        </table>
    
    如果您希望使用 Active Directory 拆分权限模型，选择“将 Active Directory 拆分权限安全模型应用到 Exchange 组织”。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Dd876845.Caution(EXCHG.150).gif" title="小心" alt="小心" />小心：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>大多数组织不需要应用 Active Directory 拆分权限模型。如果您需要分别管理 Active Directory 安全主体和 Exchange 配置，基于角色的访问控制 (RBAC) 拆分权限可能适合您。有关详细信息，请单击“?”。</td>
    </tr>
    </tbody>
    </table>
    
    单击“下一步”继续。

11. 如果安装邮箱角色，在“恶意软件保护设置”页上，选择您是否要启用或禁用恶意软件扫描。如果您禁用恶意软件扫描，可在未来启用它。单击“下一步”继续。

12. 
    
    在“准备情况检查”页上，查看状态以确定是否成功完成了组织和服务器角色先决条件检查。如果未成功完成操作，则必须解决所有报告的错误，然后才能安装 Exchange 2013。解决某些先决条件错误时，不需要退出安装程序。解决报告的错误后，单击“返回”，然后单击“下一步”运行先决条件检查。此外，请务必检查报告的所有警告。如果已成功所有准备情况检查，请单击“下一步”以安装 Exchange 2013。

13. 
    
    在“完成”页上，单击“完成”。

14. 在 Exchange 2013 完成之后重新启动计算机。

15. 通过执行 [Exchange 2013 安装后任务](exchange-2013-post-installation-tasks-exchange-2013-help.md) 中提供的任务完成部署。

## 您如何知道这有效？

要验证是否成功安装 Exchange 2013，请参阅[验证 Exchange 2013 安装](verify-an-exchange-2013-installation-exchange-2013-help.md)。

遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

您找到所需内容了吗？请花一点时间[向我们发送反馈](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedbac)，告诉我们您希望找到的信息。

