---
title: '混合部署中的单一登录: Exchange 2013 Help'
TOCTitle: 混合部署中的单一登录
ms:assetid: 050606f9-718d-4a1f-b7a6-50b08c6e9e07
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Hh563846(v=EXCHG.150)
ms:contentKeyID: 50492069
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 混合部署中的单一登录

 

_<strong>适用于：</strong>Exchange Online, Exchange Server 2013, Exchange Server 2016_

_<strong>上一次修改主题：</strong>2016-01-29_

单一登录 (SSO) 使用户可以使用一个用户名和密码访问内部部署组织和 Office 365 组织。它向用户提供了一种熟悉的登录体验，并能够允许管理员使用内部部署 Active Directory 管理工具轻松控制 Exchange Online 组织邮箱的帐户策略。尽管您不需要启用单一登录来配置混合部署，但我们强烈建议您这样做。如果不使用单一登录，用户将需要记住两组不同的凭据，一组用于您的内部部署组织，另一组用于 Office 365。下面是单一登录的其他几个优点：

  - **Exchange Online Archiving**   如果部署了单一登录，内部部署 Outlook 用户访问 Exchange Online 组织中的存档内容时，会收到提供凭据的提示。不过，用户可以通过选择“保存密码”而暂时避免以后的凭据提示，只会在更改内部部署帐户密码以后才再次收到提供凭据的提示。如果 Exchange 组织中没有部署单一登录，且启用了 Exchange Online Archiving，则内部部署用户主体名称 (UPN) 必须与 Exchange Online 帐户匹配，且用户在访问存档内容时始终会收到提供内部部署凭据的提示。

  - **策略控制**   您可通过 Active Directory 控制帐户策略，这样便能够管理密码策略、工作站限制、锁定控制等，而无需在 Office 365 组织中执行其他任务。

  - **减少支持呼叫**   忘记密码是所有公司接到支持电话的常见原因。如果用户要记住的密码较少，则他们忘记密码的可能性就较低。

部署单一登录时有多个选项：密码同步和 Active Directory 联合身份验证服务 (AD FS)。这两个选项均由 Azure Active Directory Connect 提供。我们强烈建议使用密码同步方法，除非您有使用 AD FS 的特殊需求。密码同步提供了很多与 AD FS 相同的好处，而省去了部署后者的复杂性。下表提供了每种选项的共同优缺点。

<table>
<thead>
<tr class="header">
<th><img src="images/Dn986544.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>默认情况下，如果您部署 AD FS 而您的内部部署 AD FS 服务器出于某种原因无法通过 Internet 进行访问，Office 365 将回退到密码同步来对用户进行身份验证。这允许使用 Office 365 邮箱的用户可以继续不间断地工作，即使您的内部部署服务器不可用也没有关系。</td>
</tr>
</tbody>
</table>


若要了解有关每个选项的详细信息，请参阅 [Azure AD Connect 用户登录选项](http://go.microsoft.com/fwlink/p/?linkid=723514)


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><p>单一登录方法</p></th>
<th><p>优点</p></th>
<th><p>缺点</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>密码同步（推荐）</p></td>
<td><ul>
<li><p>明显没有 AD FS 复杂</p></li>
<li><p>用户可以登录到 Office 365，即使您的内部部署 Active Directory 不可用也没有关系。</p></li>
<li><p>部署密码同步需要的额外服务器更少。</p></li>
<li><p>不需要第三方证书。</p></li>
<li><p>不需要通过 AD FS 对您的内部部署 Active Directory 进行外部访问。</p></li>
<li><p>通常可以在几小时内完成部署。</p></li>
</ul></td>
<td><ul>
<li><p>禁用您的内部部署 Active Directory 中的用户帐户不会在 Office 365 中禁用它。您需要手动禁用 Office 365 管理门户中的帐户。</p></li>
<li><p>需要内部部署 Active Directory不支持其他目录服务。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>AD FS</p></td>
<td><ul>
<li><p>更改密码比较即时。</p></li>
<li><p>在您的内部部署 Active Directory 中禁用用户将禁用其内部部署网络访问和其 Office 365 帐户。</p></li>
<li><p>支持 Active Directory 以外的目录服务。</p></li>
<li><p>支持超大型以及多样化的部署。</p></li>
<li><p>支持双重身份验证。</p></li>
</ul></td>
<td><ul>
<li><p>需要更多的服务器，且至少有一个服务器驻留在外围网络中。</p></li>
<li><p>需要在您的防火墙上打开一个公共 IP地址和 TCP 端口 443。</p></li>
<li><p>需要与内部部署 Active Directory 进行连接来检测帐户密码的更改，并且最近已启用或禁用一个帐户。</p></li>
</ul></td>
</tr>
</tbody>
</table>

