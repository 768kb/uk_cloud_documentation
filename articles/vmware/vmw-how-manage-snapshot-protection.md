---
title: How to manage Snapshot Protection for your VMs
description: Explains how to use the self-service Snapshot Protection tool to add, change or remove Snapshot Protection for your VMs
services: vmware
author: shall
reviewer: shighmoor
lastreviewed: 14/12/2021
toc_rootlink: How To
toc_sub1: 
toc_sub2:
toc_sub3:
toc_sub4:
toc_title: Manage Snapshot Protection for your VMs
toc_fullpath: How To/vmw-how-manage-snapshot-protection.md
toc_mdlink: vmw-how-manage-snapshot-protection.md
---

# How to manage Snapshot Protection for your VMs

## Overview

Protection technologies are tools used to enable you to design resilience into your cloud solutions. They protect data and provide you with the ability to recover from system outages - either caused by a disruption to the physical delivery of a service or as a result of corruption of your primary system.

The UKCloud platform offers a variety of protection options, including Snapshot Protection. Snapshot Protection automatically takes an image of your virtual machine (VM) every 24 hours and stores the image outside the core platform for either 14 or 28 days, depending on your chosen snapshot retention profile.

## How does Snapshot Protection work?

By default, VMs deployed on the UKCloud platform do not come with any protection services enabled. If you want Snapshot Protection for your VM, you must explicitly add it.

When you add Snapshot Protection to a VM, the VM is added to a daily automated backup. Backups are automatically taken for the VM once every 24 hours, sometime between the hours of 20:00 and 08:00. The status of a VM's backup is reported daily in the UKCloud Portal by 10:00, but typically within minutes of the close of the backup window.

