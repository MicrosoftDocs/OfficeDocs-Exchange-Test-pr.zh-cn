---
title: '允许用户通话: Exchange 2013 Help'
TOCTitle: 允许用户通话
ms:assetid: b6e696ce-c848-475b-a598-9035677497e2
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb232172(v=EXCHG.150)
ms:contentKeyID: 51408267
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 允许用户通话

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2015-03-09_

*外拨*是用户使用 Outlook Voice Access 号码呼叫 UM 拨号计划或向内部或外部电话号码发出或转移呼叫的过程。统一消息使用许多外拨设置为用户拨打呼叫。若要配置外拨，您必须对统一消息 (UM) 拨号计划上的拨号规则、拨号规则组和拨号授权进行配置，然后对 UM 拨号计划、UM 邮箱策略和自动助理上的外拨进行授权。您还可以配置 UM 拨号计划以进行拨号或配置接入编码、国家号码前缀以及国家/地区内或国际号码格式，从而使您能够控制组织内的外拨。本主题将介绍拨号规则、拨号规则组和拨号授权，以及如何使用它们授权和控制组织的外拨。

**目录**

概述

用户类型

外拨设置

配置外拨

应用配置的拨号规则组

应用拨号规则

## 概述

在以下情况下会发生外拨：

  - 向外部电话号码发出呼叫。

  - 将呼叫转移至自动助理。

  - 将呼叫转移至组织中的用户。

  - 启用 UM 的用户使用“在电话上播放”功能。

为了使外拨能够正常运行，必须正确配置下列设置：

  - **拨号规则**   拨号规则定义由启用 UM 的用户拨打的号码和将由专用交换机 (PBX) 或 IP PBX 拨打的号码。

  - **拨号规则组**   拨号规则组确定拨号组内的用户可以发出的呼叫类型。

  - **拨号授权**   拨号授权确定的限制可用于防止用户产生多余话费或者用于限制用户拨打长途电话。

若要为向拨号计划或自动助理发出呼叫的用户启用外拨功能，您必须：

  - 确保由与拨号计划相链接的 UM IP 网关所代表的 VoIP 网关允许传出呼叫。

  - 通过在 UM 拨号计划上创建拨号规则来创建拨号规则组。

  - 在 UM 拨号计划、UM 邮箱策略或自动助理（所关联的拨号计划与 UM IP 网关相同）上添加对国家/地区内和国际拨号规则组的拨号授权。

## 用户类型

两种类型的用户可以使用统一消息中的外拨功能：通过身份验证的用户和未通过身份验证的用户。所有呼叫 UM 自动助理的用户都被视为未通过身份验证。当用户呼叫 Outlook Voice Access 号码时，他们会被视为未通过身份验证，因为他们没有提供其分机号码和 PIN，也未登录其邮箱。用户提供其分机号码和 PIN 并成功登录其邮箱后，即会通过身份验证。

当用户拨打 UM 拨号计划上配置的 Outlook Voice Access 号码并尝试在未登录邮箱的情况下发出或转移呼叫时，只有 UM 拨号计划外拨设置可应用于该呼叫。如果匿名或未通过身份验证的用户呼叫 UM 自动助理，那么在自动助理上配置的外拨设置以及在与自动助理相关联的拨号计划上配置的外拨设置都可应用于该呼叫。

当用户拨打拨号计划上配置的 Outlook Voice Access 号码并成功登录其邮箱后，即可成为通过身份验证的用户。当用户通过身份验证后，外拨呼叫设置会使用链接到这些用户的 UM 邮箱策略上的拨号规则和拨号授权设置。

返回顶部

## 外拨设置

为了对您的组织应用外拨规则，您需要配置若干设置。除了对通过正确拨号规则和拨号授权创建的 UM 拨号计划、UM 自动助理以及 UM 邮箱策略进行配置，您还需要对 UM 拨号计划上的接入编码、号码前缀和号码格式进行配置。以下是在拨号计划、自动助理和 UM 邮箱策略上配置的外拨设置：

  - 外线、国家/地区和国际接入编码

  - 国家/地区号码前缀

  - 国家/地区内号码格式和国际号码格式

  - 配置国家/地区内拨号规则组和国际拨号规则组

  - 允许国家/地区内拨号规则组和国际拨号规则组

  - 拨号规则条目

  - 拨号授权

