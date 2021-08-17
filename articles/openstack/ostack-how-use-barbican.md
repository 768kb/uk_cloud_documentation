---
title: How to use Barbican KMaaS on UKCloud for OpenStack
description: Provides information on using Barbican Key Management as a Service (KMaaS) within your OpenStack environment
services: openstack
author: Steve Dixon
reviewer: Blane Bramble
lastreviewed: 17/08/2021

toc_rootlink: How To
toc_sub1:
toc_sub2:
toc_sub3:
toc_sub4:
toc_title: Use Barbican Key Management as a Service
toc_fullpath: How To/ostack-how-use-barbican.md
toc_mdlink: ostack-how-use-barbican.md
---

# Using Barbican Key Management as a Service (KMaaS)

> [!NOTE]
> This article does not apply to OpenStack Regions running the Pike release and lower (currently COR00005). All other Regions offer native Key Management as a Service

## Overview

OpenStack Key Manager (Barbican) is the secrets manager for Red Hat OpenStack Platform. You can use the Barbican API and command line to centrally manage the certificates, keys, and passwords used by OpenStack services. 

Barbican currently supports the following use cases described in this guide:

- Symmetric encryption keys - used for Block Storage (cinder) volume encryption, ephemeral disk encryption, and Object Storage (swift) encryption, among others.

- Asymmetric keys and certificates- used for glance image signing and verification, among others.

## Prerequisites

- Barbican uses port 13311 for communication. This port will need to be open for Barbican to work

- Running a recent version of the OpenStackCLI . To check for an update run:

```none
pip install --upgrade python-openstackclient 
```

## Use Cases

Use cases for Barbican include:

- Image signature verification

- LBaaS services

- Volume encryption (coming soon)

- Ephemeral disk encryption (coming soon)

## Managing secrets in Barbican

### Adding new secrets

A secret and payload can be created with a single command as below:

    $ openstack secret store --name testSecret --payload 'TestPayload'

    +---------------+------------------------------------------------------------------------------------+
    | Field         | Value                                                                              |
    +---------------+------------------------------------------------------------------------------------+
    | Secret href   | https://192.168.123.163:9311/v1/secrets/ecc7b2a4-f0b0-47ba-b451-0f7d42bc1746       |
    | Name          | testSecret                                                                         |
    | Created       | None                                                                               |
    | Status        | None                                                                               |
    | Content types | None                                                                               |
    | Algorithm     | aes                                                                                |
    | Bit length    | 256                                                                                |
    | Secret type   | opaque                                                                             |
    | Mode          | cbc                                                                                |
    | Expiration    | None                                                                               |
    -----------------------------------------------------------------------------------------------------+

Once a secret has been created the payload cannot be changed, you can only delete the whole secret. As an alternative to creating the secret and payload at the same time it is possible to create the secret and then set the payload. Again, once the payload is set it cannot be changed.

### Updating secrets

To create a secret without a payload and then separately update it you would use:

```none
$ openstack secret store --name testSecret2
+---------------+------------------------------------------------------------------------------------+
| Field         | Value                                                                              |
+---------------+------------------------------------------------------------------------------------+
| Secret href   | https://192.168.123.163:9311/v1/secrets/ca34a264-fd09-44a1-8856-c6e7116c3b16       |
| Name          | testSecret2                                                                        |
| Created       | None                                                                               |
| Status        | None                                                                               |
| Content types | None                                                                               |
| Algorithm     | aes                                                                                |
| Bit length    | 256                                                                                |
| Secret type   | opaque                                                                             |
| Mode          | cbc                                                                                |
| Expiration    | None                                                                               |
-----------------------------------------------------------------------------------------------------+
$ openstack secret update https://192.168.123.163:9311/v1/secrets/ca34a264-fd09-44a1-8856-c6e7116c3b16 'TestPayload2-updated'
```

### Deleting secrets

You can delete a secret by specifying its URI. For example:

```none
$ openstack secret delete https://192.168.123.163:9311/v1/secrets/ecc7b2a4-f0b0-47ba-b451-0f7d42bc1746
```

### Generating a symmetric key

Symmetric keys are suitable for certain tasks, such as nova disk encryption and swift object encryption. Rather than creating a secret directly, we create an "order" that is fulfilled by Barbican based upon the settings we use:

