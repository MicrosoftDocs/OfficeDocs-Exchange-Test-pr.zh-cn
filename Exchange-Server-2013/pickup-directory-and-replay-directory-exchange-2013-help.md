---
title: '拾取目录和重播目录: Exchange 2013 Help'
TOCTitle: 拾取目录和重播目录
ms:assetid: ae191700-953f-411c-906f-dc90feec3d5a
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb124230(v=EXCHG.150)
ms:contentKeyID: 50491298
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 拾取目录和重播目录

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2016-12-09_

默认情况下，分拣目录和重播目录存在于每台 Microsoft Exchange Server 2013 邮箱服务器或边缘传输服务器上。复制到分拣目录或重播目录中的格式正确的电子邮件文件将被提交以进行传递。分拣目录可以由管理员使用来测试邮件流，也可以由必须创建并提交各自的邮件的应用程序使用。重播目录不仅可从外部网关服务器接收邮件，也可用于重新提交管理员从 Exchange 服务器队列导出的邮件。

**目录**

电子邮件文件解析

分拣目录和重播目录如何处理邮件

分拣目录邮件文件要求

分拣目录邮件头修改

重播目录邮件文件要求

重播目录邮件头修改

分拣目录和重播目录邮件处理失败

分拣目录和重播目录的安全注意事项

分拣目录和重播目录的权限

## 电子邮件文件解析

标准 SMTP 电子邮件由*邮件信封*和邮件内容组成。邮件信封包含传输和传递邮件所需的信息。邮件内容包含邮件头字段（统称为“邮件头”）和邮件正文。RFC 2821 中规定了邮件信封，而 RFC 2822 中规定了邮件头。

发件人撰写电子邮件并将其提交以进行传递时，该邮件包含符合 SMTP 标准所需的基本信息，例如发件人、收件人、邮件撰写日期和时间、主题行（可选）以及邮件正文（可选）。此信息包含在邮件自身中，根据定义，也包含在邮件头中。

发件人的邮件服务器使用邮件头中的发件人信息和收件人信息为邮件生成邮件信封，并将邮件传输到 Internet 以传递到收件人的邮件服务器。收件人从不会看到邮件信封，因为它是由邮件传输进程生成的，实际上并不是邮件的一部分。

每个参与邮件传输的服务器可能会将与传递邮件的服务器角色有关的邮件头字段或其他应用程序特定的邮件头字段插入邮件头。收件人使用电子邮件客户端打开邮件时，电子邮件客户端会将邮件头中比较相关的信息部分（例如发件人、收件人和主题）与邮件正文一起显示。

返回顶部

## 分拣目录和重播目录如何处理邮件

在 Exchange 2013 中，分拣目录默认位于 `%ExchangeInstallPath%TransportRoles\Pickup`。重播目录默认位于 `%ExchangeInstallPath%TransportRoles\Replay`。复制到分拣目录或重播目录中的格式正确的 .eml 邮件文件将按照下列步骤进行处理以供提交：

1.  每 5 秒钟将检查一次分拣目录和重播目录中的新邮件文件。无法修改此轮询间隔。可以使用 **Set-TransportService** cmdlet 的 *PickupDirectoryMaxMessagesPerMinute* 参数调整邮件文件的处理速度。此参数会影响分拣目录和重播目录。默认值为每分钟 100 封邮件。无法打开的文件将保留在分拣目录中，并将在下一次轮询中重新对其进行评估。

2.  将检查对分拣目录中的邮件文件设定的限制，如邮件头最大大小和最大收件人数。默认情况下，邮件头的最大大小为 64 KB，最大收件人数为 100。可以使用 **Set-TransportService** cmdlet 更改这些限制。这些设置只影响分拣目录。

3.  文件由 *\<filename\>*.eml 重命名为 *\<filename\>*.tmp。如果 *\<filename\>*.tmp 文件已存在，则文件将重命名为 *\<filename\>\<datetime\>*.tmp。如果文件重命名失败，则将生成事件日志错误，分拣进程将继续处理下一个文件。

4.  成功地将 .tmp 文件转换为电子邮件之后，系统将向 .tmp 文件发出一个**delete on close**命令。.tmp 文件显示为仍位于分拣目录，但是无法打开该文件。

