---
title: Azure 上的 SAP HANA（大型实例）的高可用性和灾难恢复 | Microsoft 文档
description: 为 Azure 上的 SAP HANA（大型实例）建立高可用性并规划灾难恢复。
services: virtual-machines-linux
documentationcenter:
author: RicksterCDN
manager: timlt
editor:

ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/01/2016
ms.author: rclaus

---
# Azure 上的 SAP HANA（大型实例）的高可用性和灾难恢复

高可用性和灾难恢复是运行任务关键型 Azure 上的 SAP HANA（大型实例）服务器的重要方面。必须咨询 SAP、系统集成商和/或 Microsoft，以便正确构建和实施适当的高可用性/灾难恢复策略。此外，必须考虑到与环境相关的恢复点目标和恢复时间目标。

## 高可用性

Microsoft 支持“现成”的 SAP HANA 高可用性方法，其中包括：

- **存储复制：**存储系统能够将所有数据复制到另一个位置（在同一数据中心内部或外部）。SAP HANA 的工作独立于此方法。
- **HANA 系统复制：**将 SAP HANA 中的所有数据复制到独立的 SAP HANA 系统。通过定期复制数据最大限度地减小恢复时间目标。SAP HANA 支持异步模式、内存中同步模式和同步模式（建议仅在同一数据中心或者距离不超过 100 公里的范围内使用这些模式）。在 HANA 大型实例戳记的当前设计中，HANA 系统复制仅可用于实现高可用性。
- **主机自动故障转移：**用于替代系统复制的本地故障恢复解决方案。当主节点不可用时，以扩展模式配置一个或多个备用 SAP HANA 节点，SAP HANA 将自动故障转移到另一个节点。

有关 SAP HANA 高可用性的详细信息，请参阅以下 SAP 文档：

