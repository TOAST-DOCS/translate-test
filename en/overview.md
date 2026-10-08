<!-- pre-align:aligned sig=71a63d528337 -->

<a id="management-certificate-manager-overview"></a>
## Management > Certificate Manager > Overview { #management-certificate-manager-overview }

If you miss extending expiration dates of TLS certificate/domain, you may not access web services.
Certificate Manager helps you not to miss expiration dates by sending notifications (via SMS or Email) when you near each date.
You can manage TLS certificate/domain/user data (e.g. license) for which expiration dates exist, and specify the notifying rules and recipients for each expiration date.

<a id="features"></a>
### Features { #features }

<a id="features-manage-tls-certificatedomainuser-data"></a>
#### Manage TLS Certificate/Domain/User Data

* Register, manage, and query certificate information
* Upload and download certificate files (pem)
* Register, manage, and query certificate usage/installation information

<a id="features-auto-collect-tls-certificate-information"></a>
#### Auto-Collect TLS Certificate Information

* For uploading certificate files, read files to collect certificate's creation date, expiration date, signature type, and certification institution
* For registering certificate installation information, download certificate out of installation information so as to collect expiration date and certificate name
    * It does not collect certificate installation information if the IP of the certificate installation information is private IP.

<a id="features-auto-collect-domain-information"></a>
#### Auto-Collect Domain Information

* With auto-collection, collect domain's creation date, expiration date, registrar, registering institution, and name server.
* In registering sub-domain information, call ping as sub-domain so as to collect if response is successful or not.
   * When the lookup IP of a sub-domain is a private IP, ping response for sub-domain is not colleted.
   * When a sub-domain is not registered at DNS, notification on failed ping response for sub-domain shall not be sent.
   * (Ping response of sub-domain is to be collected for the lookup result of a public DNS name server. If a public DNS server restricts lookup, the ping response shall not be collected.)

<a id="features-manage-notification-groups"></a>
#### Manage Notification Groups

* Register, manage, and query recipients
* Register, manage, and query notification policy on expiration dates
* Send notification to users within a corresponding notification group, once the group for TLS certificate/domain/user data is specified

<a id="features-send-notifications"></a>
#### Send Notifications

* Send notification to users when it nears an expiration date or if it fails to auto-collect
* Notification Types

| Type | Notification Recipients | Delivery Time | Description |
| --- | --- | --- | --- |
| Expiration | ADMIN/MEMBER of notification group | 09:00 (UTC+09) | Guide for expiration dates of certificate/domain/user data according to setting (e.g. since x days, or every x days) of a notification group |
| Replace Certificate Installation Information | ADMIN/MEMBER of notification group | 09:00 (UTC+09) | Guide on replacement is sent, when certificate files and installation information are registered, and if the expiration date for certificate installation information is earlier than that of certificate |
| Check Information due to Failed Auto Collection | ADMIN of notification group | 09:00 (UTC+09) | Guide is sent to check certificate installation/sub-domain information, if it fails to download certificates from IP/Port registered at certificate installation information, or if it fails to get response from ping of sub-domain |
| Check Notification Group Users due to Failed Notifications | ADMIN of notification group | 10:00 (UTC+09) | Guide is sent to ADMIN of a notification group to check its user, if notification delivery fails to a user of the group |
| Check Notification Group ADMIN due to Failed Notifications | ADMIN of project | 11:00 (UTC+09) | Guide is sent to ADMIN of a project to check ADMIN of a notification group, if delivery fails for 'Notification to check Notification Group Users due to Failed Notification Delivery' |

<a id="service-targets"></a>
### Service Targets { #service-targets }

*  Those who need to be notified on data nearing expiration dates

<a id="glossary"></a>
### Glossary { #glossary }

| Term | Description |
| --- | --- |
| TLS Certificate/ Certificate | Documents required for a website communicated via https, which can be issued from a trustworthy third-party certificate institution. Each certificate includes a private key and information of the website. |
| Certificate Usage Information | Actual usage information of a certificate (e.g. web server domain or port number). |
| Certificate Installation Information | Information of a web server in which certificate is installed (e.g. IP address, https port number, or host name) |
| Domain | The host domain area serviced by DNS. (ex. toast.com) |
| Sub-domain | Actual usage information of domain (ex. www.toast.com) |
| User Data | All data which are available in text. Format is free to choose to be notified on expiration dates. |
