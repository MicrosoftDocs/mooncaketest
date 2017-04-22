---
title: ' Delete a Backup vault in Azure | Microsoft Docs '
description: How to delete an Azure Backup and Recovery Services vault. A backup vault can be called an Azure cloud vault, or Azure recovery vault. Troubleshooting problems when you can't delete a backup vault in the Classic Management Portal or Azure portal.
services: service-name
documentationcenter: dev-center-name
author: markgalioto
manager: carmonm
editor: ''

ms.assetid: 5fa08157-2612-4020-bd90-f9e3c3bc1806
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 3/14/2017
ms.author: markgal;trinadhk

---
# Delete an Azure Backup vault
The Azure Backup service has two types of vaults - the Backup vault and the Recovery Services vault. The Backup vault came first. Then the Recovery Services vault came along to support the expanded Resource Manager deployments. Because of the expanded capabilities and the information dependencies that must be stored in the vault, deleting a Backup or Recovery Services vault can be confusing. This article explains how to delete the vaults in the Classic Management Portal.  

| **Deployment Type** | **Portal** | **Vault name** |
| --- | --- | --- |
| Classic |Classic |Backup vault |
| Resource Manager |Azure |Recovery Services vault |

> [!NOTE]
> Backup vaults cannot protect Resource Manager-deployed solutions. However, you can use a Recovery Services vault to protect classically deployed servers and VMs.  
>
>

In this article, we use the term, vault, to refer to the generic form of the Backup vault or Recovery Services vault. We use the formal name, Backup vault, or Recovery Services vault, when it is necessary to distinguish between the vaults.

## Delete a backup vault in Classic Management Portal
The following instructions are for deleting a Backup vault in the Classic Management Portal. Before you can delete the Backup vault, you must delete the recovery points, or backed up items, and remove the registered servers. The registered servers are the Windows Server, workstation, or virtual machines that were registered to the vault.

1. Open the [Classic Management Portal](https://manage.windowsazure.cn).

2. From the list of backup vaults, select the vault you want to delete.

    ![delete backup data](./media/backup-azure-delete-vault/classic-portal-delete-vault-open-vault.png)

    The vault dashboard opens. Look at the number of Windows Servers and/or Azure virtual machines associated with the vault. Also, look at the total storage consumed in Azure. Stop all backup jobs and delete all data before deleting the vault.

3. Click the **Protected Items** tab, and then click **Stop Protection**

    ![delete backup data](./media/backup-azure-delete-vault/classic-portal-delete-vault-stop-protect.png)

    The **Stop protection of 'your vault'** dialog appears.
4. In the **Stop protection of 'your vault'** dialog, check **Delete associated backup data** and click ![checkmark](./media/backup-azure-delete-vault/checkmark.png). <br/>
    Optionally, you can choose a reason for stopping protection, and provide a comment.

    ![delete backup data](./media/backup-azure-delete-vault/classic-portal-delete-vault-verify-stop-protect.png)

    After deleting the items in the vault, the vault will be empty.

    ![delete backup data](./media/backup-azure-delete-vault/classic-portal-delete-vault-post-delete-data.png)
5. In the list of tabs, click **Registered Items**. The **Type** drop-down menu, enables you to choose the type of server registered to the vault. The type can be Windows Server or Azure Virtual Machine. In the following example, select the virtual machine registered to the vault, and click **Unregister**.

	![delete backup data](./media/backup-azure-delete-vault/classic-portal-unregister.png)

	If you want to delete the registration for a Windows Server, from the **Type** drop-down menu, select **Windows Server**, click ![checkmark](./media/backup-azure-delete-vault/checkmark.png) to refresh the screen, and then click **Delete**. <br/>

	![select Windows Server](./media/backup-azure-delete-vault/select-windows-server.png)

6. In the list of tabs, click **Dashboard** to open that tab. Verify there are no registered servers or Azure virtual machines protected in the cloud. Also, verify there is no data in storage. Click **Delete** to delete the vault.

    ![delete backup data](./media/backup-azure-delete-vault/classic-portal-list-of-tabs-dashboard.png)

    The Delete Backup vault confirmation screen opens. Select an option why you're deleting the vault, and click ![checkmark](./media/backup-azure-delete-vault/checkmark.png). <br/>

    ![delete backup data](./media/backup-azure-delete-vault/classic-portal-delete-vault-confirmation-1.png)

    The vault is deleted, and you return to the Classic Management Portal dashboard.


