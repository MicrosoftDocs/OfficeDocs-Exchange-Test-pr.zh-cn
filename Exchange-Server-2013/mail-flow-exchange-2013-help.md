﻿---
title: '邮件流: Exchange 2013 Help'
TOCTitle: 邮件流
ms:assetid: 14df5e1a-a5f7-4b0d-ba97-f53b76f0e7e0
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa996349(v=EXCHG.150)
ms:contentKeyID: 50490058
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 邮件流

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2015-03-09_

在 Microsoft Exchange Server 2013 中，邮件流通过传输管道进行。*传输管道*是协同工作的服务、连接、组件和队列的集合，用于将所有邮件路由到组织内邮箱服务器上的传输服务中的分类程序。

是否查找所有邮件流主题的列表？请参阅邮件流文档。

有关如何在新 Exchange 2013 组织中配置邮件流的信息，请参阅[配置邮件流和客户端访问](configure-mail-flow-and-client-access-exchange-2013-help.md)。

**目录**

传输管道

邮箱服务器上的传输服务

邮件流文档

## 传输管道

传输管道由以下服务组成：

  - **客户端访问服务器上的前端传输服务**   此服务作为 Exchange 2013 组织的所有入站和（可选）出站外部 SMTP 流量的无状态代理。前端传输服务不检查邮件内容，不与邮箱服务器上的邮箱传输服务通信，也不在本地对任何邮件进行排队。

  - **邮箱服务器上的传输服务**   此服务几乎与以前版本的 Exchange 中的集线器传输服务器角色相同。传输服务为组织处理所有 SMTP 邮件流，执行邮件分类并执行邮件内容检查。与以前版本的 Exchange 不同，传输服务从不直接与邮箱数据库通信。该任务现在由邮箱传输服务处理。传输服务在邮箱传输服务、传输服务、前端传输服务和（取决于您的配置）边缘传输服务器上的传输服务之间发送邮件。本主题稍后将详细介绍邮箱服务器上的传输服务。

  - **邮箱服务器上的邮箱传输服务**   此服务由两项单独的服务组成：邮箱传输提交服务和邮箱传输传递服务。邮箱传输传递服务从本地邮箱服务器或其他邮箱服务器上的传输服务接收 SMTP 邮件，并使用 Exchange 远程过程调用 (RPC) 连接到本地邮箱数据库以传递邮件。邮箱传输提交服务使用 RPC 连接到本地邮箱数据库以检索邮件，并通过 SMTP 将邮件提交给本地邮箱服务器或其他邮箱服务器上的传输服务。邮箱传输提交服务可以访问与传输服务相同的路由拓扑信息。与前端传输服务一样，邮箱传输服务也不在本地对任何邮件进行排队。

  - **边缘传输服务器上的传输服务**   此服务与邮箱服务器上的传输服务非常相似。如果您在外围网络安装了边缘传输服务器，从 Internet 发送或要发送到 Internet 的所有邮件都将通过传输服务边缘传输服务器发送。此服务会在本主题后面更详细地介绍。

下图显示了 Exchange 2013 传输管道中组件之间的关系。

**Exchange 2013 中的传输管道概述。**

![传输管道概览图](images/Aa996349.6f548b64-6ac2-4e98-9098-69ad6cd9f569(EXCHG.150).gif "传输管道概览图")

## 来自外部发件人的邮件

来自组织外部的邮件会通过客户端访问服务器上的前端传输服务中的接收连接器进入传输管道，然后再路由到邮箱服务器上的传输服务。

如果您在外围网络安装了 Exchange 2013 边缘传输服务器，来自组织外部的邮件将通过边缘传输服务器上的传输服务中的接收连接器进入传输管道。邮件接下来发送到哪里取决于您的内部 Exchange 服务器的配置。

  - **安装在同一台计算机上的邮箱服务器和客户端访问服务器**   在此配置中，客户端访问服务器用于入站邮件流。邮件从边缘传输服务器上的传输服务流到客户端访问服务器上的前端传输服务，然后流到邮箱服务器上的传输服务。

  - **安装在不同计算机上的邮箱服务器和客户端访问服务器**   在此配置中，入站邮件流将绕过客户端访问服务器。邮件从边缘传输服务器上的传输服务流到邮箱服务器上的传输服务。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您在外围网络中安装了 Exchange 2010 或 Exchange 2007 边缘传输服务器，则邮件流会直接在边缘传输服务器与邮箱服务器上的传输服务之间进行。有关详细信息，请参阅<a href="use-an-exchange-2010-or-2007-edge-transport-server-in-exchange-2013-exchange-2013-help.md">在 Exchange 2013 中使用 Exchange 2010 或 2007 边缘传输服务器</a>。</td>
