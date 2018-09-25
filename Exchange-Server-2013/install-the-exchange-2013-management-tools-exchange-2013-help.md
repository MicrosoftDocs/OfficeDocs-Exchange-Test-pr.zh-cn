---
title: '安装 Exchange 2013 管理工具: Exchange 2013 Help'
TOCTitle: 安装 Exchange 2013 管理工具
ms:assetid: 71fcbe4c-783b-4f77-aabb-a21aa7a4ef23
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb232090(v=EXCHG.150)
ms:contentKeyID: 50556599
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 安装 Exchange 2013 管理工具

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2013-01-28_

使用 Microsoft Exchange Server 2013 管理工具，可以远程配置和管理 Exchange 组织。Exchange 2013 管理工具包括 Exchange 命令行管理程序和 Exchange 工具箱。本主题说明如何使用 Setup.exe 或无人参与安装模式安装 Exchange 2013 管理工具。

> [!NOTE]  
> 无需执行此过程就能远程使用 Exchange 管理中心 (EAC)。EAC 是一个基于 Web 的控制台，位于运行 Exchange 2013 客户端访问服务器角色的计算机上。有关远程访问 EAC 的详细信息，请参阅 <a href="exchange-admin-center-in-exchange-2013-exchange-2013-help.md">Exchange 2013 中的 Exchange 管理中心</a>。


有关管理 Exchange 2013 的详细信息，请参阅 [Exchange 2013 中的 Exchange 管理中心](exchange-admin-center-in-exchange-2013-exchange-2013-help.md)和 [将 PowerShell 与 Exchange 2013 结合使用 (Exchange Management Shell)](https://technet.microsoft.com/zh-cn/library/bb123778\(v=exchg.150\))。

## 在开始之前，您需要知道什么？

  - 估计完成时间：10 分钟

  - 确保在安装 Exchange 2013 之前阅读了发行说明。有关详细信息，请参阅 [Exchange 2013 发行说明](release-notes-for-exchange-2013-exchange-2013-help.md)。

  - 安装管理工具的计算机必须具有支持的操作系统（如 Windows Server 2012 或 Windows 8），具有足够磁盘空间，是 Active Directory 域的成员，并满足其他要求。有关系统要求的信息，请参阅 [Exchange 2013 系统要求](exchange-2013-system-requirements-exchange-2013-help.md)。

  - 若要运行 Exchange 2013 安装程序，必须安装 Microsoft .NET Framework 4.5、Windows Management Framework 3.0 和其他所需软件。若要了解所有服务器角色的先决条件，请参阅 [Exchange 2013 先决条件](exchange-2013-prerequisites-exchange-2013-help.md)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 使用安装程序安装 Exchange 2013 管理工具

1.  登录到要安装 Exchange 2013 的计算机。

2.  导航到 Exchange 2013 安装文件的网络位置。

3.  通过双击 `Setup.exe` 启动 Exchange 2013 安装程序
    
    > [!IMPORTANT]  
    > 如果启用了用户访问控制 (UAC)，则必须右键单击 <code>Setup.exe</code> 并选择“以管理员身份运行”。


4.  在“检查更新”页面，选择是否希望安装程序连接到 Internet 并下载 Exchange 2013 的产品和安全更新。如果您选择“连接到 Internet 并检查更新”，安装程序将下载更新，并在应用这些更新后继续。如果您选择“现在不检查更新”，您可在随后手动下载和安装更新。我们建议您现在下载并安装更新。单击“下一步”继续。

5.  “简介”页开始将 Exchange 安装到组织中的过程。它将引导您完成安装。这里列出几个有助于部署的链接。我们建议您在继续安装之前访问这些链接。单击“下一步”继续。

6.  在“许可协议”页上，查看软件许可条款。如果同意这些条款，请选择“我接受许可协议中的条款”，然后单击“下一步”。

7.  在“推荐设置”页面上，选择是否要使用建议设置。如果选择“使用建议设置”，Exchange 将自动将错误报告和有关您的计算机硬件以及如何使用 Exchange 的信息发送至 Microsoft。如果选择“不使用建议设置”，这些设置将保持禁用，但是可在设置完成后随时启用它们。有关这些设置以及如何使用发送至 Microsoft 的信息的详细信息，请单击 **?**。

8.  在“服务器角色选择”页上，验证是否选择了“管理工具”。
    
    选择“自动安装要安装 Exchange Server 所需的 Windows Server 角色和功能”让安装向导安装必需的 Windows 组件。您可能需要重新启动计算机以完成一些 Windows 功能的安装。如果不选择该选项，您必须手动安装 Windows 功能。
    
    > [!NOTE]  
    > 此选项仅安装 Exchange 所需的 Windows 功能。您必须手动安装其他必备组件。有关详细信息，请参阅 <a href="exchange-2013-prerequisites-exchange-2013-help.md">Exchange 2013 先决条件</a>。
    
    单击“下一步”继续。

9.  在“安装空间和位置”页上，或者接受默认安全位置，或者单击“浏览”选择新位置。确保您要安装 Exchange 的位置有足够磁盘空间。单击“下一步”继续。

10. 如果这是第一次在组织中运行 Exchange 2013 安装程序，请在“Exchange 组织”页中键入 Exchange 组织的名称。Exchange 组织名称只能包含下列字符：
    
      - A 到 Z
    
      - a 到 z
    
      - 0 到 9
    
      - 空格（不可用于开头或结尾）
    
      - 连字符或短横线
        
        > [!NOTE]  
        > 组织名称包含的字符不能超过 64 个。组织名称不能为空。
    
    如果您希望使用 Active Directory 拆分权限模型，选择“应用 Active Directory 拆分权限模型给 Exchange 组织”。
    
    > [!CAUTION]  
    > 大多数组织不需要应用 Active Directory 拆分权限模型。如果您需要分别管理 Active Directory 安全主体和 Exchange 配置，基于角色的访问控制 (RBAC) 拆分权限可能适合您。有关详细信息，请单击“?”。
    
    单击“下一步”继续。

11. 在“准备情况检查”页上，查看状态以确定是否成功完成了组织和服务器角色先决条件检查。如果未成功完成操作，则必须解决所有报告的错误，然后才能安装 Exchange 2013。解决某些先决条件错误时，不需要退出安装程序。解决报告的错误后，单击“返回”，然后单击“下一步”运行先决条件检查。此外，需保证对报告的所有警告进行查看。如果已成功所有准备情况检查，请单击“下一步”以安装 Exchange 2013。

12. 在“完成”页上，单击“完成”。

13. 在 Exchange 2013 完成之后重新启动计算机。

## 使用无人值守安装模式安装 Exchange 2013 管理工具

1.  登录到要安装 Exchange 2013 管理工具的计算机。

2.  导航到 Exchange 2013 安装文件的网络位置。

3.  在命令的提示符下，运行以下命令。
    
    > [!IMPORTANT]  
    > 如果您启用了用户访问控制 (UAC) 功能，必须从提升的命令提示符运行 <code>Setup.exe</code>。
    
    ```powershell
    Setup.exe /Role:ManagementTools /IAcceptExchangeServerLicenseTerms
    ```

有关详细信息，请参阅[使用无人参与的模式安装 Exchange 2013](install-exchange-2013-using-unattended-mode-exchange-2013-help.md)。

