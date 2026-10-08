<!-- pre-align:aligned sig=a867bdc4fe63 -->

# Settings

**Security > Cloud Access > Console User Guide > Settings**

In the **Settings** tab, you can configure various options required to operate the Cloud Access service.

<br>

<a id="log-settings"></a>
## Log Settings { #log-settings }

<a id="default-deny-policy-log-settings"></a>
### Default Deny Policy Log Settings { #default-deny-policy-log-settings }

When the Cloud Access service is activated, a default-deny policy appears in the **Policy > ACL Policy** tab. If set to **Enabled**, logs for traffic matching this policy will be stored.

<a id="remote-log-transfer-settings"></a>
### Remote Log Transfer Settings { #remote-log-transfer-settings }

Cloud Access provides remote log transfer features via Syslog, Object Storage, and Log & Crash Search, allowing traffic logs generated during operation to be automatically sent to external destinations for long-term retention.

* Syslog: Send traffic logs to up to two specified IP addresses.

![syslog.PNG](../../static/images/2025.06.24/syslog.png)

* Object Storage: Send logs to the NHN Cloud Object Storage service.

![OBS.PNG](../../static/images/2025.06.24/OBS.png)

* Log & Crash Search: Send logs to the NHN Cloud Log & Crash Search service.

![LNCS.PNG](../../static/images/2025.06.24/LNCS.png)

<br>

!!! tip "Note"
    * Syslog supports only a single IP address (IP ranges and CIDR blocks are not supported).
    * Object Storage and Log & Crash Search services must be activated in advance to use remote log transfer.
    * For required input when setting up Object Storage, refer to the [Object Storage User Guide](/Storage/Object%20Storage/en/s3-api-guide/#aws-sdk).

<br>

<a id="general-settings"></a>
## General Settings { #general-settings }

<a id="connection-settings"></a>
### Connection Settings { #connection-settings }

* You can check the connection information provided during service activation. You may change the Customer Name and Algorithm.
    * Supports AES-256 and ChaCha20 algorithms.

<a id="login-security-settings"></a>
### Login Security Settings { #login-security-settings }

* Configure the login failure limit, password expiration period, and password policy.
    * Login Failed: Set the number of allowed failed login attempts (1 to 5).
    * Password Expiration: Set the validity period for passwords (1 to 180 days).
    * Password Policy: Set password creation rules for agent users.
        * Some mandatory policies are always enforced regardless of settings.

<a id="notice-settings"></a>
### Notice Settings { #notice-settings }

* Set a custom message to be displayed to users during agent authentication.
    * Up to 200 characters can be entered.

<a id="logo-settings"></a>
### Logo Settings { #logo-settings }

* Upload a company logo or other image that meets the requirements to be shown on the login screen.

<br>

!!! tip "Note"
    * The Domain, Customer Key, and Secret Key in the connection settings are required when adding connections in the agent. Be sure not to expose them externally.
    * If a user account is locked due to login failures or password expiration, please contact an NHN Cloud Console administrator with Cloud Access permissions.
    * The notice message can also be viewed later from the agent tray icon menu.

!!! danger "Caution"
    * Login security settings apply to all users using the Cloud Access agent. Use caution when enabling them.