If you encounter a problem with your VM, raise a Service Request via the [My Calls](https://portal.skyscapecloud.com/support/ivanti) section of the UKCloud Portal and we can use one of your VM backups to restore the whole VM image to a new VM in your VDC. You can then use this image to restore the VM or restore any required data to your original VM.

For more detailed information, see the Snapshot Protection [*Service Scope*](vmw-sco-snapshot-protection.md) and [*FAQ*](vmw-faq-snapshot-protection.md).

## Checking a VM's Snapshot Protection status

You can use the UKCloud Portal to see whether a VM uses Snapshot Protection, find out which snapshot retention policy is currently applied to a VM or check the status of your VM's snapshots.

1. [*Log in to the UKCloud Portal*](../portal/ptl-gs.md#logging-in-to-the-ukcloud-portal).

2. If necessary, switch to the account that you want to work in.

3. In the Portal navigation panel, expand **VMware Cloud** and then select the compute service that the VM belongs to.

   ![VMware Cloud menu option](images/vmw-portal-mnu-select-compute-service.png)

4. Select the **My VMs** tab.

   ![My VMs tab in the UKCloud Portal](images/ptl-tab-myvms.png)

5. From the **Currently viewing for VDC** list, select the virtual data centre (VDC) that the VM belongs to.

   ![Select VDC](images/ptl-myvms-select-vdc.png)

6. Select the **VMs** tab.

   ![VMs tab on the My VMs page](images/ptl-myvms-tab-vms.png)

7. The icon in **VM Backup** column shows the status of each VM's most recent backup:

   Icon | Description
   -----|------------
   ![Backup Successful](images/ptl-snapshot-success.png) | Backup of the VM was successful
   ![Excluded from backup](images/ptl-snapshot-excluded.png) | The VM has been excluded from backups
   ![Not in backup yet](images/ptl-snapshot-excluded.png) | A backup has not yet been created for a VM that has recently been included in backups
   ![Backup Failed](images/ptl-snapshot-fail.png) | Backup of the VM was unsuccessful
   ![Excluded from backup](images/ptl-snapshot-fail.png) | The VM has been excluded from backups but has not yet reached the end of the previous retention period<br>(when the end retention period is reached, the icon will change to the grey minus sign)

   > [!TIP]
   > You can hover over the icon to see a description of the backup status.

8. The button in the **Default Policy** column shows the Snapshot Protection option currently applied to the VM:

   - **14‑day** - VM uses Snapshot Protection, with backups retained for 14 days

   - **28-day** - VM uses Snapshot Protection, with backups retained for 28 days

   - **Manage** - VM is currently excluded from Snapshot Protection

   - **Processing** - A change in status to Snapshot Protection is currently being processed for the VM

   - **Failed** - A change in the status of Snapshot Protection for the VM failed; contact the UKCloud support team to resolve this issue.

   ![Snapshot Protection Status](images/ptl-myvms-vm-snapshots.png)

9. To find out more detail about the most recent backup of a VM, or to view information about previous backups, click the **VM Name**.

10. In the VM's *Info* page, the following fields provide information about the most recent backup of the VM:

    - **Additional information** - additional information about the backup, for example if the backup was removed from the daily automated backup, if the retention period was changed, or further details of any failures.

    - **Last backup** - the status of the most recent backup

    - **Retention length** - how long the backup will be kept for: 14 days or 28 days

    - **Backup status** - when the most recent backup was attempted

11. The *Snapshot Protection Backups* section of the page provides information about previous backups. This covers the entire retention policy period (14 or 28 days). Information includes:

    - **Status** - the status of the backup

    - **Slot** - the backup slot during which the backup was taken

    - **Start** - the date and time when the backup started

    - **End** - the date and time when the backup ended

    - **Snapshot Removal Start** - the date and time when the snapshot consolidation process started (that is, writing back any changes to the VM that occurred during the time it was locked for backup)

    - **Snapshot Removal End** - the date and time when the snapshot consolidation process ended

12. The *Snapshot Protection Policy History* section of the page lists any recent changes to the snapshot retention policy for the VM.

    - **Status** - The status of the policy change

    - **Date Requested** - The date and time when the policy change was requested

    - **User** - The user who requested the change

    - **Protection Period** - The new protection period introduced by the policy change

    - **Reason for Change** - The reason for the policy change

    - **Action** - The type of policy change request

13. To view all the VM information in a single table, from the **Actions** menu, select **Export VMs**. You can save this page to view offline and analyse further.

    ![Export VMs option](images/ptl-myvms-mnu-export.png)

## Managing Snapshot Protection for a VM

By default, VMs deployed on the UKCloud platform do not come with any protection services enabled. You can use the UKCloud Portal to add Snapshot Protection to your VM. You can also use the Portal to change the snapshot retention policy for your backups and to remove Snapshot Protection from your VM.

1. Access the **My VMs** tab for your compute service.

   For detailed steps for how to do this, see the first few steps in [Checking a VM's snapshot status](#checking-a-vms-snapshot-protection-status).

2. From the **Currently viewing for VDC** list, select the VDC that the VM belongs to.

3. Click the **VMs** tab.

4. In the **Default Policy** column, click the green button.

   The label on the button depends on the currently applied policy:

   - **Manage** if there is currently no snapshot retention policy applied to the VM

   - **14-day** if the VM's snapshot retention policy is currently 14 days

   - **28-day** if the VM's snapshot retention policy is currently 28 days

   ![Snapshot Protection options](images/ptl-myvms-snapshots-manage.png)

5. In the *Snapshot Protection Policy* dialog box, from the **New Protection Policy** list, select the snapshot retention policy that you want to apply to the VM:

   - **14-day** to apply a 14-day snapshot retention policy to the VM

   - **28-day** to apply a 28-day snapshot retention policy to the VM

   - **No Backup** to turn Snapshot Protection off for the VM

   ![Snapshot Protection Policy](images/ptl-myvms-snapshot-policy.png)

   > [!NOTE]
   > If you remove Snapshot Protection from a VM, you should consider alternatives to ensure the integrity of your data in the case of disruption. In addition to Snapshot Protection, UKCloud offers [*Journaling Protection*](vmw-sco-journaling-protection.md) options, or you may want to implement your own protection solution, possibly utilising our [*Cloud Storage*](../cloud-storage/cs-sco.md) service.

6. In the **Reason For Change** field, provide an explanation for why you're making the change to the existing snapshot retention policy.

7. Click **Submit**.

   The button in the **Snapshot Protection** column changes to an amber **Processing** button. When the changes have been applied, the button changes back to green with a label indicating the VM's snapshot retention policy (**14-day** or **28-day**) or **Manage** if you have turned off Snapshot Protection.

   The amount of time it takes for your changes to take place depends on how many requests are in the queue. If there are any problems with the request, the button in the **Snapshot Protection** column changes to a red **Failed** button; in this situation, contact UKCloud Support for further assistance.

   Backup status information is updated daily on the UKCloud Portal by 10:00, but typically within minutes of the close of the backup window.

   > [!NOTE]
   > If you remove a VM from backups, the status icon for the VM will display as a red cross until the end of the previously selected retention period. When the end of the retention period is reached, the status icon will change to the grey minus sign.

## Managing Snapshot Protection for a VDC

You can specify a snapshot retention policy to apply to all the VMs in a VDC. You can apply the policy to all new VMs or to all new and existing VMs.

1. Access the **My VMs** tab for your compute service.

   For detailed steps for how to do this, see the first few steps in [Checking a VM's snapshot status](#checking-a-vms-snapshot-protection-status).

2. From the **Currently viewing for VDC** list, select the VDC that you want to apply Snapshot Protection to.

3. Select the **Snapshot Protection** tab.

   ![Snapshot Protection tab on the My VMs page](images/ptl-myvms-tab-snapshot.png)

4. Next to **Default VM Snapshot Protection**, click the green button.

   The label on the button will depend on the currently applied policy:

   - **Manage** if there is currently no default snapshot retention policy applied to the VDC

   - **14-day** if the default snapshot retention policy is currently 14 days

   - **28-day** if the default snapshot retention policy is currently 28 days

   ![Default VM Snapshot Protection](images/ptl-myvms-snapshot-manage-vdc.png)

5. In the *Snapshot Protection Policy* dialog box, from the **New Protection Policy** list, select the snapshot retention policy that you want to apply to the VMs in this VDC:

   - **14-day** if you want to apply a 14-day snapshot retention policy to the VDC

   - **28-day** if you want to apply a 28-day snapshot retention policy to the VDC

   - **No Backup** if you do not want to apply a default snapshot retention policy to the VDC

   ![Snapshot Protection Policy](images/ptl-myvms-snapshot-policy-vdc.png)

6. In the **Reason For change** field, provide an explanation for why you're making the change to the existing snapshot retention policy.

7. If you want to apply the chosen snapshot retention policy to existing VMs in the VDC as well as new VMs, select the **Apply new policy to all existing VMs?** check box.

   > [!NOTE]
   > If you select this check box, all existing VMs will switch to the new policy when you click Submit. You will not be able to rollback this change.

8. Click **Submit**.

   The label of the **Default VM Snapshot Protection** button changes to indicate the new snapshot retention policy (**14-day** or **28-day**) or to **Manage** if you have turned off Snapshot Protection.

   Any new VMs created within the VDC will now use the specified snapshot retention policy, although you can override this for individual VMs if required by following the steps in [Managing snapshot protection for a VM](#managing-snapshot-protection-for-a-vm).

   If you selected **Apply to all existing VMs**, the button changes to an amber **Processing** button. When the changes have been applied, the button changes back to green with a label indicating the VDC's snapshot retention policy (**14-day** or **28-day**) or **Manage** if you have turned off Snapshot Protection. If the VDC contains a lot of VMs, the process of updating the policy for all existing VMs may take several minutes to complete.

   Backup status information is updated daily on the UKCloud Portal by 10:00, but typically within minutes of the close of the backup window.

   > [!NOTE]
   > When you exit the *Snapshot Protection Policy* dialog box, the **Currently viewing for VDC** list on the *My VMs* tab resets to the first VDC listed under the compute service. You'll need to reselect your VDC from the list before continuing.

9. The *Default Snapshot Protection Policy History* section of the page lists any recent changes to the snapshot protection policy for the VDC.

10. The *Recent VM Snapshot Protection Policy Actions* section of the page lists any recent changes to the snapshot protection policy for VMs in the VDC.

## Monitoring the status of Snapshot Protection

You can monitor the status of Snapshot Protection across an entire compute service to get a general overview of how your VDCs and VMs are protected.

1. [*Log in to the UKCloud Portal*](../portal/ptl-gs.md#logging-in-to-the-ukcloud-portal).

2. If necessary, switch to the account that you want to work in.

3. In the navigation panel, expand **Reports** and select **Backup Summary**.

   ![Backup summary](images/ptl-mnu-backup-summary.png)

4. Click the link for the compute service that you want to view Snapshot Protection information for.

   ![List of backup summary reports](images/ptl-backup-summary-reports.png)

5. The *Snapshot Protection Summary* page provides the following information for the selected compute service:

   - **Success Rate (Last 24 Hours)** - The percentage of successful VM backups in the previous night's backups

   - **Success Rate (Within Retention Period)** - The overall percentage success rate of all backups across the compute service

   - **Number of VMs Protected** - The total number of VMs successfully protected in the previous night's backups

   - **Number of VMs Not Protected** - The total number of VMs with Snapshot Protection that were not successfully protected in the previous night's backups

   - **VM Snapshot Protection Failures** - A list of the VMs that encountered a Snapshot Protection failure in previous night's backups

   ![VM Snapshot Protection summary](images/ptl-backup-summary-report.png)

## Next steps

For more information about what you can do with your VMs in the UKCloud Portal, see [*How to view your VMs in the UKCloud Portal*](vmw-how-portal-view-vms.md).

## Feedback

If you find a problem with this article, click **Improve this Doc** to make the change yourself or raise an [issue](https://github.com/UKCloud/documentation/issues) in GitHub. If you have an idea for how we could improve any of our services, send an email to <feedback@ukcloud.com>.
