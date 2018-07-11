---
title: '启用 Internet 日历发布: Exchange 2013 Help'
TOCTitle: 启用 Internet 日历发布
ms:assetid: b4c71696-52bb-492c-8259-0e419acd0bbc
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ853046(v=EXCHG.150)
ms:contentKeyID: 50556645
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 启用 Internet 日历发布

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2016-08-22_

**摘要：** 使用这些过程来启用 Exchange 2013 组织中的 OWA 用户来与外部组织共享日历的忙/闲信息。

Microsoft Exchange Server 2013 组织中的用户可以与非 Exchange 组织中的用户以及具有 Internet 访问权限的其他个人共享日历可用性（忙/闲）信息。Internet 日历发布提供了更好的灵活性并增加了可以共享日历可用性信息的用户的数量。

启用 Internet 日历发布包括三个常规步骤：

1.  为邮箱服务器配置 Web 代理 URL（只有组织中已存在 Web 代理 URL 时才需要执行这一步骤，否则，请跳到第 2 步）。

2.  启用客户端访问服务器的发布虚拟目录。

3.  专门为 Internet 日历发布创建一个共享策略，或者更新默认的共享策略以支持匿名域。任何一种方法都允许 Exchange 组织中的用户邀请具有 Internet 访问权限的其他用户通过访问发布的 URL 来查看有限的日历可用性信息。

> [!important]
> 完成第 3 步后，用户将需要从 Outlook 发布其日历。用户可将日历发布创建的 URL 提供给其组织外部人员。一个 URL 可使收件人使用 Outlook 或 Outlook Web App 来订阅日历，其他 URL 可使收件人在 Web 浏览器中查看日历。每个用户均可控制其他用户可看到的信息量。


有关与共享策略相关的其他管理任务，请参阅[共享策略](sharing-policies-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成该任务的时间：15 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[收件人权限](recipients-permissions-exchange-2013-help.md)主题中的“日历和共享权限”条目。

  - 共享用户的日历信息的 Exchange 组织中存在 Exchange 2013 客户端访问服务器。

  - 用户邮箱位于共享用户的日历信息的 Exchange 组织的 Exchange 2013 邮箱服务器上。

  - 只有 Outlook 2010 或更高版本以及 Outlook Web App 用户可创建共享邀请。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!tip]
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 您该如何做？

## 步骤 1：使用命令行管理程序配置 Web 代理 URL

> [!NOTE]
> 只有组织中已经存在 Web 代理 URL 时，才需要执行这一步骤。否则，请跳到步骤 2。
> 不能使用 Exchange 管理中心 (EAC) 配置 Web 代理 URL。


本示例在邮箱服务器 MAIL01 上配置 Web 代理 URL。

    Set-ExchangeServer -Identity "MAIL01" -InternetWebProxy "<Webproxy URL>"