5.  邮件成功地进入传递队列之后，系统将发出**close**命令，.tmp 文件将会从分拣目录中删除。如果删除失败，将生成事件日志错误。如果分拣目录中存在 .tmp 文件时重新启动 Microsoft Exchange 传输服务，则所有的 .tmp 文件将重命名为 .eml 文件，并将被重新处理。这可能会导致邮件重复传输。

返回顶部

## 分拣目录邮件文件要求

复制到分拣目录中的邮件文件必须满足下列要求才能成功地进行传递：

  - 邮件文件必须是符合基本 SMTP 邮件格式的文本文件。支持 MIME 邮件头字段和内容。

  - 邮件文件的文件扩展名必须是 .eml。

  - 在邮件头的 `Sender` 或 `From` 邮件头字段中必须至少存在一个电子邮件地址。如果在 `Sender` 和 `From` 字段中各存在一个电子邮件地址，则 `From` 字段中的电子邮件地址将在邮件信封中用作邮件的原始发件人。

  - `Sender` 字段中只能存在一个电子邮件地址。不允许存在多个电子邮件地址。如果 `From` 字段中只存在一个电子邮件地址，则 `Sender` 字段为可选项。

  - `From` 字段中允许存在多个电子邮件地址，但是 `Sender` 字段中还必须只存在一个电子邮件地址。`Sender` 字段中的地址随后将在邮件信封中用作邮件的原始发件人。

  - `To`、`Cc` 或 `Bcc` 字段中必须至少存在一个电子邮件地址。

  - 邮件头和邮件正文之间必须存在一个空行。

本示例显示一封使用可接受的分拣目录格式的纯文本邮件。

    To: mary@contoso.com
    From: bob@fabrikam.com
    Subject: Message subject
    
    This is the body of the message.

分拣目录邮件文件中也支持 MIME 内容。MIME 定义多种邮件内容，包括无法使用 7 位 ASCII 文本表示的语言、HTML 以及其他多媒体格式。对 MIME 及其要求的完整描述不在本主题的讨论范围之内。本示例显示一封使用可接受的分拣目录格式的简单 MIME 邮件。

    To: mary@contoso.com
    From: bob@fabrikam.com
    Subject: Message subject
    MIME-Version: 1.0
    Content-Type: text/html; charset="iso-8859-1"
    Content-Transfer-Encoding: 7bit
    
    <HTML><BODY>
    <TABLE>
    <TR><TD>cell 1</TD><TD>cell 2</TD></TR>
    <TR><TD>cell 3</TD><TD>cell 4</TD></TR>
    </TABLE>

    </BODY></HTML>

返回顶部

## 分拣目录邮件头修改

分拣目录将从邮件头中删除下列任意邮件头字段：

  - `Received`

  - `Resent-*`

  - `Bcc`
    
    > [!NOTE]
    > 在邮件头的可选 <code>Bcc</code> 邮件头字段中找到的任何电子邮件地址都将得到正确处理。在 <code>Bcc</code> 收件人提升为不可见的邮件信封收件人后，将从邮件头中删除，以保护其身份。如果邮件仅包含 <code>Bcc</code> 收件人，则<strong>Undisclosed Recipients</strong>的值将添加到邮件头中的 <code>To</code> 字段。


作为邮件提交过程的一部分，分拣目录会将其自身的 `Received` 头字段添加到邮件中。应用以下格式的 `Received` 头字段：

    Received: from localhost by Pickup with Microsoft SMTP Server id <ExchangeServerVersion><datetime>

如果下列邮件头字段丢失或其格式不正确，则分拣目录将对其进行修改：

  - **Message-Id**   如果 `Message-Id` 字段丢失或者为空，则分拣目录将使用格式 *\<GUID\>*@*\<defaultdomain\>* 添加一个 Message-Id 字段。

  - **日期** 如果 `Date` 字段丢失或其格式不正确，则分拣目录将添加分拣目录进行邮件处理的日期和时间。

返回顶部

## 重播目录邮件文件要求

重播目录用于重新提交导出的 Exchange 邮件以及从外部网关服务器接收邮件。这些邮件已针对重播目录进行格式化。管理员或应用程序几乎或根本不需要使用重播目录撰写并提交新邮件文件。应使用分拣目录创建并提交新邮件文件。

