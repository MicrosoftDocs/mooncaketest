---
linkid: ''
urlDisplayName: ''
title: MySQL Service Questions – Azure Cloud
metakeywords: Azure Cloud, technical documentation, documents and resources, MySQL, database, FAQ, Azure MySQL, MySQL PaaS, Azure MySQL PaaS, Azure MySQL Service, Azure RDS
description: Provides quick answers for common technical questions encountered by users when using MySQL Database on Azure. Contact technical support if you have any further questions.
metaCanonical: ''
services: MySQL
documentationCenter: Services
title: ''
authors: ''
solutions: ''
manager: ''
editor: ''

ms.service: mysql_en
ms.date: 07/05/2016
wacn.date: 07/05/2016
wacn.lang: en
---

#Security consulting
> [!div class="op_single_selector"]
- [All FAQs](./mysql-database-enus-tech-faq.md)
- [Service consulting](./mysql-database-enus-serviceinquiry.md)
- [Connection issues](./mysql-database-enus-connectioninquiry.md)
- [Security consulting](./mysql-database-enus-securityinquiry.md)
- [Compatibility Issues](./mysql-database-enus-compatibilityinquiry.md)

### **I noticed that the database server address is a public endpoint. Does this mean that the access request goes through the Internet before it reaches the server if my app visits a database in the same datacenter?**

No. The Azure datacenter’s network routing deduces that this is one of its own addresses and directly routes the request to the IP address via the datacenter’s internal network. This routing method is more secure, so there is less concern about third parties monitoring query requests or results. However, if your app and database are not in the same datacenter, the database query requests and results do go through the Internet. In this situation, we recommend that you use Secure Sockets Layer (SSL) to ensure the privacy of data transfers. For more detailed information on SSL connections, refer to [Use SSL to securely access MySQL Database on Azure](./mysql-database-ssl-connection.md).

<!---HONumber=Acom_0104_2016_MySql-->