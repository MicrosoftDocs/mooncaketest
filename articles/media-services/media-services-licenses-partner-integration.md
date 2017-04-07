---
title: Using partners to deliver Widevine licenses to Azure Media Services | Azure
description: This article describes how you can use Azure Media Services (AMS) to deliver a stream that is dynamically encrypted by AMS with both PlayReady and Widevine DRMs. The PlayReady license comes from Media Services PlayReady license server and Widevine license is delivered by castLabs license server.
services: media-services
documentationCenter: ''
authors: Juliako
manager: erikre
editor: ''

ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/26/2016
ms.author: juliako
---

#Using partners to deliver Widevine licenses to Azure Media Services

##Overview

Microsoft Azure Media Services enables you to deliver MPEG-DASH protected with Widevine DRM, which is encrypted per the Common Encryption (CENC) specification.

Starting with the Media Services .NET SDK version 3.5.2, Media Services enables you to configure Widevine license template and get Widevine licenses. You can also use the following AMS partners to help you deliver Widevine licenses: [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).

##castLabs

You can use [castLabs](http://castlabs.com/company/partners/azure/) to deliver Widevine licenses. For more information, see [Using castLabs to deliver DRM licenses to Azure Media Services](./media-services-castlabs-integration.md)

##See also

[Using PlayReady and/or Widevine dynamic common encryption](./media-services-protect-with-drm.md)

[Mingfei's blog](https://azure.microsoft.com/blog/azure-media-services-adds-google-widevine-packaging-for-delivering-multi-drm-stream/)