---
title: 'WhatIf、Confirm 和 ValidateOnly 开关: Exchange 2013 Help'
TOCTitle: WhatIf、Confirm 和 ValidateOnly 开关
ms:assetid: a850eea7-431e-49c5-b877-1ebde2a2b48f
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb124088(v=EXCHG.150)
ms:contentKeyID: 50491273
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# WhatIf、Confirm 和 ValidateOnly 开关

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2012-10-04_

有经验的管理员和脚本编写者以及对 Exchange 和脚本编写没有经验的管理员，都可以从使用 *WhatIf*、*Confirm* 和 *ValidateOnly* 开关中受益。这些开关使您能够控制命令运行的方式，并在命令影响数据之前准确指定命令将执行的操作。在从测试环境转换到生产环境以及执行新的脚本或命令时，此功能非常有价值。

与用于对通过使用筛选器或通过在管道中使用 **Get** 命令而返回的对象进行修改的命令一起使用时，*WhatIf*、*Confirm* 和 *ValidateOnly* 开关尤其有用。本主题将逐一介绍这些开关，并提供每个开关的一个示例命令。

> [!IMPORTANT]  
> 如果要在脚本命令中使用 <em>WhatIf</em>、<em>Confirm</em> 和 <em>ValidateOnly</em> 开关，必须将相应的开关添加到脚本内的每个命令中，而不是添加到调用脚本的命令行上。


> [!NOTE]  
> <em>WhatIf</em>、<em>Confirm</em> 和 <em>ValidateOnly</em> 称为开关参数。有关开关参数的详细信息，请参阅<a href="https://technet.microsoft.com/zh-cn/library/bb124388(v=exchg.150)">参数</a>。


## WhatIf 开关

*WhatIf* 开关指示应用该参数的命令运行，但只显示运行该命令会影响到的对象以及会对这些对象进行何种更改。该开关实际上不会更改其中的任何对象。使用 *WhatIf* 开关时，可以看到将对这些对象进行的更改是否符合您的期望结果，而不必担心会修改这些对象。

运行命令时如果带有 *WhatIf* 开关，则要将 *WhatIf* 开关放在命令的末尾，如下例所示：

    New-AcceptedDomain -Name "Contoso Domain" -DomainName "contoso.com" -WhatIf 

运行此示例命令时，命令行管理程序将返回以下文本：

```powershell
What if: Creating Accepted Domain "Contoso Domain" with domain name "contoso.com".
```

## Confirm 开关

*Confirm* 开关指示应用它的命令在进行任何更改之前停止处理。然后，该命令将提示您确认每个操作，然后再继续。使用 *Confirm* 开关时，可以分步执行对对象的更改，以确保更改只针对想要更改的特定对象。在将更改应用于很多对象并且希望精确控制命令行管理程序的操作时，此功能很有用。在命令行管理程序修改对象之前，系统将为每个对象显示确认提示。

默认情况下，命令行管理程序会自动将 *Confirm* 开关应用于具有以下谓词的 cmdlet：

  - **Clear**

  - **Disable**

  - **Dismount**

  - **Move**

  - **Remove**

  - **Stop**

  - **Suspend**

  - **Uninstall**

当包含这些谓词中的任何一个谓词的 cmdlet 运行时，命令行管理程序将自动停止执行命令，并在继续处理之前等待您确认。

如果要将 *Confirm* 开关手动应用于命令，请在命令的末尾包含 *Confirm* 开关，如下例所示：

```powershell
Get-JournalRule | Enable-JournalRule -Confirm
```

运行此示例命令时，命令行管理程序将返回以下确认提示：

    Confirm
    Are you sure you want to perform this action?
    Enabling journal rule "Litigation Journal Rule".
    [Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help
    (default is "Y"):

确认提示提供以下选择：

  - **\[Y\] 是** 键入 **Y** 可以指示命令继续执行该操作。下一个操作将显示另一个确认提示。`[Y] Yes` 是默认选项。

  - **\[A\] 全是** 键入 **A** 可以指示命令继续执行该操作以及所有后续操作。在此命令运行期间，将不再显示其他确认提示。

  - **\[N\] 否** 键入 **N** 可以指示命令跳过此操作，继续执行下一个操作。下一个操作将显示另一个确认提示。

  - **\[L\] 全否** 键入 **L** 可以指示命令跳过此操作以及所有后续操作。

  - **\[S\] 挂起** 键入 **S** 可以暂停执行当前管道并返回到该命令行。键入 **Exit** 可以继续执行管道。

  - **\[?\] 帮助** 键入 **?** 可以在命令行上显示确认提示帮助。

如果要覆盖命令行管理程序的默认行为，并使自动应用确认提示的 cmdlet 禁止显示确认提示，可以包含带有值 `$False` 的 *Confirm* 开关，如下例所示：

```powershell
Get-JournalRule | Disable-JournalRule -Confirm:$False
```

这种情况下，不显示确认提示。

> [!CAUTION]  
> <em>Confirm</em> 开关的默认值为 <code>$True</code>。命令行管理程序的默认行为是自动显示确认提示。如果禁止此默认行为，请指示命令在执行期间禁止显示所有确认提示。这样一来，该命令将处理满足该命令的条件的所有对象，而不进行确认。


## ValidateOnly 开关

*ValidateOnly* 开关指示应用它的命令在应用任何更改之前，先对执行该操作所需的所有条件和要求进行评估。*ValidateOnly* 开关可用于运行时间可能很长、对多个系统有若干依赖关系或者会影响邮箱等关键数据的 cmdlet。

将 *ValidateOnly* 开关应用到某一命令后，该命令将完成整个进程。命令执行每个操作的方式与没有 *ValidateOnly* 开关时的方式相同。但该命令不会更改任何对象。命令完成其进程后，将显示包含验证结果的摘要。如果验证指示命令已成功执行，则可以在不使用 *ValidateOnly* 开关的情况下再次运行该命令。

运行命令时如果带有 *ValidateOnly* 开关，则要将 *ValidateOnly* 开关放在命令的末尾。

