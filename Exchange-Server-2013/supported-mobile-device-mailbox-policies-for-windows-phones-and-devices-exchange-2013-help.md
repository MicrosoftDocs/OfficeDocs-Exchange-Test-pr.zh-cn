---
title: 'Windows Phone 和设备支持的移动设备邮箱策略: Exchange 2013 Help'
TOCTitle: Windows Phone 和设备支持的移动设备邮箱策略
ms:assetid: d76b1d4c-d1f6-4501-a7c9-854327aceda5
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ983805(v=EXCHG.150)
ms:contentKeyID: 52061564
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Windows Phone 和设备支持的移动设备邮箱策略

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-03-09_

随着 Windows Phone 8、Windows 8 和 Windows RT 的发布，有许多支持 Exchange ActiveSync 和移动设备邮箱策略的设备。每个设备的操作系统支持一套特定的移动设备策略设置。

## Windows 客户端和 Exchange 服务器兼容性矩阵

下表列出了 Windows Phone、Windows 8、Windows RT 和 Exchange 服务器各种版本的兼容移动邮箱策略参数。

## Windows Phone 7 支持的策略参数

下表列出了 Windows Phone 7 的移动设备邮箱策略设置。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Exchange 2007</th>
<th>Exchange 2010</th>
<th>Exchange 2013</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>DevicePasswordEnabled</p></td>
<td><p>DevicePasswordEnabled</p></td>
<td><p>DevicePasswordEnabled</p></td>
</tr>
<tr class="even">
<td><p>AllowSimpleDevicePassword</p></td>
<td><p>AllowSimpleDevicePassword</p></td>
<td><p>AllowSimpleDevicePassword</p></td>
</tr>
<tr class="odd">
<td><p>AllowIRDA</p></td>
<td><p>AllowIRDA</p></td>
<td><p>AllowIRDA</p></td>
</tr>
<tr class="even">
<td><p>MinPasswordLength</p></td>
<td><p>MinDevicePasswordLength</p></td>
<td><p>MinDevicePasswordLength</p></td>
</tr>
<tr class="odd">
<td><p>PasswordExpiration</p></td>
<td><p>DevicePasswordExpiration</p></td>
<td><p>DevicePasswordExpiration</p></td>
</tr>
<tr class="even">
<td><p>AllowDesktopSync</p></td>
<td><p>AllowDesktopSync</p></td>
<td><p>AllowDesktopSync</p></td>
</tr>
<tr class="odd">
<td><p>MaxInactivityTimeDeviceLock</p></td>
<td><p>MaxInactivityTimeDeviceLock</p></td>
<td><p>MaxInactivityTimeDeviceLock</p></td>
</tr>
<tr class="even">
<td><p>DevicePasswordHistory</p></td>
<td><p>DevicePasswordHistory</p></td>
<td><p>DevicePasswordHistory</p></td>
</tr>
<tr class="odd">
<td><p>AllowRemoteDesktop</p></td>
<td><p>AllowRemoteDesktop</p></td>
<td><p>AllowRemoteDesktop</p></td>
</tr>
<tr class="even">
<td><p>AllowStorageCard</p></td>
<td><p>AllowStorageCard</p></td>
<td><p>AllowStorageCard</p></td>
</tr>
<tr class="odd">
<td><p>AllowInternetSharing</p></td>
<td><p>AllowInternetSharing</p></td>
<td><p>AllowInternetSharing</p></td>
</tr>
<tr class="even">
<td><p>AllowNonProvisionableDevices</p></td>
<td><p>AllowNonProvisionableDevices</p></td>
<td><p>AllowNonProvisionableDevices</p></td>
</tr>
</tbody>
</table>


## Windows Phone 8 支持的策略参数

