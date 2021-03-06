---
title: Remove VMs from Azure Automation Update Management
description: This article tells how to remove machines managed with Update Management.
services: automation
ms.topic: conceptual
ms.date: 01/05/2021
ms.custom: mvc
---
# Remove VMs from Update Management

When you're finished managing updates on your VMs in your environment, you can stop managing VMs with the [Update Management](overview.md) feature. To stop managing them, you will edit the saved search query `MicrosoftDefaultComputerGroup` in your Log Analytics workspace that is linked to your Automation account.

## Sign into the Azure portal

Sign in to the [Azure portal](https://portal.azure.com).

## To remove your VMs

1. In the Azure portal, launch **Cloud Shell** from the top navigation of the Azure portal. If you are unfamiliar with Azure Cloud Shell, see [Overview of Azure Cloud Shell](../../cloud-shell/overview.md).

2. Use the following command to identify the UUID of a machine that you want to remove from management.

    ```azurecli
    az vm show -g MyResourceGroup -n MyVm -d
    ```

3. In the Azure portal, navigate to **Log Analytics workspaces**. Select your workspace from the list.

4. In your Log Analytics workspace, select **Advanced settings** and then and choose **Computer Groups** from the left-hand menu.

5. From **Computer Groups** in the right-hand pane, select **Saved groups**.

6. From the table, for the saved search query **Updates:MicrosoftDefaultComputerGroup**, click the **View Members** icon to run and view its members.

7. In the query editor, review the query and find the UUID for the VM. Remove the UUID for the VM and repeat the steps for any other VMs you want to remove.

8. Save the saved search when you're finished editing it by selecting **Save** from the top bar. When prompted, specify the following:

    * **Name**: MicrosoftDefaultComputerGroup
    * **Save as**: Function
    * **Alias**: Updates__MicrosoftDefaultComputerGroup
    * **Category**: Updates

>[!NOTE]
>Machines are still shown after you have unenrolled them because we report on all machines assessed in the last 24 hours. After removing the machine, you need to wait 24 hours before they are no longer listed.

## Next steps

To re-enable managing your virtual machine, see [Enable Update Management by browsing the Azure portal](enable-from-portal.md) or [Enable Update Management from an Azure VM](enable-from-vm.md).