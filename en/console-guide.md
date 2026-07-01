## Network > Service Gateway > Console User Guide

This guide describes how to use the **Service Gateway** service in the console.

## Service Gateway

### Create a Service Gateway

To create a service gateway, follow these steps.

1. Go to **Network > Service Gateway**.
2. Click **Create Service Gateway** to display the creation screen.
3. Enter the **name** to use for the service gateway.
4. Select the **connection type**. When you access the IP address assigned to the service gateway, it connects to the selected target.
    * **Service Endpoint**: Connects to services provided by NHN Cloud. Select the **service** to connect to from the list.
    * **Custom Endpoint**: Connects to a resource (load balancer) published by another user. Enter the **target service name** received from the endpoint publisher. The service name is in the format `{region}.sep-{12-digit hexadecimal}` (for example, `kr1.sep-0a1b2c3d4e5f`).
    > [Note] The service name entered is validated at creation, and you can connect only if you are included in the publisher's allowed projects.
5. Select a **VPC**. A service gateway associated with the selected VPC is created.
6. Select a **subnet**. The IP address of the service gateway is allocated from the selected subnet.
7. Select the **Private IP** assignment method.
    * Automatic: Automatically assigns an IP address within the CIDR range of the selected subnet.
    * Custom: Manually enter the IP address to use.
    > [Note] The IP address you enter must be within the CIDR range of the selected subnet.
8. Select whether to use **Fix NAT IP**.
    * In general, you do not need to select this option. Select it only when access control settings are required for the selected **service**.
    * This option can only be selected at creation and cannot be changed later.
    > [Note] This option is activated only for services that support it.

### View a Service Gateway

You can view service gateways that you have created on the **Network > Service Gateway** page. When you select a service gateway, its details appear at the bottom. If the connection type is **Custom Endpoint**, you can view the display name and identifier of the endpoint under **Connection Target** in the details.

### Modify a Service Gateway

To modify a service gateway, follow these steps. Only the **name** and **description** can be modified.

1. Go to **Network > Service Gateway**.
2. Click **Modify Service Gateway** and change the desired items on the modification screen.

### Delete a Service Gateway

To delete a service gateway, select the service gateway to delete on the **Network > Service Gateway** page and click **Delete Service Gateway**.

## Custom Endpoint

A custom endpoint is a feature that allows you to publish your own resource (load balancer) as an endpoint and share it so that other projects can connect to it via a service gateway. The publisher receives a **service name (service_name)** for sharing, delivers it to the targets allowed to connect, and manages the allowed projects directly.

### Create a Custom Endpoint

To create a custom endpoint, follow these steps.

1. Go to **Network > Service Gateway** and select the **Custom Endpoint** tab.
2. Click **Create Custom Endpoint** to display the creation screen.
3. Enter the **name** to use for the endpoint. (Up to 255 characters; only letters, numbers, hyphens (-), and underscores (_) are allowed.)
4. Enter the **display name**. This is the name displayed on service gateways that connect to this endpoint. If omitted, the name is used as the display name.
5. Select the **resource type** and **target resource**. Currently, only **Load Balancer** is supported as the resource type. Select the load balancer to publish as the endpoint from **Target Resource**.
6. Enter the **maximum number of gateways**. This is the maximum number of service gateways that can be created using this endpoint.
    * If left blank: There is no limit on the number of gateways that can be created.
    * If set to 0: Creation is blocked.
7. If necessary, enter a **description** and click **OK**.
8. When creation is complete, a **service name** for sharing (`{region}.sep-{12-digit hexadecimal}`) is automatically issued. Deliver this service name to the consumers that you want to allow to connect.

> [Note] You can create up to 5 custom endpoints per project by default.

### View Custom Endpoints

You can view the list of endpoints that you have created on the **Custom Endpoint** tab. When you select an endpoint, its details appear at the bottom, including **Basic Information** (service name, resource type, target resource, maximum number of gateways, etc.), **Allowed Projects**, and **Usage**.

### Modify a Custom Endpoint

Only the **name**, **display name**, **maximum number of gateways**, and **description** can be modified. The resource type and target resource cannot be changed.

1. On the **Custom Endpoint** tab, select the endpoint to modify.
2. Click **Modify** and change the desired items on the modification screen.

