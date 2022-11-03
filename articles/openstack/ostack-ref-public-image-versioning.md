---
title: OpenStack public image versioning
description: Describes how image versioning works in the UKCloud public catalog for UKCloud for OpenStack
services: openstack
author: Sue Highmoor
reviewer: srelf
lastreviewed: 15/07/2021
toc_rootlink: Reference
toc_sub1:
toc_sub2:
toc_sub3:
toc_sub4:
toc_title: OpenStack public image versioning
toc_fullpath: Reference/ostack-ref-public-image-versioning.md
toc_mdlink: ostack-ref-public-image-versioning.md
---

#### UKCloud Limited (“UKC”) and Virtual Infrastructure Group Limited (“VIG”) (together “the Companies”) – in Compulsory Liquidation

On 25 October 2022, the Companies were placed into Liquidation with the Official Receiver appointed as Liquidator and J Robinson and A M Hudson simultaneously appointed as Special Managers to manage the liquidation process on behalf of the Official Receiver.

Further information regarding the Liquidations can be found here: <https://www.gov.uk/government/news/virtual-infrastructure-group-limited-and-ukcloud-limited-information-for-creditors-and-interested-parties>

Contact details:<br>
For any general queries relating to the Liquidations please email <ukcloud@uk.ey.com><br>
For customer related queries please email <ukcloudcustomers@uk.ey.com><br>
For supplier related queries please email <ukcloudsuppliers@uk.ey.com>

# OpenStack public image versioning

## Overview

When you create an instance in OpenStack, its disk is cloned from an image managed by OpenStack. To get you started quickly, we publish a public catalog on our platform that provides several instance images for commonly-used instance sizes and operating systems.

## Image versioning

We update our supported images once a quarter. We will not remove images from the platform until they are no longer in use by any customer.

UKCloud always recommends using the latest available image, and recommends that all instances have their packages updated as often as possible.

## Image naming convention

Within the public catalog, we use the following image naming convention to enable you to easily identify images and select the best image to meet your requirements:

`<distributionName>-<distributionVersionNumber>-CURRENT` - This will be the most recent image for the quarter.

`<distributionName>-<distributionVersionNumber>-<DATE>` - The date indicates when the image was rotated from being the current image.

For example:

`win2012-r2-CURRENT`

`win2012-r2-01-01-2019`

## Feedback

If you find a problem with this article, click **Improve this Doc** to make the change yourself or raise an [issue](https://github.com/UKCloud/documentation/issues) in GitHub. If you have an idea for how we could improve any of our services, send an email to <feedback@ukcloud.com>.
