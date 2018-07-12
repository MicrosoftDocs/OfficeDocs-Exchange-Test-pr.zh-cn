---
title: '共享: Exchange 2013 Help'
TOCTitle: 共享
ms:assetid: 09e6732a-4e99-44d0-801d-9463fdc57a9b
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd638083(v=EXCHG.150)
ms:contentKeyID: 50489887
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 共享

 

_**适用于：** Exchange Server 2013, Outlook 2013_

_**上一次修改主题：** 2015-02-27_

与人一起共事或计划社交活动时，您可能需要与不同组织中的用户或朋友和家人协调计划。通过 Exchange 2013，管理员可以设置不同的日历访问级别，以允许企业与其他企业协调并让用户与其他人共享计划。可以通过创建*组织关系*来设置企业与企业的日历共享。用户与用户的日历共享则可通过应用*共享策略*来设置。

> [!IMPORTANT]  
> Exchange Server 2013 的此项功能与由世纪互联在中国运营的 Office 365 不完全兼容，可能需要遵循一些功能限制。有关详细信息，请参阅<a href="https://go.microsoft.com/fwlink/?linkid=313640">了解由世纪互联运营的 Office 365</a>。


**目录**

Exchange 2013 中的共享方案

忙/闲共享的限制

联合共享的防火墙注意事项

与 Exchange 2010 共存

与 Exchange 2007 共存

共享文档

## Exchange 2013 中的共享方案

Exchange 2013 中支持以下共享方案：


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>共享目标</th>
<th>要使用的设置</th>
<th>要求</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>与 Office 365 组织共享日历</p></td>
<td><p>组织关系</p></td>
<td><p>Office 365 组织已做好配置准备。内部部署 Exchange 管理员必须设置与云的身份验证关系（也称为“联盟”），且必须满足最低软件要求。要了解有关设置联盟的详细信息，请参阅<a href="federation-exchange-2013-help.md">联盟</a>。</p></td>
</tr>
<tr class="even">
<td><p>与其他内部部署 Exchange 组织共享日历</p></td>
<td><p>组织关系</p></td>
<td><p>内部部署 Exchange 组织必须设置联盟，且必须满足最低软件要求。</p></td>
</tr>
<tr class="odd">
<td><p>与 Internet 用户共享 Exchange 用户的日历</p></td>
<td><p>共享策略</p></td>
<td><p>无，已准备好配置</p></td>
</tr>
<tr class="even">
<td><p>与其他 Exchange 内部部署用户共享 Exchange 用户的日历</p></td>
<td><p>共享策略</p></td>
<td><p>内部部署 Exchange 组织必须设置联盟，且必须满足最低软件要求。</p></td>
</tr>
</tbody>
</table>


下表列出了组织关系与共享策略之间的差异。

### 组织关系与共享策略

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>组织关系</th>
<th>共享策略</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>您的组织是否需要联合身份验证信任</p></td>
<td><p>是</p></td>
<td><p>是（当与其他联盟域组织共享时）。对于 Internet 共享策略不是必需的。</p></td>
</tr>
<tr class="even">
<td><p>是否建议联合外部域</p></td>
<td><p>是</p></td>
<td><p>是（当与其他联盟域组织共享时）。对于 Internet 共享策略不是必需的。</p></td>
</tr>
<tr class="odd">
<td><p>是否允许为一组多个用户与外部组织共享忙/闲信息（包括主题和位置）。</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p>是否允许共享包含忙/闲信息的“日历”文件夹</p></td>
<td><p>否</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p>是否允许共享包含忙/闲信息（包括主题和正文）的“日历”文件夹</p></td>
<td><p>否</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>是否需要用户向外部收件人发送共享邀请</p></td>
<td><p>否</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p>是否提供了访问方法</p></td>
<td><p>您的客户端访问服务器可访问外部组织的客户端访问服务器，并在请求时检索外部用户的忙/闲信息。</p></td>
<td><p>您的客户端访问服务器可访问外部组织的客户端访问服务器，并订阅外部用户的“日历”文件夹。对于 Internet 共享策略，外部用户可访问客户端访问服务器上的受限或公用 URL。</p></td>
</tr>
<tr class="even">
<td><p>是否可以应用于所有外部域</p></td>
<td><p>否（两个 Exchange 2013 组织之间存在的一对一关系）</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p>是否为用户提供了与外部收件人之间的多种共享体验</p></td>
<td><p>否</p></td>
<td><p>是，这基于应用的共享策略</p></td>
</tr>
<tr class="even">
<td><p>是否对某些用户禁用共享</p></td>
<td><p>是，通过为组织关系指定安全通讯组禁用共享</p></td>
<td><p>是，通过禁用应用的共享策略禁用共享</p></td>
</tr>
<tr class="odd">
<td><p>是否需要邮箱驻留在 Exchange 2013 邮箱服务器上</p></td>
<td><p>否</p></td>
<td><p>是</p></td>
</tr>
</tbody>
</table>


