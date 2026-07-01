## Network > Service Gateway > Console User Guide

This guide describes how to use the **Service Gateway** service in the console.

## Service Gateway

### Create a Service Gateway

To create a service gateway:

1. Go to **Network > Service Gateway**.
2. Click the **Create Service Gateway** button to open the creation screen.
3. Enter a **Name** for the service gateway.
4. Select a **Connection Type**. When you access the IP address assigned to the service gateway, it connects to the selected target.
    * **Service Endpoint**: Connects to a service provided by NHN Cloud. Select the **Service** to connect to from the list.
    * **Custom Endpoint**: Connects to a resource (load balancer) published by another user. Enter the **Target Service Name** provided by the endpoint publisher. The service name is in the format `{region}.sep-{12-digit hexadecimal}` (e.g., `kr1.sep-0a1b2c3d4e5f`).
    > [Note] The service name that you enter is validated upon creation and can only be connected if it is included in the publisher's allowed projects.
5. Select a **VPC**. A service gateway is created that is associated with the selected VPC.
6. Select a **Subnet**. The IP address for the service gateway is assigned from the selected subnet.
7. Select a method for assigning a **Private IP**.
    * Automatic: Automatically assigned within the CIDR range of the selected subnet.
    * Custom: Manually enter the IP address to use.
    > [Note] The IP address that you enter must be within the CIDR range of the selected subnet.
8. Select whether to enable **Fix NAT IP**.
    * In general, you do not need to select this option. Select it only when access control settings are required for the selected **service**.
    * This option can only be selected at creation and cannot be changed later.
    > [Note] This option is activated only for services that support it.

### View a Service Gateway

You can view the service gateways that you created on the **Network > Service Gateway** screen. Select a service gateway to view its information at the bottom of the screen. If the connection type is **Custom Endpoint**, you can view the display name and identifier of the endpoint under **Connection Target** in the details.

### Modify a Service Gateway

To modify a service gateway, you can only change the **Name** and **Description**.

1. Go to **Network > Service Gateway**.
2. Click the **Modify Service Gateway** button and make the desired changes in the modification screen.

### Delete a Service Gateway

To delete a service gateway, go to the **Network > Service Gateway** screen, select the service gateway to delete, and click the **Delete Service Gateway** button.

## Custom Endpoint

A custom endpoint is a feature that allows you to publish your own resource (load balancer) as an endpoint and share it so that other projects can connect to it through a service gateway. The publisher obtains a **service name (service_name)** for sharing, passes it to those authorized to connect, and manages the allowed projects directly.

### Create a Custom Endpoint

To create a custom endpoint:

1. Go to **Network > Service Gateway** and select the **Custom Endpoint** tab.
2. Click the **Create Custom Endpoint** button to open the creation screen.
3. Enter a **Name** for the endpoint. (Up to 255 characters; only letters, numbers, hyphens (-), and underscores (_) are allowed.)
4. Enter a **Display Name**. This is the name displayed on the service gateway that connects to this endpoint. If omitted, the name is used as the display name.
5. Select a **Resource Type** and **Target Resource**. Currently, only **Load Balancer** is supported as the resource type. Select the load balancer to publish as an endpoint from the target resource.
6. Enter the **Maximum Number of Creations**. This is the maximum number of service gateways that can be created for this endpoint.
    * If left blank: Unlimited creations are allowed.
    * 0: Creation is blocked.
7. Optionally, enter a **Description** and click the **OK** button.
8. Once the creation is complete, a **service name** (`{region}.sep-{12-digit hexadecimal}`) for sharing is automatically generated. Pass this service name to the consumers who are authorized to connect.

> [Note] You can create up to 5 custom endpoints per project by default.

### View a Custom Endpoint

You can view the list of endpoints that you created on the **Custom Endpoint** tab. Select an endpoint to view its details at the bottom of the screen, including **Basic Information** (service name, resource type, target resource, maximum number of creations, etc.), **Allowed Projects**, and **Usage Status**.

### Modify a Custom Endpoint

You can only change the **Name**, **Display Name**, **Maximum Number of Creations**, and **Description**. The resource type and target resource cannot be changed.

1. Select the endpoint to modify on the **Custom Endpoint** tab.
2. Click the **Modify** button and make the desired changes in the modification screen.

> [Note] Even if you reduce the maximum number of creations, service gateways that have already been created are retained. However, you cannot create additional service gateways while the current number exceeds the maximum number of creations.

