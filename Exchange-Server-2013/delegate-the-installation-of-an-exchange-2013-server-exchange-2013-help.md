---
title: '委派 Exchange 2013 服务器安装: Exchange 2013 Help'
TOCTitle: 委派 Exchange 2013 服务器安装
ms:assetid: f2fc8680-0c7c-4a29-b8f5-d77404fec280
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb201741(v=EXCHG.150)
ms:contentKeyID: 62614010
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 委派 Exchange 2013 服务器安装

 

_**适用于：** Exchange Online, Exchange Server, Exchange Server 2013_

_**上一次修改主题：** 2014-07-31_

Exchange Server 2013 使您可以将 Exchange 服务器安装委派给不属于 Exchange 2013 组织管理角色组的人员。这有利于安装和设置服务器的人员与管理服务的人员不是同一人的大型公司（如 Exchange）。如果这听起来正是您要做的事情，则本主题对您很适用。

通常情况下，当安装 Exchange 时，安装人员需要是 [组织管理](organization-management-exchange-2013-help.md) 角色组的成员。因为当安装 Exchange 时，将更改 Active Directory，且只有属于组织管理角色组的 Exchange 管理员才可以进行这些更改。以下列表显示了所做的更改：

  - 在 **CN=Servers,CN=Exchange Administrative Group (FYDIBOHF23SPDLT),CN=Administrative Groups,CN=\<组织名称\>,CN=Microsoft Exchange,CN=Services,CN=Configuration,DC=\<根域\>** 配置分区中创建服务器对象。

  - 将以下访问控制条目 (ACE) 添加到“委派安装”角色组配置分区内的服务器对象：
    
      - 对服务器对象及其子对象的完全控制权
    
      - 代理发送扩展权限的拒绝访问控制条目
    
      - “代理接收”扩展权限的“拒绝”访问控制条目
    
      - 拒绝对 Exchange 公用文件夹存储对象的 CreateChild 和 DeleteChild 权限。
    
    > [!NOTE]  
    > 公用文件夹在组织级别中进行管理；因此，只有 Exchange 管理员可以创建和删除公用文件夹存储。


  - 将服务器的 Active Directory 计算机帐户添加到 Exchange 服务器组。

  - 将此服务器添加为 Exchange 管理中心内已设置的服务器。

在大型公司中，安装和设置新服务器的人员通常不是 Exchange 管理员。为使他们可以安装 Exchange，Exchange 管理员可以*配置*Active Directory 中的服务器。当配置服务器时，对于 Active Directory，新 Exchange 服务器运行所需的所有更改与计算机上 Exchange 的实际安装分开进行。在新计算机上安装 Exchange 前，Exchange 管理员可以在数小时甚至数天内在 Active Directory 中配置一个新服务器。配置服务器后，安装人员需要仅作为[委派安装](delegated-setup-exchange-2013-help.md)角色组成员安装 Exchange。“委派安装”角色组仅允许成员安装配置的服务器。

在思考如何使用委派安装程序时，请牢记以下事项：

  - 可委派其他服务器的安装之前，至少已安装一个 Exchange 2013 服务器。安装第一台服务器的人员必须是 Exchange 管理员。有关详细信息，请查看[检查表：执行 Exchange 2013 的新安装](checklist-perform-a-new-installation-of-exchange-2013-exchange-2013-help.md)。

  - 委派的用户无法卸载 Exchange 服务器。若要卸载 Exchange 服务器，您需要是 Exchange 管理员。

## 如何配置 Exchange 2013 服务器？

若要为 Exchange 配置服务器，您需要使用 Exchange 2013 命令行安装程序。如果您不是非常熟悉 Windows 命令提示，请不要担心。此主题可以引导您正确执行所需操作。在开始之前，应记住以下几个注意事项：

  - 您需要是组织管理角色组的成员才能配置服务器。

  - 您应该有最新版本的 Exchange 2013。您可以从 [Exchange 2013 更新](updates-for-exchange-2013-exchange-2013-help.md)获得下载链接。

配置服务器所需使用的命令取决于您是正在要配置的计算机上运行安装程序还是正在另一台计算机上运行安装程序。在以下步骤中选择与运行安装程序位置匹配的命令：

1.  按 Windows 键 +“R”以打开“运行”窗口。

2.  在“打开”中，键入 **cmd.exe**，然后按“Enter”打开“Windows 命令提示符”。

3.  将目录改到下载并展开 Exchange 2013 安装文件的位置。如果安装文件位于 `C:\Downloads\Exchange 2013` 中，则使用以下命令。
    
    ```powershell
    CD "C:\Downloads\Exchange 2013"
    ```

4.  选择与要运行安装程序的位置相匹配的命令：
    
      - **如果您正在配置的计算机上运行安装程序**，则运行以下命令：
        
        ```powershell
        Setup.exe /NewProvisionedServer /IAcceptExchangeServerLicenseTerms
        ```
    
      - **如果您正在另一台计算机上运行安装程序**，则运行以下命令：
        
        ```powershell
        Setup.exe /NewProvisionedServer:<ComputerName> /IAcceptExchangeServerLicenseTerms
        ```

5.  配置服务器后，需确保已将可以在配置的服务器上安装 Exchange 的用户添加到“委派安装”角色组。若要了解如何将用户添加到角色组，请参阅[Add members to a role group](manage-role-group-members-exchange-2013-help.md)。

完成这些步骤后，计算机就可以对 Exchange 进行安装。通过使用[使用安装向导安装 Exchange 2013](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md) 中的步骤在已配置的服务器上安装 Exchange 2013。

## 我如何知道这有效？

若要确保服务器针对 Exchange 进行了正确配置，您可以执行以下操作：

1.  转到“启动”\>“管理工具”，然后打开“Active Directory 用户和计算机”。

2.  选择“Microsoft Exchange 安全组”，双击“Exchange 服务器”，然后选择“成员”选项卡。

3.  在“成员”选项卡上，查看刚刚配置的服务器是否已列为安全组成员。

如果您的服务器已列为 Exchange 服务器安全组的成员，则配置正确。“委派安装”角色组的成员现在可以在该服务器上安装 Exchange。

遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

您找到所需内容了吗？请花一点时间[向我们发送反馈](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedbac)，告诉我们您希望找到的信息。