为了使您能够对组织的外拨功能成功进行配置，您首先需要了解外拨组件的使用方式以及各组件的配置方式。下表对外拨正确运行前需要在 UM 拨号计划、UM 自动助理和 UM 邮箱策略上配置的各组件进行了介绍。

### 外拨组件

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>组件</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>拨号代码、号码前缀和号码格式</p></td>
<td><p>UM 使用拨号代码、号码前缀和号码格式来确定发出传出呼叫时要拨出的正确号码。您可以配置拨号代码、号码前缀和号码格式以限制拨打与 UM 拨号计划相关联的 UM 自动助理的用户的拨出电话，或限制拨打在拨号计划上配置的 Outlook Voice Access 号码的用户的拨出电话。</p></td>
</tr>
<tr class="even">
<td><p>拨号规则组</p></td>
<td><p>创建拨号规则组使您可以在电话号码发送至专用交换机 (PBX) 以进行拨出呼叫之前对其进行修改。拨号规则组可以删除或添加 UM 拨打的电话号码。例如，您可以创建一个拨号规则组，自动将 9 添加为某个 7 位电话号码的前缀以接入外线。在此示例中，发出拨出电话的用户不必拨 9 就可以将电话号码接到组织外部的某个人。</p>
<p>每个拨号规则组都包含拨号规则，用于确定拨号规则组内的用户可以发出的国家/地区内呼叫和国际呼叫的类型。拨号规则组适用于与 UM 拨号计划相关联的用户、或适用于与该 UM 拨号计划相关联的 UM 自动助理和 UM 邮箱策略。各拨号规则组必须包含至少一个拨号规则。</p></td>
</tr>
<tr class="odd">
<td><p>拨号规则条目</p></td>
<td><p>拨号规则用于确定拨号规则组内的用户可以发出的呼叫类型。创建拨号规则组时，可以配置一个或多个拨号规则。</p>
<p>配置各拨号规则时，您必须输入拨号规则名称、用以转换（<em>号码掩码</em>）的号码模式以及拨打的号码。还可以输入注释。注释可用于说明如何使用拨号规则，或者用于说明该拨号规则所适用的用户组。当向拨号规则添加号码掩码和拨打的号码时，您可以用字母 x 替代电话号码中的数字，例如，91425xxxxxxx。也可以使用星号 (*) 符号作为通配符，例如，91425*。</p></td>
</tr>
<tr class="even">
<td><p>拨号授权</p></td>
<td><p>拨号授权使用拨号规则组将拨号限制应用于与特定 UM 邮箱策略、拨号计划或自动助理相关联的用户。希望用户向国际/地区内的电话号码或国际电话号码发出呼叫时，也可以使用这些拨号规则组。</p>
<p>在 UM 拨号计划上创建完拨号规则之后，将该拨号规则组添加到 UM 邮箱策略、拨号计划或自动助理。将拨号规则组添加到 UM 邮箱策略后，定义的所有设置或规则都将应用于与 UM 邮箱策略相链接的启用 UM 的用户。</p></td>
</tr>
</tbody>
</table>


返回顶部

## 配置外拨

拨号规则组是在 UM 拨号计划上配置的一个或多个拨号规则的集合。可以在 UM 拨号计划上配置两种类型的拨号规则组：国家/地区内拨号规则组和国际拨号规则组。国家/地区内拨号规则组适用于在同一个国家或地区内拨打的电话号码。国际拨号规则组适用于从一个国家或地区拨打到另一个国家或地区的国际电话号码。

每个 UM 拨号计划可以包含一个或多个拨号规则组。若要将拨号规则组应用于一组用户，在创建该拨号规则组后，您必须将其添加到 UM 拨号计划、UM 自动助理和与 UM 拨号计划相关联的 UM 邮箱策略上允许的拨号规则组列表。

拨号规则组使您能够指定想要应用于属于特定类别的一组启用 UM 的用户的拨号规则。例如，您可以使用拨号规则组指定哪个用户组可以进行国际呼叫，哪个组只能进行国内或本地呼叫。您可以使用 Exchange 管理中心 (EAC) 或 命令行管理程序内的 **Set-UMDialPlan** cmdlet 创建拨号规则组。创建拨号规则组时，您必须为该拨号规则组定义至少一个拨号规则。