下表列出了 Windows Phone 8 的移动设备邮箱策略设置。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Exchange 2007</th>
<th>Exchange 2010</th>
<th>Exchange 2013</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>DevicePasswordEnabled</p></td>
<td><p>DevicePasswordEnabled</p></td>
<td><p>DevicePasswordEnabled</p></td>
</tr>
<tr class="even">
<td><p>AllowSimpleDevicePassword</p></td>
<td><p>AllowSimpleDevicePassword</p></td>
<td><p>AllowSimpleDevicePassword</p></td>
</tr>
<tr class="odd">
<td><p>AlphanumericDevicePasswordRequired</p></td>
<td><p>AlphanumericDevicePasswordRequired</p></td>
<td><p>AlphanumericDevicePasswordRequired</p></td>
</tr>
<tr class="even">
<td><p>MinDevicePasswordLength</p></td>
<td><p>MinDevicePasswordLength</p></td>
<td><p>MinDevicePasswordLength</p></td>
</tr>
<tr class="odd">
<td><p>MinDevicePasswordComplexCharacters</p></td>
<td><p>MinDevicePasswordComplexCharacters</p></td>
<td><p>MinDevicePasswordComplexCharacters</p></td>
</tr>
<tr class="even">
<td><p>RequireDeviceEncryption</p></td>
<td><p>RequireDeviceEncryption</p></td>
<td><p>RequireDeviceEncryption</p></td>
</tr>
<tr class="odd">
<td><p>MaxInactivityTimeDeviceLock</p></td>
<td><p>MaxInactivityTimeDeviceLock</p></td>
<td><p>MaxInactivityTimeDeviceLock</p></td>
</tr>
<tr class="even">
<td><p>DevicePasswordHistory</p></td>
<td><p>DevicePasswordHistory</p></td>
<td><p>DevicePasswordHistory</p></td>
</tr>
<tr class="odd">
<td><p>不适用</p></td>
<td><p>IRMEnabled</p></td>
<td><p>IRMEnabled</p></td>
</tr>
<tr class="even">
<td><p>DeviceWipeThreshold</p></td>
<td><p>MaxDevicePasswordFailedAttempts</p></td>
<td><p>MaxDevicePasswordFailedAttempts</p></td>
</tr>
<tr class="odd">
<td><p>AllowNonProvisionableDevices</p></td>
<td><p>AllowNonProvisionableDevices</p></td>
<td><p>AllowNonProvisionableDevices</p></td>
</tr>
<tr class="even">
<td><p>DevicePasswordExpiration</p></td>
<td><p>DevicePasswordExpiration</p></td>
<td><p>DevicePasswordExpiration</p></td>
</tr>
</tbody>
</table>


## Windows 8 和 Windows RT 支持的策略参数

下表列出了 Windows 8 和 Windows RT 的移动设备邮箱策略设置。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Exchange 2007</th>
<th>Exchange 2010</th>
<th>Exchange 2013</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>DevicePasswordEnabled</p></td>
<td><p>DevicePasswordEnabled</p></td>
<td><p>DevicePasswordEnabled</p></td>
</tr>
<tr class="even">
<td><p>AllowSimpleDevicePassword</p></td>
<td><p>AllowSimpleDevicePassword</p></td>
<td><p>AllowSimpleDevicePassword</p></td>
</tr>
<tr class="odd">
<td><p>MinDevicePasswordLength</p></td>
<td><p>MinDevicePasswordLength</p></td>
<td><p>MinDevicePasswordLength</p></td>
</tr>
<tr class="even">
<td><p>MinDevicePasswordComplexCharacters</p></td>
<td><p>MinDevicePasswordComplexCharacters</p></td>
<td><p>MinDevicePasswordComplexCharacters</p></td>
</tr>
<tr class="odd">
<td><p>RequireDeviceEncryption</p></td>
<td><p>RequireDeviceEncryption</p></td>
<td><p>RequireDeviceEncryption</p></td>
</tr>
<tr class="even">
<td><p>MaxInactivityTimeDeviceLock</p></td>
<td><p>MaxInactivityTimeDeviceLock</p></td>
<td><p>MaxInactivityTimeDeviceLock</p></td>
</tr>
<tr class="odd">
<td><p>DevicePasswordHistory</p></td>
<td><p>DevicePasswordHistory</p></td>
<td><p>DevicePasswordHistory</p></td>
</tr>
<tr class="even">
<td><p>DeviceWipeThreshold</p></td>
<td><p>MaxDevicePasswordFailedAttempts</p></td>
<td><p>MaxDevicePasswordFailedAttempts</p></td>
</tr>
<tr class="odd">
<td><p>AllowNonProvisionableDevices</p></td>
<td><p>AllowNonProvisionableDevices</p></td>
<td><p>AllowNonProvisionableDevices</p></td>
</tr>
<tr class="even">
<td><p>DevicePasswordExpiration</p></td>
<td><p>DevicePasswordExpiration</p></td>
<td><p>DevicePasswordExpiration</p></td>
</tr>
</tbody>
</table>