重播目录的邮件大量使用 *X-Header* 字段。X-Header 是邮件头中用户定义的非正式邮件头字段。X-Header 在 RFC 2822 中未专门介绍，但是可以使用以“X-”开头的未定义邮件头字段将非正式邮件头字段添加到邮件中。在重播目录的邮件文件中使用的特定于 Exchange 的 X-Header 可以实际设置邮件信封中通常存在的传递信息。使用重播目录处理从其他 Exchange 服务器导出的邮件时，需要使用此功能来保留原始邮件信息。

复制到重播目录中的邮件文件必须满足下列要求才能成功地进行传递：

  - 邮件文件必须是符合基本 SMTP 邮件格式的文本文件。支持 MIME 邮件头字段和内容。

  - 邮件文件的文件扩展名必须是 .eml。

  - X-Header 必须出现在所有常规邮件头字段的前面。

  - 邮件头字段和邮件正文之间必须存在一个空行。

重播目录中的邮件需要下表中所述的 X-Header：

  - **X-Sender**   此 X-Header 替换典型 SMTP 邮件中的 `From` 邮件头字段要求。必须有一个包含一个电子邮件地址的 `X-Sender` 字段。尽管收件人的电子邮件客户端会将 `From` 邮件头字段（如果存在该字段）的值显示为邮件的发件人，但是重播目录将忽略 `From` 邮件头字段。其他参数通常在 `X-Sender` 字段中，如下例所示。
    
        X-Sender: <bob@fabrikam.com> BODY=7bit RET=HDRS ENVID=12345ABCD auth=<someAuth>
    
    > [!NOTE]
    > 这些参数是通常由发送服务器生成的邮件信封值。在导出的邮件文件中可以看到类似的参数。<br />
    > <code>RET</code> 指定无法传递邮件时，是将整个邮件还是只将邮件头返回给发件人。<code>RET</code> 的值可以是 <code>HDRS</code> 或 <code>FULL</code>。<code> ENVID</code> 是邮件信封标识符。<code>BODY</code> 指定邮件的文本编码。<code>auth</code> 指定邮件服务器的身份验证机制（如 RFC 2554 中所述）。


  - **X-Receiver**   此 X-Header 替换典型 SMTP 邮件中的 `To` 邮件头字段要求。必须至少存在一个包含一个电子邮件地址的 `X-Receiver` 字段。允许多个收件人具有多个 `X-Receiver` 字段。尽管收件人的电子邮件客户端会将 `To` 邮件头字段（如果存在该字段）的值显示为邮件的收件人，但是重播目录将忽略 `To` 邮件头字段。其他可选参数可能在 `X-Receiver` 字段中，如下例所示。
    
        X-Receiver: <mary@contoso.com> NOTIFY=NEVER ORcpt=mary@contoso.com
    
    > [!NOTE]
    > 这些参数是通常由发送服务器生成的邮件信封值。在导出的邮件文件中可以看到类似的参数。这些参数与发送状态通知 (DSN) 邮件有关（如 RFC 1891 中所述）。<br />
    > <code>NOTIFY</code> 的值可以是 <code>NEVER</code>、<code>DELAY</code> 或 <code>FAILURE</code>。<code>ORcpt</code> 用于保留邮件的原始收件人。


对于重播目录中的邮件文件，下表中所述的 X-Header 是可选的：

  - **X-CreatedBy**   用于邮件头防火墙功能。如果此 X-Header 存在，则不得为空。如果 `X-CreatedBy` 字段不存在，则为该字段添加**Unspecified**值。通常，此字段的值为 **MSExchange15**，但是还可以包含为发送连接器设置的非 SMTP 地址空间类型，例如**Notes**。

  - **X-EndOfInjectedXHeaders**   存在的所有 X-Header 的大小（字节数）。此 X-Header 可以作为一个标记，用于指示常规邮件头字段开始之前的最后一个 X-Header。

  - **X-ExtendedMessageProps**   邮件的扩展邮件属性。

  - **X-HeloDomain** 在初始 SMTP 协议转换期间提供的 HELO/EHLO 域字符串。

  - **X-Source**   由 **MessageSourceName** 列下的队列查看器使用。如果未指定此 X-Header 的值，则使用**Replay**值。此 X-Header 其他可能的值包括 **Smtp Receive Connector**和**Smtp Send Connector**。

  - **X-SourceIPAddress** 发送服务器的 IP 地址。如果未指定 IP 地址，则此字段为 `0.0.0.0`。

