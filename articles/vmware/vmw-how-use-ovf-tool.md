---
title: How to use the VMware OVF Tool
description: Describes how to use the VMware OVF Tool to assist in the distribution of virtual machines and vApps
services: vmware
author: shall
reviewer: swthomas
lastreviewed: 11/11/2021
toc_rootlink: How To
toc_sub1: 
toc_sub2:
toc_sub3:
toc_sub4:
toc_title: Use the VMware OVF Tool
toc_fullpath: How To/vmw-how-use-ovf-tool.md
toc_mdlink: vmw-how-use-ovf-tool.md
---

<br>**UKCloud Limited (“UKC”) and Virtual Infrastructure Group Limited (“VIG”) (together “the Companies”) – in Compulsory Liquidation**

On 25 October 2022, the Companies were placed into Liquidation with the Official Receiver appointed as Liquidator and J Robinson and A M Hudson simultaneously appointed as Special Managers to manage the liquidation process on behalf of the Official Receiver.

Further information regarding the Liquidations can be found here: <https://www.gov.uk/government/news/virtual-infrastructure-group-limited-and-ukcloud-limited-information-for-creditors-and-interested-parties>

Contact details:<br>
For any general queries relating to the Liquidations please email <ukcloud@uk.ey.com><br>
For customer related queries please email <ukcloudcustomers@uk.ey.com><br>
For supplier related queries please email <ukcloudsuppliers@uk.ey.com>

# How to use the VMware OVF Tool

## Overview

The VMware OVF Tool is a conversion program freely downloadable from VMware that assists in the distribution of virtual machines (VMs) and vApps, converting them between OVF, VMX and OVA formats. It also includes a command‑line facility to import and export OVF packages between environments or from third party suppliers. The OVF Tool is a command‑line interface (CLI) tool only.

- **OVF (Open Virtualisation Format)** is a packaging standard created by leading virtualisation vendors. It is a platform independent, efficient, open packaging and distribution format for VMs.

- **VMX (the VM configuration file)** is a simple text file with various parameters relating to the guest VM.

- **The OVA file extension** is associated with Open Virtual Machine Format. Compared to the OVF file format, the OVA format contains all VM files and `*.ovf` files compressed into one single OVA archive file instead of many files in a folder.

## Downloading the OVF Tool

You can download the OVF Tool via the following link:

<https://customerconnect.vmware.com/downloads/get-download?downloadGroup=OVFTOOL443>

You must have a VMware account to download the tool. You can download the OVF Tool for Windows 32-bit and 64-bit, Linux 32-bit and 64-bit, or Mac OS X.

After downloading and installing the OVF Tool, you must then go to the directory in which you installed the tool to run it. There is no icon or program logo on your desktop for the OVF Tool, so to launch it, you must use the command prompt. Go to the installation folder and run:

    ovftool

## Getting started with the OVF Tool

The OVF Tool is a CLI tool, so some level of familiarity with CMD commands helps in using the tool. There are a number of help commands, which are a good source of information:

    ovftool --help
    ovftool --help examples
    ovftool --help locators
    ovftool --help config

You can also find the OVF Tool User Guide at:

<https://developer.vmware.com/docs/11748/ovf-tool-user-s-guide>

## Basic import and export commands

You'll mainly use the OVF Tool to import (deploy) and export VMs or appliances into and out of your UKCloud environment.

The basic syntax to do this using the OVF Tool is:

    ovftool <source> <target>

Refer to the OVF Tool User Guide for further commands and switches.

## Importing a .vmx file to a vApp template

To import a `.vmx` file:

1. In your UKCloud environment, create a catalog to contain the vApp template.

   ![Catalog for OVF Tool](images/vmw-vcd-ovf-catalog.png)

   For detailed instructions, see [*How to create a catalog*](vmw-how-create-catalog.md).

2. Make sure you are in the correct directory, that is, the directory containing the file you want to import.

3. Run the following command:

        ovftool --vCloudTemplate --acceptAllEulas --overwrite <filename> "vcloud://<username>@<apiURL>?org=<computeServiceID>&vappTemplate=<newTemplate>&catalog=<catalogID>"

    Where:

    - `vCloudTemplate` indicates that you're uploading a new vApp template

    - `acceptAllEulas` indicates that you accept all end user licence agreements

    - `overwrite` indicates that you're replacing an existing vApp with the new one being uploaded

    - `filename` is the name of the `.vmx` file that are importing

    - `username` is your UKCloud Portal user ID

    - `apiURL` is your Cloud Director API URL. This URL is different depending on the region in which your environment is located. For more information, see [*How to access VMware Cloud Director through the Cloud Director API*](vmw-how-access-vcloud-api.md).

    - `computeServiceID` is the ID of your UKCloud compute service (sometimes also called an org or vOrg)

    - `vappTemplate` is the ID of the vApp template

    - `catalogID` is the ID of the catalog in which the vApp template is located

    For example:

          ovftool --vCloudTemplate --acceptAllEulas --overwrite centos71.vmx "vcloud://auser@vcd.portal.skyscapecloud.com:443?org=1-2-3-a4b56c& vappTemplate=centos71&catalog=OVFTool-test"

    > [!TIP]
    > Make sure you use double quotes (`"`) rather than single quotes (`'`).

4. The `.vmx` file is uploaded as a vApp template into your environment.

    In VMware Cloud Director, expand the *Recent Tasks* panel to check the status.

## Importing an .iso file to a vApp template

To upload an ISO image:

1. Make sure you are in the correct directory, that is, the directory containing the ISO file you want to import.

2. Run the following command:

        ovftool -sourceType="ISO" "<path>\<filename>.iso" "vcloud://<username>@<apiURL>?vdc=<targetVDC>&org=<computeServiceID> &media=<name>&catalog=<catalogID>"

    Where:

    - `sourceType` (or `st`) indicates the type of the source file: `ISO`

    - `path\filename.iso` is the full location of the source `.iso` file you want to import

    - `username` is your UKCloud Portal user ID

    - `apiURL` is your Cloud Director API URL. This URL is different depending on the region in which your environment is located. For more information, see [*How to access VMware Cloud Director through the Cloud Director API*](vmw-how-access-vcloud-api.md).

    - `targetVDC` is the VDC where you want to upload the file

    - `computeServiceID` is the ID of your UKCloud compute service (sometimes also called an org or vOrg)

    - `name` is the name to display for the file in VMware Cloud Director

    - `catalogID` is the ID of the catalog to which you want to upload the file

    For example:

          ovftool -st="ISO" "C:\example.iso\" "vcloud://auser@vcd.portal.skyscapecloud.com:443?vdc=myVDC&org=1-2-3-a4b56c&media=CentOS_ISO&catalog=OVFTool-test"

    > [!TIP]
    > Make sure you use double quotes (`"`) rather than single quotes (`'`).

3. When the `ovftool` command has finished, the source and target locations are listed and then you're prompted for your username and password. When you are authenticated, the upload process is initiated.

## Feedback

If you find a problem with this article, click **Improve this Doc** to make the change yourself or raise an [issue](https://github.com/UKCloud/documentation/issues) in GitHub. If you have an idea for how we could improve any of our services, send an email to <feedback@ukcloud.com>.
