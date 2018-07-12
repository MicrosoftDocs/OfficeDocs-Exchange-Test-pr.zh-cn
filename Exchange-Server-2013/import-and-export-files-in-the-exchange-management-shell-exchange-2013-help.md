---
title: '在 Exchange 命令行管理程序中导入和导出文件: Exchange 2013 Help'
TOCTitle: 在 Exchange 命令行管理程序中导入和导出文件
ms:assetid: b4b669e8-a3aa-4b0b-ad34-f1f15d9c9369
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd638170(v=EXCHG.150)
ms:contentKeyID: 50556662
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 在 Exchange 命令行管理程序中导入和导出文件

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-03-09_

Microsoft Exchange Server 2013 使用 Windows PowerShell 命令行接口在您通过其管理 Exchange 的服务器或工作站和您正在管理的运行 Exchange 2013 的服务器之间建立远程连接。在 Exchange 2013 中，这称为远程 Exchange 命令行管理程序或远程命令行管理程序。即使您管理的是本地 Exchange 2013 服务器，也可以使用远程命令行管理程序进行连接。有关本地和远程命令行管理程序的详细信息，请参阅[将 PowerShell 与 Exchange 2013 结合使用 (Exchange Management Shell)](https://technet.microsoft.com/zh-cn/library/bb123778\(v=exchg.150\))。

在 Exchange 2013 中将文件导入 Exchange 服务器或从中导出文件的方式不同于 Exchange Server 2007 中的方式。这是因为在 Exchange 2013 中使用了远程命令行管理程序。本主题将介绍为什么需要此新过程以及如何在本地服务器或工作站和 Exchange 2013 服务器之间导入和导出文件。

## Windows PowerShell 会话

要了解为什么需要特殊语法才能在远程命令行管理程序中导入和导出文件，您需要了解如何在 Exchange 2013 中实现命令行管理程序。命令行管理程序使用 Windows PowerShell 会话，这些会话是变量、cmdlet 等可以在其中共享信息的环境。每次打开新的命令行管理程序窗口时，都会创建一个新的会话。在每个窗口中运行的 cmdlet 可以访问该窗口中存储的变量及其他信息，但无法访问其他打开的命令行管理程序窗口中的变量。这是因为这些变量分别包含在其自己的 Windows PowerShell 会话中。Windows PowerShell 会话也可以称为运行空间。

Exchange 2013 中的远程命令行管理程序包含两个会话，本地会话和远程会话。本地会话是在本地计算机上运行的 Windows PowerShell 会话。此会话包含 Windows PowerShell 附带的所有 cmdlet。它还可以访问本地文件系统。

远程会话是在远程 Windows 服务器上运行的 Exchange PowerShell 会话。此会话是所有 Exchange cmdlet 的运行位置。它可以访问 Exchange 服务器的文件系统。

在连接到远程 Exchange 服务器时，会在计算机上的本地会话与 Exchange 服务器上的远程会话之间建立连接。此连接使您可以在本地会话中的远程 Exchange 服务器上运行 Exchange cmdlet，即使本地计算机没有安装任何 Exchange cmdlet 也是如此。即使 Exchange cmdlet 表现为在本地计算机上运行，实际上是在 Exchange 服务器上运行。

> [!IMPORTANT]  
> 即使在 Exchange 2013 服务器上打开命令行管理程序，也会发生相同的连接过程并创建两个会话。这意味着必须使用相同的新语法来导入和导出文件，无论是在 Exchange 2013 服务器上还是从远程客户端工作站打开了命令行管理程序。


在远程 Exchange 服务器上的远程会话中运行的 Exchange cmdlet 不能访问本地文件系统。这意味着您无法仅靠使用 Exchange cmdlet 将文件导入到本地文件系统中或将其从中导出。需要使用其他语法将文件传输到本地文件系统或从中传输出来，以便在远程 Exchange 服务器上运行的 Exchange cmdlet 可以使用该数据。有关所需语法的详细信息，请参阅本主题后面的\&quot;在远程命令行管理程序中导入和导出文件\&quot;。

## 在远程命令行管理程序中导入和导出文件

导入和导出文件需要使用特定的语法，因为邮箱服务器和客户端访问服务器使用远程命令行管理程序，无法访问本地计算机的文件系统。

## 在远程命令行管理程序中导入文件

每当要从本地计算机或服务器将文件发送到在 Exchange 2013 服务器上运行的 cmdlet 时，都可以使用在 Exchange 2013 中导入文件的语法。从本地计算机上的文件接受数据的 cmdlet 将包含一个名为 *FileData* 的参数或类似参数。若要确定要使用的正确参数，请参阅有关使用的 cmdlet 的帮助信息。

命令行管理程序必须知道您要发送到 Exchange 2013 cmdlet 的文件以及接受数据的参数。为此，请使用以下语法。

    <Cmdlet> -FileData ([Byte[]]$(Get-Content -Path <local path to file> -Encoding Byte -ReadCount 0))

例如，以下命令将文件 C:\\MyData.dat 导入到 **Import-SomeData** 虚构 cmdlet 上的 *FileData* 参数。

    Import-SomeData -FileData (Byte[]]$(Get-Content -Path "C:\MyData.dat" -Encoding Byte -ReadCount 0))