返回顶部

## 忙/闲共享的限制

在 Exchange 组织间共享忙/闲信息时，适用以下限制：

1.  **Outlook Web Access 2003**   当 Exchange 2003 组织中的用户使用 Outlook Web Access 访问远程 Exchange 2013 组织中用户的忙/闲信息时，请求将失败。源自 Exchange 2003 的 Outlook Web Access 连接无法建立到忙/闲系统文件夹的 WebDAV（基于 Web 的分布式创作和版本管理）连接，因此无法检索远程用户的忙/闲信息。由于 Exchange 2013 不支持 WebDAV 连接，因此 Exchange 2003 服务器无法连接到 Exchange 2013 CAS 服务器上的 External (FYDIBOHF25SPDLT) 以支持 Outlook Web Access 请求。Outlook 客户端没有这种限制，因为它们在连接到 External (FYDIBOHF25SPDLT) 时使用的是 MAPI 而不是 WebDAV。

2.  **广域网 (WAN) 延迟**   在 Exchange 2003 组织中，所有忙/闲文件夹的副本都必须驻留在 Exchange 2010 SP2 或更高版本的邮箱服务器上。在 Exchange 2003 公用文件夹数据库位于多个物理站点的环境中，如果内部忙/闲查询必须遍历 WAN 链接来访问不在同一个物理站点中的 Exchange 2010 公用文件夹数据库，则可能会出现过多的延迟或性能问题。

3.  **忙/闲信息期**   从 Exchange 2013 组织向 Exchange 2007 组织发出的忙/闲信息请求可能会因为请求的忙/闲信息期不匹配而失败。默认情况下，Exchange 2007 接受 42 天忙/闲信息的可用性请求，Exchange 2013 可以请求 62 天的忙/闲信息。如果请求超出了 Exchange 2007 规定的默认限制值 42，则请求将失败。
    
    请执行以下步骤配置 Exchange 2007 CAS 服务器以接受更长时期的忙/闲信息请求：
    
    1.  在所有 Exchange 2007 CAS 服务器上，使用记事本等文本编辑器打开以下文件：\<Exchange 安装路径\>\\V14\\ClientAccess\\ExchWeb\\EWS\\web.config
        
        > [!CAUTION]  
        > 在对 web.config 文件进行任何更改前，请为该文件创建一个副本，并且将其存储在安全位置。
    
    2.  在 web.config 文件中找到 **appSettings** 部分。
    
    3.  添加新键值 \<add key="maximumQueryIntervalDays" value="62" /\>，并保存 web.config 文件。
        
        > [!NOTE]  
        > 默认情况下不提供 maximumQueryIntervalDays 值。如果此值不存在，Exchange 2007 将使用默认间隔 42 天。
    
    4.  在所有 Exchange 2007 CAS 服务器上停止并重新启动 Microsoft Internet 信息服务 (IIS)。

