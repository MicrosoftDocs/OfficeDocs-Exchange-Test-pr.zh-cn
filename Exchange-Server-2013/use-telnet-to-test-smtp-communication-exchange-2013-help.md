---
title: '使用 Telnet 测试 SMTP 通信: Exchange 2013 Help'
TOCTitle: 使用 Telnet 测试 SMTP 通信
ms:assetid: 8a5f6715-baa4-48dd-8600-02c6b3d1aa9d
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb123686(v=EXCHG.150)
ms:contentKeyID: 52061527
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 使用 Telnet 测试 SMTP 通信

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2016-12-09_

本主题展示了如何使用 Telnet 测试邮件服务器之间的简单邮件传输协议 (SMTP) 通信。默认情况下，SMTP 侦听端口 25。如果在端口 25 上使用 Telnet，则可以输入用于连接 SMTP 服务器和发送邮件的 SMTP 命令，如同 Telnet 会话是 SMTP 邮件服务器一样。还可以查看连接和邮件提交过程中每个步骤成功与否。

下面说明了使用 Telnet 测试到或来自  Microsoft Exchange 组织中存在的传输服务器的 SMTP 通信的方案。

  - 从位于外围网络之外的主机连接到组织的面向 Internet 的 Exchange 服务器，并发送一封测试邮件。

  - 从组织的面向 Internet 的 Exchange 服务器连接到远程邮件服务器，并发送一封测试邮件。

本主题展示了如何使用 Microsoft Windows 附带的组件 Telnet 客户端。第三方 Telnet 客户端可能需要使用与 Windows Telnet 组件不同的语法。

## 在开始之前，您需要知道什么？

  - 估计完成时间：30 分钟

  - Exchange 权限不适用于本主题介绍的过程。这些过程是在 Exchange Server 或客户端计算机的操作系统中执行。

  - 本主题中介绍的过程最适用于与允许匿名连接的面向 Internet 的服务器进行连接。内部 Exchange 服务器间的邮件传输是经过加密和身份验证的。若要使用 Telnet 连接邮箱服务器上的集线器传输服务，需要创建一个接收连接器，并将其配置为允许匿名访问或基本身份验证，然后才能接收邮件。如果连接器允许基本身份验证，需要使用一个实用工具将用户名和密码的文本字符串转换成 Base64 格式。由于使用基本身份验证时，用户名和密码非常容易辨别，因此不建议在未加密情况下使用基本身份验证。

  - 如果连接远程邮件服务器，请考虑在面向 Internet 的 Exchange 服务器上执行本主题中介绍的过程。这有助于避免配置为验证源 IP 地址、相应域名系统 (DNS) 的域名以及试图向服务器发送邮件的所有 Internet 主机的反向查找 IP 地址的远程邮件服务器拒绝测试邮件。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 您该如何做？

## 第 1 步：在 Windows 中安装 Telnet 客户端

