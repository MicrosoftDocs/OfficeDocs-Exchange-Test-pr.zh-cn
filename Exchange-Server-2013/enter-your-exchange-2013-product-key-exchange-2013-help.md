---
title: '输入您的 Exchange 2013 产品密钥: Exchange 2013 Help'
TOCTitle: 输入您的 Exchange 2013 产品密钥
ms:assetid: ccb14685-4bdc-42a4-a985-35cd2a1a415c
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb124582(v=EXCHG.150)
ms:contentKeyID: 51408264
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Servers.EnterProductKeyWizardForm.EnterProductKeyWizardPage
ms.translationtype: HT
---

# 输入您的 Exchange 2013 产品密钥

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2016-12-09_

产品密钥告知 Exchange Server 2013 您已经购买了标准版或企业版的许可证。如果您购买的产品密钥是一个企业版的许可证，它除了可以提供标准版许可证所能提供的一切之外，还允许您每台服务器上安装超过五个数据库。如果您想了解有关 Exchange 许可的详细信息，请参阅 [Exchange 2013：版次和版本](exchange-2013-editions-and-versions-exchange-2013-help.md)。

如果您不输入产品密钥，您的服务器就会自动许可为试用版。试用版功能与 Exchange 标准版相同，如果您想在购买之前试用 Exchange，或在实验室中运行检测，它会很有帮助。唯一的区别就是，您对许可为试用版的 Exchange 服务器的试用期只有 180 天。如果您想使服务器的使用天数超过 180 天，就需要输入产品密钥，否则 Exchange 管理中心 (EAC) 将提醒您需要输入产品密钥才能使服务器获得许可证。

> [!TIP]  
> 我们已经注意到此页面的访问用户在查找关于如何安装或激活 Office 的信息。如果您是其中之一，请查看这些页面：
> <ul>
> <li><p><a href="http://go.microsoft.com/fwlink/p/?linkid=403360">安装 Office</a></p></li>
> <li><p><a href="http://go.microsoft.com/fwlink/p/?linkid=403361">需要关于您的 Office 产品密钥的帮助?</a></p></li>
> </ul>
> 如果您想要在 Exchange 2010 服务器上输入产品密钥，请转到<a href="http://go.microsoft.com/fwlink/p/?linkid=403370">输入 Exchange 2010 产品密钥</a>。<br />
> 如果您想要在 Exchange 2013 服务器上输入产品密钥，您就来对了地方！请继续阅读。


## 在开始之前，您需要知道什么？

  - 估计完成该过程的时间：不超过 5 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[Exchange 和命令行管理程序基础结构权限](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md)主题中的“产品密钥”条目。

  - 如果您正在许可运行邮件服务器角色的 Exchange 服务器，在您输入产品密钥之后，将需要重启服务器上的 Microsoft Exchange 信息存储服务。

  - 如果您希望将 Exchange 服务器从标准版许可证升级为企业版许可证，请遵循本主题中的步骤。

  - 如果您希望将 Exchange 服务器从企业版许可证降级为标准版许可证，您需要重新安装 Exchange。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 您想执行什么操作？

## 使用 EAC 输入产品密钥

1.  浏览到 https://\<*客户端访问服务器的名称*\>/ecp，打开 EAC。

2.  在“域名\\用户名”和“密码”中输入用户名和密码，然后单击“登录”。

3.  转到“服务器”\>“服务器”。选择要认证的连接器，然后单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

4.  （可选）如果要将服务器从标准版许可证升级到企业版许可证，请在“常规”页面上选择“更改产品密钥”。如果服务器已获得许可，您将只会看到此选项。

5.  在“常规”页面上的“输入有效密钥”文本框中输入产品密钥。

6.  单击“保存”。

7.  如果您许可了运行邮箱服务器角色的 Exchange 服务器，请采取以下步骤重启 Microsoft Exchange 信息存储服务：
    
    1.  打开“控制面板”，转到“管理工具”，然后打开“服务”。
    
    2.  右键单击“Microsoft Exchange 信息存储”，然后单击“重新启动”。

## 使用命令行管理程序输入产品密钥

本示例将使用 **set-ExchangeServer** cmdlet 输入产品密钥。

> [!NOTE]  
> 可以在同一服务器上再次执行该命令，将其从标准版许可证升级到企业版许可证。


```powershell
Set-ExchangeServer ExServer01 -ProductKey aaaaa-aaaaa-aaaaa-aaaaa-aaaaa
```

有关语法和参数的详细信息，请参阅 [Set-ExchangeServer](https://technet.microsoft.com/zh-cn/library/bb123716\(v=exchg.150\))。

如果您许可了运行邮箱服务器角色的 Exchange 服务器，请采取以下步骤重启 Microsoft Exchange 信息存储服务：

1.  打开“控制面板”，转到“管理工具”，然后打开“服务”。

2.  右键单击“Microsoft Exchange Information Store”，然后单击“重新启动”。

## 您如何知道操作成功？

要使用 EAC 验证是否已成功将服务器许可为标准版或企业版，请执行以下操作：

1.  在“域名\\用户名”和“密码”中输入用户名和密码，然后单击“登录”。

2.  转到“服务器”\>“服务器”。

3.  选择要查看的服务器，然后查看服务器详细信息窗格。如果已接受该产品密钥，“已认证”将与 Exchange 2013 版本一起显示。

要使用命令行管理程序验证是否已成功将服务器许可为标准版或企业版，请执行以下操作：

1.  打开命令行管理程序。

2.  运行以下命令，查看特定 Exchange 服务器的许可状态。
    
        Get-ExchangeServer ExServer01 | Format-Table Edition,*Trial*

3.  （可选）运行以下命令，查看组织中所有 Exchange 服务器的许可状态。
    
        Get-ExchangeServer | Format-Table Name, Edition, *Trial* -Auto

