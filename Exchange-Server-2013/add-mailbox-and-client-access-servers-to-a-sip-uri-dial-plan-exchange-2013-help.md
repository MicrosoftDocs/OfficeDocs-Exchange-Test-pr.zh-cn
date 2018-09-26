---
title: '将邮箱服务器和客户端访问服务器添加到 SIP URI 的拨号计划: Exchange 2013 Help'
TOCTitle: 将邮箱服务器和客户端访问服务器添加到 SIP URI 的拨号计划
ms:assetid: 17fed308-ff0d-4e61-b9f9-e6680b6eccaa
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa996399(v=EXCHG.150)
ms:contentKeyID: 52061483
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 将邮箱服务器和客户端访问服务器添加到 SIP URI 的拨号计划

 

_**适用于：** Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2013-04-16_

您可以添加客户端访问和邮箱服务器 SIP URI 拨号计划。客户端访问和邮箱服务器不能与电话分机或 E.164 拨号计划相关联，但服务器将应答所有传入呼叫。

如果要部署 Microsoft Lync Server，以便让出站呼叫能正常工作，您必须手动将所有客户端访问服务器和邮箱服务器添加到所有为 Lync Server 创建的 SIP URI 拨号计划。

有关与 UM 拨号计划相关的其他管理任务，请参阅 [UM 拨号计划过程](um-dial-plan-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：小于 1 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 拨号计划\&quot;条目。

  - 在执行这些步骤之前，请确认已创建了 SIP URI 的拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](https://technet.microsoft.com/zh-cn/library/bb123819(v=exchg.150))。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 使用 EAC 将邮箱服务器添加到 SIP URI 拨号计划

1.  在 EAC 中，导航到\&quot;服务器\&quot;\>\&quot;服务器\&quot;。

2.  在列表视图中，选择要修改的邮箱服务器，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在\&quot;Exchange 服务器\&quot;页面上，单击\&quot;统一消息\&quot;。

4.  在\&quot;UM 服务设置\&quot;\>\&quot;关联的拨号计划\&quot;下，单击\&quot;添加\&quot;![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。

5.  在\&quot;选择 UM 拨号计划\&quot;窗口中，选择 SIP URI 拨号计划，单击\&quot;添加\&quot;，单击\&quot;确定\&quot;，然后单击\&quot;保存\&quot;。

## 使用命令行管理程序将邮箱服务器添加到 SIP URI 拨号计划

本示例添加邮箱服务器名为`MyMailboxServer`到名为`MySIPDialPlan`的 SIP URI 拨号计划，防止其接受新的呼叫。它也为双模式，从而使邮箱服务器接受 TCP 和 TLS 请求设置的启动模式。

```powershell
    Set-UMService -Identity MyMailboxServer -DialPlans MySIPDialPlan -Status Disabled -UMStartupMode Dual
```

此示例将名为 `MyMailboxServer` 的邮箱服务器添加到名为 `MySIPDialPlan` 和 `MySIPDialPlan2` 的两个 SIP 拨号计划，并进行了以下设置：

  - 允许 IPv4 和 IPv6 地址。

  - 将最大传入呼叫数设置为 50。

  - 为 Lync Server 配置 SIP 访问服务。

<!-- end list -->

```powershell
    Set-UMService -Identity MyMailboxServer -DialPlans MySIPDialPlan, MySIPDialPlan2 -IPAddressFamily Any -MaxCallsAllowed 50 -SipAccessService northamerica.lyncpoolna.contoso.com
```

## 使用 EAC 将客户端访问服务器添加到 SIP URI 拨号计划

1.  在 EAC 中，导航到\&quot;服务器\&quot;\>\&quot;服务器\&quot;。

2.  在此列表视图中，选择您要修改的客户端访问服务器，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在\&quot;Exchange 服务器\&quot;页面上，单击\&quot;统一消息\&quot;。

4.  在\&quot;UM 呼叫路由器设置\&quot;\>\&quot;关联的拨号计划\&quot;下，单击\&quot;添加\&quot;![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。

5.  在\&quot;选择 UM 拨号计划\&quot;窗口中，选择 SIP URI 拨号计划，单击\&quot;添加\&quot;，单击\&quot;确定\&quot;，然后单击\&quot;保存\&quot;。

## 使用命令行管理程序将客户端访问服务器添加到 SIP URI 拨号计划

本示例将名为`MyClientAccessServer`到名为`MySIPDialPlan`的 SIP URI 拨号计划的客户端访问服务器。它也为双模式，允许客户端访问服务器接受 TCP 和 TLS 请求设置的启动模式。

```powershell
Set-UMCallRouterSettings -DialPlans MySIPDialPlan -Server MyClientAccessServer -UMStartupMode Dual
```

此示例将名为 `MyClientAccessServer` 的客户端访问服务器添加到名为 `MySIPDialPlan` 和 `MySIPDialPlan2` 的两个 SIP 拨号计划，并允许服务器使用 IPv4 和 IPv6 地址。

```powershell
    Set-UMCallRouterSettings -DialPlans MySIPDialPlan, MySIPDialPlan2 -IPAddressFamily Any -Server MyClientAccessServer
```
