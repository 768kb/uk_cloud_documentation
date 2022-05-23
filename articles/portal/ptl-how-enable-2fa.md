---
title: How to enable two-factor authentication in the UKCloud Portal
description: Describes how to enable two-factor authentication (2FA) for a UKCloud Portal account
services: portal
author: shighmoor
reviewer: shighmoor
lastreviewed: 21/04/2022

toc_rootlink: How To
toc_sub1: 
toc_sub2:
toc_sub3:
toc_sub4:
toc_title: Enable 2FA in the Portal
toc_fullpath: How To/ptl-how-enable-2fa.md
toc_mdlink: ptl-how-enable-2fa.md
---

# How to enable two-factor authentication in the UKCloud Portal

## Overview

To provide additional security, you may want to enable two-factor authentication (2FA) in the UKCloud Portal. 2FA requires that users enter a randomly generated code, as well as their user name and password, when logging in to the Portal.

![Two-Factor Authentication dialog box in the UKCloud Portal](images/ptl-2fa.png)

To set up 2FA, a Portal administrator must first enable 2FA for the Portal customer account. After enabling 2FA for the account, the next time a user attempts to log in, they will be prompted to set up 2FA for their user account by registering their account with an authenticator app, such as Google Authenticator.

### Intended audience

To enable 2FA, you must be a Portal administrator.

## Enabling 2FA in the UKCloud Portal

To enable 2FA:

1. [*Log in to the UKCloud Portal*](ptl-gs.md#logging-in-to-the-ukcloud-portal) as an administrator.

2. If necessary, [*switch to the account*](ptl-how-switch-account.md) for which you want to enable 2FA.

3. In the navigation panel, select **Settings**.

   ![Settings menu option in the UKCloud Portal](images/ptl-mnu-settings.png)

4. On the *Settings* page, select the **Security Settings** tab.

   ![Security Settings tab of the Settings page](images/ptl-settings-tab-security.png)

5. Click **Google Two-Factor Authentication (2FA)** to expand the section.

6. Select the **Enable Google Two-Factor Authentication (2FA)** check box.

   ![Enable 2FA security setting](images/ptl-2fa-enable.png)

7. When you're done, click **Save**.

   The next time a user logs in to the Portal to access the account, they will be prompted to set up 2FA for their user account. For more information, see [*How to set up two-factor authentication for a user account*](ptl-how-setup-2fa.md).

## Related articles

- [*How to set up two-factor authentication for a user account*](ptl-how-setup-2fa.md)

- [*How to reset two-factor authentication for a user account*](ptl-how-reset-2fa.md)

## Feedback

If you find a problem with this article, click **Improve this Doc** to make the change yourself or raise an [issue](https://github.com/UKCloud/documentation/issues) in GitHub. If you have an idea for how we could improve any of our services, send an email to <feedback@ukcloud.com>.
