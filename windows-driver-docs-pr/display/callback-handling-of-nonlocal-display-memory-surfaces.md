---
title: Callback Handling Of Nonlocal Display Memory Surfaces
description: Callback Handling Of Nonlocal Display Memory Surfaces
ms.assetid: 803c52df-93c4-4124-9e17-6ef6c734a15f
keywords: ["display memory WDK DirectDraw , callbacks", "nonlocal display memory WDK DirectDraw , callbacks", "AGP WDK DirectDraw , callbacks", "drawing AGP support WDK DirectDraw , callbacks", "DirectDraw AGP support WDK Windows 2000 display , callbacks", "memory WDK DirectDraw AGP , callbacks", "callbacks WDK DirectDraw nonlocal memory"]
---

# Callback Handling Of Nonlocal Display Memory Surfaces


## <span id="ddk_callback_handling_of_nonlocal_display_memory_surfaces_gg"></span><span id="DDK_CALLBACK_HANDLING_OF_NONLOCAL_DISPLAY_MEMORY_SURFACES_GG"></span>


Nonlocal display memory surfaces are treated in exactly the same way as local display memory surfaces in terms of driver callbacks. For example, a driver's [*DdCanCreateSurface*](https://msdn.microsoft.com/library/windows/hardware/ff549213) callback is called when attempting to create nonlocal (as well as local) display memory surfaces, [*DdBlt*](https://msdn.microsoft.com/library/windows/hardware/ff549205) is called when blitting between local and nonlocal display memory surfaces, and [*DdDestroySurface*](https://msdn.microsoft.com/library/windows/hardware/ff549281) is called when the surface memory is being discarded.

Because the same driver functions are used for both local and nonlocal display memory surfaces, drivers must explicitly check the memory type of incoming surfaces. The memory type can be identified by checking the **ddsCaps.dwCaps** member of the local surface object [**DD\_SURFACE\_LOCAL**](https://msdn.microsoft.com/library/windows/hardware/ff551733) passed to the driver against the capability bits DDSCAPS\_LOCALVIDMEM and DDSCAPS\_NONLOCALVIDMEM.

Applications and AGP hardware access the bits of a DirectDraw surface using two different addresses. Applications use a virtual address that is translated through the operating system's page table to a portion of physical address space. This physical address space is mapped by the GART hardware to appear contiguous. Hardware accesses this physical linear address (again remapped to real, discontinuous pages of memory by the GART). The **fpVidMem** member of the [**DD\_SURFACE\_GLOBAL**](https://msdn.microsoft.com/library/windows/hardware/ff551726) structure holds the virtual linear address useful to applications (and potentially some driver operations). The device-side physical address can be found from:

```
fpStartOffset = pSurface->fpHeapOffset - pSurface->lpVidMemHeap->fpStart;
```

This offset is then added to the device's GART physical base address (contained in the **liPhysAGPBase** member of the [**VMEMHEAP**](https://msdn.microsoft.com/library/windows/hardware/ff570561) structure).

In all other respects, nonlocal display memory surfaces behave exactly like local display memory surfaces. The driver receives lock requests when an application is trying to access the surface data of nonlocal display memory surfaces. Operations such as blts between nonlocal display memory and local display memory can be asynchronous, just as they can be between local display memory surfaces. Attempts to lock nonlocal display memory surfaces when operations involving those surfaces are still pending should be failed by the driver with DDERR\_WASSTILLDRAWING error code in the usual way.

Furthermore, although DirectDraw manages the allocation and freeing of nonlocal display memory surfaces on behalf of the driver, the driver is still notified of the creation and destruction of surfaces in nonlocal display memory. When a nonlocal display memory surface is destroyed, the driver should not return until the surface is no longer in use.

Nonlocal display memory is [lost](losing-and-restoring-directdraw-surfaces.md) in exactly the same way as local display memory, that is, when a mode switch occurs or when exclusive mode changes, all local and nonlocal display memory surfaces are lost and the [*DdDestroySurface*](https://msdn.microsoft.com/library/windows/hardware/ff549281) driver callback is invoked for each surface. However, DirectDraw does not guarantee that the actual reserved address ranges and committed memory are preserved. DirectDraw may choose to discard all committed memory and the reserved address ranges, or it may choose to decommit memory but preserve the address range. It may also preserve both and simply mark the surfaces as lost. A driver should not make assumptions based on any one of these scenarios.

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[display\display]:%20Callback%20Handling%20Of%20Nonlocal%20Display%20Memory%20Surfaces%20%20RELEASE:%20%282/10/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")



