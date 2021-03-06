---
title: Network Module Detachment
description: Network Module Detachment
ms.assetid: f41ac030-0bfc-47e2-9840-2c3550bc7d33
keywords:
- network modules WDK Network Module Registrar , detachment
- provider modules WDK Network Module Registrar , detachment
- detaching network modules
- client modules WDK Network Module Registrar , detachment
- deregistering network modules
- Network Module Registrar WDK , detaching network modules
- NMR WDK , detaching network modules
ms.author: windowsdriverdev
ms.date: 04/20/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.localizationpriority: medium
---

# Network Module Detachment


An attached pair of network modules are detached from each other when either the client module or the provider module deregisters with the Network Module Registrar (NMR). A client module deregisters with the NMR by calling the [**NmrDeregisterClient**](https://msdn.microsoft.com/library/windows/hardware/ff568774) function and a provider module deregisters with the NMR by calling the [**NmrDeregisterProvider**](https://msdn.microsoft.com/library/windows/hardware/ff568778) function. The following diagram illustrates the network modules initiating deregistration.

![diagram illustrating the network modules initiating deregistration](images/nmrdetach1.png)

When either network module deregisters with the NMR, the NMR calls both the client module's [*ClientDetachProvider*](https://msdn.microsoft.com/library/windows/hardware/ff544908) callback function and the provider module's [*ProviderDetachClient*](https://msdn.microsoft.com/library/windows/hardware/ff570397) callback function to initiate detaching the network module. The following diagram illustrates the NMR initiating the detachment.

![diagram illustrating the nmr initiating the detachment](images/nmrdetach2.png)

If the client module is unable to detach itself from the provider module immediately, it calls the [**NmrClientDetachProviderComplete**](https://msdn.microsoft.com/library/windows/hardware/ff568772) function after it completes detaching itself from the provider module. Likewise, if the provider module cannot detach itself from the client module immediately, it calls the [**NmrProviderDetachClientComplete**](https://msdn.microsoft.com/library/windows/hardware/ff568781) function after it completes detaching itself from the client module. The following diagram illustrates the network modules completing the detachment.

![diagram illustrating the network modules completing the detachment](images/nmrdetach3.png)


After both the client module and the provider module have completed detachment from each other, the NMR calls the client module's [*ClientCleanupBindingContext*](https://msdn.microsoft.com/library/windows/hardware/ff544904) callback function and the provider module's [*ProviderCleanupBindingContext*](https://msdn.microsoft.com/library/windows/hardware/ff570396) callback function so that the network modules can clean up their respective binding contexts for the attachment. The following diagram illustrates the NMR initiating cleanup.

![diagram illustrating the nmr initiating cleanup](images/nmrdetach4.png)


If the client module deregistered with the NMR, the deregistration of the client module is not complete until the client module has completely detached from all of the provider modules that it was previously attached to and all of those provider modules have completely detached from the client module. The client module waits for the deregistration to complete by calling the [**NmrWaitForClientDeregisterComplete**](https://msdn.microsoft.com/library/windows/hardware/ff568786) function. Likewise, if the provider module deregistered with the NMR, the deregistration of the provider module is not complete until the provider module has completely detached from all of the client modules that it was previously attached to and all of those client modules have completely detached from the provider module. The provider module waits for the deregistration to complete by calling the [**NmrWaitForProviderDeregisterComplete**](https://msdn.microsoft.com/library/windows/hardware/ff568787) function. The following diagram illustrates the network modules waiting for deregistration to complete.

![diagram illustrating the network modules waiting for deregistration to complete](images/nmrdetach5.png)