有关语法和参数的详细信息，请参阅 [Set-ExchangeServer](https://technet.microsoft.com/zh-cn/library/bb123716\(v=exchg.150\))。

## 您如何知道此步骤有效？

若要验证是否成功配置了 Web 代理 URL，可运行以下命令行管理程序命令验证 *InternetWebProxy* 参数信息。

    Get-ExchangeServer | format-list

## 步骤 2：使用命令行管理程序启用发布虚拟目录

> [!NOTE]
> 不能使用 EAC 启用发布虚拟目录。


本示例在客户端访问服务器 CAS01 上启用发布虚拟目录。

    Set-OwaVirtualDirectory -Identity "CAS01\owa (Default Web Site)" -ExternalUrl "<URL for CAS01>" -CalendarEnabled $true

其中标识 `CAS01\owa (Default Web Site)` 是服务器名称和 Outlook Web App 虚拟目录。

有关语法和参数的详细信息，请参阅 [Set-OwaVirtualDirectory](https://technet.microsoft.com/zh-cn/library/bb123515\(v=exchg.150\))。

## 您如何知道此步骤有效？

若要验证是否成功启用了发布虚拟目录，可运行以下命令行管理程序命令验证 *ExternalURL* 参数信息。

    Get-OwaVirtualDirectory | format-list

## 步骤 3：专门为 Internet 日历发布创建或配置一个共享策略。

> [!NOTE]
> 第 3 步中的下列选项仅适用于 Exchange Online 环境。


可以选择为 Internet 日历发布创建共享策略（选项 1），或为 Internet 日历发布配置默认共享策略（选项 2）。借助这两个选项，可以选择使用 EAC 或 Shell。

## 选项 1：专门为 Internet 日历发布创建一个共享策略

如果要专门为 Internet 日历发布创建共享策略，请完成以下步骤。

## 使用 EAC

1.  导航到“组织”\>“共享”。

2.  在列表视图中的“单个共享”下，单击“新建”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。

3.  在“共享策略”中，在“策略名称”字段中为共享策略键入一个友好名称（例如 **Internet**）。

4.  单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标") 定义共享策略的共享规则。

5.  在“共享规则”中，单击“与特定域共享”，然后在对应的框中键入 **Anonymous**。

6.  若要指定要为共享策略强制实施的日历共享级别，可选择“共享日历文件夹”复选框，然后选择以下选项之一：
    
      - **仅包含时间的日历忙/闲信息**
    
      - **包含时间、主题和位置的日历忙/闲信息**
    
      - **所有日历约会信息，包括时间、主题、位置和标题**

7.  单击“保存”设置共享策略的规则。

8.  在“共享策略”中，单击“保存”以创建策略。

## 使用命令行管理程序

此示例创建一个名为 Internet 的 Internet 日历发布共享，并将此策略配置为仅共享可用性信息。已启用此策略。

    New-SharingPolicy -Name "Internet" -Domains 'Anonymous: CalendarSharingFreeBusySimple' -Enabled $true

本示例向用户邮箱添加共享策略 Internet。

    Set-Mailbox -Identity <user name> -SharingPolicy "Internet"

本示例向组织单位 (OU) 添加共享策略 Internet。

    Set-Mailbox -OrganizationalUnit <OU name> -SharingPolicy "Internet"

有关语法和参数的详细信息，请参阅 [New-SharingPolicy](https://technet.microsoft.com/zh-cn/library/dd298186\(v=exchg.150\)) 和 [Set-Mailbox](https://technet.microsoft.com/zh-cn/library/bb123981\(v=exchg.150\))。

## 您如何知道此步骤有效？

若要验证是否已经成功创建了共享策略，可运行以下命令行管理程序命令验证共享策略信息。

    Get-SharingPolicy <policy name> | format-list

## 选项 2：为 Internet 日历发布配置默认共享策略

如果要为 Internet 日历发布配置默认共享策略，请完成以下步骤。

## 使用 EAC

1.  导航到“组织” \>“分享”。

2.  在列表视图中的“单个共享”下，选择“默认共享策略”，然后单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在“共享策略”中，单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标") 将共享规则添加到策略中。

4.  在“共享规则”中，单击“与特定域共享”，然后在对应的框中键入 **Anonymous**。

5.  若要指定要为共享策略强制实施的日历共享级别，可选择“共享日历文件夹”复选框，然后选择以下选项之一：
    
      - **仅包含时间的日历忙/闲信息**
    
      - **包含时间、主题和位置的日历忙/闲信息**
    
      - **所有日历约会信息，包括时间、主题、位置和标题**

6.  单击“保存”设置共享策略的规则。

7.  在“共享策略”中，单击“保存”以保存策略。

## 使用命令行管理程序

此示例更新默认共享策略，并将该策略配置为仅共享可用性信息。已启用此策略。

    Set-SharingPolicy -Name "Default Sharing Policy" -Domains 'Anonymous: CalendarSharingFreeBusySimple' -Enabled $true

有关语法和参数的详细信息，请参阅 [Set-Mailbox](https://technet.microsoft.com/zh-cn/library/bb123981\(v=exchg.150\))。

## 您如何知道此步骤有效？

若要验证是否成功更新了默认共享策略，可运行以下命令行管理程序命令验证共享策略信息。

    Get-SharingPolicy <policy name> | format-list

