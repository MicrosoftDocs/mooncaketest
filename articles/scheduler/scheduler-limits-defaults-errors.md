---
title: Scheduler Limits and Defaults
description: Scheduler Limits and Defaults
services: scheduler
documentationCenter: .NET
authors: krisragh
manager: dwrede
editor: ''

ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/18/2016
wacn.date: ''
ms.author: krisragh
---

# Scheduler Limits and Defaults

## Scheduler Quotas, Limits, Defaults, and Throttles

[!INCLUDE [scheduler-limits-table](../../includes/scheduler-limits-table.md)]

## The x-ms-request-id Header

Every request made against the Scheduler service returns a response header named**x-ms-request-id**. This header contains an opaque value that uniquely identifies the request.

If a request is consistently failing and you have verified that the request is properly formulated, you may use this value to report the error to Microsoft. In your report, include the value of x-ms-request-id, the approximate time that the request was made, the identifier of the subscription, job collection, and/or job, and the type of operation that the request attempted.

## See Also

 [What is Scheduler?](./scheduler-intro.md)

 [Azure Scheduler concepts, terminology, and entity hierarchy](./scheduler-concepts-terms.md)

 [Get started using Scheduler in the Azure portal](./scheduler-get-started-portal.md)

 [Plans and billing in Azure Scheduler](./scheduler-plans-billing.md)

 [Azure Scheduler REST API Reference](https://msdn.microsoft.com/zh-cn/library/mt629143)   

 [Azure Scheduler PowerShell cmdlets reference](./scheduler-powershell-reference.md)

 [Azure Scheduler High-Availability and Reliability](./scheduler-high-availability-reliability.md)

 [Azure Scheduler Outbound Authentication](./scheduler-outbound-authentication.md)