</tr>
</tbody>
</table>


## 来自内部发件人的邮件

来自组织内部的 SMTP 邮件可采用下列其中一种方法通过邮箱服务器上的传输服务进入传输管道：

  - 通过接收连接器。

  - 通过分拣目录或重播目录。

  - 通过邮箱运输服务。

  - 通过代理提交。

邮件基于路由目标或交付组路由。有关详细信息，请参阅[邮件路由](mail-routing-exchange-2013-help.md)。

如果邮件具有外部收件人，邮件将从邮箱服务器上的传输服务路由到 Internet，或者从邮箱服务器路由到客户端访问服务器上的前端传输服务，然后路由到 Internet，前提是发送连接器配置为通过客户端访问服务器来代理出站连接。有关详细信息，请参阅[为发送到 Internet 的电子邮件创建发送连接器](create-a-send-connector-for-email-sent-to-the-internet-exchange-2013-help.md)。

如果您在外围网络中安装了边缘传输服务器，具有外部收件人的邮件将从不通过客户端访问服务器上的前端传输服务路由。邮件将从邮箱服务器上的传输服务路由到边缘传输服务器上的传输服务。

## 邮箱服务器上的传输服务

在 Exchange 2013 组织中发送或接收的每封邮件都必须在邮箱服务器上的传输服务中进行分类，然后才能路由和传递该邮件。对邮件进行了分类之后，会将其放入传递队列中，以传递给目标邮箱数据库、目标数据库可用性组 (DAG)、Active Directory 站点或 Active Directory 林，或是传递给组织外部的目标域。

邮箱服务器上的传输服务包含下列组件和过程：

  - **SMTP 接收**   当传输服务收到邮件时，会执行邮件内容检查，应用传输规则，并执行反垃圾邮件和反恶意软件检查（如果已启用）。SMTP 会话包含一系列以特定顺序协同工作的事件，以便在接受邮件之前验证邮件内容。通过 SMTP 接收功能完全传递邮件之后，如果接收事件或反垃圾邮件和反恶意软件代理未拒绝该邮件，则会将该邮件放在提交队列中。

  - **提交** 提交是将邮件放入提交队列中的过程。分类程序会一次拣选一个邮件进行分类。提交通过下列三种方法来进行：
    
      - 对于通过接收连接器的 SMTP 接收。
    
      - 通过分拣目录或重播目录。这些目录存在于邮箱服务器和边缘传输服务器上。已复制到分拣目录或重播目录中的格式正确的邮件文件，将直接放入提交队列中。
    
      - 通过传输代理。

  - **分类程序** 分类程序从提交队列中一次拣选一个邮件。分类程序完成以下步骤：
    
      - 收件人解析，其中包括顶级寻址、展开和收件人拆分。
    
      - 路由解析。
    
      - 内容转换。
    
    此外，还会应用由组织定义的邮件流规则。对邮件进行分类后，会将其放入基于邮件目标的传递队列中。邮件按目标邮箱数据库、DAG、Active Directory 站点、Active Directory 林或外部域进行排队。

  - **SMTP 发送**   从传输服务路由邮件的方式取决于邮件收件人相对于进行分类所在的邮箱服务器的位置。邮件可以路由到以下位置：
    
      - 同一邮箱服务器上的邮箱传输服务。
    
      - 属于同一 DAG 的不同邮箱服务器上的邮箱传输服务。
    
      - 不同 DAG、Active Directory 网站或 Active Directory 林中的邮箱服务器上的传输服务。
    
      - 通过同一邮箱服务器上的发送连接器、不同邮箱服务器上的传输服务、客户端访问服务器上的前端传输服务或外围网络中的边缘传输服务器上的传输服务交付到 Internet。

## 边缘传输服务器上的传输服务

边缘传输服务器上的传输服务的组件与邮箱服务器上的传输服务相同。但是，边缘传输服务器上每个处理阶段实际发生的事各不相同。以下列表描述了这些差异。

  - **SMTP 接收**   当边缘传输服务器订阅到内部 Active Directory 网站时，默认的接收连接器将自动配置为从内部邮箱服务器和 Internet 接受邮件。当 Internet 邮件到达边缘传输服务器时，防垃圾邮件代理将过滤连接和邮件内容，并在接受邮件进入组织时识别发件人和收件人。防垃圾邮件代理为默认安装和启用。提供其他附件过滤和连接过滤功能，但不提供内置恶意软件过滤。此外，传输规则由边缘规则代理控制。与邮箱服务器上的传输规则代理相比，仅少数传输规则条件在边缘传输服务器上可用。但是，边缘传输服务器上仅提供与 SMTP 连接相关的独特传输规则操作。

  - **提交**   在边缘传输服务器上，邮件通常通过接收连接器进入提交队列。但提供分拣目录和重播目录。

  - **分类程序**   在边缘传输服务器上，分类是直接将文件放入交付队列以交付给内部或外部收件人的简短过程。

  - **SMTP 发送**   当边缘传输服务器订阅到内部 Active Directory 网站时，将自动创建和配置两个发送连接器。一个负责将出站邮件发送到 Internet 收件人，另一个负责将来自 Internet 的入站邮件发送到内部收件人。入站邮件将发送到所订阅 Active Directory 网站中的可用邮箱服务器上的传输服务。