运行该命令时将执行下列操作：

1.  远程命令行管理程序接受该命令。

2.  远程命令行管理程序对该命令求值并确定提供给 *FileData* 参数的值中存在嵌入的命令。

3.  远程命令行管理程序停止对 **Import-SomeData** 命令求值并运行 **Get-Content** 命令。**Get-Content** 命令从 MyData.dat 文件读取数据。

4.  远程命令行管理程序临时将来自 **Get-Content** 命令的数据存储为 `Byte[]` 对象，以便可以将其传递到 **Import-SomeData** cmdlet。

5.  将继续执行 **Import-SomeData** 命令。远程命令行管理程序向远程 Exchange 2013 服务器发送运行 **Import-SomeData** cmdlet 的请求以及 **Get-Content** cmdlet 创建的对象。

6.  在远程 Exchange 2013 服务器上，将运行 **Import-SomeData** cmdlet，而由 **Get-Content** cmdlet 创建的临时对象中存储的数据将传递到 *FileData* 参数。**Import-SomeData** cmdlet 处理输入并执行所需的任何操作。

某些 cmdlet 使用以下替代语法，来完成与上述语法相同的操作。

    [Byte[]]$Data = Get-Content -Path <local path to file> -Encoding Byte -ReadCount 0
    Import-SomeData -FileData $Data

使用此替代语法会出现相同的操作过程。唯一的区别是不会一次执行整个操作，从本地文件检索的数据存储在可以在创建后引用的变量中。接着将该变量用在导入命令中，以将本地文件的内容传递到 **Import-SomeData** cmdlet 中。如果您希望在多个命令中使用来自本地文件的数据，则此两步过程非常有用。

在导入文件时，有一些限制因素必须考虑。有关详细信息，请参阅本主题后面部分中的\&quot;导入文件的限制\&quot;。

有关如何将数据导入 Exchange 2013 的特定信息，请参阅有关您所管理的功能的帮助主题。

## 导入文件的限制

在远程命令行管理程序中导入数据时必须设置限制以保持转换的数据的完整性。如果正在进行的传输中断，则该传输将不能恢复。此外，由于传输的数据存储在远程服务器的内存中，必须防止服务器因数据量过大而耗尽内存。

由于这些原因，从本地计算机或服务器传输到远程 Exchange 2013 服务器的数据量有下列限制：

  - 对于每个运行的 cmdlet 为 500 MB

  - 对于传递到 cmdlet 的每个对象为 75 MB

如果超过以上任一限制，cmdlet 及其关联的管道将停止执行，并且您将收到一个错误。请参阅下表中的示例来了解这些限制如何起作用。