本示例显示一封使用可接受的重播目录格式的纯文本邮件。

    X-Receiver: <mary@contoso.com> NOTIFY=NEVER ORcpt=mary@contoso.com
    X-Sender: <bob@fabrikam.com> BODY=7bit ENVID=12345AB auth=<someAuth>
    Subject: Optional message subject
    
    This is the body of the message.

重播目录邮件文件中还支持 MIME 内容。MIME 定义多种邮件内容，包括无法使用 7 位 ASCII 文本表示的语言、HTML 以及其他多媒体格式。对 MIME 及其要求的完整描述不在本主题的讨论范围之内。本示例显示一封使用可接受的重播目录格式的简单 MIME 邮件。

    X-Receiver: <mary@contoso.com> NOTIFY=NEVER ORcpt=mary@contoso.com
    X-Sender: <bob@fabrikam.com> BODY=7bit ENVID=12345ABCD auth=<someAuth>
    To: mary@contoso.com
    From: bob@fabrikam.com
    Subject: Optional message subject
    MIME-Version: 1.0
    Content-Type: text/html; charset="iso-8859-1"
    Content-Transfer-Encoding: 7bit
    
    <HTML><BODY>
    <TABLE>
    <TR><TD>cell 1</TD><TD>cell 2</TD></TR>
    <TR><TD>cell 3</TD><TD>cell 4</TD></TR>
    </TABLE>

    </BODY></HTML>

返回顶部

## 重播目录邮件头修改

重播目录将 `Bcc` 邮件头字段从邮件文件中删除。

在邮件提交过程中，重播目录将自己的 `Received` 邮件头字段添加到邮件中。“接收时间”邮件头字段采用以下格式。

    Received: from <ReceivingServerName> by Replay with <ExchangeServerVersion><DateTime>

重播目录修改邮件头中的以下邮件头字段：

  - **Message-ID**   如果缺少此邮件头字段或此字段为空，重播目录将使用 *\<GUID\>*@*\<默认域\>* 格式添加一个“邮件 ID”邮件头字段。

  - **日期** 如果缺少此邮件头字段或此字段格式不正确，重播目录将使用重播目录处理邮件的日期和时间添加“日期”邮件头字段。

返回顶部

## 分拣目录和重播目录邮件处理失败

复制到分拣目录或重播目录中的邮件文件可能不会成功地排入队列以等待传递。可能会出现下列类别的邮件提交故障：

  - **传递失败**   格式正确的邮件文件可与无法成功提交以进行传递的有效发件人一起生成一个未送达报告 (NDR)。格式不正确的内容或分拣目录邮件限制违规也可能导致 NDR。如果在邮件处理期间生成了 NDR，则原始邮件文件将附加到 NDR 邮件中，并且邮件文件将会从分拣目录或重播目录中删除。
    
    > [!NOTE]
    > 提交到传输管道的格式正确的邮件可能会在以后遇到传递失败的问题，并将随 NDR 返回至发件人。这种失败可能由与分拣目录或重播目录无关的传输问题所引起，例如邮件传递路径沿途的消息服务器故障或路由故障。


  - **死信** 分类为*死信*的邮件具有严重的问题，这些问题将阻止分拣目录或重播目录提交邮件进行传递。导致产生死信的另一种情况是，邮件格式正确，但是收件人无效，因为发件人无效，所以无法向发件人发送 NDR 邮件。
    
    确定为死信的邮件文件将保留在分拣目录或重播目录，并将从 *\<filename\>*.eml 重命名为 *\<filename\>*.bad。如果 *\<filename\>*.bad 文件已存在，该文件将重命名为 *\<filename\>\<datetime\>*.bad。如果分拣目录或重播目录中存在死信，则将生成事件日志错误，但是相同的死信邮件不会生成重复的事件日志错误。
    
    > [!NOTE]
    > 将邮件文件复制到分拣目录以供传递之前，请始终在其他位置撰写和保存邮件文件。分拣目录每 5 秒钟轮询一次新邮件。因此，如果您尝试在分拣目录自身中撰写和保存邮件文件，则分拣目录可能会在您完成撰写之前尝试处理邮件文件。