当用户拨打电话号码时，UM 接收该号码，并寻找匹配的拨号规则。如果找到匹配规则，UM 会通过查看该电话号码或该拨号规则**拨打的号码**部分中所列的数字来使用该拨号规则确定要拨打的号码。将拨打该拨号规则**拨打的号码**框中所列的号码。

下表给出了有关拨号规则组和拨号规则的一个示例。在此示例中，“Local-Calls-Only”和“Low-Rate”是已创建的拨号规则组。拨号规则组“Local-Calls-Only”有两个拨号规则：91425\* 和 91206\*，同时拨号规则组“Low-Rate”也有两个拨号规则：91509\* 和 91360\*。

### 拨号规则组和拨号规则

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>名称</th>
<th>号码掩码</th>
<th>拨打的号码</th>
<th>注释</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Local-Calls-Only</p></td>
<td><p>91425*</p></td>
<td><p>91*</p></td>
<td><p>本地呼叫</p></td>
</tr>
<tr class="even">
<td><p>Local-Calls-Only</p></td>
<td><p>91206*</p></td>
<td><p>91*</p></td>
<td><p>本地呼叫</p></td>
</tr>
<tr class="odd">
<td><p>Low-Rate</p></td>
<td><p>91509*</p></td>
<td><p>9*</p></td>
<td><p>国内呼叫</p></td>
</tr>
<tr class="even">
<td><p>Low-Rate</p></td>
<td><p>91360*</p></td>
<td><p>9*</p></td>
<td><p>国内呼叫</p></td>
</tr>
</tbody>
</table>


例如，当用户拨打 9-1-425-555-1234 时，UM 会拨打 4255551234。UM 会删除任何非数字字符（在此例中为连字符）并采用拨号规则中的号码掩码。在此示例中，UM 采用的号码掩码是 91\*。这表示 UM 不会拨打 9 或 1，而是会拨打电话号码中数字 1 右边出现的其他所有数字。这包括由星号 (\*) 代表的所有数字。

您可以使用 EAC 或命令行管理程序创建并配置一个或多个国家/地区内和国际拨号规则组以及拨号规则。但是，如果您要创建许多或复杂的拨号规则组和拨号规则，则可以在命令行管理程序中使用逗号分隔值 (.csv) 文件。您可以导入或导出拨号规则组和拨号规则的列表。

若要导入在 .csv 文件中定义的拨号规则组和拨号规则的列表，请运行 **Set-UMDialPlan** cmdlet，如下所示。

    Set-UMDialPlan "MyUMDialPlan" -ConfiguredInCountryOrRegionGroups $(IMPORT-CSV c:\dialrules\InCountryRegion.csv)

若要检索在 UM 拨号计划上配置的拨号规则组的列表，请运行 **Get-UMDialPlan** cmdlet，如下所示。

    (Get-UMDialPlan -id "MyUMDialPlan").ConfiguredInCountryOrRegionGroups | EXPORT-CSV C:\incountryorregion.csv

.csv 文件必须以正确的格式进行创建和保存。.csv 文件中的每一行代表一个拨号规则。但是，每个拨号规则都在同一个拨号规则组中进行配置。文件中的各个规则均有四个部分，各部分用逗号分隔。这些部分是名称、号码掩码、拨打的号码和注释。每个部分都是必需的，您必须在每个部分（除了注释部分）中输入正确的信息。文本条目与下一部分的逗号之间不应该有空格，各规则之间或末尾也不应该有空行。以下是 .csv 文件的示例，该文件可用于创建国家/地区内拨号规则组和拨号规则。

**Name,NumberMask,DialedNumber,Comment**

**Low-rate,91425xxxxxxx,9xxxxxxx,Local call**

**Low-rate,9425xxxxxxx,9xxxxxxx,Local call**

**Low-rate,9xxxxxxx,9xxxxxxx,Local call**

**Any,91\*,91\*,Open access to in-country/region numbers**

**Long-distance,91408\*,91408\*,long distance**

以下是 .csv 文件的示例，该文件可用于创建国际拨号规则组和拨号规则条目。