4.  **同时拥有内部部署用户和云用户的 Exchange 组织**   如果设置日历共享时的另一个 Exchange 组织是在使用 Microsoft Office 365 的混合部署中配置的，则对基于 Office 365 的用户或已移到云的远程用户的忙/闲可用性查找将会失败。因为 Exchange 组织的组织关系是与远程本地 Exchange 组织的关系，而不是与基于 Office 365 的 Exchange Online 组织的关系，因此忙/闲请求无法查询基于 Office 365 的用户。Exchange 2013 不支持通过本地组织将这些可用性请求代理到 Office 365 服务的功能。

有关如何在常见 Exchange 部署之间配置忙/闲共享的详细信息，请参阅[在 Exchange 组织之间配置联合共享](configuring-federated-sharing-between-exchange-organizations-exchange-2013-help.md)。

## 联合共享的防火墙注意事项

联合共享功能需要您所在组织中的客户端访问服务器使用 HTTPS 出站访问 Internet。您必须允许出站 HTTPS 访问（TCP 的端口是 443）组织中的所有 Exchange 2013 邮箱服务器。

为了使外部组织能够访问您所在组织的忙/闲信息，必须将至少一个客户端访问服务器发布到 Internet 上。这需要在 Internet 上通过入站 HTTPS 访问客户端访问服务器。Active Directory 站点（该站点未将客户端访问服务器发布到 Internet 上）中的客户端访问服务器可使用能够从 Internet 访问的其他 Active Directory 站点中的客户端访问服务器。未发布到 Internet 上的客户端访问服务器必须将 Web 服务虚拟目录的外部 URL 设置为对外部组织可见的 URL。

返回顶部

## 与 Exchange 2010 共存

在同时包含 Exchange 2010 和 Exchange 2013 服务器的组织中，拥有 Exchange 2010 邮箱服务器上的邮箱的用户可以使用组织关系与外部 Exchange 2013 联盟域组织中的收件人共享忙/闲信息。Exchange 2010 客户端访问和邮箱服务器必须运行 SP2 或更高版本，且您必须在 Exchange 2010 组织中具有至少一个 Exchange 2013 客户端访问服务器。

## 与 Exchange 2007 共存

在同时包含 Exchange 2013 和 Exchange 2007 服务器的组织中，拥有 Exchange 2007 邮箱服务器上的邮箱的用户可以使用组织关系与外部联盟域组织中的收件人共享忙/闲信息。该邮箱服务器必须运行 Exchange 2007 SP2 或更高版本，且 Exchange 组织中必须包含至少一个 Exchange 2013 客户端访问服务器。通过在组织中引入单个 Exchange 2013 客户端访问服务器即可使用组织关系，这提供了一个比同步忙/闲信息且需要 GAL 同步的解决方案更强大的解决方案。

当使用 Outlook 2010 或 Outlook Web App 在 Exchange 2007 服务器上安排会议时，拥有 Exchange 2007 服务器上的邮箱的用户可以查看外部组织中的用户的忙/闲信息。Exchange 2007 邮箱的忙/闲信息对外部组织中的收件人是可见的。

为 Exchange 2013 邮箱用户分配共享策略。若要使用共享策略，邮箱必须位于 Exchange 2013 邮箱服务器上。只有 Outlook 2010 和 Outlook Web App 客户端可用于生成或响应共享邀请。

返回顶部

## 共享文档

下表包含帮助您了解和管理 Exchange 2013 中的共享的主题链接。


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
<td><p><a href="federation-exchange-2013-help.md">联盟</a></p></td>
<td><p>了解有关支持共享的基本信任基础结构的详细信息，这是用户与外部收件人共享日历信息的简单方法。</p></td>
</tr>
<tr class="even">
<td><p><a href="organization-relationships-exchange-2013-help.md">组织关系</a></p></td>
<td><p>了解有关启用日历忙/闲共享的 Exchange 组织之间一对一关系的详细信息。</p></td>
</tr>
<tr class="odd">
<td><p><a href="sharing-policies-exchange-2013-help.md">共享策略</a></p></td>
<td><p>了解有关启用共享的个人与个人策略。</p>
<p></p></td>
</tr>
</tbody>
</table>

