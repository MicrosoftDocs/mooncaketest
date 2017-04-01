---
title: Build integrated solutions with SQL Data Warehouse | Azure
description: Tools and partners with solutions that integrate with SQL Data Warehouse. 
services: sql-data-warehouse
documentationCenter: NA
authors: lodipalm
manager: barbkess
editor: ''

ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 10/31/2016
wacn.date: ''
---

# Leverage other services with SQL Data Warehouse
In addition to its core functionality, SQL Data Warehouse enables users to leverage many of the other services in Azure alongside it.  Specifically, we have currently taken steps to deeply integrate with the following:

+ Azure Stream Analytics

We are working to connect with more services across the Azure ecosystem.

##Azure Stream Analytics
Azure Stream Analytics is a complex, fully managed infrastructure for processing and consuming event data generated from Azure Event Hub.  Integration with SQL Data Warehouse allows for streaming data to be effectively processed and stored alongside relational data enabling deeper, more advanced analysis.  

+ **Job Output:** Send output from Stream Analytics jobs directly to SQL Data Warehouse.

See [Integrate with Azure Stream Analytics](./sql-data-warehouse-integrate-azure-stream-analytics.md) or the [Azure Stream Analytics documentation](../stream-analytics/index.md) for more information.

<!--Image references-->

<!--Article references-->
[development overview]: ./sql-data-warehouse-overview-develop.md

[Azure Data Factory]: ./sql-data-warehouse-integrate-azure-data-factory.md
[Azure Machine Learning]: ./sql-data-warehouse-integrate-azure-machine-learning.md
[Azure Stream Analytics]: ./sql-data-warehouse-integrate-azure-stream-analytics.md
[Power BI]: ./sql-data-warehouse-integrate-power-bi.md
[Partners]: /documentation/articles/sql-data-warehouse-integrate-solution-partners/

<!--MSDN references-->

<!--Other Web references-->