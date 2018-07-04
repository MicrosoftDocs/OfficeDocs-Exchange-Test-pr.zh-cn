---
title: '创建用户的拨号规则: Exchange Online Help'
TOCTitle: 创建用户的拨号规则
ms:assetid: c11e3d62-3eb1-4d7e-8741-9bede593e2df
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ898502(v=EXCHG.150)
ms:contentKeyID: 51408273
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 创建用户的拨号规则

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2015-03-09_

拨号规则组包括拨号规则条目。拨号规则用于修改之前将其发送到内部电话系统 (PBX) 或者 IP PBX 用于拨出呼叫的电话号码。拨号规则有两个用途 ︰

  - 它们指定可以拨出电话的拨打号码。当您创建拨号规则时，则指定可以拨打的数字格式。任意数量不匹配您指定的格式之一将被拒绝。如果您不设定任何拨号规则，调用方可以呼叫您的组织内，但不能进行任何传出调用。

  - 他们将拨发送到内部电话系统之前的数字。拨号规则可以去除从数字或拨打的号码添加数字。例如，可以使用拨号规则添加外线接入编码电话系统也可以添加或移除远程或本地号码的国家/地区代码。

若要指定您想要允许为 UM 拨号计划拨出呼叫类型，请使用拨号规则创建拨号规则组，并使用它们来授权为 Outlook Voice Access 用户和拨入 UM 自动助理的调用方打出的电话。创建单独的拨号规则组的国家/地区和国际电话。

> [!NOTE]
> 如果您正在集成 UM 和 Microsoft Lync Server，我们建议您创建至少一个拨号规则组并对 SIP URI 拨号计划、UM 邮箱策略和 UM 自动助理上的拨号规则组进行授权以允许所有传出呼叫转移至 Lync Server。


有关外拨的其他管理任务，请参阅[允许用户进行调用过程](allowing-users-to-make-calls-procedures-exchange-2013-help.md)。

## 常用拨号规则的示例


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>号码模式</strong></p></td>
<td><p><strong>拨打的号码</strong></p></td>
<td><p><strong>何时使用此拨号规则？</strong></p></td>
</tr>
<tr class="even">
<td><p>*</p></td>
<td><p>*</p></td>
<td><p>允许所有传出呼叫。</p></td>
</tr>
<tr class="odd">
<td><p>1425xxxxxxx</p></td>
<td><p>91425xxxxxxx</p></td>
<td><p>防止用户在忘记拨打外线接入编码时接入到内部分机号码或出现错误。</p></td>
</tr>
<tr class="even">
<td><p>1xxxxxxxxxx</p></td>
<td><p>1xxxxxxxxxx</p></td>
<td><p>允许以 1 开头的所有号码。</p></td>
</tr>
<tr class="odd">
<td><p>xxxxxxx</p></td>
<td><p>1425xxxxxxx</p></td>
<td><p>向 7 位数的号码添加 1 和本地区域代码 425。</p></td>
</tr>
</tbody>
</table>


## 在开始之前，您需要知道什么？

  - 估计完成时间 ︰ 少于 3 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 拨号计划\&quot;条目。

  - 在执行这些步骤之前，先确认已创建 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

  - 如果要将拨号规则组为 UM 邮箱策略，您需要确认已创建 UM 邮箱策略。有关详细步骤，请参阅[创建 UM 邮箱策略](create-a-um-mailbox-policy-exchange-2013-help.md)。

  - 如果要将拨号规则组到 UM 自动助理，您需要确认已创建 UM 自动助理。有关详细步骤，请参阅[创建 UM 自动助理](create-a-um-auto-attendant-exchange-2013-help.md)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!tip]
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 使用 EAC 创建拨号规则

1.  在 EAC 中，导航到\&quot;统一消息\&quot;\>\&quot;UM 拨号计划\&quot;。在此列表视图中，选择您要更改的 UM 拨号计划，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

2.  在\&quot;UM 拨号计划\&quot;页上，单击\&quot;配置\&quot;。

3.  在\&quot;UM 拨号计划\&quot;页面 \>\&quot;拨号规则\&quot;上，单击\&quot;国家/地区内拨号规则\&quot;或\&quot;国际拨号规则\&quot;下的\&quot;添加\&quot;![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。

4.  在\&quot;新建拨号规则\&quot;页面上，输入以下信息：
    
      - **拨号规则名称**  输入的名称拨号规则组此规则的一部分。若要将其与其他规则结合，使用相同的组名。若要创建新的拨号规则组，请输入新的唯一名称。
    
      - **要转换 （数字掩码） 的数字模式**  输入转换前，例如，91425xxxxxxx 的数字模式。如果呼叫者拨叫号码相匹配时，UM 将其转换到拨叫的号码拨打电话之前。请输入仅包含数字和通配符 (x)。号码的模式也被称为*数字掩码*。
    
      - **Dialed 号**输入要拨打的号码。仅使用数字和通配符 (x)，如下所示数字模式 9xxxxxxx。通配符 (x) 会替换为从原来的号码，用户拨入的数字。确保拨叫的号码中的通配符的数数中的数字模式的通配符相同。
    
      - **注释**输入的注释或说明此拨号规则。您可以使用注释来描述规则作用，例如，"添加 a 9 到拨出电话。"

5.  单击**确定**以保存拨号规则。您可以继续输入规则，使用您要授权在一起的规则相同的拨号规则组名称。

