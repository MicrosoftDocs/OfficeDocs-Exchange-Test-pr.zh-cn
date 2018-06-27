---
title: 'Exchange 2013 中的可用性服务: Exchange 2013 Help'
TOCTitle: Exchange 2013 中的可用性服务
ms:assetid: 9722dea2-2bf8-437c-85c0-3ab65b8a07b9
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb232134(v=EXCHG.150)
ms:contentKeyID: 52061536
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2013 中的可用性服务

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2016-12-09_

Exchange 2013 可用性服务可向 Microsoft Outlook 和 Outlook Web App 客户端提供忙/闲信息。可用性服务通过提供安全、一致、最新的忙/闲信息，改善信息工作者的日历和会议安排体验。

Outlook 和 Outlook Web App 使用可用性服务执行下列任务：

  - 检索 Exchange 2013 邮箱的当前忙/闲信息

  - 检索其他 Exchange 2013 组织的当前忙/闲信息

  - 从公用文件夹检索版本早于 Exchange 的服务器上的邮箱的已发布忙/闲信息

  - 查看与会者的工作时间

  - 显示会议时间的建议

**目录**

可用性服务概述

有关离开状态的信息

可用性服务 API

可用性服务网络负载平衡

用于检索忙/闲信息的方法

## 可用性服务概述

可用性服务直接从目标邮箱检索 Exchange 2013、 Exchange 2010 或 Exchange 2007 上的用户的忙/闲信息，并且可以配置为检索以前版本的 Exchange 上的用户的忙/闲信息。对于在所有客户端中均运行 Outlook 2007 或更高版本的 Exchange 2007、Exchange 2010 或 Exchange 2013 邮箱的拓扑，可用性服务用于检索忙/闲信息。

Outlook 使用 Exchange 自动发现服务来获取可用性服务的 URL。有关自动发现服务的详细信息，请参阅[自动发现服务](autodiscover-service-for-exchange-2013.md)。

您可以使用 Exchange 命令行管理程序配置可用性服务。不能使用 Exchange 管理中心 (EAC) 配置可用性服务。

## 有关离开状态的信息

可用性服务也提供了对用户不在办公室或长时间离开而发送的自动应答邮件的访问。

信息工作人员可在其无法答复电子邮件时使用 Outlook 和 Outlook Web App 中的“自动应答”功能（以前称为“外出”）来通知其他人员。此功能使信息工作人员和管理员在设置和管理自动应答邮件时更为简便。

## 可用性服务 API

可用性服务是 Exchange 2013 编程接口的一部分，它可用作 Web 服务，让开发人员编写用于实现集成的第三方工具。

## 可用性服务网络负载平衡

在运行可用性服务的客户端访问服务器上使用网络负载平衡 (NLB) 可提高依赖忙/闲信息的用户的绩效和可靠性。Outlook 使用自动发现服务发现可用性服务 URL。要与可用性服务一起使用 NLB，必须对配置进行更改。

内部 URL 通过 Intranet 使用，外部 URL 通过 Internet 使用。如果您要让内部和外部流量均使用同一 URL，请确保 DNS 已正确配置为将内部流量直接路由至内部 URL。同时，确保此 URL 可从内部和外部访问。为了使自动发现服务和可用性服务能够正常运行，必须对 DNS 进行配置，以便 mail.\<*域名*\>.com 和 autodiscover.mail.\<*域名*\>.com 指向负载平衡解决方案的虚拟 IP (VIP)，其中 \<*域名*\> 是您的域的名称。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>有关详细信息，请参阅<a href="https://go.microsoft.com/fwlink/p/?linkid=45959">网络负载平衡技术参考指南</a>和<a href="https://go.microsoft.com/fwlink/p/?linkid=49315">网络负载平衡群集</a>。您还可以搜索第三方负载平衡软件网站。</td>
</tr>
</tbody>
</table>


## 用于检索忙/闲信息的方法

下表列出了在各种单个林拓扑中用于检索忙/闲信息的不同方法。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>客户端</th>
<th>邮箱检索忙/闲信息正在运行中</th>
<th>目标邮箱正在运行中</th>
<th>忙/闲检索方法</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook 2013</p></td>
<td><p>Exchange 2013、Exchange 2010 或 Exchange 2007</p></td>
<td><p>Exchange 2013、Exchange 2010 或 Exchange 2007</p></td>
<td><p>可用性服务从目标邮箱中读取忙/闲信息。</p></td>
</tr>
<tr class="even">
<td><p>Outlook 2007</p></td>
<td><p>Exchange 2013、Exchange 2010 或 Exchange 2007</p></td>
<td><p>Exchange 2010 或者Exchange 2007</p></td>
<td><p>可用性服务从目标邮箱中读取忙/闲信息。</p></td>
</tr>
<tr class="odd">
<td><p>Outlook 2007</p></td>
<td><p>Exchange 2010 或者Exchange 2007</p></td>
<td><p>Exchange 2003</p></td>
<td><p>可用性服务生成指向 Exchange 2003 邮箱 /public 虚拟目录的 HTTP 连接。</p></td>
</tr>
<tr class="even">
<td><p>Outlook Web App</p></td>
<td><p>Exchange 2013、Exchange 2010 或 Exchange 2007</p></td>
<td><p>Exchange 2013、Exchange 2010 或 Exchange 2007</p></td>
<td><p>Exchange 2010 中的 Outlook Web App 或 Exchange 2007 中的 Outlook Web Access 调用可用性服务 API，使其从目标邮箱中读取闲/忙信息。</p></td>
</tr>
</tbody>
</table>

