---
title: '配置通过所订阅的边缘传输服务器的 Internet 邮件流: Exchange 2013 Help'
TOCTitle: 配置通过订阅的边缘传输服务器的 Internet 邮件流
ms:assetid: d12ea770-99ce-4ab4-a373-96f2554641fa
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb738158(v=EXCHG.150)
ms:contentKeyID: 61183395
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 配置通过所订阅的边缘传输服务器的 Internet 邮件流

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-04-08_

若要建立通过边缘传输服务器的 Internet 邮件，需要将边缘传输服务器订阅到 Active Directory 站点。此将会自动为 Internet 邮件流创建所需的两个发送连接器：

  - 一个配置为向所有 Internet 域发送出站电子邮件的发送连接器。

  - 一个配置为从边缘传输服务器向 Exchange 2013 邮箱服务器发送入站电子邮件的发送连接器。

如果不希望将边缘传输服务器订阅到 Active Directory 站点，则可以手动创建在邮箱服务器和边缘传输服务器之间建立邮件流所需的发送连接器。有关详细信息，请参阅[不使用 EdgeSync 的情况下通过边缘传输服务器配置 Internet 邮件流](configure-internet-mail-flow-through-an-edge-transport-server-without-using-edgesync-exchange-2013-help.md)。但是，我们建议只要可能就将边缘传输服务器订阅到 Active Directory 站点。

## 开始之前

  - 估计完成时间：20 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[邮件流权限](mail-flow-permissions-exchange-2013-help.md)主题中的“EdgeSync”条目和“边缘传输服务器”条目。

  - 在将边缘传输服务器订阅到您的组织前，首先需要为您的 Exchange 组织配置权威域和电子邮件地址策略。

  - 通过将您的外围网络与 Exchange 组织隔开的防火墙启用安全 LDAP 端口 50636/TCP。边缘传输服务器需要能够与订阅的 Active Directory 站点中的所有 Exchange 2013 邮箱服务器进行通信。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 配置通过所订阅的边缘传输服务器的 Internet 邮件流

1.  在边缘传输服务器上，使用以下语法创建边缘订阅文件。
    
    ```powershell
        New-EdgeSubscription -FileName <FileName>.xml [-Force]
    ```
    
    以下示例在文件夹 C:\\My Documents 中创建了名为“EdgeSubscriptionInfo.xml”的边缘订阅文件。*Force* 参数禁止确认边缘传输服务器上将禁用的命令以及配置数据将被覆盖的警告的提示。
    
    ```powershell
    New-EdgeSubscription -FileName "C:\My Documents\EdgeSubscriptionInfo.xml" -Force
    ```

2.  将生成的边缘订阅文件复制到您将边缘传输服务器订阅到的 Active Directory 站点中的邮箱服务器。

3.  在邮箱服务器上，使用以下语法导入边缘订阅文件。
    
    ```powershell
        New-EdgeSubscription -FileData ([byte[]]$(Get-Content -Path "<FileName>.xml" -Encoding Byte -ReadCount 0)) -Site <SiteName>
    ```
    
    此示例导入文件夹 D:\\Data 中名为“EdgeSubscriptionInfo.xml”的边缘订阅文件，并将边缘传输服务器订阅到名为“Default-First-Site-Name”的 Active Directory 站点。
    
    ```powershell
        New-EdgeSubscription -FileData ([byte[]]$(Get-Content -Path "D:\Data\EdgeSubscriptionInfo.xml" -Encoding Byte -ReadCount 0)) -Site "Default-First-Site-Name"
    ```
    
    > [!NOTE]  
    > 可以使用 <em>CreateInternetSendConnector</em> 或 <em>CreateInboundSendConnector</em> 参数阻止自动创建所需的一个或两个发送连接器。有关详细信息，请参阅<a href="edge-subscriptions-exchange-2013-help.md">边缘订阅</a>。


4.  在邮箱服务器上，运行以下命令，以开始第一次 EdgeSync 同步。
    
    ```powershell
    Start-EdgeSynchronization
    ```

5.  完成后，我们强烈建议将边缘订阅文件从边缘传输服务器和邮箱服务器中删除。边缘订阅文件包含在 LDAP 通信过程中使用的凭据的相关信息。

