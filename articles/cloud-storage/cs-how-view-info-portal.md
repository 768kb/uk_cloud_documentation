---
title: How to view Cloud Storage information in the UKCloud Portal
description: Describes how to access information about your Cloud Storage service in the UKCloud Portal
services: cloud-storage
author: shighmoor
reviewer: sbeck
lastreviewed: 31/03/2022

toc_rootlink: How To
toc_sub1:
toc_sub2:
toc_sub3:
toc_sub4:
toc_title: View Cloud Storage information in the UKCloud Portal
toc_fullpath: How To/cs-how-view-info-portal.md
toc_mdlink: cs-how-view-info-portal.md
---

<br>**UKCloud Limited (“UKC”) and Virtual Infrastructure Group Limited (“VIG”) (together “the Companies”) – in Compulsory Liquidation**

On 25 October 2022, the Companies were placed into Liquidation with the Official Receiver appointed as Liquidator and J Robinson and A M Hudson simultaneously appointed as Special Managers to manage the liquidation process on behalf of the Official Receiver.

Further information regarding the Liquidations can be found here: <https://www.gov.uk/government/news/virtual-infrastructure-group-limited-and-ukcloud-limited-information-for-creditors-and-interested-parties>

Contact details:<br>
For any general queries relating to the Liquidations please email <ukcloud@uk.ey.com><br>
For customer related queries please email <ukcloudcustomers@uk.ey.com><br>
For supplier related queries please email <ukcloudsuppliers@uk.ey.com>

# How to view Cloud Storage information in the UKCloud Portal

## Overview

Cloud Storage is UKCloud's object storage solution based on Dell EMC Elastic Cloud Storage (ECS). Although you'll mostly interact with Cloud Storage through the API, the UKCloud Portal provides access to some information about your service.

Within the UKCloud Portal you can view:

- Information about the namespaces within your Cloud Storage environment

- A list of users with access to a namespace

- Information about the buckets within a namespace

- A graphical representation of the storage consumed over the last 30 days

You can also use the UKCloud Portal to create new Cloud Storage users. For more information, see [*How to create a new Cloud Storage user in the UKCloud Portal*](cs-how-create-user.md).

### Intended audience

To complete the steps in this guide you must have a UKCloud Portal account with access to the relevant namespace.

## Granting Portal permissions for Cloud Storage

To view Cloud Storage information in the Portal, a user must be granted access to the relevant namespace. Once access is granted, the user will be able to see the namespace, list the buckets in the namespace and reset the secret key. They will also be able to see consumption data for namespaces and buckets, with a graphical representation of average consumption for buckets.

To grant Portal permissions for Cloud Storage:

1. [*Log in to the UKCloud Portal*](../portal/ptl-gs.md#logging-in-to-the-ukcloud-portal) and select your account.

2. In the Portal navigation panel, expand the **Contacts** option and select **All Contacts**.

   ![All Contacts menu option in UKCloud Portal](images/cs-portal-mnu-all-contacts.png)

3. Find the contact for whom you want to grant permissions and click the **Edit** button.

   ![Edit contact button](images/cs-portal-btn-edit-contact.png)

4. Click the *Permissions* tab.

   ![Permissions tab](images/cs-portal-tab-permissions.png)

5. Scroll down to the *Permissions for Cloud Storage* section and select the **Access** check box for the relevant namespace.

   ![Cloud Storage permissions](images/cs-portal-permissions.png)

## Viewing namespace and bucket information

In ECS, objects are stored in buckets. In the UKCloud Portal, you can drill down through your namespaces to see the allocated buckets available in your Cloud Storage service. You can also view storage consumption over the last 30 days.

![Structure of objects in ECS](images/cs-namespace-buckets.png)

> [!NOTE]
> It's not possible to view objects within the UKCloud Portal.

1. In the Portal navigation panel, expand the **Cloud Storage** option and select **ECS**.

   ![ECS Cloud Storage option in the Portal menu](images/cs-portal-mnu-cloud-storage.png)

2. The *Storage* tab lists the namespaces within the currently selected account. You can see:

   - The number of buckets in the namespace

   - The total amount of storage (in GiB) currently consumed by the objects in all the buckets in the namespace

   - The service level of the namespace:

     - STANDARD - data is stored in a single data centre

     - ENHANCED - data is stored in a primary named data centre and copied to a second geographically remote data centre

   ![Namespaces page](images/cs-portal-namespaces.png)

3. To list the buckets in a namespace, click the **Buckets** button for the namespace.

   ![Buckets button](images/cs-portal-btn-buckets.png)

4. On the *Buckets* tab, you can see the following information for each bucket in the selected namespace:

   - The total amount of storage (in GiB) currently consumed by the objects in the bucket

   - The number of objects in the bucket

   ![Buckets page](images/cs-portal-buckets.png)

5. To view a graph that shows the amount of storage (in GiB) consumed by the objects in the bucket over the last 30 days, click the **Show Consumption** button for the bucket.

   ![Show Consumption button](images/cs-portal-btn-consumption.png)

   ![Consumption information](images/cs-portal-consumption.png)

## Next steps

This guide has shown you how you can view information about your Cloud Storage service in the UKCloud Portal. For information about how to use the service, see the following articles:

- [*Getting Started Guide for Cloud Storage*](cs-gs.md)

- [*How to create a new Cloud Storage user in the UKCloud Portal*](cs-how-create-user.md)

- [*How to install Dell EMC GeoDrive*](cs-how-install-geodrive2-client.md)

- [*How to use file browsers with Cloud Storage*](cs-how-use-file-browsers.md)

## Feedback

If you find a problem with this article, click **Improve this Doc** to make the change yourself or raise an [issue](https://github.com/UKCloud/documentation/issues) in GitHub. If you have an idea for how we could improve any of our services, send an email to <feedback@ukcloud.com>.