### Delete a Custom Endpoint

On the **Custom Endpoint** tab, select the endpoint to delete and click the **Delete** button.

> [Caution] You cannot delete an endpoint if even one service gateway is using it. Deleting an endpoint also deletes the registered allowed projects.

### Reissue Service Name

If the shared service name is leaked or needs to be changed for any reason, you can reissue the service name.

1. On the **Custom Endpoint** tab, select the endpoint and click the **Reissue** button next to the service name in **Basic Information**.
2. In the confirmation dialog, click the **Reissue** button.

> [Caution] Once reissued, the existing service name is immediately invalidated and is no longer accessible. Service gateways that were created using the existing service name continue to work normally, but you must use the reissued service name to create new service gateways.<br>
> [Note] Only members (owners) of the project that created the endpoint can reissue the service name.

### Manage Allowed Projects

Allowed projects is a list that manages the targets authorized to connect (create a service gateway) to this endpoint.

1. Select the endpoint and go to the **Allowed Projects** tab in the details.
2. Click the **Add** button and select an **Allowed Scope**.
    * **All Projects (*)**: Allows connections from all projects.
    * **Specific Project**: Enter the **Tenant ID** (32-digit hexadecimal) of the project to allow.
3. Optionally, enter a **Description** and click the **OK** button.

> [Note] If you register both an all-allow (*) entry and specific projects, the narrower scope (specific projects) takes effect. You can use this to switch the allowed scope without any service interruption. For example, if you add specific projects while an all-allow (*) entry is active and then delete the all-allow (*) entry, the scope switches to allow only specific projects without interrupting any connections.

For existing allowed targets, you can only change the **Description**. The allowed scope and tenant ID cannot be changed. To delete an allowed target, select the target from the list and click the **Delete** button.

### View Usage Status

On the **Usage Status** tab in the endpoint details, you can view the list of service gateways currently connected to this endpoint. (Read-only)

## Use a Service Gateway

### Check the Service Gateway IP Address

1. Go to **Network > Service Gateway**.
2. Check the **IP Address** in the service gateway list.<br>
   When you access this IP address from a VM Instance, you are connected to the service that the service gateway is connected to.

### Connect to the Service Gateway

If the IP address of the created service gateway is `192.168.1.42`, you can access the service in the following ways:

* If you connect to the service gateway IP from a VM Instance, you are connected to the service selected when creating the service gateway and can use the service.
    * Using the IP address with the HTTPS protocol may cause certificate-related errors.
    * If you need to use HTTPS, add the IP address and URL to the `/etc/hosts` file of the VM Instance.
    * Example) Download a file from Object Storage using the IP address

            ~# wget http://192.168.1.42/v1/AUTH_8222a22c22244badbf876dcd521f3f98/test-obs/test_file.txt

* URLs are not supported when accessing the service using a service gateway. If you need URL access, you need to add the URL to the `/etc/hosts` file as in the example below.
    * Example) Download a file from **Object Storage** using a URL<br>
      Add the IP address of the service gateway and the URL of Object Storage to the `/etc/hosts` file as follows:

            192.168.1.42    kr1-api-object-storage.nhncloudservice.com

        Access using the URL added to `/etc/hosts` instead of the IP address:

            ~# wget https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_8222a22c22244badbf876dcd521f3f98/test-obs/test_file.txt

## Object Storage Usage Example with Service Gateway

The content related to **Object Storage** is described only at the level needed for the example. For detailed instructions on how to use Object Storage, refer to **User Guide > Storage > Object Storage**.

### Create a Service Gateway

To use the **Object Storage API**, you must obtain an **authentication token**. To use Object Storage in a VPC in an isolated environment where internet access is not available, you must also obtain the authentication token through a service gateway. Create the service gateways by following these steps:

1. Select the **Object Storage** service to create a service gateway.<br>
   This service gateway is for accessing the Object Storage API.
2. Select the **IaaS API Identity** service to create a service gateway.<br>
   This service gateway is for issuing authentication tokens.
3. Check the IP addresses of the two created service gateways.

### Edit the /etc/hosts File

For example, if the IP address of the Service Gateway created by selecting **Object Storage** is 192.168.1.42 and 192.168.1.57 is assigned as the IP address of the Service Gateway created by selecting **IaaS API Identity**, add the IP addresses and URLs to the `/etc/hosts` file of the VM Instance, as shown below.

