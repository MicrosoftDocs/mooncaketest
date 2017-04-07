---
title: Compute benchmark scores for Windows VMs | Azure
description: Compare SPECint compute benchmark scores for Azure VMs running Windows Server
services: virtual-machines-windows
documentationcenter: ''
author: cynthn
manager: timlt
editor: ''
tags: azure-resource-manager,azure-service-management

ms.assetid: 69ae72ec-e8be-4e46-a8f0-e744aebb5cc2
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 09/22/2016
wacn.date: ''
ms.author: cynthn

---
# Compute benchmark scores for Windows VMs
The following SPECInt benchmark scores show compute performance for Azure's high-performance VM lineup running Windows Server. Compute benchmark scores are also available for [Linux VMs](virtual-machines-linux-compute-benchmark-scores.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## Dv2-series
| Size | vCPUs | NUMA nodes | CPU | Runs | Avg base rate | StdDev |
| --- | --- | --- | --- | --- | --- | --- |
| Standard_D1_v2 |1 |1 |Intel Xeon E5-2673 v3 @ 2.4 GHz |83 |36.6 |2.6 |
| Standard_D2_v2 |2 |1 |Intel Xeon E5-2673 v3 @ 2.4 GHz |27 |70.0 |3.7 |
| Standard_D3_v2 |4 |1 |Intel Xeon E5-2673 v3 @ 2.4 GHz |19 |130.5 |4.4 |
| Standard_D4_v2 |8 |1 |Intel Xeon E5-2673 v3 @ 2.4 GHz |19 |238.1 |5.2 |
| Standard_D5_v2 |16 |2 |Intel Xeon E5-2673 v3 @ 2.4 GHz |14 |460.9 |15.4 |
| Standard_D11_v2 |2 |1 |Intel Xeon E5-2673 v3 @ 2.4 GHz |19 |70.1 |3.7 |
| Standard_D12_v2 |4 |1 |Intel Xeon E5-2673 v3 @ 2.4 GHz |2 |132.0 |1.4 |
| Standard_D13_v2 |8 |1 |Intel Xeon E5-2673 v3 @ 2.4 GHz |17 |235.8 |3.8 |
| Standard_D14_v2 |16 |2 |Intel Xeon E5-2673 v3 @ 2.4 GHz |15 |460.8 |6.5 |

## About SPECint
Windows numbers were computed by running [SPECint 2006](https://www.spec.org/cpu2006/results/rint2006.html) on Windows Server. SPECint was run using the base rate option (SPECint_rate2006), with one copy per core. SPECint consists of 12 separate tests, each run three times, taking the median value from each test and weighting them to form a composite score. Those tests were then run across multiple VMs to provide the average scores shown.

## Next steps
* For storage capacities, disk details, and additional considerations for choosing among VM sizes, see [Sizes for virtual machines](virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).