- [SAP HANA 高可用性白皮书](http://go.sap.com/documents/2016/05/f8e5eeba-737c-0010-82c7-eda71af511fa.html)
- [SAP HANA 管理指南](http://help.sap.com/hana/SAP_HANA_Administration_Guide_en.pdf)
- [有关 SAP HANA 系统复制的 SAP 学院视频](http://scn.sap.com/community/hana-in-memory/blog/2015/05/19/sap-hana-system-replication)
- [SAP 支持说明 #1999880 - 有关 SAP HANA 系统复制的常见问题](https://bcs.wdf.sap.corp/sap/support/notes/1999880)
- [SAP 支持说明 #2165547 - SAP HANA 系统复制环境中的 SAP HANA 备份和还原](https://websmp230.sap-ag.de/sap(bD1lbiZjPTAwMQ==)/bc/bsp/sno/ui_entry/entry.htm?param=69765F6D6F64653D3030312669765F7361706E6F7465735F6E756D6265723D3231363535343726)
- [SAP 支持说明 #1984882 - 使用 SAP HANA 系统复制在最大限度地减少停机时间/不停机的情况下实现硬件更换](https://websmp230.sap-ag.de/sap(bD1lbiZjPTAwMQ==)/bc/bsp/sno/ui_entry/entry.htm?param=69765F6D6F64653D3030312669765F7361706E6F7465735F6E756D6265723D3139383438383226)

## 灾难恢复

Azure 上的 SAP HANA（大型实例）在一个地缘政治区域中的两个 Azure 区域中提供。两个不同区域的两个大型实例戳记之间建立了直接网络连接，用于在灾难恢复期间复制数据。数据复制基于存储基础结构。默认情况下不会执行复制，只会针对订购了灾难恢复功能的客户配置执行复制。在当前设计中，HANA 系统复制不可用于灾难恢复。

但是，若要利用灾难恢复，需要规划好与两个不同 Azure 区域之间的网络连接。为此，需要使用一条 Azure ExpressRoute 线路从本地连接到主要 Azure 区域，使用另一个线路从本地连接到灾难恢复区域。这种措施可以应对整个 Azure 区域（包括 Microsoft 企业边缘路由器 (MSEE) 位置）出现问题。

第二种措施是将连接到一个区域中的 Azure 上的 SAP HANA（大型实例）的所有 Azure 虚拟网络都连接到这两条 ExpressRoute 线路。这种措施可以避免当 Azure 中断服务时，只有一个 MSEE 位置连接到本地位置。

下图显示了灾难恢复的最佳配置：

![灾难恢复的最佳配置](./media/sap-hana-overview-high-availability-disaster-recovery/image1-optimal-configuration.png)  


灾难恢复配置的最佳方案是使用两条 ExpressRoute 线路从本地连接到两个不同的 Azure 区域。一条线路连接到运行生产实例的区域 #1。第二条 ExpressRoute 线路连接到运行某些非生产 HANA 实例的区域 #2。（如果整个 Azure 区域（包括 MSEE 和大型实例戳记）发生电网故障，则这种措施就很重要）。

另一种措施是将不同的虚拟网络连接到与 Azure 上的 SAP HANA（大型实例）连接的不同 ExpressRoute 线路。这样就可以绕过发生 MSEE 故障的位置，或者降低灾难恢复的恢复点目标，稍后将予以阐述。

灾难恢复设置的其他要求如下：

- 订购的 Azure 上的 SAP HANA（大型实例）的 SKU 大小必须与生产 SKU 大小相同，并且应部署在灾难恢复区域中。可以使用这些实例来运行测试、沙盒或 QA HANA 实例。
- 必须为想要在灾难恢复站点中恢复的每个 Azure 上的 SAP HANA（大型实例）SKU 订购灾难恢复配置文件。这种措施可以分配存储卷，而存储卷是从生产区域复制到灾难恢复区域的存储复制目标。

满足上述要求后，你需要负责启动存储复制。在用于 Azure 上的 SAP HANA（大型实例）的存储基础结构上，存储复制的基础是存储快照。若要启动灾难恢复复制，需要执行以下操作：

- 如前所述创建引导 LUN 的快照。
- 如前所述创建 HANA 相关卷的快照。

执行这些快照后，卷的初始副本将植入到与灾难恢复区域中的灾难恢复配置文件关联的卷中。

随后，将每隔一小时使用最新的存储快照来复制存储卷上开发的增量数据。

使用此配置实现的恢复点目标为 60 到 90 分钟。在灾难恢复方案中，若要实现更好的恢复点目标，需要将 Azure 上的 SAP HANA（大型实例）中的 HANA 事务日志备份复制到其他 Azure 区域。若要实现此恢复点目标，请执行以下操作：

1. 尽可能频繁地将 HANA 事务日志备份到 /hana/log/backup。
2. 将完成的事务日志备份复制到与 Azure 上的 SAP HANA（大型实例）服务器连接的虚拟网络中的 Azure 虚拟机 (VM) 上。
3. 将该备份从该 VM 复制到灾难恢复区域中某个虚拟网络内的某个 VM 上。
4. 在该区域中的 VM 上保留事务日志备份。

发生灾难时，可在实际服务器上部署灾难恢复配置文件后，将事务日志备份从该 VM 复制到灾难恢复区域中现在充当主服务器的 Azure 上的 SAP HANA（大型实例），然后还原这些备份。之所以能够进行这种恢复，是因为灾难恢复磁盘上的 HANA 状态就是 HANA 快照的状态。这是可以实现进一步还原事务日志备份的偏移点。

## 备份和还原

在操作数据库方面，一个要点是确保能够在发生各种灾难事件时保护数据库。这些事件可能由多种因素导致，包括自然灾难、简单的人为失误，等等。

备份数据库并具备还原到任意时间点（例如，在某人删除关键数据之前的时间点）的能力，可以尽可能地还原到发生中断之前所处的状态。

为获得最佳结果，必须执行两种类型的备份：

- 数据库备份
- 事务日志备份

除了在应用程序级别执行完整数据库备份以外，还可以使用存储快照执行更全面的备份。执行日志备份对于还原数据库（以及从已提交的事务中清空日志）也很重要。

Azure 上的 SAP HANA（大型实例）提供两个备份和还原选项：

- 自制 (DIY)。计算并确保有足够的磁盘空间后，使用磁盘备份方法执行完整的数据库和日志备份（备份到这些磁盘）。在不同的时间内，备份将复制到 Azure 存储帐户（使用容量基本上无限的存储设置基于 Azure 的文件服务器后），或者使用 Azure 备份保管库或 Azure 冷存储。另一个选项是将备份复制到存储帐户后，使用第三方数据保护工具（如 Commvault）来存储备份。对于出于合规性和审核目的而需要长期存储的数据，也有必要使用 DIY 备份选项。
- 使用 Azure 上的 SAP HANA（大型实例）底层基础结构提供的备份和还原功能。此选项可满足备份的需要，使得人工备份基本上遭到淘汰（出于合规性目的而需要保留数据备份除外）。本部分的余下内容介绍 HANA（大型实例）提供的备份和还原功能。

> [!NOTE] HANA（大型实例）底层基础结构使用的快照技术依赖于 SAP HANA 快照。SAP HANA 快照无法与 SAP HANA 多租户数据库容器配合工作。因此，无法使用此备份方法来部署 SAP HANA 多租户数据库容器。

### 使用 Azure 上的 SAP HANA（大型实例）的存储快照

Azure 上的 SAP HANA（大型实例）的底层存储基础结构支持卷的存储快照的概念。支持备份和还原特定的卷，不过需要注意以下事项：

- 它不是创建数据库备份，而是频繁创建存储卷的快照。
- 存储快照在执行存储快照之前启动 SAP HANA 快照。在恢复存储快照后，此 SAP HANA 快照是最终日志还原的设置点。
- 成功执行存储快照时，将删除 SAP HANA 快照。
- 日志备份需频繁创建，并存储在日志备份卷或 Azure 中。
- 如果必须将数据库还原到某个特定的时间点，可请求 Microsoft Azure 支持（生产中断）或 Azure 上的 SAP HANA 服务管理部门还原到特定的存储快照（例如，按计划将沙盒系统还原到其原始状态）。
- 存储快照中包含的 SAP HANA 快照是创建存储快照后，应用执行并存储的日志备份的偏移点。
- 创建这些日志备份是为了将数据库还原到某个时间点。

指定 backup\_name 会创建以下卷的快照：

- hana/data
- hana/log
- hana/log\_backup（在 hana/log 中装载为备份）
- hana/shared

### 存储快照注意事项

>[!NOTE] 存储快照_不是_免费提供的，因为必须分配额外的存储空间。

Azure 上的 SAP HANA（大型实例）的存储快照的特定机制包括：

- 特定的存储快照（在最初创建时）只会消耗极少的存储空间。
- 随着数据内容以及存储卷上 SAP HANA 数据文件内容的不断更改，快照需要存储原始块内容。
- 因此，存储快照的大小会不断增长。快照保留的时间越长，存储快照就会变得越大。
- 在存储快照的生存期内对 SAP HANA 数据库卷所做的更改越多，存储快照消耗的空间也就越大。

Azure 上的 SAP HANA（大型实例）为 SAP HANA 数据卷和日志卷使用固定的卷大小。执行这些卷的快照会大幅消耗卷空间，因此，客户需责任计划好存储快照（在 Azure 上的 SAP HANA [大型实例] 流程中）。

以下部分提供了有关执行这些快照的信息，提供了一般性的建议：

- 尽管硬件可以保留每个卷的 255 个快照，但我们强烈建议保留的快照数远低于此数字。
- 执行存储快照之前，请监视并跟踪可用空间。
- 根据可用空间减少存储快照数量。可能需要减少保留的快照数量，或者需要扩展卷。（可以 1-TB 为单位订购额外的存储。）
- 在使用系统迁移工具将数据移入 SAP HANA（使用 R3load，或者从备份还原 SAP HANA 数据库）或执行其他活动期间，我们强烈建议不要执行任何存储快照。（系统迁移是在新 SAP HANA 系统上完成的，因此不需要执行存储快照。）
- 在对 SAP HANA 表进行重大重组期间，应尽可能地避免执行存储快照。
- 存储快照是实现 Azure 上的 SAP HANA（大型实例）灾难恢复功能的先决条件。

### 设置存储快照

1. 确保在 HANA（大型实例）服务器上的 Linux 操作系统中安装 Perl。
2. 修改 /etc/ssh/ssh\_config，添加代码行 _MACs hmac-sha1_。
3. 在运行的每个 SAP HANA 实例的主节点上创建一个 SAP HANA 备份用户帐户（如果适用）。
4. 必须在所有 SAP HANA（大型实例）服务器上安装 SAP HANA HDB 客户端。
5. 在每个区域的第一台 SAP HANA（大型实例）服务器上，必须创建一个公钥用于访问对快照创建操作进行控制的底层存储基础结构。
6. 将 /scripts 中的脚本 azure\_hana\_backup.pl 复制到安装的 SAP HANA 系统中的 **hdbsql** 位置。
7. 将 /scripts 中的 HANABackupDetails.txt 文件复制到 Perl 脚本所在的同一位置。
8. 必要时，根据相应的客户规范修改 HANABackupDetails.txt 文件。

### 步骤 1：安装 SAP HANA HDBClient

Azure 上的 SAP HANA（大型实例）上安装的 Linux 包含所需的文件夹和脚本用于针对备份和灾难恢复目的执行 SAP HANA 存储快照。但是，客户需负责在安装 SAP HANA 时安装 SAP HANA HDBclient。（Microsoft 不会安装 HDBclient 和 SAP HANA。）

### 步骤 2：更改 /etc/ssh/ssh\_config

按如下所示更改 /etc/ssh/ssh\_config，添加 _MACs hmac-sha1_ 代码行。
```
#   RhostsRSAAuthentication no
#   RSAAuthentication yes
#   PasswordAuthentication yes
#   HostbasedAuthentication no
#   GSSAPIAuthentication no
#   GSSAPIDelegateCredentials no
#   GSSAPIKeyExchange no
#   GSSAPITrustDNS no
#   BatchMode no
#   CheckHostIP yes
#   AddressFamily any
#   ConnectTimeout 0
#   StrictHostKeyChecking ask
#   IdentityFile ~/.ssh/identity
#   IdentityFile ~/.ssh/id_rsa
#   IdentityFile ~/.ssh/id_dsa
#   Port 22
Protocol 2
#   Cipher 3des
#   Ciphers aes128-ctr,aes192-ctr,aes256-ctr,arcfour256,arcfour128,aes128-cbc,3des-cbc
#   MACs hmac-md5,hmac-sha1,umac-64@openssh.com,hmac-ripemd160
MACs hmac-sha1
#   EscapeChar ~
#   Tunnel no
#   TunnelDevice any:any
#   PermitLocalCommand no
#   VisualHostKey no
#   ProxyCommand ssh -q -W %h:%p gateway.example.com
```

### 步骤 3：创建公钥

在每个 Azure 区域中的第一台 Azure 上的 SAP HANA（大型实例）服务器上，创建一个公钥用于访问存储基础结构，以便能够创建快照。公钥可以确保无需使用密码登录到存储，并且不会保留密码凭据。在 SAP HANA（大型实例）服务器上的 Linux 中，执行以下命令生成公钥：
```
  ssh-keygen ¨Ct dsa ¨Cb 1024
```
新位置为 \_/root/.ssh/id\_dsa.pub。请不要输入实际的通行短语，否则，每次登录时都需要输入通行短语。应该按 **Enter** 两次，这样就不需要在登录时输入通行短语。

确保公钥按预期方式正常工作，方法是将文件夹切换到 /root/.ssh/，然后执行 **ls** 命令。如果密钥存在，请运行以下命令复制公钥：

![运行此命令复制公钥](./media/sap-hana-overview-high-availability-disaster-recovery/image2-public-key.png)  


此时，请联系 Azure 的 SAP HANA 服务管理部门并提供密钥。服务代表会使用该公钥将 SAP HANA 注册到底层存储基础结构中。

### 步骤 4：创建 SAP HANA 用户帐户

在 SAP HANA Studio 中创建用于备份的 SAP HANA 用户帐户。此帐户必须拥有以下权限：“备份管理”和“目录读取”。本示例创建了用户帐户 SCADMIN。

![在 HANA Studio 中创建用户](./media/sap-hana-overview-high-availability-disaster-recovery/image3-creating-user.png)  


### 步骤 5：为 SAP HANA 用户帐户授权

为脚本使用的 SAP HANA 用户帐户授权（这样就不需要在每次运行脚本时都要授权）。使用 SAP HANA 命令 `hdbuserstore` 可以创建存储在一个或多个 SAP HANA 节点上的 SAP HANA 用户密钥。用户还可以使用用户密钥从下面所述的脚本流程内部访问 SAP HANA，而无需管理密码。

>[!IMPORTANT] 以 `_root_` 身份运行以下命令。否则脚本无法正常工作。

按如下所示输入 `hdbuserstore` 命令：

![输入 hdbuserstore 命令](./media/sap-hana-overview-high-availability-disaster-recovery/image4-hdbuserstore-command.png)  


以下示例中，用户为 SCADMIN01，主机名为 lhanad01，命令为：
```
hdbuserstore set SCADMIN01 lhanad01:30115 <backup username> <password>
```
从 HANA 扩展实例的单个服务器管理所有脚本。在本示例中，必须在每台主机上更改 SCADMIN01 的 SAP HANA 密钥，反映与该密钥相关的主机。即，使用 HANA DB **lhanad** 的实例数目修正 SAP HANA 备份帐户。该密钥必须在其分配到的主机上拥有管理权限，用于横向扩展的备份用户必须有权访问所有 SAP HANA 实例。
```
hdbuserstore set SCADMIN01 lhanad:30015 SCADMIN <password>
hdbuserstore set SCADMIN02 lhanad:30115 SCADMIN <password>
hdbuserstore set SCADMIN03 lhanad:30215 SCADMIN <password>
```

### 步骤 6：复制 /scripts 文件夹中的项

将 /scripts 文件夹（包含在安装黄金映像中）中的以下项复制到 **hdbsql** 的工作目录。对于当前 HANA 安装，此目录为 /hana/shared/D01/exe/linuxx86\_64/hdb。
```
azure\_hana\_backup.pl
testHANAConnection.pl
testStorageSnapshotConnection.pl
removeTestStorageSnapshot.pl
HANABackupCustomerDetails.txt
```
如果运行横向扩展或 OLAP，请复制以下项：
```
azure\_hana\_backup\_bw.pl
testHANAConnectionBW.pl
testStorageSnapshotConnectionBW.pl
removeTestStorageSnapshotBW.pl
HANABackupCustomerDetailsBW.txt
```
可以针对纵向扩展部署，按如下所示修改 HANABackupCustomerDetails.txt 文件。它是脚本的控制与配置文件，用于运行存储快照。在部署实例后，应会收到 Azure 上的 SAP HANA 服务管理部门提供的_存储备份名称_和_存储 IP 地址_。不能修改任何变量的顺序、排序或空格，否则脚本无法正常运行。

对于纵向扩展部署，配置文件如下所示：
```
#Provided by Microsoft Service Management
Storage Backup Name: lhanad01backup
Storage IP Address: 10.250.20.21
#Created by customer using hdbuserstore
HANA Backup Name: SCADMIND01
```
对于横向扩展配置，HANABackupCustomerDetailsBW.txt 文件如下所示：
```
#Provided by Microsoft Service Management
Storage Backup Name: lhanad01backup
Storage IP Address: 10.250.20.21
#Node IP addresses, instance numbers, and HANA backup name
#provided by customer.  HANA backup name created using
#hdbuserstore utility.
Node 1 IP Address: 10.254.15.21
Node 1 HANA instance number: 01
Node 1 HANA Backup Name: SCADMIN01
Node 2 IP Address: 10.254.15.22
Node 2 HANA instance number: 02
Node 2 HANA Backup Name: SCADMIN02
Node 3 IP Address: 10.254.15.23
Node 3 HANA instance number: 03
Node 3 HANA Backup Name: SCADMIN03
Node 4 IP Address: 10.254.15.24
Node 4 HANA instance number: 04
Node 4 HANA Backup Name: SCADMIN04
Node 5 IP Address: 10.254.15.25
Node 5 HANA instance number: 05
Node 5 HANA Backup Name: SCADMIN05
Node 6 IP Address: 10.254.15.26
Node 6 HANA instance number: 06
Node 6 HANA Backup Name: SCADMIN06
Node 7 IP Address: 10.254.15.27
Node 7 HANA instance number: 07
Node 7 HANA Backup Name: SCADMIN07
Node 8 IP Address: 10.254.15.28
Node 8 HANA instance number: 08
Node 8 HANA Backup Name: SCADMIN08
```
>[!NOTE] 实际的 HANA 存储快照脚本中目前仅使用节点 1 的详细信息。建议测试是否能够与所有 HANA 节点相互访问，以便在主备份节点必须经常变动的情况下，可以通过修改节点 1 中的详细信息，确保其他任何节点可以取代主节点。

若要检查配置文件中的配置是否正确或者是否与 HANA 实例建立了正确的连接，请运行以下脚本之一：
- 对于纵向扩展配置（独立于 SAP 工作负荷）：

 ```
testHANAConnection.pl
```
- 对于横向扩展配置：

 ```
testHANAConnectionBW.pl
```

确保 HANA 主实例有权访问全部所需的 HANA 服务器。脚本中不带参数，但必须完成相应的 HANABackupCustomerDetails/ HANABackupCustomerDetailsBW 文件才能使脚本正常运行。由于只会返回 shell 命令错误代码，因此脚本无法检查每个特定实例中的错误。但尽管如此，脚本确实会提供一些有用的注释来帮助用户做仔细检查。

若要运行该脚本，请执行以下操作：
```
 ./testHANAConnection.pl
```
 如果脚本成功获取 HANA 实例的状态，将显示 HANA 连接成功的消息。

此外，可以使用另一种类型的脚本检查 HANA 主实例服务器是否能够登录到存储。在执行 azure\_hana\_backup(\_bw).pl 脚本之前，必须先执行以下脚本。如果某个卷不包含任何快照，就无法确定该卷是否为空，或者在获取快照详细信息时会发生 ssh 失败。因此，脚本将执行两个步骤：

- 验证存储控制台是否可访问。
- 根据 HANA 实例为每个卷创建一个测试或虚构快照。

因此，HANA 实例包含为参数。同样，无法提供与存储连接相关的错误检查，但执行失败时，脚本会提供有用的提示。

脚本的运行方式：
```
 ./testStorageSnapshotConnection.pl <hana instance>
```
或使用以下运行方式：
```
./testStorageSnapshotConnectionBW.pl <hana instance>
```
脚本还会显示消息，指出你可以正常登录到根据你所拥有的服务器实例使用的逻辑单元号 (LUN) 组织的已部署存储租户。

在执行第一个基于存储快照的备份之前，请运行后面的脚本来确保配置正确。

运行这些脚本后，可执行以下命令删除快照：
```
./removeTestStorageSnapshot.pl <hana instance>
```
或
```
./removeTestStorageSnapshot.pl <hana instance>
```

### 步骤 7：执行按需快照

按如下所述执行按需快照（以及使用 cron 计划定期快照）。

对于纵向扩展配置，请执行以下脚本：
```
./azure_hana_backup.pl lhanad01 customer 20
```
对于横向扩展配置，请执行以下脚本：
```
./azure_hana_backup_bw.pl lhanad01 customer 20
```
横向扩展脚本会执行一些附加检查，确保在继续创建 SAP HANA 或存储快照之前，可以访问所有 HANA 服务器，并且所有 HANA 实例返回实例的相应状态。

必须指定以下参数：

- 需要备份的 HANA 实例。
- 存储快照的快照前缀。
- 为特定的前缀保留的快照数。

```
./azure_hana_backup.pl lhanad01 customer 20
```

执行该脚本将在以下三个不同的阶段创建存储快照：

- 执行 HANA 快照。
- 执行存储快照。
- 删除 HANA 快照。

从脚本已复制到的 HDB 可执行文件文件夹调用该脚本，将它执行。该脚本至少会备份以下卷，但同时还会备份卷名称中包含显式 SAP HANA 实例名称的任何卷。
```
hana_data_<hana instance>_prod_t020_vol
hana_log_<hana instance>_prod_t020_vol
hana_log_backup_<hana instance>_prod_t020_vol
hana_shared_<hana instance>_prod_t020_vol
```
保留期将根据执行脚本时作为参数提供的快照数（例如 20，如上所示）严格管理。因此，时间量取决于执行期限，以及脚本调用中的快照数。如果保留的快照数超过了脚本调用中指定为参数的数字，则执行新快照之前，将删除此标签中最旧的存储快照（在上述示例中为 _custom_）。这意味着，作为最后一个调用参数指定的数字是可用于控制快照数的数字。

>[!NOTE] 更改标签后，将立即重新开始计数。

如果 Azure 上的 SAP HANA 服务管理部门为多节点环境创建快照，则你需要包含他们提供的 HANA 实例名称作为参数。在单节点环境中，提供 Azure 上的 SAP HANA（大型实例）单元名称便已足够，但我们仍建议提供 HANA 实例名称。

此外，可以使用同一个脚本备份引导卷\\LUN。首次运行 HANA 时，必须至少备份引导卷一次，不过，我们建议在 cron 中为引导卷制定每周或每夜备份计划。无需添加 SAP HANA 实例名称，只需在脚本中插入 _boot_ 作为参数，如下所示：
```
./azure_hana_backup boot customer 20
```
相同的保留策略也会应用到引导卷。如上所述的按需快照只能用于特殊场合（例如在 SAP 增强包 (EHP) 升级期间，或者需要创建不同的存储快照时）。

建议使用 cron 执行计划的存储快照，使用同一个脚本来满足所有备份和灾难恢复需求（修改脚本输入，使之与请求的不同备份时间匹配）。可以根据快照执行时间，在 cron 中做好上述一切计划：每小时、12 小时、每天或每周。cron 计划旨在为长期场外备份创建符合上述保留标签的存储快照。脚本中包含可根据请求的频率备份所有生产卷的命令（数据和日志文件每小时备份一次，而引导卷每日备份一次）。

以下 cron 脚本中的项将分别在每小时后的第 10 分钟、每 12 小时后的第 10 分钟和每 24 小时后的第 10 分钟运行一次。cron 作业的创建方式是在任意特定的小时内只发生一次 SAP HANA 存储快照，因此，在相同的时间 (12:10 AM)，每小时和每日备份都不会发生。为了帮助优化快照创建和复制过程，Azure 上的 SAP HANA 服务管理部门将提供运行备份的建议时间。

/etc/crontab 中默认的 cron 计划如下：
```
10 1-11,13-23 * * * ./azure_hana_backup.pl lhanad01 hourly 66
10 12 * * *  ./azure_hana_backup.pl lhanad01 12hour 14
```
在前面的 cron 说明中，HANA 卷（不包括引导卷）每小时获取一个带有标签的快照。在这些快照中，将保留 66 个。此外，将保留 14 个带有 12 小时标签的快照。因此，可能会获得三天的每小时快照，加上四天的 12 小时快照，也就是说，可以获得一整周的快照。

在 cron 中计划快照可能很棘手，因为在任意特定的时间只应执行一个脚本，除非该脚本错开执行几分钟时间。如果需要创建每日备份供长期保留，可以创建每日快照和 12 小时快照（保留计数各为 7），或者在 10 分钟后错开创建每小时快照。生产卷中只保留一个每日快照。
```
10 1-11,13-23 * * * ./azure_hana_backup.pl lhanad01 hourly 66
10 12 * * *  ./azure_hana_backup.pl lhanad01 12hour 7
10 0 * * * ./azure_hana_backup.pl lhanad01 daily 7
```
此处所列的频率仅为示例。若要得出最佳的快照数，请遵循以下准则：

- 时间点恢复的恢复时间目标要求。
- 空间使用量。
- 潜在灾难恢复的恢复点目标和恢复时间目标要求。
- 针对磁盘最终执行的 HANA 完整数据库备份。每当针对磁盘执行完整数据库备份或执行 _backint_ 接口时，存储快照的执行就会失败。如果打算基于存储快照执行完整数据库备份，请确保在此期间已禁用存储快照执行。

>[!IMPORTANT] 仅当与 SAP HANA 日志备份配合执行存储快照时，才能针对 SAP HANA 备份使用存储快照。这些日志备份需要能够涵盖执行存储快照的间隔时间段。如果向用户承诺时间点恢复目标为 30 天，则需要满足以下条件：

- 能够访问期限已达 30 天的存储快照。
- 提供过去 30 天的连续日志备份。

在日志备份的范围内，同时为备份日志卷创建快照。但是，请务必执行定期日志备份，以便：

- 提供所需的连续日志备份来执行时间点恢复。
- 防止 SAP HANA 日志卷的空间不足。

最后的步骤之一是在 SAP HANA Studio 中计划 SAP HANA 备份日志。SAP HANA 备份日志的目标是包含装入点 /hana/log/backups 的专门创建的 hana/log\_backups 卷。

![在 SAP HANA Studio 中计划 SAP HANA 备份日志](./media/sap-hana-overview-high-availability-disaster-recovery/image5-schedule-backup.png)  


可以选择频率高于 15 分钟的备份。某些用户甚至会每隔一分钟执行日志备份一次，不过，我们不建议_高于_ 15 分钟的频率。

最后一步是执行基于文件的备份（在最初安装 SAP HANA 后），以创建必须在备份目录中存在的单个备份项。否则，SAP HANA 无法启动指定的日志备份。

![创建基于文件的备份用于创建单个备份项](./media/sap-hana-overview-high-availability-disaster-recovery/image6-make-backup.png)  


### 监视磁盘卷上的快照数量和大小

在特定的存储卷上，可以监视快照的数量以及快照的存储消耗量。`ls` 命令不会显示快照目录或文件。但是，Linux OS 命令 `du` 则可以，命令如下：

- `du ¨Csh .snapshot` 提供快照目录中所有快照的总数。
- `du ¨Csh --max-depth=1` 列出 .snapshot 文件夹中保存的所有快照，以及每个快照的大小。
- `du ¨Chc` 提供所有快照占用的总大小。

使用以下命令可确保创建和存储的快照不会耗尽卷上的所有存储。

### 减少服务器上的快照数

如前所述，可以减少存储的带有特定标签的快照数。用于启动快照的命令的最后两个参数是要保留的快照的标签与数量。
```
./azure_hana_backup.pl lhanad01 customer 20
```
在上面的示例中，快照标签为 _customer_，要保留的带有此标签的快照数为 _20_。对磁盘空间消耗量做出响应时，你可能想要减少存储的快照数。减少快照数的简单方法是将脚本的最后一个参数设置为 5 并运行该脚本：
```
./azure_hana_backup.pl lhanad01 customer 5
```
使用此设置运行脚本后，快照数（包括新存储快照）为 _5_。

 >[!NOTE] 仅当最近创建的快照超过一小时的情况下，此脚本才能减少快照数。该脚本不会删除不超过一小时的快照。

这些限制与提供的可选灾难恢复功能相关。

如果你不再想要保留一组包含该前缀的快照，可以使用 _0_ 作为保留数量来执行该脚本，这样即可删除所有与该前缀匹配的快照。但是，删除所有快照可能会影响灾难恢复的功能。

### 恢复到最近的 HANA 快照

在遇到生产中断的情况时，可以向 Azure 上的 SAP HANA 服务管理部门提出客户事件，启动从存储快照恢复的过程。这种意外的情景可能是由于在生产系统中删除了数据造成的高度紧急问题，这时，检索数据的唯一办法就是还原生产数据库。

另一方面，时间点恢复可能不太紧急，因此可以提前几天规划。可与 Azure 上的 SAP HANA 服务管理部门合作规划这种恢复，而不要提出高优先级问题。例如，如果你尝试通过应用新的增强包升级了 SAP 软件，然后又需要还原到升级 EHP 之前的快照状态，则可以进行这种规划。

提出请求之前，需要做好一些准备工作。然后，Azure 上的 SAP HANA 服务管理团队便可以处理请求，提供还原的卷。接下来，你需要负责基于快照还原 HANA 数据库。下面说明了如何准好请求准备：

>[!NOTE] 根据所用的 SAP HANA 版本，你的用户界面可能与下面所示的屏幕截图不同。

1. 确定要还原的快照。除非另有说明，否则只能还原 HANA/数据卷。

2. 关闭 HANA 实例。

 ![关闭 HANA 实例](./media/sap-hana-overview-high-availability-disaster-recovery/image7-shutdown-hana.png)  


3. 每个 HANA 数据库节点上的数据卷。如果不卸载数据卷，快照还原将会失败。

 ![卸载每个 HANA 数据库节点上的数据卷](./media/sap-hana-overview-high-availability-disaster-recovery/image8-unmount-data-volumes.png)  


4. 提出 Azure 支持请求，指示要还原特定的快照。

 - 还原过程中：Azure 上的 SAP HANA 服务管理部门可能要求你参加一场电话会议，确保不会丢失任何数据。

 - 还原后：Azure 上的 SAP HANA 服务管理部门将会告知存储快照已还原。

5. 完成还原过程后，请重新装载所有数据卷。

 ![重新装载所有数据卷](./media/sap-hana-overview-high-availability-disaster-recovery/image9-remount-data-volumes.png)  


6. 在 SAP HANA Studio 中选择恢复选项（如果在通过 SAP HANA Studio 重新连接到 HANA DB 时未自动显示）。以下示例演示如何还原到最后一个 HANA 快照。存储快照中嵌入了一个 HANA 快照，如果要还原到最近的存储快照，该快照应是最近的 HANA 快照。（如果要还原到较旧的存储快照，需要根据存储快照的创建时间找到 HANA 快照。）

 ![在 SAP HANA Studio 中选择恢复选项](./media/sap-hana-overview-high-availability-disaster-recovery/image10-recover-options-a.png)  


7. 选择“将数据库恢复到特定的数据备份或存储快照”。

 ![“指定恢复类型”窗口](./media/sap-hana-overview-high-availability-disaster-recovery/image11-recover-options-b.png)  


8. 选择“指定不包含目录的备份”。

 ![“指定备份位置”窗口](./media/sap-hana-overview-high-availability-disaster-recovery/image12-recover-options-c.png)  


9. 在“目标类型”列表中，选择“快照”。

 ![“指定用于恢复的备份”窗口](./media/sap-hana-overview-high-availability-disaster-recovery/image13-recover-options-d.png)  


10. 单击“完成”启动恢复过程。

 ![单击“完成”启动恢复过程](./media/sap-hana-overview-high-availability-disaster-recovery/image14-recover-options-e.png)  


11. HANA 数据库已还原并恢复到存储快照包含的 HANA 快照。

 ![HANA 数据库已还原并恢复到 HANA 快照](./media/sap-hana-overview-high-availability-disaster-recovery/image15-recover-options-f.png)  


### 恢复到最新状态

以下过程将还原存储快照中包含的 HANA 快照。然后，将事务日志备份还原到还原存储快照之前的最新数据库状态。

>[!IMPORTANT] 在继续下一步之前，请确保具备完整且连续的事务日志备份链。如果没有这些备份，则无法还原数据库的当前状态。

1. 执行上述“恢复到最近的 HANA 快照”过程的步骤 1-6。

2. 选择“将数据库恢复到其最近状态”。

 ![选择“将数据库恢复到其最近状态”](./media/sap-hana-overview-high-availability-disaster-recovery/image16-recover-database-a.png)  


3. 指定最新 HANA 日志备份的位置。该位置需要包含从创建 HANA 快照开始，到处于最新状态为止的所有 HANA 事务日志备份。

 ![指定最新 HANA 日志备份的位置](./media/sap-hana-overview-high-availability-disaster-recovery/image17-recover-database-b.png)  


4. 选择一个备份用作恢复数据库的基础。在本示例中，此备份为存储快照中包含的 HANA 快照。（以下屏幕截图中只列出了一个快照。）

 ![选择一个备份用作恢复数据库的基础](./media/sap-hana-overview-high-availability-disaster-recovery/image18-recover-database-c.png)  


5. 如果增量备份在创建 HANA 快照之后、处于最近状态之前不存在，请清除“使用增量备份”复选框。

 ![如果不存在增量备份，则清除“使用增量备份”复选框](./media/sap-hana-overview-high-availability-disaster-recovery/image19-recover-database-d.png)  


6. 在摘要屏幕上单击“完成”启动还原过程。

 ![在摘要屏幕上单击“完成”](./media/sap-hana-overview-high-availability-disaster-recovery/image20-recover-database-e.png)  


### 恢复到另一个时间点
若要恢复到 HANA 快照（包含在存储快照中）与晚于 HANA 快照时间点恢复之间的时间点，请执行以下操作：

1. 确保提供从创建 HANA 快照开始，到要恢复到的时间为止的所有事务日志备份。
2. 在“恢复到最新状态”下面开始恢复过程。
3. 执行步骤 2 时，请在“指定恢复类型”窗口中选择“将数据库恢复到以下时间点”，指定时间点，然后完成步骤 3-6。

## 监视快照执行

需要监视存储快照的执行。执行存储快照的脚本会将输出写入某个文件，并将其保存在 Perl 脚本所在的同一位置。将会针对每个快照单独写入一个文件。每个文件的输出明确显示了快照脚本执行的各个阶段：

- 查找需要创建快照的卷
- 查找基于这些卷创建的快照
- 根据指定的快照数量删除最终的现有快照
- 创建 HANA 快照
- 基于卷创建存储快照
- 删除 HANA 快照
- 将最新的快照重命名为 **.0**

脚本的最重要部分为：
```
**********************Creating HANA snapshot**********************
Creating the HANA snapshot with command: "./hdbsql -n localhost -i 01 -U SCADMIN01 "backup data create snapshot"" ...
HANA snapshot created successfully.
**********************Creating Storage snapshot**********************
Taking snapshot hourly.recent for hana_data_lhanad01_t020_vol ...
Snapshot created successfully.
Taking snapshot hourly.recent for hana_log_backup_lhanad01_t020_vol ...
Snapshot created successfully.
Taking snapshot hourly.recent for hana_log_lhanad01_t020_vol ...
Snapshot created successfully.
Taking snapshot hourly.recent for hana_shared_lhanad01_t020_vol ...
Snapshot created successfully.
Taking snapshot hourly.recent for sapmnt_lhanad01_t020_vol ...
Snapshot created successfully.
**********************Deleting HANA snapshot**********************
Deleting the HANA snapshot with command: "./hdbsql -n localhost -i 01 -U SCADMIN01 "backup data drop snapshot"" ...
HANA snapshot deletion successfully.
```
从此示例中可以看到脚本如何记录 HANA 快照的创建过程。在横向扩展部署中，此过程在主节点上启动。主节点在每个辅助角色节点上启动快照的同步创建。然后创建存储快照。成功执行存储快照后，将删除 HANA 快照。

<!---HONumber=Mooncake_0320_2017-->