---
title: '需要重新启动计算机才能继续安装: Exchange 2013 Help'
TOCTitle: 需要重新启动计算机才能继续安装
ms:assetid: f2d8e504-18c1-4b86-9b97-7654d0391b19
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/ms.exch.setupreadiness.pendingrebootwindowscomponents(v=EXCHG.150)
ms:contentKeyID: 50491973
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 需要重新启动计算机才能继续安装

 

_**适用于：**Exchange Server_

_**上一次修改主题：**2016-12-09_

Microsoft Exchange Server 2013 不能继续安装，因为检测到本地计算机需要重启，才能完成其他程序或 Windows 更新的安装。

## 这是什么原因？

当安装程序和 Windows 更新时，它们会对存储在您的计算机中的文件进行更改。在安装期间，有时程序或 Windows 更新需要对正在使用的文件进行更改。发生这种情况时，您需要重新启动计算机，然后才能安装任何其他程序，如 Exchange 2013。Exchange 安装程序要求所有其他安装都已完成，以便验证已安装正常工作所需的所有必备组件。

有时，以前的某个程序或 Windows 更新的安装可能无法成功完成。发生这种情况时，它会丢弃使 Windows 和其他程序认为需要重新启动的更改。遗憾的是，因为安装失败永远不会清理这些更改，安装 Windows 更新和其他程序可能会受到阻止。如果发生这种情况，每次运行 Exchange 安装程序时都会看到此错误。

## 如何解决这个问题？

在大多数情况下，只需重新启动计算机即可跳过此错误。但是，有时即使您已重新启动计算机，仍可能会收到此错误。当程序或 Windows 更新安装需要进行其他更改，并且这些更改还需要重新启动计算机时，可能会发生这种情况。如果您在重新启动计算机后看到此错误，请再次尝试重新启动。

如果您已重新启动计算机超过两次或三次，但仍看到此错误，请尝试并重新安装您最近安装的任何程序或 Windows 更新。这可能会使失败的安装成功完成。

如果您在重新启动计算机并重新安装任何最近的程序或 Windows 更新之后，您*仍*收到此错误，我们建议您与 Microsoft 支持部门联系。他们将帮助您查找 Windows 和其他程序认为您的计算机需要重新启动的原因。要与 Microsoft 支持部门联系，请转到 [Microsoft Exchange Server 的支持](https://go.microsoft.com/fwlink/p/?linkid=525940)。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876845.Caution(EXCHG.150).gif" title="小心" alt="小心" />小心：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>我们强烈建议您不要尝试通过手动删除或更改 Windows 注册表中的键或值来解决此问题，尽管此操作很容易执行。虽然这样做可能会立即解决此问题，但以后可能导致问题。如果安装失败的是 Windows 更新，这一点尤其重要。</td>
</tr>
</tbody>
</table>