### 导入数据限制示例

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>对象的数目</th>
<th>对象大小 (MB)</th>
<th>总大小 (MB)</th>
<th>操作结果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>10</p></td>
<td><p>40</p></td>
<td><p>400</p></td>
<td><p>操作成功，因为各个对象的大小均未超过 75 MB，并且传递到 cmdlet 的总数据量未超过 500 MB。</p></td>
</tr>
<tr class="even">
<td><p>5</p></td>
<td><p>80</p></td>
<td><p>400</p></td>
<td><p>操作失败，因为尽管传递到 cmdlet 的总数据量只有 400 MB，但每个单个对象的大小都超过了 75 MB 的限制。</p></td>
</tr>
<tr class="odd">
<td><p>120</p></td>
<td><p>5</p></td>
<td><p>600</p></td>
<td><p>操作失败，因为尽管每个单个对象只有 5 MB，但传递到 cmdlet 的总数据量超过了 500 MB 的限制。</p></td>
</tr>
</tbody>
</table>


因为对可以在远程 Exchange 2013 服务器和本地计算机之间传输的数据量进行了大小限制，并不是所有支持导入的 cmdlet 都支持此数据传输方法。要确定特定的 cmdlet 是否支持此方法，请参阅特定 cmdlet 的帮助信息。

这些限制适合可以在 Exchange 2013 服务器上执行的大多数典型操作。如果降低这些限制，您会发现一些正常操作会失败，由于它们超过了新的限制。如果提高这些限制，正在传输的数据的传输时间会变长，而且更可能发生中断数据传输的短暂情况。并且，如果您未安装足够的内存来允许服务器存储传输期间的全部数据，则可能会耗尽远程服务器上的内存。以上每种可能性都可能导致丢失数据，因此建议您不要更改默认限制。

## 在远程命令行管理程序中导出文件

如果您要从在远程 Exchange 2013 服务器上运行的 cmdlet 接受数据并将该数据存储在本地计算机或服务器，则随时可以使用在 Exchange 2013 中导出文件的语法。提供您可以保存到本地文件中的数据的 cmdlet 将输出包含 **FileData** 属性（或类似属性）的对象。根据 cmdlet，仅对在特定情况下输出的对象填充 **FileData** 属性。若要确定要使用的正确属性以及何时使用，请参阅有关您使用的 cmdlet 的帮助信息。

命令行管理程序必须知道您要将存储在 **FileData** 属性中的数据保存到本地计算机。为此，请使用以下语法。

    <cmdlet> | ForEach { $_.FileData | Add-Content <local path to file> -Encoding Byte }

例如，以下命令导出存储在由 **Export-SomeData** 虚构 cmdlet 创建的对象上的 **FileData** 属性中的数据。导出的数据存储在您在本地计算机上指定的文件中，在此示例中为 MyData.dat。

> [!NOTE]  
> 此步骤使用 <strong>ForEach</strong> cmdlet、对象以及管道传输。有关 each 的详细信息，请参阅<a href="https://technet.microsoft.com/zh-cn/library/aa998260(v=exchg.150)">管道传输</a>和<a href="https://technet.microsoft.com/zh-cn/library/aa996386(v=exchg.150)">结构化数据</a>。


    Export-SomeData | ForEach { $_.FileData | Add-Content C:\MyData.dat -Encoding Byte }

运行该命令时将执行下列操作：

1.  远程命令行管理程序接受该命令。

2.  远程命令行管理程序在远程 Exchange 2013 服务器上调用 **Export-SomeData** cmdlet。

3.  由 **Export-SomeData** cmdlet 创建的输出对象通过管道传递回本地命令行管理程序会话。

4.  该输出对象接着通过管道传递到 **ForEach** cmdlet，其中包含一个脚本块。

5.  在脚本块中，将访问管道中当前对象上的 **FileData** 属性。**FileData** 属性中包含的数据通过管道传递到 **Add-Content** cmdlet。

6.  **Add-Content** cmdlet 保存从 **FileData** 属性通过管道传递到本地文件系统上的 MyData.dat 文件的数据。

有关如何从 Exchange 2013 导出数据的特定信息，请参阅有关您所管理的功能的帮助主题。

