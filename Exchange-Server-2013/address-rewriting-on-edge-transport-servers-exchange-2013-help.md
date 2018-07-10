---
title: '边缘传输服务器上的地址重写: Exchange 2013 Help'
TOCTitle: 边缘传输服务器上的地址重写
ms:assetid: 23f1eaf6-247a-4671-ad72-aae19d9b511d
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa996806(v=EXCHG.150)
ms:contentKeyID: 61060575
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 边缘传输服务器上的地址重写

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-03-09_

地址重写修改通过边缘传输服务器进入或离开组织的邮件中的发件人和收件人电子邮件地址。边缘传输服务器上的两个传输代理提供重写功能：地址重写入站代理和地址重写出站代理。对出站邮件进行地址重写的主要原因是为了向外部收件人提供一个一致的电子邮件域。对入站邮件进行地址重写的主要原因是为了向正确的收件人传递邮件。

您创建的地址重写条目指定了内部地址（要更改的电子邮件地址）和外部地址（所需的最终电子邮件地址）。您可以指定是在入站和出站邮件中对电子邮件地址进行重写，还是仅在出站邮件中对电子邮件地址进行重写。您可以为单个用户（chris@contoso.com 至 support@contoso.com）、单一域（contoso.com 至 fabrikam.com）中的所有用户、或者含有例外的多个子域（\*.fabrikam.com 至 contoso.com，legal.fabrikam.com 除外）中的用户创建地址写入条目。

> [!important]
> 不论您打算如何使用地址重写，都需要验证所生成的电子邮件地址在您的组织中是否具有唯一性，这样便可以避免重复。这是因为地址重写不会验证重写的电子邮件地址的唯一性。


**目录**

地址重写情景

通过地址重写修改的邮件属性

地址重写不更改的内容

仅出站地址重写的注意事项

入站和出站地址重写的注意事项

重写多个域中的电子邮件地址的注意事项

地址重写条目的优先级

数字签名、加密和受权限保护的邮件

## 地址重写情景

下面介绍了有关如何使用地址重写的示例情景：

  - **组合并**   某些组织将其内部业务划分成基于业务或技术要求的单独域。此配置会让电子邮件看起来好像来自不同的组，甚至来自不同的组织。
    
    下面的示例展示了一个名为 Contoso, Ltd. 的组织如何隐藏其内部子域，使其不对外部收件人可见：
    
      - 从 northamerica.contoso.com、europe.contoso.com 和 asia.contoso.com 域发送的出站邮件在经过重写后看起来好像全都来自同一个 contoso.com 域。通过在整个组织和 Internet 之间提供 SMTP 连接的边缘传输服务器后，所有邮件都会被重写。
    
      - 向 contoso.com 收件人发送的入站邮件由边缘传输服务器中继到邮箱服务器。该邮件根据收件人邮箱上配置的代理地址传递到正确的收件人。

  - **合并与收购**   虽然被收购的公司可能会作为独立的企业继续运营下去，但您可以使用地址重写使两个组织看起来好像是同一个完整的组织。
    
    下面的示例展示了 Contoso, Ltd. 如何隐藏刚收购的公司 Fourth Coffee 的电子邮件域：
    
      - Contoso, Ltd. 希望使从 Fourth Coffee 的 Exchange 组织发送的所有出站邮件看起来好像全都来自 contoso.com。从这两个组织发送的所有邮件都通过 Contoso, Ltd. 的边缘传输服务器进行发送，电子邮件在该服务器上从 *user*@fourthcoffee.com 重写为 *user*@contoso.com。
    
      - 向 *user*@contoso.com 发送的入站邮件经重写并路由至 *user*@fourthcoffee.com 邮箱。向 *user*@fourthcoffee.com 发送的入站邮件直接路由至 Fourth Coffee 的电子邮件服务器。

  - **合作伙伴**   很多组织都使用外部合作伙伴来为其客户、其他组织或组织自身提供服务。为了避免发生混淆，组织可能用自己的电子邮件域替换合作伙伴组织的电子邮件域。
    
    下面的示例展示了 Contoso, Ltd. 如何隐藏合作伙伴的电子邮件域：
    
      - Contoso 公司为更大的 Wingtip Toys 组织提供支持。Wingtip Toys 希望为其客户带来统一的电子邮件体验，因此要求由 Contoso, Ltd. 的支持人员发送的所有邮件看起来好像全都发送自 Wingtip Toys。与 Wingtip Toys 相关的所有出站邮件均通过其边缘传输服务器发送，因此所有 contoso.com 电子邮件地址都会重写为 wingtiptoys.com 电子邮件地址。
    
      - 向 support@wingtiptoys.com 发送的入站邮件由 Wingtip Toys 的边缘传输服务器接受、重写并路由至 support@contoso.com 电子邮件地址。

返回顶部

## 通过地址重写修改的邮件属性

