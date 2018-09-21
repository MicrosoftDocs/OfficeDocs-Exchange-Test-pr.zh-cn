---
title: '配置用户邮箱位于 Exchange 2013 服务器上的旧版公用文件夹: Exchange 2013 Help'
TOCTitle: 配置用户邮箱位于 Exchange 2013 服务器上的旧版公用文件夹
ms:assetid: 1d5ca19e-696e-4054-a634-15dd34d952b7
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dn690134(v=EXCHG.150)
ms:contentKeyID: 62281154
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 配置用户邮箱位于 Exchange 2013 服务器上的旧版公用文件夹

 

_**适用于：** Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2017-03-27_

如何启用 Exchange 2013 或交换 2016年用户访问 Exchange 2010 或更早的公用文件夹 （也称为旧版公用文件夹）。

## 在开始之前，您需要知道什么？

其邮箱位于 Exchange Server 2013年或 Exchange Server 2016年的用户将不能访问旧式公用文件夹从 Outlook Web App、 Outlook web 上的或 Outlook 的 mac。这篇文章中的步骤适用于 Exchange 2013 和交换 2016年。

> [!NOTE]  
> 请按照本文中的步骤后，Mac 用户的 outlook 2016 可以访问旧式的公用文件夹。如果您的组织中的客户端的 Mac 使用 Outlook 2016，请确保他们安装 4 月 2016年更新。否则，这些用户将不能访问共存或混合拓扑中的公用文件夹。有关详细信息，请参阅<a href="accessing-public-folders-with-outlook-2016-for-mac-exchange-2013-help.md">通过 Outlook 2016 for Mac 访问公用文件夹</a>。


## 步骤 1：使 Exchange 2010 公用文件夹可发现

1.  如果 Exchange 2010 或更高版本的服务器上有自己的公用文件夹，则需要有一个公用文件夹数据库的所有邮箱服务器上安装客户端访问服务器角色。这允许 Microsoft Exchange RpcClientAccess 服务处于运行状态，从而允许所有客户端访问公用文件夹。客户端访问角色并不是必需的 Exchange 2007 公用文件夹服务器，和此步骤不是必需。有关详细信息，请参阅[安装 Exchange Server 2010年](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md)。
    
    > [!NOTE]  
    > 客户端负载平衡不需要包含此服务器。有关详细信息，请参阅<a href="https://technet.microsoft.com/zh-cn/library/ff625247(v=exchg.141).aspx">了解 Exchange 2010 中的负载平衡</a>。


2.  在每个公用文件夹服务器上创建一个空的邮箱数据库。
    
    对于 Exchange 2010，运行以下命令。此命令会将邮箱数据库从邮箱配置负载平衡器中排除。这样可以阻止新建邮箱被自动添加至该数据库。
    
        New-MailboxDatabase -Server <PFServerName_with_CASRole> -Name <NewMDBforPFs> -IsExcludedFromProvisioning $true 
    
    对于 Exchange 2007，运行以下命令：
    
    ```powershell
New-MailboxDatabase -StorageGroup "<PFServerName>\StorageGroup>" -Name <NewMDBforPFs>
```
    
    > [!NOTE]  
    > 我们建议您只将在步骤 3 中创建的代理邮箱添加至此数据库。不应在此邮箱数据库中创建任何其他邮箱。


3.  在新建邮箱数据库内创建一个代理邮箱，并在通讯簿中将其隐藏。该邮箱的 SMTP 会由自动发现返回为 *DefaultPublicFolderMailbox* SMTP，因此通过解析此 SMTP，客户端可以进入旧版 Exchange 服务器以访问公用文件夹。
    ```
        New-Mailbox -Name <PFMailbox1> -Database <NewMDBforPFs> 
    ```
    ```
    ```powershell
Set-Mailbox -Identity <PFMailbox1> -HiddenFromAddressListsEnabled $true
```
    ```
    
4.  对于 Exchange 2010，启用自动发现以返回代理公用文件夹邮箱。此步骤对于 Exchange 2007 并非必需步骤。
    
    ```powershell
Set-MailboxDatabase <NewMDBforPFs> -RPCClientAccessServer <PFServerName_with_CASRole>
```

5.  对组织中的每个公用文件夹服务器重复执行前面的步骤。

## 步骤 2：将用户邮箱配置为访问旧版公用文件夹

此过程中的最后一步是配置用户邮箱以允许访问旧版内部部署公用文件夹。

使 Exchange Server 2013 内部部署用户可以访问旧版公用文件夹。您可以指向在[Step 2: Make remote public folders discoverable](configure-legacy-on-premises-public-folders-for-a-hybrid-deployment-exchange-2013-help.md)中创建的所有代理公用文件夹邮箱。从具有 CU5 或更高版本更新的 Exchange 2013 服务器运行以下命令。

    Set-OrganizationConfig -PublicFoldersEnabled Remote -RemotePublicFolderMailboxes ProxyMailbox1,ProxyMailbox2,ProxyMailbox3

> [!NOTE]  
> 您必须等待 ActiveDirectory 同步完成才能查看更改。此进程可能需要几个小时。


## 我如何知道这有效？

对于邮箱位于 Exchange Server 2013 CU5 或更高版本服务器上的用户，登录到 Outlook 并执行以下公用文件夹测试：

1.  确保 Outlook 客户端正在运行。

2.  按住 CTRL 键，在 Windows 任务栏右侧的通知区域中右键单击 Outlook 图标。

3.  选择\&quot;测试电子邮件自动配置…\&quot;

4.  确保\&quot;测试电子邮件自动配置\&quot;工具在 XML 选项卡中返回以下信息：
    
      - \<PublicFolderInformation\>
    
      - \<SmtpAddress\>\<公用文件夹邮箱的 SMTP 地址\</SmtpAddress\>
    
      - \</PublicFolderInformation\>

5.  在 Outlook 客户端中，执行以下任务：
    
      - 查看公用文件夹层次结构。
    
      - 检查权限。
    
      - 创建和删除公用文件夹。
    
      - 发布内容到公用文件夹并从公用文件夹删除内容。