> [Note] Even if you reduce the maximum number of gateways, service gateways that have already been created are retained. However, you cannot create additional service gateways while the current number exceeds the maximum number of gateways.

### Delete a Custom Endpoint

On the **Custom Endpoint** tab, select the endpoint to delete and click **Delete**.

> [Caution] You cannot delete an endpoint if any service gateway is currently using it. Deleting an endpoint also deletes all registered allowed projects.

### Reissue a Service Name

If a change is needed, such as when the shared service name has been exposed externally, you can reissue the service name.

1. On the **Custom Endpoint** tab, select the endpoint, and then click **Reissue** next to the service name in **Basic Information**.
2. In the confirmation dialog, click **Reissue**.

> [Caution] When you reissue the service name, the existing service name is immediately invalidated and can no longer be found. Service gateways created with the existing service name continue to work normally, but you must use the reissued service name to create new service gateways.<br>
> [Note] Only members (owners) of the project that created the endpoint can reissue the service name.

### Manage Allowed Projects

Allowed projects is a list for managing the targets that are allowed to connect (create service gateways) to this endpoint.

1. Select the endpoint and navigate to the **Allowed Projects** tab in the details.
2. Click **Add** and select the **allowed scope**.
    * **All Projects (*)**: Allows connections from all projects.
    * **Specific Project**: Enter the **tenant ID** (32-digit hexadecimal) of the project to allow.
3. If necessary, enter a **description** and click **OK**.

> [Note] If both all projects (*) and a specific project are registered, the narrower scope (specific project) takes precedence. You can use this to switch the allowed scope without interruption. For example, if you add a specific project while all projects (*) is enabled and then delete the all projects (*) entry, the scope switches to allowing only the specific project without any connection interruption.

For existing allowed targets, only the **description** can be modified; the allowed scope and tenant ID cannot be changed. To delete an allowed target, select the target from the list and click **Delete**.

### Check Usage

You can view the list of service gateways currently connected to this endpoint on the **Usage** tab in the endpoint details. (Read-only)

## Use a Service Gateway

### Check the Service Gateway IP Address

1. Go to **Network > Service Gateway**.
2. Check the **IP address** in the service gateway list.<br>
   When you connect to this IP address from a VM Instance, you are connected to the service that the service gateway is linked to.

### Connect to the Service Gateway

If the IP address of the created service gateway is `192.168.1.42`, you can access the service in the following ways.

* When you connect to the service gateway IP address from a VM Instance, you are connected to the service selected when creating the service gateway and can use the service.
    * When using the https protocol with an IP address, certificate-related errors may occur.
    * If you need to use https, add the IP address and URL to the `/etc/hosts` file of the VM Instance.
    * Example: Download a file from Object Storage using an IP address.

            ~# wget http://192.168.1.42/v1/AUTH_8222a22c22244badbf876dcd521f3f98/test-obs/test_file.txt

* URLs are not supported when accessing the service using a service gateway. If you need URL access, you need to add the URL to the `/etc/hosts` file as in the example below.
    * Example: Download a file from **Object Storage** using a URL<br>
      Add the IP address of the service gateway and the URL of Object Storage to the `/etc/hosts` file as shown below.

            192.168.1.42    kr1-api-object-storage.nhncloudservice.com

        Access using the URL added to `/etc/hosts` instead of the IP address.

            ~# wget https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_8222a22c22244badbf876dcd521f3f98/test-obs/test_file.txt

## Example: Using Object Storage via Service Gateway

Object Storage-related content is described only to the extent necessary for the example. For detailed instructions on using Object Storage, see **User Guide > Storage > Object Storage**.

### Create a Service Gateway

To use the **Object Storage API**, you must obtain an **authentication token**. To use Object Storage from a VPC in an isolated environment without internet access, the authentication token must also be obtained via a service gateway. Create service gateways by following these steps.

1. Create a service gateway by selecting the **Object Storage** service.<br>
   This service gateway is for accessing the Object Storage API.
2. Create a service gateway by selecting the **IaaS API Identity** service.<br>
   This service gateway is for obtaining an authentication token.
3. Check the IP addresses of the two created service gateways.

### Edit the /etc/hosts File

For example, if the IP address of the service gateway created by selecting **Object Storage** is 192.168.1.42 and 192.168.1.57 is assigned as the IP address of the service gateway created by selecting **IaaS API Identity**, add the IP addresses and URLs to the `/etc/hosts` file of the VM Instance, as shown below.

