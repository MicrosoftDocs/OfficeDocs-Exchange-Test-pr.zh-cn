---
title: '设置 POP3 的连接超时限制: Exchange 2013 Help'
TOCTitle: 设置 POP3 的连接超时限制
ms:assetid: 40003115-be4e-4cf1-97b4-f5ca05b314dc
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa997604(v=EXCHG.150)
ms:contentKeyID: 50556555
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 设置 POP3 的连接超时限制

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2012-11-28_

您可以使用 EAC 或命令行管理程序为经过身份验证和未经身份验证的空闲 POP3 连接配置连接超时限制。

有关与 POP3 相关的其他信息，请参阅 [Exchange Server 2013 中的 POP3 和 IMAP4](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：5 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[客户端和移动设备权限](clients-and-mobile-devices-permissions-exchange-2013-help.md)主题中的“POP3 设置”条目。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 使用 EAC 为 POP3 设置连接超时限制

1.  在 EAC 中，导航到“服务器”**\>**“服务器”。

2.  在服务器列表中，选择客户端访问服务器，然后单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在服务器属性页面上，单击“POP3”。

4.  向下滚动并单击“更多选项”。

5.  在“超时设置”下，使用以下设置：
    
      - “身份验证超时(秒)”    指定在关闭经过身份验证的空闲连接之前等待的时间。默认值为 1,800。可能的值从 30 到 86,400。
    
      - “未经身份验证的超时(秒)”   指定在关闭未经身份验证的空闲连接之前等待的时间。默认值为 60。可能的值从 30 到 3,600。

6.  单击“应用”，然后单击“确定”保存您的更改。

为 POP3 设置连接超时限制后，您必须重新启动 POP3 服务，设置才能生效。 有关如何重新启动 POP3 服务的信息，请参阅[启动和停止 POP3 服务](start-and-stop-the-pop3-services-exchange-2013-help.md)。

## 使用命令行管理程序为 POP3 设置连接超时限制

此示例为经过身份验证的空闲连接设置连接超时限制。

```powershell
Set -PopSettings -Identity CAS01 -AuthenticatedConnectionTimeout TimeValue
```

此示例为未经身份验证的空闲连接设置连接超时限制。

```powershell
Set -PopSettings -Identity CAS01 -PreAuthenticatedConnectionTimeout TimeValue
```

为 POP3 设置连接超时限制后，您必须重新启动 POP3 服务，设置才能生效。 有关如何重新启动 POP3 服务的信息，请参阅[启动和停止 POP3 服务](start-and-stop-the-pop3-services-exchange-2013-help.md)。

有关语法和参数的详细信息，请参阅[Set-PopSettings](https://technet.microsoft.com/zh-cn/library/aa997154\(v=exchg.150\))。

## 您如何知道这有效？

要验证是否成功设置了连接限制，请执行以下操作之一：

1.  在 EAC 中，导航到“服务器”**\>**“服务器”。

2.  在服务器列表中，选择客户端访问服务器，然后单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在服务器属性页面上，单击“POP3”。

4.  向下滚动并单击“更多选项”。

5.  在“超时设置”下，验证连接设置是否正确。

或

1.  在命令行管理程序中运行以下命令。
    
    ```powershell
Get-PopSettings | format-list
```

2.  验证连接设置是否正确。

## 详细信息

为 POP3 设置连接超时限制后，您可能还希望：

[在 Exchange 2013 中启用 POP3](enable-pop3-in-exchange-2013-exchange-2013-help.md)

[设置 POP3 的连接限制](set-connection-limits-for-pop3-exchange-2013-help.md)