返回顶部

## 分拣目录和重播目录的安全注意事项

下表介绍分拣目录和重播目录共同存在的安全问题：

  - 任何在接收连接器上配置的安全性检查（例如反垃圾邮件、反恶意软件、发件人筛选或收件人筛选操作），都不会对通过分拣目录或重播目录提交的邮件执行。

  - 存在安全风险的分拣目录或重播目录可以充当开放中继。这样，可以使用其他服务器重新提交或“中继”邮件，以屏蔽邮件的真实来源。

下表介绍适用于重播目录的其他安全问题：

  - 通过重播目录使用的 X-Header 可以手动创建邮件信封。`X-Sender` 和 `X-Receiver` 字段中的信息可以与电子邮件客户端显示的 `To` 或 `From` 邮件头字段完全不同。这种冒充发件人和域的行为通常称为“电子欺骗”。“欺骗邮件”是指发送地址已被修改的电子邮件，该邮件看起来发自某个发件人，但此发件人并不是实际的发件人。

  - 如果 `X-CreatedBy` 字段的值为 **MSExchange15**，则认为目标是可信的，不会应用邮件头防火墙。通过*邮件头防火墙*，Exchange 可以保留在可信 Exchange 服务器之间传输的邮件中的 X-Header，或从传输到 Exchange 组织外部的不可信目标的邮件中删除可能会泄漏的 X-Header。可以使用这些 X-Header 在经过授权的 Exchange 服务器之间共享 Exchange 信息，例如垃圾邮件可信度 (SCL)、邮件签名或加密。如果向未经授权的源泄露这些信息，可能会造成潜在的安全风险。有关邮件头防火墙的详细信息，请参阅[了解邮件头防火墙](https://go.microsoft.com/fwlink/?linkid=268394)。

由于存在与重播目录相关联的其他安全风险，因此应向重播目录应用较高的安全性。可以向必须生成和提交邮件的用户或应用程序授予对分拣目录的访问权限，但是这些用户或应用程序不应要求对重播目录的访问权限。

默认情况下，所有邮箱服务器和边缘传输服务器上都会启用分拣目录和重播目录。如果组织中特定的邮箱服务器或边缘传输服务器上不需要分拣目录或重播目录，可以通过将分拣目录路径或重播目录路径设置为值 `$null`，在该服务器上禁用分拣目录或重播目录。有关详细信息，请参阅[配置拾取目录和重播目录](configure-the-pickup-directory-and-the-replay-directory-exchange-2013-help.md)。

返回顶部

## 分拣目录和重播目录的权限

分拣目录和重播目录需要下列权限：

  - 管理员：完全控制

  - 系统：完全控制

  - 网络服务：读取、写入和删除子文件夹和文件

默认情况下，Microsoft Exchange 传输服务使用网络服务用户帐户的安全凭据来管理分拣目录和重播目录的位置和权限。网络服务帐户要求对分拣目录具有这些权限，以便可以打开 .eml 文件、重命名为 .tmp 并将其删除，或重命名为 .bad（如果邮件被分类为死信）。

可以使用 **Set-TransportService** cmdlet 上的 *PickupDirectoryPath* 和 *ReplayDirectoryPath* 参数移动这两个目录的位置。能否成功地更改分拣目录的位置取决于向网络服务帐户授予的对新分拣目录位置的权利，以及是否已存在新分拣目录。如果尚未存在新分拣目录，并且网络服务帐户具有创建文件夹和在新位置应用权限所需的权利，则将新建分拣目录，并向其应用正确的权限。如果新目录已经存在，则不会检查现有文件夹权限。每次通过同时使用 *PickupDirectoryPath* 或 *ReplayDirectoryPath* 参数与 **Set-TransportService** cmdlet 来移动该目录位置时，最好验证一下新目录是否存在以及其应用的权限是否正确。

返回顶部

