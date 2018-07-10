---
title: '使用拨号规则授权通话: Exchange Online Help'
TOCTitle: 使用拨号规则授权通话
ms:assetid: 4c18bc07-f55c-42b7-81c1-729878aa93aa
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ898499(v=EXCHG.150)
ms:contentKeyID: 51408221
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 使用拨号规则授权通话

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2015-03-09_

默认情况下，用户无法发出传出呼叫。要指定用户可以发出的呼叫类型，首先需要创建拨号规则，然后在 UM 拨号计划、UM 邮箱策略或 UM 自动助理中对这些拨号规则组进行授权。在可以对拨号规则组授权之前，必须定义 UM 拨号计划中的拨号规则。有关详细信息，请参阅[创建用户的拨号规则](create-dialing-rules-for-users-exchange-2013-help.md)。

创建的每个拨号规则都会包含允许用户访问的呼叫类型或数字模式。可以允许不同类型的用户发出不同类型的呼叫。允许的呼叫可以位于某个国家或地区内，也可以是国际呼叫。

要授权或限制拨号，必须正确配置下列设置：

  - **拨号规则**   拨号规则定义启用 UM 的用户拨打的号码，以及将从统一消息发送并由专用交换机 (PBX) 或 IP PBX 拨打的号码。通过添加拨号规则创建拨号规则组。创建拨号规则组后，将其添加到国家/地区内或国际拨号规则组的授权呼叫列表中。

  - **拨号规则组**   拨号规则组确定拨号组内的用户可以发出的呼叫类型。

  - **拨号授权**   拨号授权用于确定为防止用户产生多余的电话费用或拨打长途电话而应用的限制。

## 如何对拨号规则组授权？

在哪里对拨号规则组授权取决于允许发出传出呼叫的呼叫者类型。例如，如果只希望 Outlook Voice Access 用户发出传出呼叫，则需要创建拨号规则，然后允许这些拨号规则组访问 Outlook Voice Access 用户链接到的 UM 邮箱策略。以下表格显示如何为不同类型的呼叫者授权呼叫。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>呼叫者类型</th>
<th>在此处授权拨号规则组</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>拨打 Outlook Voice Access 号码且未输入 PIN 的未经身份验证的呼叫者</p></td>
<td><p>UM 拨号计划。有关详细信息，请参阅<a href="authorize-calls-for-users-in-a-dial-plan-exchange-2013-help.md">拨号计划中授权用户的呼叫</a>。</p></td>
</tr>
<tr class="even">
<td><p>拨打 Outlook Voice Access 号码且已输入 PIN 的经过身份验证的呼叫者</p></td>
<td><p>呼叫者的 UM 邮箱策略。有关详细信息，请参阅<a href="authorize-calls-for-a-group-of-users-exchange-2013-help.md">授权一组用户的呼叫</a>。</p></td>
</tr>
<tr class="odd">
<td><p>拨打在 UM 自动助理中配置的电话号码的未经身份验证的呼叫者</p></td>
<td><p>UM 自动助理。有关详细信息，请参阅<a href="authorize-calls-for-auto-attendant-callers-exchange-2013-help.md">用于自动助理调用方授权调用</a>。</p></td>
</tr>
</tbody>
</table>


根据要授予发出出站呼叫权限的用户，您将使用 Exchange 管理中心 (EAC) 中拨号计划、自动助理或 UM 邮箱策略的\&quot;拨号授权\&quot;页面。

