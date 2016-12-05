---
title: Using Updated Core Print Drivers
author: windows-driver-content
description: Using Updated Core Print Drivers
MS-HAID:
- 'prtinst\_9a959555-ecbf-4ee7-b9ab-128038ea9e83.xml'
- 'print.using\_updated\_core\_print\_drivers'
MSHAttr:
- 'PreferredSiteName:MSDN'
- 'PreferredLib:/library/windows/hardware'
ms.assetid: a2a31627-a453-4776-b4f2-13660e4ad7a3
---

# Using Updated Core Print Drivers


Most manufacturer-supplied print drivers implement only device-dependent functions, and they rely on the system-supplied core driver components to manage generic printer functions. UniDrv, PostScript, and XPSDrv are examples of core driver components that many manufacturer-supplied drivers rely on to help with printer control and configuration.

Typically, printer manufacturers do not include Microsoft's core print drivers in their print driver packages. Instead, the INF files in their driver packages simply invoke Microsoft's printer INF file, Ntprint.inf, which installs the appropriate core print drivers.

However, Microsoft periodically releases updated versions of its core print drivers, and some manufacturers might supply driver packages that require features that are available only in the updated versions. This section describes the steps for installing with the required core print driver versions.

### Packages

In Windows Vista and Windows Server 2008, the operating system treats all print driver packages as unique objects. The operating system stores the files from each driver package in a separate folder in the Windows driver store. The Windows printer installer configures the driver package to operate independently of the other driver packages, and each driver package is separately managed by the operating system.

Windows stores each driver package as a complete unit, and, during point and print, the entire driver package is downloaded from the print server to a client and installed. A package-aware driver is compatible with the management of driver packages as independent objects. Package-aware print drivers have [entries](printer-inf-file-entries.md) in their INF files to enable point-and-print operations even if their packages have print driver dependencies on files outside of the package.

### Updates in Windows Vista

To support independent driver packages and still allow hardware manufacturers to take advantage of the core driver components, Windows Vista (and later) allows a package-aware driver to register a dependency on a core driver package. Microsoft supplies only one core driver package for printers in Windows Vista. That package is described by the driver-information file Ntprint.inf. Nearly all manufacturer-supplied print drivers, including package-aware drivers, depend on this core driver package.

Periodically, Microsoft releases updated versions of this core driver package. For example, Service Pack 1 for Windows Vista includes an updated version of the core driver package. Some manufacturers might find that they need to take advantage of these updates, and that their drivers can no longer rely on the version of the core driver package contained in the initial Windows Vista release.

This section explains how to construct a package-aware driver that has dependencies on updated core driver files, and how to ensure that the updated core driver package is installed when the manufacturer-supplied package-aware driver is installed.

The following topics are discussed:

[Constructing a Package-Aware Driver with Updated Core Drivers](constructing-a-package-aware-driver-with-updated-core-drivers.md)

[Updating Core Drivers Files for Non-Package-Aware Drivers](updating-core-drivers-files-for-non-package-aware-drivers.md)

[Creating a Single Driver Package for Windows XP and Windows Vista](creating-a-single-driver-package-for-windows-xp-and-windows-vista.md)

 

 


--------------------
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bprint\print%5D:%20Using%20Updated%20Core%20Print%20Drivers%20%20RELEASE:%20%289/1/2016%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")