> [Note] You can find the API endpoint URL for Object Storage by clicking the **API Endpoint Settings** button in **Storage > Object Storage** on the console.<br>
> [Caution] The Object Storage API URL differs by region, so make sure to check the URL in **API Endpoint Settings**.

```
192.168.1.42	api-identity-infrastructure.nhncloudservice.com
192.168.1.57	kr1-api-object-storage.nhncloudservice.com
```

### Issue an Authentication Token

Set the **API Password** for Object Storage and obtain an authentication token.

* Set the API Password
    1. In **Storage > Object Storage**, click the **API Endpoint Settings** button.
    2. In the **API Endpoint Settings** screen, enter the password to use in the **API Password** field and click the **Change** button.
    > [Note] For detailed instructions, refer to [User Guide > Storage > Object Storage > API Guide](https://docs.nhncloud.com/ko/Storage/Object%20Storage/ko/api-guide/).

* Request to issue an authentication token<br>
  Request to obtain the token to the URL of the Service Gateway created for the **IaaS API Identity** service using the **NHN Cloud login ID** and the password of **Set API Password** set previously.
    * Use your NHN Cloud login ID for `auth.passwordCredentials.username`.
    * Use the password entered in API Password for `auth.passwordCredentials.password`.
  

            ~# curl -X POST -H 'Content-Type:application/json' https://api-identity-infrastructure.nhncloudservice.com/v2.0/tokens -d '{"auth": {"tenantId": "2fda9d4b88244a0a92ff23841198e2e6", "passwordCredentials": {"username": "example@nhn.com", "password": "example123"}}}'

* Authentication token response<br>
  In the response below, the value of the `access.token.id` field is the authentication token. The authentication token is valid until the time recorded in `access.token.expires`.

            {"access":{"token":{"id":"gAAAAABiVnmCOJVJhh1W2eXGo3aL0eaZxXmd-SMDMIE3zmip2lXy6eH0BlZAlTZBG20dWEm7TF4zi4YIOTKnc6yKh_wqZsyxgMWKkpVNShzE-k6GaSThBP54QeUePSjC2t-R10X6G4xL_Wecl-V-lV-bnOfVo6Ccpz6rv9eLYJnbJw7KrIMSSiY","expires":"2022-04-13T19:19:30Z","tenant":{"id":"2fda9d4b8821111192ff23841198e2e6","name":"tTMgSSSF","groupId":"XXj2zkH7777modGU","description":"","enabled":true,"project_domain":"NORMAL","swift":true},"issued_at":"2022-04-13T07:32:14.000441"},"serviceCatalog":[{"endpoints":[{"region":"KR1","publicURL":"https://api-identity.infrastructure.cloud.toast.com/v2.0"}],"type":"identity","name":"keystone"},{"endpoints":[{"region":"KR2","publicURL":"https://kr2-api-storage.cloud.toast.com/v1/AUTH_2fda9d4b88244a0a92ff23841198e2e6"},{"region":"KR1","publicURL":"https://api-storage.cloud.toast.com/v1/AUTH_2fda9d4b88244a0a92ff23841198e2e6"}],"type":"object-store","name":"swift"}],"user":{"id":"80884888887b45dbaf9b815117130671","username":"5111111c-b111-4b11-b11b-01111f81111f","name":"5211122c-bfc4-4115-b11b-05b52f84

### Use the Object Storage API

When you have finished obtaining the authentication token, you can use the Object Storage API. Assuming that a container named example is created in the object storage and test_file.txt is uploaded to the container, you can query the file in the container by using the API as shown below.

* Request<br>
  Add the authentication token to `X-Auth-Token` and send the request.

        ~# curl -X GET -H 'X-Auth-Token:gAAAAABiVnmCOJVJhh1W2eXGo3aL0eaZxXmd-SMDMIE3zmip2lXy6eH0BlZAlTZBG20dWEm7TF4zi4YIOTKnc6yKh_wqZsyxgMWKkpVNShzE-k6GaSThBP54QeUePSjC2t-R10X6G4xL_Wecl-V-lV-bnOfVo6Ccpz6rv9eLYJnbJw7KrIMSSiY' https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2fda9d4b88244a0a92ff23841198e2e6/example

* Response<br>
  View the list of files in the Object Storage container.

        test_file.txt