## 邮件流文档

下表包含帮助您了解和管理 Exchange 2013 中的邮件流的主题链接。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>主题</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="mail-routing-exchange-2013-help.md">邮件路由</a></p></td>
<td><p>邮件路由描述在邮件服务器之间传输邮件的方式。</p></td>
</tr>
<tr class="even">
<td><p><a href="connectors-exchange-2013-help.md">连接器</a></p></td>
<td><p>连接器定义与 Exchange 服务器之间来回传输邮件的位置和方式。</p></td>
</tr>
<tr class="odd">
<td><p><a href="domains-exchange-2013-help.md">域</a></p></td>
<td><p>接受的域定义在 Exchange 组织中使用的 SMTP 地址空间。远程域为发送到外部域的邮件配置邮件格式和编码设置。</p></td>
</tr>
<tr class="even">
<td><p><a href="transport-agents-exchange-2013-help.md">传输代理</a></p></td>
<td><p>传输代理在邮件通过 Exchange 传输管道时对邮件进行操作。</p></td>
</tr>
<tr class="odd">
<td><p><a href="transport-high-availability-exchange-2013-help.md">传输高可用性</a></p></td>
<td><p>传输高可用性描述 Exchange 2013 在传输过程中及传递之后保留邮件冗余副本的方式。</p></td>
</tr>
<tr class="even">
<td><p><a href="transport-logs-exchange-2013-help.md">传输日志</a></p></td>
<td><p>传输日志记录在邮件流过传输管道时邮件遇到的情况。</p></td>
</tr>
<tr class="odd">
<td><p><a href="manage-message-approval-exchange-2013-help.md">管理邮件审批</a></p></td>
<td><p>仲裁传输要求对发送到特定收件人的邮件进行审批。</p></td>
</tr>
<tr class="even">
<td><p><a href="content-conversion-exchange-2013-help.md">内容转换</a></p></td>
<td><p>内容转换控制针对外部收件人的传输中性编码格式 (TNEF) 邮件转换选项以及针对内部收件人的 MAPI 转换选项。</p></td>
</tr>
<tr class="odd">
<td><p><a href="dsns-and-ndrs-in-exchange-2013-exchange-2013-help.md">Exchange 2013 中的 DSN 和 NDR</a></p></td>
<td><p>传递状态通知 (DSN) 是发送给邮件发件人的系统邮件，例如未送达报告 (NDR)。</p></td>
</tr>
<tr class="even">
<td><p><a href="track-messages-with-delivery-reports-exchange-2013-help.md">使用送达报告跟踪邮件</a></p></td>
<td><p>送达报告是一个邮件跟踪工具，可用于按照某个特定主题搜索组织通讯簿中的用户发送或接收的电子邮件的传递状态。可以跟踪通过组织中的任何特定邮箱收发的邮件的传递信息。</p></td>
</tr>
<tr class="odd">
<td><p><a href="message-size-limits-exchange-2013-help.md">邮件大小限制</a></p></td>
<td><p>本主题介绍对邮件施加的大小和各个组件限制。</p></td>
</tr>
<tr class="even">
<td><p><a href="queue-viewer-exchange-2013-help.md">队列查看器</a></p></td>
<td><p>使用 Exchange 工具箱中的队列查看器可查看队列和队列中的邮件并对它们进行操作。</p></td>
</tr>
<tr class="odd">
<td><p><a href="pickup-directory-and-replay-directory-exchange-2013-help.md">拾取目录和重播目录</a></p></td>
<td><p>分拣和重播目录用于将邮件文件插入传输管道。</p></td>
</tr>
<tr class="even">
<td><p><a href="use-an-exchange-2010-or-2007-edge-transport-server-in-exchange-2013-exchange-2013-help.md">在 Exchange 2013 中使用 Exchange 2010 或 2007 边缘传输服务器</a></p></td>
<td><p>本主题介绍在 Exchange 2013 中使用以前 Exchange 版本提供的边缘传输服务器时的注意事项。</p></td>
</tr>
</tbody>
</table>