1. Generate a new 256-bit key using `order create` and store it in Barbican. For example:

    ```none
    $ openstack secret order create --name swift_key --algorithm aes --mode ctr --bit-length 256 --payload-content-type=application/octet-stream key
    ```

    ```none
    +----------------+-----------------------------------------------------------------------------------+
    | Field          | Value                                                                             |
    +----------------+-----------------------------------------------------------------------------------+
    | Order href     | https://192.168.123.173:9311/v1/orders/043383fe-d504-42cf-a9b1-bc328d0b4832       |
    | Type           | Key                                                                               |
    | Container href | N/A                                                                               |
    | Secret href    | None                                                                              |
    | Created        | None                                                                              |
    | Status         | None                                                                              |
    | Error code     | None                                                                              |
    | Error message  | None                                                                              |
    +----------------+-----------------------------------------------------------------------------------+
    ```

    - **--mode** - Generated keys can be configured to use a particular mode, such as `ctr` or `cbc`. For more information, see *NIST SP 800-38A*.

2. View the details of the order to identify the location of the generated key, shown here as the
`Secret href` value:

    ```none
    $ openstack secret order get https://192.168.123.173:9311/v1/orders/043383fe-d504-42cfa9b1-bc328d0b4832
    ```

    ```none
    +----------------+------------------------------------------------------------------------------------+
    | Field          | Value                                                                              |
    +----------------+------------------------------------------------------------------------------------+
    | Order href     | https://192.168.123.173:9311/v1/orders/043383fe-d504-42cf-a9b1-bc328d0b4832        |
    | Type           | Key                                                                                |
    | Container href | N/A                                                                                |
    | Secret href    | https://192.168.123.173:9311/v1/secrets/efcfec49-b9a3-4425-a9b6-5ba69cb18719       |
    | Created        | 2018-01-24T04:24:33+00:00                                                          |
    | Status         | ACTIVE                                                                             |
    | Error code     | None                                                                               |
    | Error message  | None                                                                               |
    +----------------+------------------------------------------------------------------------------------+
    ```

3. Retrieve the details of the secret:
   
    ```none
    $ openstack secret get https://192.168.123.173:9311/v1/secrets/efcfec49-b9a3-4425-a9b6-5ba69cb18719
    ```

    ```none
    +---------------+------------------------------------------------------------------------------------+
    | Field         | Value                                                                              |
    +---------------+------------------------------------------------------------------------------------+
    | Secret href   | https://192.168.123.173:9311/v1/secrets/efcfec49-b9a3-4425-a9b6-5ba69cb18719       |
    | Name          | swift_key                                                                          |
    | Created       | 2018-01-24T04:24:33+00:00                                                          |
    | Status        | ACTIVE                                                                             |
    | Content types | {u'default': u'application/octet-stream'}                                          |
    | Algorithm     | aes                                                                                |
    | Bit length    | 256                                                                                |
    | Secret type   | symmetric                                                                          |
    | Mode          | ctr                                                                                |
    | Expiration    | None                                                                               |
    +---------------+------------------------------------------------------------------------------------+
    ```

### Listing secrets

Secrets are identified by their URI, indicated as a `href` value. This example shows the secret you created in the previous steps:

```none
$ openstack secret list
```

```none
+------------------------------------------------------------------------------------+------+---------------------------+--------+-------------------------------------------+---------------+------------+-------------+------+------------+
| Secret href                                                                        | Name | Created                   | Status | Content types                             | Algorithm     | Bit length | Secret type | Mode | Expiration |
+------------------------------------------------------------------------------------+------+---------------------------+--------+-------------------------------------------+---------------+------------+-------------+------+------------+
| https://192.168.123.169:9311/v1/secrets/24845e6d-64a5-4071-ba99-0fdd1046172e       | None | 2018-01-22T02:23:15+00:00 | ACTIVE | {u'default': u'application/octet-stream'} | aes           | 256        | symmetric   | None | None       |
+------------------------------------------------------------------------------------+------+---------------------------+--------+-------------------------------------------+---------------+------------+-------------+------+------------+
```

## Feedback

If you find a problem with this article, click **Improve this Doc** to make the change yourself or raise an [issue](https://github.com/UKCloud/documentation/issues) in GitHub. If you have an idea for how we could improve any of our services, send an email to <feedback@ukcloud.com>.
