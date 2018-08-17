---
title: '使用命令输出: Exchange 2013 Help'
TOCTitle: 使用命令输出
ms:assetid: 8320e1a5-d3f5-4615-878d-b23e2aaa6b1e
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb123533(v=EXCHG.150)
ms:contentKeyID: 50490943
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 使用命令输出

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-03-09_

Exchange 命令行管理程序提供了可用来设置命令输出格式的多种方法。本主题介绍以下内容：

  - How to format data：如何使用 **Format-List**、**Format-Table** 和 **Format-Wide** cmdlet 控制数据的显示格式。

  - How to output data：使用 **Out-Host** 和 **Out-File** cmdlet 确定是将数据输出到命令行管理程序控制台窗口，还是输出到文件。本主题中包含的示例脚本是将数据输出到 MicrosoftInternet Explorer。

  - How to filter data：使用以下筛选方法之一来筛选数据：
    
      - 服务器端筛选，在某些 cmdlet 中可用。
    
      - 客户端筛选，在所有 cmdlet 中可用，方法是将命令结果通过管道传递给 **Where-Object** cmdlet。

若要使用本主题介绍的功能，必须了解以下概念：

  - [管道传输](https://technet.microsoft.com/zh-cn/library/aa998260\(v=exchg.150\))

  - [命令行管理程序变量](https://technet.microsoft.com/zh-cn/library/bb124036\(v=exchg.150\))

  - [比较运算符](https://technet.microsoft.com/zh-cn/library/bb125229\(v=exchg.150\))

## 如何设置数据格式

如果在管道末端调用格式设置 cmdlet，则可以覆盖默认格式，以控制显示的数据和数据显示方式。格式设置 cmdlet 有 **Format-List**、**Format-Table** 和 **Format-Wide**。每一个 cmdlet 都有其不同于其他格式设置 cmdlet 的输出样式。

## Format-List

**Format-List** cmdlet 接受来自管道的输入并将每个对象的所有指定属性以垂直列表格式输出。可以使用 *Property* 参数指定要显示的属性。如果调用 **Format-List** cmdlet 而未指定任何参数，则将输出所有属性。**Format-List** cmdlet 会自动换行，而不是截断行。**Format-List** cmdlet 的最佳用途之一就是覆盖某个 cmdlet 的默认输出，以便检索其他信息或更受关注的信息。

例如，调用 **Get-Mailbox** cmdlet 时，看到的只是以表格格式显示的有限信息量。如果将 **Get-Mailbox** cmdlet 的输出通过管道传递给 **Format-List** cmdlet，并添加针对需要查看的其他信息或更受关注信息的参数，则可检索所需的输出。

还可以使用通配符\&quot;\*\&quot;指定部分属性名。如果包含通配符，则可以匹配多个属性，而不必分别键入每个属性名。例如，`Get-Mailbox | Format-List -Property Email* ` 返回以 `Email` 开头的所有属性。

以下示例显示用不同方式查看 **Get-Mailbox** cmdlet 返回的相同数据。

    Get-Mailbox TestUser1
    
    Name                      Alias                ServerName       ProhibitSendQuo
                                                                    ta
    ----                      -----                ----------       ---------------
    TestUser1                 TestUser1            mbx              unlimited

在第一个示例中，调用 **Get-Mailbox** cmdlet 但未指定格式，因此，默认输出为表格格式并包含一组预定义的属性。

    Get-Mailbox TestUser1 | Format-List -Property Name,Alias,EmailAddresses
    
    Name           : TestUser1
    Alias          : TestUser1
    EmailAddresses : {SMTP:TestUser1@contoso.com}

在第二个示例中，将 **Get-Mailbox** cmdlet 的输出连同其特定属性通过管道传递给 **Format-List** cmdlet。可以看到，输出的格式和内容有明显不同。

    Get-Mailbox TestUser1 | Format-List -Property Name, Alias, Email*
    Name                      : Test User
    Alias                     : TestUser1
    EmailAddresses            : {SMTP:TestUser1@contoso.com}
    EmailAddressPolicyEnabled : True

在最后一个示例中，与第二个示例相同，将 **Get-Mailbox** cmdlet 的输出通过管道传递给了 **Format-List** cmdlet。但是，在最后一个示例中，使用通配符来匹配以 `Email` 开头的所有属性。

如果有多个对象传递到 **Format-List** cmdlet，则为每个对象指定的所有属性都将显示并按对象进行分组。显示顺序取决于该 cmdlet 的默认参数。默认参数通常是 *Name* 参数或 *Identity* 参数。例如，调用 **Get-Childitem** cmdlet 时，默认显示顺序是文件名按字母顺序排列。若要更改此行为，必须调用 **Format-List** cmdlet 和 *GroupBy* 参数，以及要按其对输出进行分组的属性值名称。例如，以下命令将列出目录中的所有文件，并将这些文件按文件扩展名进行分组。

    Get-Childitem | Format-List Name,Length -GroupBy Extension
    
        Extension: .xml
    
    Name   : Config_01.xml
    Length : 5627
    
    Name   : Config_02.xml
    Length : 3901
    
    
        Extension: .bmp
    
    Name   : Image_01.bmp
    Length : 746550
    
    Name   : Image_02.bmp
    Length : 746550
    
    
        Extension: .txt
    
    Name   : Text_01.txt
    Length : 16822
    
    Name   : Text_02.txt
    Length : 9835

在本示例中，**Format-List** cmdlet 已按 *GroupBy* 参数指定的 *Extension* 属性对项目进行了分组。可以将 *GroupBy* 参数与管道流中对象的任一有效属性结合使用。

## Format-Table

可以使用 **Format-Table** cmdlet 以表格格式显示项目，其中包含标签标题和属性数据列。默认情况下，许多 cmdlet（如 **Get-Process** 和 **Get-Service** cmdlet）都使用表格格式输出。**Format-Table** cmdlet 的参数包括 *Properties* 和 *GroupBy* 参数。这些参数的作用与其在 **Format-List** cmdlet 中的作用完全相同。

**Format-Table** cmdlet 还使用 *Wrap* 参数。此参数可以完全显示较长的属性信息行，不会在行的末尾截断。若要了解如何使用 *Wrap* 参数显示返回的信息，请比较以下两个示例中 **Get-Command** 命令的输出。

在第一个示例中，使用 **Get-Command** cmdlet 显示有关 **Get-Process** cmdlet 的命令信息时，*Definition* 属性的信息被截断。

    Get-Command Get-Process | Format-Table Name,Definition
    
    Name                                    Definition
    ----                                    ----------
    get-process                             get-process [[-ProcessName] String[]...

在第二个示例中，命令中添加了 *Wrap* 参数，以强制显示 *Definition* 属性的完整内容。

    Get-Command Get-Process | Format-Table Name,Definition -Wrap
    
    Get-Process                             Get-Process [[-Name] <String[]>] [-Comp
                                            uterName <String[]>] [-Module] [-FileVe
                                            rsionInfo] [-Verbose] [-Debug] [-ErrorA
                                            ction <ActionPreference>] [-WarningActi
                                            on <ActionPreference>] [-ErrorVariable
                                            <String>] [-WarningVariable <String>] [
                                            -OutVariable <String>] [-OutBuffer <Int
                                            32>]
                                            Get-Process -Id <Int32[]> [-ComputerNam
                                            e <String[]>] [-Module] [-FileVersionIn
                                            fo] [-Verbose] [-Debug] [-ErrorAction <
                                            ActionPreference>] [-WarningAction <Act
                                            ionPreference>] [-ErrorVariable <String
                                            >] [-WarningVariable <String>] [-OutVar
                                            iable <String>] [-OutBuffer <Int32>]
                                            Get-Process [-ComputerName <String[]>]
                                            [-Module] [-FileVersionInfo] -InputObje
                                            ct <Process[]> [-Verbose] [-Debug] [-Er
                                            rorAction <ActionPreference>] [-Warning
                                            Action <ActionPreference>] [-ErrorVaria
                                            ble <String>] [-WarningVariable <String
                                            >] [-OutVariable <String>] [-OutBuffer
                                            <Int32>]

与在 **Format-List** cmdlet 中使用时相同，也可以使用通配符\&quot;`*`\&quot;指定部分属性名。通过包含通配符，可以匹配多个属性，而不必分别键入每个属性名。

## Format-Wide

**Format-Wide** cmdlet 提供比其他格式 cmdlet 都更简单的输出控制。默认情况下，**Format-Wide** cmdlet 尝试在一个输出行显示尽可能多的属性值列。通过添加参数，可以控制列数以及输出空间的使用方式。

最基本的用法是，不使用任何参数调用 **Format-Wide** cmdlet，使输出按适合页面大小的列数进行排列。例如，如果运行 **Get-Childitem** cmdlet 并将其输出通过管道传递给 **Format-Wide** cmdlet，则信息将如下显示：

    Get-ChildItem | Format-Wide
    
        Directory: FileSystem::C:\WorkingFolder
    
    Config_01.xml                           Config_02.xml
    Config_03.xml                           Config_04.xml
    Config_05.xml                           Config_06.xml
    Config_07.xml                           Config_08.xml
    Config_09.xml                           Image_01.bmp
    Image_02.bmp                            Image_03.bmp
    Image_04.bmp                            Image_05.bmp
    Image_06.bmp                            Text_01.txt
    Text_02.txt                             Text_03.txt
    Text_04.txt                             Text_05.txt
    Text_06.txt                             Text_07.txt
    Text_08.txt                             Text_09.txt
    Text_10.txt                             Text_11.txt
    Text_12.txt

通常，不使用任何参数调用 **Get-Childitem** cmdlet 时，将会在一个属性表格中显示目录中所有文件的名称。在本示例中，将 **Get-Childitem** cmdlet 的输出通过管道传递给 **Format-Wide** cmdlet，输出将以两列名称显示。请注意，一次只能显示一种属性类型，该类型由接在 **Format-Wide** cmdlet 后的属性名称指定。如果添加 *Autosize* 参数，则输出会从两列更改为适合屏幕宽度的列数。

    Get-ChildItem | Format-Wide -AutoSize
    
        Directory: FileSystem::C:\WorkingFolder
    
    Config_01.xml   Config_02.xml   Config_03.xml   Config_04.xml   Config_05.xml
    Config_06.xml   Config_07.xml   Config_08.xml   Config_09.xml   Image_01.bmp
    Image_02.bmp    Image_03.bmp    Image_04.bmp    Image_05.bmp    Image_06.bmp
    Text_01.txt     Text_02.txt     Text_03.txt     Text_04.txt     Text_05.txt
    Text_06.txt     Text_07.txt     Text_08.txt     Text_09.txt     Text_10.txt
    Text_11.txt     Text_12.txt

在本示例中，表格按五列排列，而不是两列。*Column* 参数允许按如下方式指定信息显示的最大列数，从而可提供更多控制：

    Get-ChildItem | Format-Wide -Column 4
    
        Directory: FileSystem::C:\WorkingFolder
    
    Config_01.xml       Config_02.xml       Config_03.xml       Config_04.xml
    Config_05.xml       Config_06.xml       Config_07.xml       Config_08.xml
    Config_09.xml       Image_01.bmp        Image_02.bmp        Image_03.bmp
    Image_04.bmp        Image_05.bmp        Image_06.bmp        Text_01.txt
    Text_02.txt         Text_03.txt         Text_04.txt         Text_05.txt
    Text_06.txt         Text_07.txt         Text_08.txt         Text_09.txt
    Text_10.txt         Text_11.txt         Text_12.txt

在本示例中，使用 *Column* 参数将列数强制限制为四列。

## 如何输出数据

## Out-Host 和 Out-File cmdlet

**Out-Host** cmdlet 是管道末端一个不可见的默认 cmdlet。应用了所有格式之后，**Out-Host** cmdlet 将最终输出发送到控制台窗口进行显示。**Out-Host** cmdlet 是默认输出，因此无需显式调用。通过将调用 **Out-File** cmdlet 作为命令中最后一个 cmdlet，可以取代将输出发送到控制台窗口的操作。**Out-File** cmdlet 则将输出写入到命令中指定的文件，如下例所示：

    Get-ChildItem | Format-Wide -Column 4 | Out-File c:\OutputFile.txt

在本示例中，**Out-File** cmdlet 将 **Get-ChildItem | Format-Wide -Column 4** 命令显示的信息写入名为 `OutputFile.txt` 的文件中。还可以使用重定向运算符（右尖括号 `>` ），将管道输出重定向到文件。若要将某个命令的管道输出附加到现有文件末尾而不替换原始文件，请使用两个右尖括号 (`>>`)，如下例所示：

    Get-ChildItem | Format-Wide -Column 4 >> C:\OutputFile.txt

在本示例中，**Get-Childitem** cmdlet 的输出通过管道传递给 **Format-Wide** cmdlet 进行格式设置，然后写入 `OutputFile.txt` 文件的末尾。请注意，如果 `OutputFile.txt` 文件不存在，则使用两个右尖括号 (`>>`) 会创建该文件。

有关管道的详细信息，请参阅[管道传输](https://technet.microsoft.com/zh-cn/library/aa998260\(v=exchg.150\))。

有关以上示例中所用语法的详细信息，请参阅[语法](https://technet.microsoft.com/zh-cn/library/bb123552\(v=exchg.150\))。

## 在 Internet Explorer 中查看数据

由于在 Exchange 命令行管理程序中可以灵活简便地编写脚本，因此可以接受命令返回的数据，并以几乎无限制的方式设置其格式并输出。

以下示例说明如何使用一个简单脚本输出某个命令返回的数据，并在 Internet Explorer 中显示。此脚本接受通过管道传递的对象，打开 Internet Explorer 窗口，然后在 Internet Explorer 中显示数据：

    $Ie = New-Object -Com InternetExplorer.Application
    $Ie.Navigate("about:blank")
    While ($Ie.Busy) { Sleep 1 }
    $Ie.Visible = $True
    $Ie.Document.Write("$Input")
    # If the previous line doesn't work on your system, uncomment the line below.
    # $Ie.Document.IHtmlDocument2_Write("$Input")
    $Ie

若要使用此脚本，请将其保存到要运行脚本的计算机上的 `C:\Program Files\Microsoft\Exchange Server\V15\Scripts` 目录中。将文件命名为 `Out-Ie.ps1`。保存文件后，即可将脚本作为普通 cmdlet 使用。

> [!NOTE]  
> 若要在 Exchange 2013 中运行脚本，必须将脚本添加到无作用域的管理角色，而且您必须已直接获得或通过管理角色组获得管理角色。有关详细信息，请参阅<a href="understanding-management-roles-exchange-2013-help.md">了解管理角色</a>。


`Out-Ie` 脚本假定其收到的数据是有效的 HTML 格式。若要将要查看的数据转换为 HTML 格式，必须将命令的结果通过管道传递给 **ConvertTo-Html** cmdlet。然后，可以将该命令的结果通过管道传递给 `Out-Ie` 脚本。以下示例说明了如何在 Internet Explorer 窗口中查看目录列表：

    Get-ChildItem | Select Name,Length | ConvertTo-Html | Out-Ie

## 如何筛选数据

命令行管理程序使您能够访问有关组织中的服务器、邮箱、Active Directory 以及其他对象的大量信息。虽然访问这些信息有助于更好地了解所处的环境，但是海量信息可能会令您不知所措。命令行管理程序使您能够控制这些信息，并通过使用筛选只返回需要查看的数据。以下筛选类型可用：

  - **服务器端筛选：** 服务器端筛选接受在命令行中指定的筛选器，并将其提交到接受查询的 Exchange 服务器。该服务器处理查询，并且只返回与指定的筛选器匹配的数据。
    
    仅针对那些可能返回数万或数十万结果的对象执行服务器端筛选。因此，只有收件人管理 cmdlet（如 **Get-Mailbox** cmdlet）和查询管理 cmdlet（如 **Get-Queue** cmdlet）才支持服务器端筛选。这些 cmdlet 都支持 *Filter* 参数。此参数接受指定的筛选器表达式，并将其提交给服务器进行处理。

  - **客户端筛选：** 对当前正在进行操作的本地控制台窗口中的对象执行客户端筛选。使用客户端筛选时，该 cmdlet 检索与正在执行的任务匹配的所有对象，并提交到本地控制台窗口中。然后，命令行管理程序接受所有返回的结果，对这些结果应用客户端筛选，并且只返回与筛选器匹配的结果。所有 cmdlet 都支持客户端筛选。将命令结果通过管道传递给 **Where-Object** cmdlet 可调用此筛选。

## 服务器端筛选

服务器端筛选的实现特定于它所支持的 cmdlet。仅针对返回的对象上的特定属性启用服务器端筛选。有关详细信息，请参阅以下 cmdlet 的帮助：


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Get-ActiveSyncDevice</p></td>
<td><p>Get-ActiveSyncDeviceClass</p></td>
<td><p>Get-CASMailbox</p></td>
<td><p>Get-Contact</p></td>
<td><p>Get-DistributionGroup</p></td>
</tr>
<tr class="even">
<td><p>Get-DynamicDistributionGroup</p></td>
<td><p>Get-Group</p></td>
<td><p>Get-Mailbox</p></td>
<td><p>Get-MailboxStatistics</p></td>
<td><p>Get-MailContact</p></td>
</tr>
<tr class="odd">
<td><p>Get-MailPublicFolder</p></td>
<td><p>Get-MailUser</p></td>
<td><p>Get-Message</p></td>
<td><p>Get-MobileDevice</p></td>
<td><p>Get-Queue</p></td>
</tr>
<tr class="even">
<td><p>Get-QueueDigest</p></td>
<td><p>Get-Recipient</p></td>
<td><p>Get-RemoteMailbox</p></td>
<td><p>Get-RoleGroup</p></td>
<td><p>Get-SecurityPrincipal</p></td>
</tr>
<tr class="odd">
<td><p>Get-StoreUsageStatistics</p></td>
<td><p>Get-UMMailbox</p></td>
<td><p>Get-User</p></td>
<td><p>Get-UserPhoto</p></td>
<td><p>Remove-Message</p></td>
</tr>
<tr class="even">
<td><p>Resume-Message</p></td>
<td><p>Resume-Queue</p></td>
<td><p>Retry-Queue</p></td>
<td><p>Suspend-Message</p></td>
<td><p>Suspend-Queue</p></td>
</tr>
</tbody>
</table>


## 客户端筛选

客户端筛选可以与任何 cmdlet 一起使用。此功能包含那些同样支持服务器端筛选的 cmdlet。本主题前面部分已介绍，客户端筛选接受管道中上一个命令返回的所有数据，但只返回与指定筛选器匹配的结果。**Where-Object** cmdlet 可执行此筛选。该 cmdlet 可缩写为 **Where**。

数据通过管道传递时，**Where** cmdlet 收到上一个对象的数据，然后将数据筛选后传递到下一个对象。该筛选基于 **Where** 命令中定义的脚本块。该脚本块根据对象的属性和值来筛选数据。

**Clear-Host** cmdlet 用于清除控制台窗口。在本示例中，如果运行以下命令，则可以找到为 **Clear-Host** cmdlet 定义的所有别名：

    Get-Alias | Where {$_.Definition -eq "Clear-Host"}
    
    CommandType     Name                            Definition
    -----------     ----                            ----------
    Alias           clear                           clear-host
    Alias           cls                             clear-host

**Get-Alias** cmdlet 与 **Where** 命令一起使用，可以返回为 **Clear-Host** cmdlet 定义的别名列表，无需其他 cmdlet。下表列出了本示例中使用的 **Where** 命令的每个元素。

### Where 命令的元素

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>元素</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>{ }</code></p></td>
<td><p>一对大括号，用于括起定义筛选器的脚本块。</p></td>
</tr>
<tr class="even">
<td><p><code>$_</code></p></td>
<td><p>此特殊变量可自动启动并绑定到管道中的对象。</p></td>
</tr>
<tr class="odd">
<td><p><code>Definition</code></p></td>
<td><p><code>Definition</code> 属性是当前管道对象用于存储别名定义的属性。<code>Definition</code> 与 <code>$_</code> 变量一起使用时，在属性名称前加上句点。</p></td>
</tr>
<tr class="even">
<td><p><code>-eq</code></p></td>
<td><p>&amp;quot;等于&amp;quot;比较运算符，用于指定结果必须与表达式中提供的属性值完全匹配。</p></td>
</tr>
<tr class="odd">
<td><p>&quot;<strong>Clear-Host</strong>&quot;</p></td>
<td><p>在本示例中，&amp;quot;<strong>Clear-Host</strong>&amp;quot;是命令要分析的值。</p></td>
</tr>
</tbody>
</table>


在本示例中，**Get-Alias** cmdlet 返回的对象代表系统中所有已定义的别名。即使从命令行看不到这些别名，它们也会被收集并通过管道传递给 **Where** cmdlet。**Where** cmdlet 使用脚本块中的信息对这些别名对象应用筛选器。

特殊变量 `$`\_ 代表被传递的对象。`$_` 变量将由命令行管理程序自动启动并绑定到当前管道对象。有关此特殊变量的详细信息，请参阅[命令行管理程序变量](https://technet.microsoft.com/zh-cn/library/bb124036\(v=exchg.150\))。

使用标准的\&quot;点\&quot;表示法 (object.property)，可添加 `Definition` 属性以定义待评估对象的准确属性。然后，`-eq` 比较运算符将此属性的值与 `"Clear-Host"` 进行比较。只有那些具有与此条件匹配的 `Definition` 属性的对象才被传递到控制台窗口进行输出。有关比较运算符的详细信息，请参阅[比较运算符](https://technet.microsoft.com/zh-cn/library/bb125229\(v=exchg.150\))。

**Where** 命令筛选了由 **Get-Alias** cmdlet 返回的对象之后，您可以将筛选的对象通过管道传递给另一个命令。下一个命令将只处理这些由 Where 命令返回的已筛选对象。