**Name,NumberMask,DialedNumber,Comment**

**International, 901144\*, 901144\*, international call**

**International, 901133\*, 901133\*, international call**

返回顶部

## 应用配置的拨号规则组

拨号规则组是在 UM 拨号计划上创建的。您可以使用 EAC 或命令行管理程序中的 **Set-UMDialPlan** cmdlet 创建国家/地区内拨号规则组或国际拨号规则组。在 UM 拨号计划上创建相应的拨号规则组并定义拨号规则之后，您可以根据用户访问语音邮件系统的方式，将所创建的拨号规则组应用于 UM 拨号计划、UM 自动助理或与 UM 邮箱策略相关联的用户。

您可以将在 UM 拨号计划上创建的拨号规则组应用于以下对象：

  - **同一个拨号计划** 这些设置适用于所有呼叫 Outlook Voice Access 号码但没有登录其邮箱的用户。若要将名为 `MyAllowedDialRuleGroup` 的国家/地区内拨号规则组应用于同一个拨号计划，请使用命令行管理程序的 **Set-UMDialPlan** cmdlet，如下所示。
    
        Set-UMDialPlan -Identity MyUMDialPlan -AllowedInCountryOrRegionGroups MyAllowedDialRuleGroup

  - **单个或多个 UM 邮箱策略**   在 UM 邮箱策略上配置的设置适用于与 UM 邮箱策略相链接的所有用户。在 UM 邮箱策略上配置的设置适用于呼叫 Outlook Voice Access 号码并登录其邮箱的用户。若要将名为 `MyAllowedDialRuleGroup` 的国家/地区内拨号规则组应用于单个 UM 邮箱策略，请使用 EAC 中 UM 邮箱策略上的“拨号授权”页面或使用命令行管理程序中的 **Set-UMMailboxPolicy** cmdlet，如下所示。
    
        Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -AllowedInCountryOrRegionGroups MyAllowedDialRuleGroup

  - **单个或多个与 UM 拨号计划相关联的自动助理** 这将应用于呼叫 UM 自动助理的所有用户。若要将名为 `MyAllowedDialRuleGroup` 的国家/地区内拨号规则组应用于单个 UM 自动助理，请使用 EAC 中自动助理上的“拨号授权”页面或使用命令行管理程序中的 **Set-UMAutoAttendant** cmdlet，如下所示。
    
        Set-UMAutoAttendant -Identity MyUMAutoAttendant -AllowedInCountryOrRegionGroups MyAllowedDialRuleGroup

下表总结了在统一消息中应用拨号规则组的方法。

### 应用外拨规则

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>呼叫者类型</th>
<th>作用域</th>
<th>应用的外拨设置</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook Voice Access 号码</p></td>
<td><p>用户呼叫拨号计划的 Outlook Voice Access 号码并登录邮箱</p></td>
<td><p>UM 邮箱策略</p></td>
</tr>
<tr class="even">
<td><p>匿名呼叫者</p></td>
<td><p>用户呼叫拨号计划 Outlook Voice Access 号码</p></td>
<td><p>UM 拨号计划</p></td>
</tr>
<tr class="odd">
<td><p>匿名呼叫者</p></td>
<td><p>用户呼叫自动助理引导或分机号码</p></td>
<td><p>UM 自动助理</p></td>
</tr>
<tr class="even">
<td><p>组织内部的呼叫者</p></td>
<td><p>用户呼叫“电话上播放”号码</p></td>
<td><p>UM 邮箱策略</p></td>
</tr>
</tbody>
</table>


返回顶部

## 应用拨号规则

满足下列条件时，即会发生外拨过程：

  - 统一消息向呼叫者的外部电话号码发出呼叫。

  - 统一消息将呼叫转移至自动助理。

  - 统一消息将呼叫转移至组织中的用户。

  - 启用 UM 的用户使用“在电话上播放”功能。

在每个外拨方案中，UM 会应用已配置的拨号规则，然后向该用户发出呼叫。但是，根据方案和用户发出呼叫的方式的不同，UM 可能仅将部分拨号规则应用于要拨打的电话号码。在其他外拨方案中，UM 可能会将配置的所有外拨规则应用于要拨打的电话号码。

返回顶部

