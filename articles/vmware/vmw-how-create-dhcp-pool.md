---
title: How to create a DHCP pool
description: Shows how to configure DHCP within the vCloud Director/VMware Cloud Director Tenant Portal
services: vmware
author: shighmoor
reviewer: shighmoor
lastreviewed: 17/09/2020

toc_rootlink: How To
toc_sub1:
toc_sub2:
toc_sub3:
toc_sub4:
toc_title: Create a DHCP pool
toc_fullpath: How To/vmw-how-create-dhcp-pool.md
toc_mdlink: vmw-how-create-dhcp-pool.md
---

# How to create a DHCP pool

## Overview

With VDC networks you have the option of creating an IP pool of addresses to be assigned automatically or manually (known as a static IP pool). These addresses are injected into virtual machines (VMs) via VMware Tools during guest customisation. They appear in the usual places in Windows and Linux where you would interrogate IP settings and show as static addresses.

In some situations, you may require true DHCP functionality in your VMs, so that IP addresses are shown as dynamically defined. As with an IP pool, you're defining a non-overlapping range of IP addresses to use on the network.

## Creating a DHCP pool

To create a DHCP pool:

### [vCloud Director 9.7](#tab/tabid-a)

1. In the vCloud Director *Virtual Datacenters* dashboard, select the VDC that contains the edge gateway in which you want to create the DHCP pool.

2. In the left navigation panel, click **Edges**.

    ![Edges menu option in vCloud Director](images/vmw-vcd91-mnu-edges.png)

3. Select the edge that you want to configure and click **Configure Services**.

    ![Configure Services button](images/vmw-vcd-edge-btn-config.png)

4. Select the **DHCP** tab.

    ![DHCP tab](images/vmw-vcd-adv-edge-tab-dhcp.png)

5. On the **Pools** tab, click the **Add** button.

    ![Add DHCP button](images/vmw-vcd-btn-add-dhcp-adv.png)

6. Select the network to which you want to apply the DHCP pool, then define an IP range for the pool. You can leave the lease times as default or change them.

    ![Add DHCP Pool dialog box](images/vmw-vcd-add-dhcp-pool-adv.png)

7. When you're finished, click **Keep**.

### [VMware Cloud Director 10.1](#tab/tabid-b)

1. In the VMware Cloud Director *Virtual Data Center* dashboard, select the VDC that contains the edge gateway in which you want to create the DHCP pool.

2. In the left navigation panel, under *Networking*, select **Edges**.

    ![Edges menu option in VMware Cloud Director](images/vmw-vcd10.1-mnu-edges.png)

3. Select the edge that you want to configure and click **Services**.

    ![Services button](images/vmw-vcd10.1-edge-btn-services.png)

4. Select the **DHCP** tab.

    ![DHCP tab](images/vmw-vcd10.1-edge-tab-dhcp.png)

5. Select the **Pools** tab, then click the **Create** button.

    ![Add DHCP button](images/vmw-vcd10.1-btn-add-dhcp.png)

6. In the *Add DHCP Pool* dialog box, select the network to which you want to apply the DHCP pool, then define an IP range for the pool. You can leave the lease times as default or change them.

    ![Add DHCP Pool dialog box](images/vmw-vcd10.1-add-dhcp-pool.png)

7. When you're finished, click **Keep**.

***

## Next steps

In this article you've learned how to create a DHCP pool. For other edge gateway configuration tasks, see:

- [*How to create firewall rules*](vmw-how-create-firewall-rules.md)

- [*How to create NAT rules*](vmw-how-create-nat-rules.md)

- [*How to configure IPsec VPN*](vmw-how-configure-ipsec-vpn.md)

- [*How to configure a load balancer*](vmw-how-configure-load-balancer.md)

- [*How to create a static route*](vmw-how-create-static-route.md)

## Feedback

If you find a problem with this article, click **Improve this Doc** to make the change yourself or raise an [issue](https://github.com/UKCloud/documentation/issues) in GitHub. If you have an idea for how we could improve any of our services, send an email to <feedback@ukcloud.com>.
