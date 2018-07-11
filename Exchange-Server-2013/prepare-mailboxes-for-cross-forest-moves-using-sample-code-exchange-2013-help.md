---
title: '使用示例代码准备跨林移动的邮箱: Exchange 2013 Help'
TOCTitle: 使用示例代码准备跨林移动的邮箱
ms:assetid: f35ac7a5-bb84-4653-b6d0-65906e93627b
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Ee861124(v=EXCHG.150)
ms:contentKeyID: 50491975
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 使用示例代码准备跨林移动的邮箱

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2016-12-09_

Microsoft Exchange 2013 支持使用 **New-MoveRequest** 和 **New-MigrationBatch** cmdlet 进行邮箱移动和迁移。您还可以通过 Exchange 管理中心 (EAC) 移动邮箱。可以将邮箱从源 Exchange 林移到目标 Exchange 2010 林中。

若要运行 **New-MoveRequest**，邮件用户必须在目标 Exchange 林中存在且必须拥有所需 Active Directory 属性的最小集。您可以通过自定义您的 Microsoft Identity Lifecycle Manager (ILM) 2007 部署在目标 Exchange 林中创建所需的邮件用户。本主题中所述的基于 ILM 的规则扩展示例代码说明了如何自定义您的当前 ILM，以在目标 Exchange 2013 林中创建所需的启用邮件用户。

有关准备跨林移动的详细信息，包括必需 Active Directory 属性的介绍，请参阅[为跨林移动请求准备邮箱](prepare-mailboxes-for-cross-forest-move-requests-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 请从 Microsoft 下载中心中的[准备联机邮箱移动](https://go.microsoft.com/fwlink/p/?linkid=177882) 页下载示例代码。

  - 若要运行示例代码，需要 ILM 2007 Feature Pack 1 Service Pack 1 (SP1)。若要下载该 Feature Pack，请参阅 Microsoft 知识库文章 977791，[Identity Lifecycle Manager 2007 Feature Pack 1 中提供了 Service Pack 1（内部版本 3.3.1139.2）](http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=977791)。

  - 还需要注意以下各项：
    
      - 运行邮箱当前所在的 Exchange 2013 的源林。
    
      - 安装了 Exchange 2013 的目标林，这是邮箱将要移动到的位置。

  - 要连接 Exchange 2013 目标林，您必须拥有相应的权限以调用 **UpdateRecipient** cmdlet。若要查看您需要哪些权限，请参阅 [收件人权限](recipients-permissions-exchange-2013-help.md) 主题中的"收件人资源调配权限"部分。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 您该如何做？

## 步骤 1：安装 ILM 示例代码

1.  在 Microsoft Visual Studio 2008 中，打开 Microsoft.Exchange.Sample.OneWayGALSync.sln 查看示例代码。该示例代码包括以下内容：
    
      - Microsoft.MetadirectoryServicesEx.dll 是 ILM 2007 FP1 SP1 随附的一个二进制文件，在“\\Program Files\\Microsoft Identity Integration Server\\Bin\\Assemblies”下。它由示例代码引用。
    
      - OneWaySync.xml，由示例代码引用。
    
      - “ILMServerConfig”文件夹中包含源管理代理 (MA)、目标 MA 以及 ILM Metaverse (MV) 的 ILM 配置文件。
    
      - Microsoft.Exchange.Sample.OneWayGALSync.MARules.dll 和 Microsoft.Exchange.Sample.OneWayGALSync.MVRules.dll（从示例代码生成），在“\\obj\\Debug”下

2.  在 ILM 服务器上，将以下内容复制到 \\Program Files\\Microsoft Identity Integration Server\\Extensions：
    
      - OneWaySync.xml
    
      - Microsoft.Exchange.Sample.OneWayGALSync.MARules.dll
    
      - Microsoft.Exchange.Sample.OneWayGALSync.MVRules.dll

3.  编辑在步骤 1 中复制到 ILM Extensions 文件夹的文件 OneWaySync.xml，以便在要创建邮件用户的目标 Exchange 林中指定 TargetOU 容器的 distinguishedName (DN)。如果您不知道 TargetOU 容器的名称，则可以使用 LDP.exe 或 ADSIEdit.exe 以浏览找到 TargetOU 容器。
    
    > [!NOTE]  
    > 如果正在与 ILM GalSync 2007 一同使用此示例，则请将此容器排除在 GalSync2007 托管的容器列表之外。


4.  在 ILM 标识管理器控制台上，转至“文件”\>“导入服务器配置”，以从文件夹“ILMServerConfig”导入 ILM 服务器配置。此操作导入 Metaverse 架构和设置规则的同时还将导入两个 Active Directory 管理代理。
    
    > [!NOTE]  
    > 在导入期间，必须提供林名称和凭据，并将导入的 Active Directory 管理代理 (ADMA) 的分区与配置中的源 ADMA 和目标 ADMA 的分区名称相匹配。


5.  为使 ADMA 支持 Exchange 2013 目标林，请在“创建管理代理”页面的“配置扩展”窗格上，选择“设置”下拉列表中的“Exchange 2013”，然后在“Exchange 2013 RPS URI”中输入 Exchange 2010 客户端访问服务器的远程 Windows PowerShell URI。
    
    **创建管理代理页**
    
    ![Exchange 2010 管理代理设置](images/Aa998597.8f403cda-e5e4-4edf-887f-c1ed46cee3f5(EXCHG.150).gif "Exchange 2010 管理代理设置")  

6.  在 ILM 标识管理器控制台上的“创建管理代理”窗格上，打开源林管理代理的“属性”。选择“配置目录分区”向导，然后单击“容器”以选择将包含要移动到目标林的邮箱的容器。清除对所有其他容器的选择，即将管理代理限制为仅管理这一个容器。同样，对于目标林 MA，请选择已启用邮件的用户将设置到的容器，即在第 2 步中指定的 TargetOU。
    
    > [!NOTE]  
    > 如果将此示例与 ILM GalSync 2007 一同使用，则请将这些容器都排除在 GalSync 2007 托管的容器的列表之外。


7.  在目标 MA 上执行初始完全导入（仅阶段），以便 ILM 可以发现在第 2 步中指定的 TargetOU。

## 步骤 2：在目标 Exchange 林中创建邮件用户

现在，您已安装示例代码，请使用以下步骤在目标 Exchange 林中创建必需邮件用户，以便可以运行 **New-MoveRequest** 以执行联机邮箱移动。

1.  在源数据林中，使用 Exchange 管理中心在通过第 4 步“安装 ILM 示例代码”中选择的容器中创建邮箱用户。您也可以使用 Active Directory 用户和计算机移动现有邮箱用户至容器。

2.  在源 MA 上执行增量导入和增量同步，以发现添加到源容器的邮箱，并为目标 MA 设置邮件用户。

3.  在目标 MA 上执行导出，以便将在第 1 步中设置的邮件用户导出到目标 Active Directory。

4.  在目标 MA 上执行增量导入以确认在第 2 步中导出的更改。

5.  在目标林中，打开 Exchange 命令行管理程序并使用 **New-MoveRequest** cmdlet 从源林移动邮箱。

## 您如何知道这有效？

要验证您是否已成功完成迁移，请执行下列操作：

  - 在目标林中，验证已从源数据林中移出的用户是否已经在目标林中。