> [Note] You can find the API URL of Object Storage by clicking **API Endpoint Settings** under **Storage > Object Storage** in the console.<br>
> [Caution] The API URL of Object Storage differs by region, so you must verify the URL in **API Endpoint Settings**.

```
192.168.1.42	api-identity-infrastructure.nhncloudservice.com
192.168.1.57	kr1-api-object-storage.nhncloudservice.com
```

### Obtain an Authentication Token

Set the **API password** for Object Storage and obtain an authentication token.

* Set the API password
    1. Go to **Storage > Object Storage** and click **API Endpoint Settings**.
    2. On the **API Endpoint Settings** screen, enter the password to use in **Set API Password** and click **Change**.
    > [Note] For detailed instructions, refer to [User Guide > Storage > Object Storage > API Guide](https://docs.nhncloud.com/ko/Storage/Object%20Storage/ko/api-guide/).

* Request to obtain an authentication token<br>
  Request to obtain the token to the URL of the Service Gateway created for the **IaaS API Identify** service using the **NHN Cloud login ID** and the password of **Set API Password** set previously.
    * Use your NHN Cloud login ID for `auth.passwordCredentials.username`.
    * Use the password entered in the API password settings for `auth.passwordCredentials.password`.
  

            ~# curl -X POST -H 'Content-Type:application/json' https://api-identity-infrastructure.nhncloudservice.com/v2.0/tokens -d '{"auth": {"tenantId": "2fda9d4b88244a0a92ff23841198e2e6", "passwordCredentials": {"username": "example@nhn.com", "password": "example123"}}}'

* Authentication token response<br>
  In the response below, the value of `access.token.id` is the authentication token. The authentication token is valid until the time recorded in `access.token.expires`.

            {"access":{"token":{"id":"gAAAAABiVnmCOJVJhh1W2eXGo3aL0eaZxXmd-SMDMIE3zmip2lXy6eH0BlZAlTZBG20dWEm7TF4zi4YIOTKnc6yKh_wqZsyxgMWKkpVNShzE-k6GaSThBP54QeUePSjC2t-R10X6G4xL_Wecl-V-lV-bnOfVo6Ccpz6rv9eLYJnbJw7KrIMSSiY","expires":"2022-04-13T19:19:30Z","tenant":{"id":"2fda9d4b8821111192ff23841198e2e6","name":"tTMgSSSF","groupId":"XXj2zkH7777modGU","description":"","enabled":true,"project_domain":"NORMAL","swift":true},"issued_at":"2022-04-13T07:32:14.000441"},"serviceCatalog":[{"endpoints":[{"region":"KR1","publicURL":"https://api-identity.infrastructure.cloud.toast.com/v2.0"}],"type":"identity","name":"keystone"},{"endpoints":[{"region":"KR2","publicURL":"https://kr2-api-storage.cloud.toast.com/v1/AUTH_2fda9d4b88244a0a92ff23841198e2e6"},{"region":"KR1","publicURL":"https://api-storage.cloud.toast.com/v1/AUTH_2fda9d4b88244a0a92ff23841198e2e6"}],"type":"object-store","name":"swift"}],"user":{"id":"80884888887b45dbaf9b815117130671","username":"5111111c-b111-4b11-b11b-01111f81111f","name":"5211122c-bfc4-4115-b11b-05b52f84

### Use the Object Storage API

When you have finished obtaining the authentication token, you can use the Object Storage API. Assuming that a container named example is created in the object storage and test_file.txt is uploaded to the container, you can query the file in the container by using the API as shown below.

* Request<br>
  Add the authentication token to `X-Auth-Token` and send the request.

        ~# curl -X GET -H 'X-Auth-Token:gAAAAABiVnmCOJVJhh1W2eXGo3aL0eaZxXmd-SMDMIE3zmip2lXy6eH0BlZAlTZBG20dWEm7TF4zi4YIOTKnc6yKh_wqZsyxgMWKkpVNShzE-k6GaSThBP54QeUePSjC2t-R10X6G4xL_Wecl-V-lV-bnOfVo6Ccpz6rv9eLYJnbJw7KrIMSSiY' https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2fda9d4b88244a0a92ff23841198e2e6/example

* Response<br>
  View the list of files in the Object Storage container.

        test_file.txt