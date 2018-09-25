---
title: '创建共享策略: Exchange 2013 Help'
TOCTitle: 创建共享策略
ms:assetid: cae8cab0-6265-448b-8add-5202cdb20678
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ657494(v=EXCHG.150)
ms:contentKeyID: 50491697
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 创建共享策略

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-04-07_

您可以使用共享策略控制 Exchange 组织中的用户与组织外的用户共享日历信息的方式。共享策略允许与不同类型的外部用户进行用户建立的、人对人的日历信息共享。这些策略支持与外部联合组织（如 Office 365 或其他本地 Exchange 组织）、外部非联合组织以及可以访问 Internet 的个人共享日历信息。若要将特定的共享策略应用于用户，请参阅[将共享策略应用于邮箱](apply-a-sharing-policy-to-mailboxes-exchange-2013-help.md)。

> [!IMPORTANT]  
> 创建共享策略是在 Exchange 组织中设置联合共享的若干步骤之一。首先需要建立与本地 Exchange 组织的 Azure Active Directory 身份验证系统的联合身份验证信任，然后才能与其他联合 Exchange 组织共享日历信息。Internet 共享策略不需要联合身份验证信任。


若要了解有关联合共享的详细信息，请参阅[共享](sharing-exchange-2013-help.md)。

有关联合身份验证的更多管理任务，请参阅[联合程序](federation-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：15 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[收件人权限](recipients-permissions-exchange-2013-help.md)主题中的“日历和共享权限”部分。

  - 联盟 Exchange 组织之间的共享策略需要满足以下要求：
    
      - 每个 Exchange 组织中都存在一个 Exchange 2013 客户端访问服务器。在 Exchange 组织之间也支持共享策略，其中一个组织拥有 Exchange 2013 客户端访问服务器，而另一个组织拥有 Exchange 2010 SP3 或更高版本的客户端访问服务器。
    
      - 每个 Exchange 组织都已创建了与 Azure AD 身份验证系统的联合身份验证信任。有关详细信息，请参阅[配置联合身份验证信任](configure-a-federation-trust-exchange-2013-help.md)。
    
      - 每个 Exchange 组织都配置了联盟组织标识符。用于生成用户的电子邮件地址的域已添加到组织标识符中。
    
      - 用户邮箱位于每个 Exchange 组织的 Exchange 2013 邮箱服务器或 Exchange 2010 邮箱服务器上。
    
      - 只有 Outlook 2010 或更高版本以及 Outlook Web App 用户可创建共享邀请。

  - 与非联盟 Exchange 组织或个人之间的共享策略需要满足以下要求：
    
      - 共享用户的日历信息的 Exchange 组织中存在 Exchange 2013 客户端访问服务器。
    
      - 用户邮箱位于共享用户的日历信息的 Exchange 组织的 Exchange 2013 邮箱服务器上。
    
      - 必须启用 Exchange 2013 客户端访问服务器以进行 Outlook Web App 访问。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

## 您想执行什么操作？

## 使用 EAC 创建共享策略

1.  导航到“组织”\>“共享”。

2.  在列表视图中的“单个共享”下，单击“新建”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。

3.  在“新建共享策略”中，在“策略名称”框中为共享策略键入一个友好名称。

4.  单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标") 指定共享策略的共享规则。

5.  在“共享规则”中，选择以下选项之一以指定要共享的域：
    
      - **与所有域共享**
    
      - **与特定域共享**

6.  如果选择了“与特定域共享”，请键入要共享的域的名称。如果需要为此共享策略输入多个域，请保存第一个域的设置，然后编辑共享规则，以添加更多的域。

7.  若要定义要为共享策略强制实施的日历共享级别，可选择“共享日历文件夹”复选框，然后选择以下选项之一：
    
      - **仅包含时间的日历忙/闲信息**
    
      - **包含时间、主题和位置的日历忙/闲信息**
    
      - **所有日历约会信息，包括时间、主题、位置和标题**

8.  单击“保存”设置共享策略的规则。

9.  如果希望将该共享策略作为您 Exchange 组织中用户的默认共享策略，可选择“将该策略作为我的默认共享策略”复选框。

10. 单击“保存”创建共享策略。

## 使用 EAC 以允许所有用户共享完整的日历详细信息

您可以编辑默认的共享策略，以允许您的所有用户与组织外的用户共享完整日历详细信息。

1.  导航到“组织”\>“共享”。

2.  在列表视图中的“单个共享”下，选择“默认共享策略”，然后单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在“共享策略”对话框中，选择“与所有域共享”，然后单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

4.  在“共享规则”对话框的“指定要共享的信息”下，选择“所有日历约会信息，包括时间、主题、位置和标题”，然后单击“保存”。

5.  在“共享策略”对话框中，单击“保存”设置共享策略的规则。

## 使用命令行管理程序创建共享策略

  - 本示例为外部联盟域 contoso.com 创建共享策略 Contoso。该策略允许 contoso.com 域中的用户查看用户的详细日历可用性（忙/闲）信息。默认情况下，启用此策略。
    
    ```powershell
      New-SharingPolicy -Name "Contoso" -Domains contoso.com: CalendarSharingFreeBusyDetail
    ```

  - 本示例将使用为每个域配置的不同的共享操作为两个不同的联盟域（contoso.com 和 woodgrovebank.com）创建共享策略 ContosoWoodgrove。已启用此策略。
    
    ```powershell
      New-SharingPolicy -Name "ContosoWoodgrove" -Domains 'contoso.com: CalendarSharingFreeBusySimple', 'woodgrovebank.com: CalendarSharingFreeBusyDetail -Enabled $false
    ```

  - 本示例将使用为有限的日历可用性信息配置的共享操作为具有客户端访问服务器 CAS01 和邮箱服务器 MAIL01 的 Exchange 组织创建共享策略匿名。此策略允许 Exchange 组织中的用户通过向其他用户发送一个链接来邀请这些用户进行 Internet 访问以查看其日历可用性信息。已启用此策略。
    
    1.  设置 MAIL01 的 Web 代理 URL。
        
        ```powershell
          Set-ExchangeServer -Identity "Mail01" -InternetWebProxy "<Webproxy URL>"
        ```
    
    2.  启用 CAS01 上的发布虚拟目录。
        
        ```powershell
            Set-OwaVirtualDirectory -Identity "CAS01" -ExternalURL "<URL for CAS01>" -CalendarPublishingEnabled $true
        ```

    3.  创建共享策略匿名和配置有限的日历信息共享。
        
        ```powershell
            New-SharingPolicy -Name "Anonymous" -Domains 'Anonymous: CalendarSharingFreeBusySimple' -Enabled $true
        ```

有关语法和参数的详细信息，请参阅下列主题：

  - [New-SharingPolicy](https://technet.microsoft.com/zh-cn/library/dd298186\(v=exchg.150\))

  - [Set-ExchangeServer](https://technet.microsoft.com/zh-cn/library/bb123716\(v=exchg.150\))

  - [Set-OwaVirtualDirectory](https://technet.microsoft.com/zh-cn/library/bb123515\(v=exchg.150\))

## 您如何知道这有效？

若要验证是否已经成功创建了共享策略，可运行以下命令行管理程序命令验证共享策略信息。

```powershell
  Get-SharingPolicy <policy name> | format-list
```

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。