标准 SMTP 电子邮件由邮件信封 和邮件内容组成。邮件信封包含在 SMTP 邮件服务器之间传输和传递邮件所需的信息。邮件内容包含邮件头字段（统称为邮件头）和邮件正文。RFC 2821 中介绍了邮件信封，RFC 2822 中介绍了邮件头。

当发件人撰写并提交电子邮件以进行传递时，该邮件包含符合 SMTP 标准所需的基本信息，例如发件人、收件人、邮件撰写日期和时间、主题行（可选）以及邮件正文（可选）。此类信息包含在邮件自身中；根据定义，也包含在邮件头中。

发件人的邮件服务器使用在邮件头中找到的发件人和收件人信息生成邮件的邮件信封。然后，它将该邮件传输至 Internet 以传递至收件人的邮件服务器。收件人从不会看到邮件信封，因为它是由邮件传输过程生成，实际上并不是邮件的组成部分。

地址重写通过重写邮件头或邮件信封中的特定字段更改电子邮件地址。地址重写更改出站邮件中的多个字段，但只更改入站电子邮件中的一个字段。下表展示了出站和入站邮件中被重写的 SMTP 头字段。

### 出站和入站邮件中被重写的邮件字段

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>字段名</th>
<th>位置</th>
<th>出站邮件</th>
<th>入站邮件</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>MAIL FROM</strong></p></td>
<td><p>邮件信封</p></td>
<td><p>重写</p></td>
<td><p>不重写</p></td>
</tr>
<tr class="even">
<td><p><strong>RCPT TO</strong></p></td>
<td><p>邮件信封</p></td>
<td><p>不重写</p></td>
<td><p>重写</p></td>
</tr>
<tr class="odd">
<td><p><strong>To</strong></p></td>
<td><p>邮件头</p></td>
<td><p>重写</p></td>
<td><p>不重写</p></td>
</tr>
<tr class="even">
<td><p><strong>Cc</strong></p></td>
<td><p>邮件头</p></td>
<td><p>重写</p></td>
<td><p>不重写</p></td>
</tr>
<tr class="odd">
<td><p><strong>From</strong></p></td>
<td><p>邮件头</p></td>
<td><p>重写</p></td>
<td><p>不重写</p></td>
</tr>
<tr class="even">
<td><p><strong>Sender</strong></p></td>
<td><p>邮件头</p></td>
<td><p>重写</p></td>
<td><p>不重写</p></td>
</tr>
<tr class="odd">
<td><p><strong>Reply-To</strong></p></td>
<td><p>邮件头</p></td>
<td><p>重写</p></td>
<td><p>不重写</p></td>
</tr>
<tr class="even">
<td><p><strong>Return-Receipt-To</strong></p></td>
<td><p>邮件头</p></td>
<td><p>重写</p></td>
<td><p>不重写</p></td>
</tr>
<tr class="odd">
<td><p><strong>Disposition-Notification-To</strong></p></td>
<td><p>邮件头</p></td>
<td><p>重写</p></td>
<td><p>不重写</p></td>
</tr>
<tr class="even">
<td><p><strong>Resent-From</strong></p></td>
<td><p>邮件头</p></td>
<td><p>重写</p></td>
<td><p>不重写</p></td>
</tr>
<tr class="odd">
<td><p><strong>Resent-Sender</strong></p></td>
<td><p>邮件头</p></td>
<td><p>重写</p></td>
<td><p>不重写</p></td>
</tr>
</tbody>
</table>


返回顶部

## 地址重写不更改的内容

地址重写不修改可破坏 SMTP 功能的任何邮件头字段。例如，修改某些头字段可能会影响路由循环检测、使签名无效或者使受权限保护的邮件不可读。因此，地址重写不会修改以下头字段。

  - **Return-Path**

  - **Received**

  - **Message-ID**

  - **X-MS-TNEF-Correlator**

  - **Content-Type Boundary=string**

  - MIME 正文部分内的头字段

地址重写忽略不受 Exchange 组织控制的域。也就是说，地址重写不会重写包含 Exchange 组织对其不是权威组织的域的头字段。重写此类域会导致失控的邮件中继形式。

地址重写也不会修改其他邮件的嵌入邮件的头字段。发件人和收件人希望只要邮件不触发发件人和收件人之间所实现的传输规则，嵌入邮件就保持完好，在不被修改的情况下进行传递。

返回顶部

## 仅出站地址重写的注意事项

边缘传输服务器上的仅出站地址重写可在邮件离开 Exchange 组织时修改发件人的电子邮件地址。您可以为单个用户（chris@contoso.com 至 support@contoso.com）或单个域（contoso.com 至 fabrikam.com）中的所有用户配置仅出站地址重写。您必须为多个子域（\*.fabrikam.com 至 .contoso.com）中的用户配置仅出站地址重写。

