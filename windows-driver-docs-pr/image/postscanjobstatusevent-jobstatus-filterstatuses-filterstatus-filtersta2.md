---
title: PostScanJobStatusEvent.JobStatus.FilterStatuses.FilterStatus.FilterState
description: PostScanJobStatusEvent.JobStatus.FilterStatuses.FilterStatus.FilterState
ms.assetid: 56d290bc-91fd-460f-a27a-a5286a8597a3
keywords: ["PostScanJobStatusEvent.JobStatus.FilterStatuses.FilterStatus.FilterState"]
ms.author: windowsdriverdev
ms.date: 11/28/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# PostScanJobStatusEvent.JobStatus.FilterStatuses.FilterStatus.FilterState


The **FilterState** element contains a token that indicates the state of a filter in a post-scan job.

The **FilterState** element supports the following values:

<span id="Pending"></span><span id="pending"></span><span id="PENDING"></span>**Pending**  
The filter is waiting to process image data from the post-scan job.

<span id="Processing"></span><span id="processing"></span><span id="PROCESSING"></span>**Processing**  
The filter is processing image data from the post-scan job.

<span id="Canceled"></span><span id="canceled"></span><span id="CANCELED"></span>**Canceled**  
Image processing by this filter has been canceled.

<span id="CompletedSuccessfully"></span><span id="completedsuccessfully"></span><span id="COMPLETEDSUCCESSFULLY"></span>**CompletedSuccessfully**  
Image processing by this filter completed successfully.

<span id="CompletedWithErrors"></span><span id="completedwitherrors"></span><span id="COMPLETEDWITHERRORS"></span>**CompletedWithErrors**  
Image processing by this filter completed with errors.

<span id="CompletedWithWarnings"></span><span id="completedwithwarnings"></span><span id="COMPLETEDWITHWARNINGS"></span>**CompletedWithWarnings**  
Image processing by this filter completed with warnings.

This element has no sub-elements.

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bimage\image%5D:%20PostScanJobStatusEvent.JobStatus.FilterStatuses.FilterStatus.FilterState%20%20RELEASE:%20%2811/8/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




