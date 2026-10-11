## Game > Launching > Overview  

To execute a mobile app, a variety of information is needed, including server information, URL for Notice, and URL for Download, and changing any such information requires re-deployment of the app. However, with the Launching Service, information required for an initial app execution can be applied in real time, with no need of app redeployment, even if information is changed.   

## Main Features 

Launching provides the following features: 

* **Change service information available for dynamic changes, without server or mobile app patches**
  Information that are open for change, such as server, CDN, or maintenance status, which are required for an initial mobile app execution, can be managed under the launching service, so that any change of information does not require server or mobile app patches. 

* **Manage previous versions, even on a new mobile app version**
  With the release of a new version for mobile app, operations can be configured for previous versions, such as notification for upgrades, force updates, or restriction of access.   

* **Restrict service access on particular devices or OS versions**
  When iOS/Android version updates encounter service disruption, particular devices can be restricted from service, without server or mobile app patches.  

* **Announce messages on mobile app during user-configured period**
  Notices for maintenance schedule and events can be announced only during user-configured period; while maintenance is underway, maintenance messages can be posted with the service suspended.  

## Glossary 

Terms as follows are used for the Launching Service: 

| Term | Description                                                       |
| --- | --------------------------------------------------------------------- |
| Launching | Initial information required to run an app on a service device |
| Folder | Launching information has the tree structure, and the nodes in the middle are called 'folders': a folder can have other folders or keys. |
| Key | The lowest-level device node in the tree structure, with a value. |
| Subkey | A key to get only partial data out of the entire launching information: started with 'launching' and combined with '.'. |
| Key Pattern | A relative key of JSON-format configuration information route: started with '$' and combined with '.'. |

## Service Flow 

![[그림 1 Launching 서비스 활성화]](http://static.toastoven.net/prod_launching/en/overview_serviceflow.png)