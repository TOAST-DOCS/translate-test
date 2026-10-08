<!-- pre-align:aligned sig=f4b3b577c934 -->

# Cloud Access Troubleshooting Guide

**Security > Cloud Access > Troubleshooting Guide**

<br>

<a id="connected-agent-but-cannot-access-the-instance"></a>
## Connected agent, but cannot access the instance { #connected-agent-but-cannot-access-the-instance }

To access the instance after logging in, make sure to configure the following settings:

* Route Settings
    * For details, refer to [Console User Guide - Getting Started](./console-user-guide/cloud-access-start/)
* ACL Policy Settings
    * This is an access control policy applied when accessing internal instances. You must allow the IP in the **ACL Policy** tab.
* Security Groups Settings
    * You must allow the source IP in the instance's security group settings.

<br>

<a id="after-entering-information-to-add-a-connection-a-failure-message-will-be-displayed-during-verification"></a>
## After entering information to add a connection, a failure message will be displayed during verification. { #after-entering-information-to-add-a-connection-a-failure-message-will-be-displayed-during-verification }

The Cloud Access agent can access both public and private clouds. Go to **Settings - Cloud Preferences** in the tray icon menu to check out the environment you wish to add a connection to.

<br>

<a id="im-a-windows-user-but-biometric-authentication-is-not-working"></a>
## I'm a Windows user, but biometric authentication is not working { #im-a-windows-user-but-biometric-authentication-is-not-working }

Cloud Access biometric authentication requires a device that supports fingerprint or facial recognition. If your device does not support biometric authentication, you can configure a PIN from Account > Sign-in options and use it as an alternative method.

<br>

<a id="the-user-account-is-created-but-nothing-appears-when-clicking-the-add-user-object-button"></a>
## The user account is created, but nothing appears when clicking the Add User Object button { #the-user-account-is-created-but-nothing-appears-when-clicking-the-add-user-object-button }

In the following cases, the user object will not appear in the list:

* Immediately after account creation, before authentication is complete
    * IP confirmation is only possible once authentication is complete.
* If the account is created with a dynamic IP type

<br>

<a id="password-policy-is-enabled-but-login-is-possible-with-an-invalid-password"></a>
## Password policy is enabled, but login is possible with an invalid password { #password-policy-is-enabled-but-login-is-possible-with-an-invalid-password }

Even if the password policy is **enabled** and saved, it will not apply to existing users or users who have already changed their password.
The policy only applies to newly created users when the **Force Initial Password Change** option is enabled. In this case, reset the password of the user account and prompt the user to use a password that complies with the policy. 

<br>

<a id="force-initial-password-change-is-enabled-but-the-change-screen-does-not-appear-on-login"></a>
## Force Initial Password Change is enabled, but the change screen does not appear on login { #force-initial-password-change-is-enabled-but-the-change-screen-does-not-appear-on-login }

This option only applies to new user accounts created after enabling it. It does not apply to existing accounts even if the setting is changed afterward. Reset the password for the user account and proceed with the password change.

<br>

<a id="clicking-the-link-account-button-shows-a-popup-saying-no-activated-services"></a>
## Clicking the Link Account button shows a popup saying no activated services { #clicking-the-link-account-button-shows-a-popup-saying-no-activated-services }

If the Cloud Access service is not active, account linking is not possible. Activate the service before linking again or delete unnecessary connections.

<br>

<a id="after-activating-services-in-both-pangyo-and-pyeongchon-regions-deactivating-a-single-region-is-not-supported"></a>
## After activating services in both Pangyo and Pyeongchon regions, deactivating a single region is not supported { #after-activating-services-in-both-pangyo-and-pyeongchon-regions-deactivating-a-single-region-is-not-supported }

Currently, deactivation is applied to all regions at once, so deactivating a specific region individually is not supported.
To use the service in only one region, deactivate it first, then reactivate it in the desired region. (Support for deleting individual regions is planned for a future update.)

<br>

!!! tip "If the problem is not resolved"
    If you followed the troubleshooting guide and your issue persists, please contact the NHN Cloud Customer Center.
    * [1:1 Online Inquiry](https://www.nhncloud.com/kr/support/inquiry?alias=tab16_15)
    * Representative Phone: 1588-7967 (Operating hours: Monday to Friday 10:00-19:00)