默认情况下，Telnet 客户端没有安装在大多数客户端或服务器版本的 Microsoft Windows 操作系统。若要安装此更新，请参阅[安装 Telnet 客户端](https://go.microsoft.com/fwlink/p/?linkid=179054)。

## 第 2 步：使用 Nslookup 在远程 SMTP 服务器的 MX 记录中查找 FQDN 或 IP 地址

若要在端口 25 上使用 Telnet 连接目标 SMTP 服务器，必须使用 SMTP 服务器的完全限定的域名 (FQDN) 或 IP 地址。如果 FQDN 或 IP 地址未知，查找此信息的最简便方法是使用 Nslookup 命令行工具查找目标域的 MX 记录。

1.  在命令提示符处，键入 **nslookup**，然后按 Enter。此命令将打开 Nslookup 会话。

2.  键入 **set type=mx** 并按 Enter 键。

3.  键入 **set timeout=20**，然后按 Enter。默认情况下，Windows DNS 服务器具有 15 秒的递归 DNS 查询超时限制。

4.  键入要查找其 MX 记录的域名。例如，若要查找 fabrikam.com 域的 MX 记录，请键入 **fabrikam.com.**，然后按 Enter。
    
    > [!NOTE]  
    > 尾随句点 (<strong>.</strong>) 表示 FQDN。使用尾随句点可防止无意中将为网络配置的默认 DNS 后缀添加到域名中。
    
    输出的命令将与以下内容类似：
    
        fabrikam.com mx preference=10, mail exchanger = mail1.fabrikam.com
        fabrikam.com mx preference=20, mail exchanger = mail2.fabrikam.com
        mail1.fabrikam.com internet address = 192.168.1.10
        mail2 fabrikam.com internet address = 192.168.1.20
    
    可以将与 MX 记录关联的任何主机名或 IP 地址用作目标 SMTP 服务器。较低的首选项值表示首选 SMTP 服务器。可以使用多个 MX 记录和不同的首选项值，以实现负载平衡和容错。

5.  准备结束 Nslookup 会话时，请键入 **exit** 并按 Enter 键。

> [!NOTE]  
> 组织的内部网络规定的防火墙或 Internet 代理限制可能会阻止您使用 Nslookup 工具查询 Internet 上的公用 DNS 服务器。


## 第 3 步：在端口 25 上使用 Telnet 测试 SMTP 通信

在此示例中，使用下列值：

  - **目标 SMTP 服务器**   mail1.fabrikam.com

  - **源域**   contoso.com

  - **发件人的电子邮件地址**   chris@contoso.com

  - **收件人的电子邮件地址**   kate@fabrikam.com

  - **邮件主题**   来自 Contoso 的测试

  - **邮件正文**   这是一封测试邮件

> [!NOTE]  
> <ul>
> <li><p>Telnet 客户端中的命令不区分大小写。为清楚起见，SMTP 命令动词均使用大写。</p></li>
> <li><p>在 Telnet 会话中连接目标 SMTP 服务器后，无法使用 Backspace 键。如果在键入 SMTP 命令时出错，必须按 ENTER，然后重新键入命令。无法识别的 SMTP 命令或语法错误会导致生成如下错误消息：</p>
> <pre><code>500 5.3.3 Unrecognized command</code></pre></li>
> </ul>


1.  在命令提示符处，键入 **telnet**，然后按 Enter。此命令将打开 Telnet 会话。

2.  键入 **set localecho**，然后按 Enter。借助此可选命令，可以一边键入字符，一边查看这些字符。对于某些 SMTP 服务器，可能必须这样设置。

3.  键入 **set logfile** *\<filename\>*。此可选命令可以将 Telnet 会话记录到指定的日志文件中。如果仅指定了文件名，日志文件的位置将是当前工作目录。如果指定了路径和文件名，路径必须位于计算机本地。指定的路径和文件名都必须以 Microsoft DOS 8.3 格式输入。指定的路径必须已存在。如果你指定了不存在的日志文件，系统会为你创建一个。

4.  键入 **open mail1.fabrikam.com 25** 并按 Enter 键。

5.  键入 **EHLO contoso.com** 并按 Enter 键。

6.  键入 **MAIL FROM:chris&#64;contoso.com** 并按 Enter 键。

7.  键入 **RCPT TO:kate&#64;fabrikam.com NOTIFY=success,failure**，然后按 Enter。可选的 NOTIFY 命令可定义目标 SMTP 服务器必须向发件人提供的特定传递状态通知 (DSN) 邮件。RFC 1891 中定义了 DSN 邮件。此示例是要请求获取有关邮件传递成功与否的 DSN 邮件。

8.  键入 **DATA**，然后按 Enter。响应如下：
    
    ```powershell
354 Start mail input; end with <CLRF>.<CLRF>
```

9.  键入 **主题：来自 Contoso 的测试**，然后按 Enter。

10. 按 Enter。RFC 2822 要求在 `Subject:` 头字段和邮件正文间留一个空白行。

11. 键入 **这是一封测试邮件**，再按 ENTER 键。

12. 按 Enter，键入句点 (**.**)，然后按 Enter。响应如下：
    
    ```powershell
250 2.6.0 <GUID> Queued mail for delivery
```

13. 若要与目标 SMTP 服务器断开连接，请键入 **QUIT**，然后按 Enter。响应如下：
    
    ```powershell
221 2.0.0 Service closing transmission channel
```

14. 若要关闭 Telnet 会话，请键入 **quit** 并按 Enter 键。

## 第 4 步：评估 Telnet 会话的结果

针对以上示例中所使用的以下命令，本节提供有关这些命令响应的信息：

  - 打开 mail1.fabrikam.com 25

  - EHLO contoso.com

  - MAIL FROM:chris@contoso.com

  - RCPT TO:kate@fabrikam.com NOTIFY=success,failure
    
    > [!NOTE]  
    > RFC 2821 中定义的 3 位数 SMTP 响应代码对所有 SMTP 邮件服务器都一样。对于某些 SMTP 邮件服务器，文本说明可能略有不同。


## 打开 mail1.fabrikam.com 25

**成功响应：**  `220 mail1.fabrikam.com Microsoft ESMTP MAIL Service ready at <day-date-time>`

**失败响应：**  `Connecting to mail1.fabrikam.com...Could not open connection to the host, on port 25: Connect failed`

**失败的可能原因**

  - 目标 SMTP 服务不可用。

  - 对目标防火墙有所限制。

  - 对源防火墙有所限制。

  - 指定的目标 SMTP 服务器的 FQDN 或 IP 地址不正确。

  - 指定的端口号不正确。

## EHLO contoso.com

**成功响应：**  `250 mail1.fabrikam.com Hello [<sourceIPaddress>]`

**失败响应：**  `501 5.5.4 Invalid domain name`

**失败的可能原因**   域名中存在无效字符。或者，目标 SMTP 服务器上有连接限制。

> [!NOTE]  
> EHLO 是 RFC 2821 中定义的已扩展简单邮件传输协议 (ESMTP) 命令动词。ESMTP 服务器可在初始连接时公布其功能。这些功能包括其可接受的邮件大小上限，以及支持的身份验证方法。HELO 是 RFC 821 中定义的旧版 SMTP 命令动词。大多数 SMTP 邮件服务器都支持 ESMTP 和 EHLO。


## MAIL FROM:chris@contoso.com

**成功响应：**  `250 2.1.0 Sender OK`

**失败响应：**  `550 5.1.7 Invalid address`

**可能的失败原因：** 发件人的电子邮件地址中存在语法错误。

**失败响应：**  `530 5.7.1 Client was not authenticated`

**失败的可能原因**   目标服务器不接受匿名邮件提交。如果试图使用 Telnet 直接向集线器传输服务器提交邮件，则会看到此错误消息。

## RCPT TO:kate@fabrikam.com NOTIFY=success,failure

**成功响应：**  `250 2.1.5 Recipient OK`

**失败响应：**  `550 5.1.1 User unknown`

**可能的失败原因**   指定的收件人在组织中不存在。

