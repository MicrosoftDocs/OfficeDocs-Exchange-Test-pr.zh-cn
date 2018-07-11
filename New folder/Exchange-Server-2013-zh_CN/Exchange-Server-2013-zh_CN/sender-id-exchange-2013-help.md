---
title: '发件人 ID: Exchange 2013 Help'
TOCTitle: 发件人 ID
ms:assetid: 0f628f83-df8c-43fb-bf49-7aaa9ec69ab1
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa996295(v=EXCHG.150)
ms:contentKeyID: 50489919
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 发件人 ID

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2016-12-09_

发件人 ID 代理是 Microsoft Exchange Server 2013 中提供的反垃圾邮件代理。发件人 ID 代理依赖于所收到的 SMTP 标头和对发送系统的 DNS 服务的查询，确定要对入站邮件执行的操作（如果有）。

发件人 ID 主要用于阻止冒充发件人和域的行为，该行为通常称为\&quot;电子欺骗\&quot;*。\&quot;欺骗邮件\&quot;*是指发送地址已被修改的电子邮件，该邮件看起来发自某个发件人，但此发件人并不是实际的发件人。

欺骗邮件通常包含一个\&quot;发件人:\&quot;地址，声称来自某个组织。过去，在 SMTP 会话（如 MAIL FROM:头）和 RFC 2822 邮件数据（如 From:"Masato Kawai" masato@contoso.com）中欺骗\&quot;发件人:\&quot;地址都相对较为容易，这是因为系统不会对邮件头进行验证。

**目录**

Using Sender ID to combat spoofing

Updating your organization's Internet-facing DNS to support Sender ID

Specifying recipients and sender domains to exclude from Sender ID filtering

## 使用发件人 ID 防止欺骗

发件人 ID 将使欺骗更加难以实施。启用发件人 ID 时，每个邮件都将在邮件的元数据中包含发件人 ID 状态。接收电子邮件时，Exchange 服务器将查询发件人的 DNS 服务器，以验证发送邮件的 IP 地址是否得到授权可针对邮件头中所指定的域发送邮件。有权发送邮件的服务器的 IP 地址称为假设负责地址 (PRA)。

域管理员发布其 DNS 服务器上的发件人策略框架 (SPF) 记录。SPF 记录标识授权的出站电子邮件服务器。如果发件人的 DNS 服务器上配置的 SPF 记录中，Exchange 服务器将分析 SPF 记录并确定从中接收消息的 IP 地址是否已被授权代表消息中指定的域发送电子邮件。SPF 记录所包含的内容以及如何创建的 SPF 记录有关的详细信息，请参阅[发件人 ID](https://go.microsoft.com/fwlink/p/?linkid=50977)。

Exchange 服务器将根据 SPF 记录来更新含有发件人 ID 状态的邮件元数据。Exchange 服务器更新邮件元数据之后，邮件传递将以常见方式进行。

## 发件人 ID 状态值

发件人 ID 评估过程会为邮件生成发件人 ID 状态。发件人 ID 状态用于评估邮件的垃圾邮件可信度 (SCL) 分级。此状态可以设置为下列值之一：

  - **Pass**   IP 地址和假设负责地址 (PRA) 都通过了发件人 ID 验证检查。

  - **Neutral**   发布的发件人 ID 数据明显不具有决定性。

  - **Soft fail**   PRA 的 IP 地址可能在禁止的集合内。

  - **Fail**   IP 地址不允许使用；在传入邮件中未找到任何 PRA，或发件人域不存在。

  - **None**   发件人的 DNS 中没有任何已发布的 SPF 数据。

  - **TempError** 出现临时 DNS 失败，例如 DNS 服务器不可用。

  - **PermError**   DNS 记录无效，例如，记录格式错误。

发件人 ID 状态将被添加到邮件元数据中，稍后将被转换为 MAPI 属性。在生成 SCL 值期间，Microsoft Outlook 中的垃圾邮件筛选器将使用该 MAPI 属性。

Outlook 既不显示发件人 ID 状态，也不一定会以特定发件人 ID 值将邮件标记为垃圾邮件。Outlook 只在计算 SCL 值期间才使用发件人 ID 状态值。

除了七种生成发件人 ID 状态的情况以外，发件人 ID 评估过程还可能会显示\&quot;发件人:\&quot;IP 地址丢失的情形。如果\&quot;发件人:\&quot;IP 地址丢失，则无法设置发件人 ID 状态。如果无法设置发件人 ID 状态，则 Exchange 将继续处理邮件，但不在邮件中包括发件人 ID 状态。该邮件不会被放弃或拒绝。在此方案中，将不设置发件人 ID 状态，会在日志中记录一个应用程序事件。

有关发件人 ID 状态在邮件中的显示方式的详细信息，请参阅[反垃圾邮件标记](anti-spam-stamps-exchange-2013-help.md)。

## 用于处理欺骗邮件和无法访问的 DNS 服务器的发件人 ID 选项

还可以定义 Exchange 服务器如何处理被标识为欺骗邮件的邮件，以及当无法访问 DNS 服务器时，Exchange 服务器将如何处理邮件。Exchange 服务器如何处理欺骗邮件和无法访问的 DNS 服务器的选项包括下列操作：

  - **标记状态**   此选项是默认操作。进入组织的所有入站邮件都具有包括在邮件元数据中的发件人 ID 状态。

  - **拒绝**   此选项将拒绝邮件，并向发送方服务器发送 SMTP 错误响应。SMTP 错误响应是 5*xx* 级协议响应，其文本对应于发件人 ID 状态。

  - **删除**   此选项将删除邮件，但不会将此删除操作通知给发送系统。实际上，Exchange 服务器将向发送服务器发送假的\&quot;OK\&quot;SMTP 命令，然后删除该邮件。由于发送服务器认为邮件已发送，因此不会在相同会话中再次尝试发送该邮件。

有关如何配置发件人 ID 代理的详细信息，请参阅[管理发件人 ID](manage-sender-id-exchange-2013-help.md)。

返回顶部

## 更新组织中面向 Internet 的 DNS 以支持发件人 ID

发件人 ID 的有效性取决于特定的 DNS 数据。使用 SPF 记录更新面向 Internet 的 DNS 服务器的组织越多，发件人 ID 识别欺骗电子邮件的能力就越强。

支持发件人 ID 基础结构，您必须通过创建 SPF 记录和承载公共 DNS 服务器上的 SPF 记录更新您的面向 Internet 的 DNS 数据。有关如何创建和部署 SPF 记录的详细信息，请参阅[发件人 ID](https://go.microsoft.com/fwlink/p/?linkid=50977)。

返回顶部

## 将收件人域和发件人域指定为排除在发件人 ID 筛选之外

您可能想要将指定的收件人域和发件人域排除在发件人 ID 筛选之外。为此，请在 Exchange 命令行管理程序中使用 **Set-SenderIdConfig** cmdlet 指定收件人域和发件人域。有关详细信息，请参阅 [Set-SenderIdConfig](https://technet.microsoft.com/zh-cn/library/aa998859\(v=exchg.150\))。

返回顶部