必须将重写的电子邮件地址配置为受影响的收件人的代理地址。例如，如果将 laura@sales.contoso.com 重写为 laura@contoso.com，则必须在 Laura 的邮箱中配置代理地址 laura@contoso.com。这样，答复和入站邮件便可以正确传递。

返回顶部

## 入站和出站地址重写的注意事项

边缘传输服务器上的入站和出站或双向地址重写可以修改离开 Exchange 组织的邮件的发件人电子邮件地址，也可以修改进入 Exchange 组织的邮件的收件人电子邮件地址。

您可以为单个用户（chris@contoso.com 至 support@contoso.com）或单个域（contoso.com 至 fabrikam.com）中的所有用户配置仅出站地址重写。您不能为多个子域（\*.fabrikam.com 至 .contoso.com）中的用户配置双向地址重写。

返回顶部

## 重写多个域中的电子邮件地址的注意事项

当您将多个内部域或子域合并到一个单独的外部域时，需要考虑以下因素：

  - **验证别名的唯一性**   所有电子邮件别名（@ 符号左边的部分）必须在所有子域中都具有唯一性。例如，如果有 joe@sales.contoso.com，就不能有 joe@marketing.contoso.com，因为对这两个用户的重写的电子邮件地址为 joe@contoso.com。

  - **添加代理地址**   必须将重写的电子邮件地址配置为受影响的域中所有受影响的发件人的代理地址。例如，如果 joe@sales.contoso.com 重写为 joe@contoso.com，那么您需要向 Joe 的邮箱添加代理地址 joe@contoso.com。这样，答复和入站邮件便可以正确传递。

  - **非 Exchange 组织的邮件联系人**   如果您要重写来自非 Exchange 电子邮件系统的电子邮件地址，则需要在 Exchange 中创建电子邮件联系人来表示非 Exchange 电子邮件系统中的用户。此类电子邮件联系人必须包含原始电子邮件地址和重写的电子邮件地址。例如，如果 joe@unix.contoso.com 重写为 joe@contoso.com，您需要创建一个将 joe@unix.contoso.com 用作外部电子邮件地址，并将 joe@contoso.com 用作代理地址的邮件联系人。

## 验证别名的唯一性

在重写多个子域中的电子邮件地址时，您需要确保所有电子邮件别名在所有子域中都具有唯一性。为举例说明，请考虑以下配置：

以下用户分别位于 sales.contoso.com、marketing.contoso.com 和 research.contoso.com 子域中：

  - maria@sales.contoso.com

  - chris@sales.contoso.com

  - david@marketing.contoso.com

  - brian@marketing.contoso.com

  - chris@research.contoso.com

  - adam@research.contoso.com

假设您想将子域 sales.contoso.com、marketing.contoso.com 和 research.contoso.com 重写到单个域 contoso.com 中。

在每个子域中的电子邮件地址重写后，chris@sales.contoso.com 和 chris@research.contoso.com 会发生冲突，因为这两个电子邮件地址均重写为 chris@contoso.com。若要解决此冲突，您需要更改其中一位受影响的收件人的电子邮件地址。例如，您可以将 chris@research.contoso.com 更改为 christopher@research.contoso.com，这样该电子邮件地址就会重写为 christopher@contoso.com。

返回顶部

## 地址重写条目的优先级

如果用户的电子邮件地址匹配多个地址重写条目，则该电子邮件地址只会根据最近似匹配重写一次。下面的列表按照从最高到最低优先级的顺序介绍了地址重写条目的优先级顺序：

1.  **个人电子邮件地址**   地址重写条目配置为将 john@contoso.com 电子邮件地址重写为 support@contoso.com。

2.  **域或子域映射**   地址重写条目配置为将所有 contoso.com 电子邮件地址重写为 northwindtraders.com，或将所有 sales.contoso.com 电子邮件地址重写为 contoso.com。

3.  **域合并**   地址重写条目配置为将 \*.contoso.com 电子邮件地址重写为 contoso.com。

例如，假设边缘传输服务器配置了以下出站地址重写条目：

  - 将 \*.contoso.com 电子邮件地址重写为 contoso.com

  - 将 japan.sales.contoso.com 电子邮件地址重写为 contoso.jp

如果 masato@japan.sales.contoso.com 发送了一封电子邮件，那么该地址会重写为 masato@contoso.jp，因为该条目最匹配发件人的电子邮件地址。

返回顶部

## 数字签名、加密和受权限保护的邮件

地址重写不应影响大多数签名、加密或受权限保护的邮件。如果地址重写会以任何方式使这些类型的邮件的安全状态无效或发生变化，那么地址重写将不适用。

下面的值可以重写，因为此类信息不属于邮件签名、加密或权限保护：

  - 邮件信封中的字段

  - 顶级邮件正文头

下面的值不可以重写，因为此类信息属于邮件签名、加密或权限保护：

  - 可能经签名的 MIME 正文部分内的头字段

  - MIME 内容类型的边界字符串参数

返回顶部

