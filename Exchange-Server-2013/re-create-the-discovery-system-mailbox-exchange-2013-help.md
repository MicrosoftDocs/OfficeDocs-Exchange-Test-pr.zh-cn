---
title: 'Re-create the Discovery system mailbox: Exchange 2013 Help'
TOCTitle: Re-create the Discovery system mailbox
ms:assetid: 5ae8426b-5661-4ecb-99c4-cdd342107fb1
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Gg588318(v=EXCHG.150)
ms:contentKeyID: 50490637
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Re-create the Discovery system mailbox

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2018-01-17_

就地电子数据展示使用系统邮箱存储就地电子数据展示搜索元数据。此发现系统邮箱的显示名为\&quot;SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9}\&quot;。由于系统邮箱在 Exchange 管理中心 (EAC) 中或在 Exchange 地址列表中不可见，因此很少会无意中将其删除。

但是，如果意外地删除了发现系统邮箱，则发现管理员将无法执行就地电子数据展示搜索或管理现有搜索。在这种情况下，要启用电子数据展示功能，必须重新创建发现系统邮箱。

## 在开始之前应了解的内容

  - 估计完成时间：10 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [收件人权限](recipients-permissions-exchange-2013-help.md)主题中的\&quot;收件人设置权限\&quot;部分。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

## 使用命令行管理程序重新创建发现系统邮箱

1.  如果 Active Directory 中存在 SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9} 用户帐户，则将其删除。默认情况下，Exchange Server 2013 安装程序在 Active Directory 的用户容器中创建邮箱。有关如何从 Active Directory 中删除用户帐户的详细信息，请参阅[删除用户帐户](https://go.microsoft.com/fwlink/p/?linkid=215850)。

2.  使用命令行管理程序启用发现系统邮箱。
    
    > [!NOTE]  
    > 无法使用 EAC 启用发现系统邮箱。
    > 下面的命令必须运行相同的目录中提取 Exchange 安装媒体的位置。
    
    若要重新创建搜索系统邮箱，请运行以下命令：
    
    ```powershell
.\Setup /preparead /IAcceptExchangeServerLicenseTerms
```

## 我如何知道这有效？

若要验证是否成功重新创建了发现系统邮箱，请将 **Get-Mailbox** cmdlet 与 *Arbitration* 开关结合使用来检索系统邮箱。查看该命令的结果以验证是否重新创建了系统邮箱 `SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9}`。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。

