<!-- pre-align:aligned sig=4cffce67e4ac -->

<a id="network-service-gateway-console-user-guide"></a>
## Network > Service Gateway > Console User Guide { #network-service-gateway-console-user-guide }

This guides describes how to use the **Service Gateway** service from the console.

<a id="service-gateway"></a>
## Service Gateway { #service-gateway }

<a id="create-a-service-gateway"></a>
### Create a Service Gateway { #create-a-service-gateway }

To create a service gateway, use the following steps:

1. Go to **Network > Service Gateway**.
2. Click the **Create Service Gateway** button, and the creation screen appears.
3. Enter the **Name** to use for the service gateway.
4. Select a **Connection Type**. When you access the IP assigned to the service gateway, it connects to the selected target.
    * **Service Endpoint**: Connects to a service provided by NHN Cloud. Select the **Service** to connect to from the list.
    * **Custom Endpoint**: Connects to a resource (load balancer) published by another user. Enter the **Target Service Name** provided by the endpoint publisher. The service name is in the format `{region}.sep-{12-digit hexadecimal}` (e.g., `kr1.sep-0a1b2c3d4e5f`).

!!! tip "Note"
    The service name you enter is validated upon creation, and you can connect to it only if it is included in the publisher's allowed projects.

5. Select **VPC**. A service gateway subordinate to the selected VPC is created.
6. Select **Subnet**. An IP for the service gateway is assigned from the selected subnet.
7. Select the **Private IP** assignment method.
    * Auto-assigned: Automatically assigns an IP within the CIDR range of the selected subnet.
    * Custom: Manually enter the IP address to use.

!!! tip "Notice"
    The IP address you enter must be within the CIDR range of the selected subnet.

8. Select whether to enable **NAT IP Static**.
    * In general, you do not need to select this option. Select it only if the **service** you chose requires access control configuration.
    * This option can only be selected at creation time and cannot be changed.

!!! tip "Note"
    This is enabled only for services that support selection.

<a id="view-a-service-gateway"></a>
### View a Service Gateway { #view-a-service-gateway }

You can check the created service gateway on the **Network > Service Gateway** page. If you select a service gateway, the service gateway information appears at the bottom. If the connection type is **Custom Endpoint**, you can check the display name and identifier of the endpoint under **Connection Target** in the details.

<a id="modify-a-service-gateway"></a>
### Modify a Service Gateway { #modify-a-service-gateway }

A service gateway can be modified as follows. You can only change the **Name** and **Description**.

1. Go to **Network > Service Gateway**.
2. Click **Change Service Gateway** and change items on the change screen.

<a id="delete-a-service-gateway"></a>
### Delete a Service Gateway { #delete-a-service-gateway }

To delete a service gateway, select the service gateway you want to delete in the **Network > Service Gateway** page and click the **Delete Service Gateway** button.

<a id="custom-endpoints"></a>
## Custom Endpoints { #custom-endpoints }

A custom endpoint is a feature that allows you to publish your own resources (load balancers) as endpoints, sharing them so that other projects can connect to them through a service gateway. The publisher receives a shared ***service name** (`service_name`), delivers it to the parties that are allowed to connect, and directly manages the list of allowed projects.

<a id="create-a-custom-endpoint"></a>
### Create a Custom Endpoint { #create-a-custom-endpoint }

To create a custom endpoint, follow these steps:

1. Go to **Network > Service Gateway** and select the **Custom Endpoint** tab.
2. Click **Create Custom Endpoint** to open the creation screen.
3. Enter a **Name** for the endpoint. (Up to 255 characters; only letters, numbers, hyphens (-), and underscores (_) are allowed.)
4. Enter a **Display Name**. This is the name that appears on service gateways connected to this endpoint. If omitted, the name is used as the display name.
5. Select a **Resource Type** and a **Target Resource**. Currently, only **Load Balancer** is supported as a resource type. Select the load balancer to publish as an endpoint from the target resource list.
6. Select the **Maximum Creation Count**. This is the maximum number of service gateways that can be created for this endpoint.
    * Unlimited: No limit on the number of service gateways that can be created. Select this option if you need more than 1,000.
    * Custom: Enter a value from 0 to 1,000. Entering 0 blocks creation.
7. Enter a **Description** if needed, and click **OK**.
8. Once creation is complete, a **Service Name** for sharing (`{region}.sep-{12-digit hexadecimal}`) is automatically issued. Provide this service name to the consumers that you want to allow connections from.

!!! tip "Note"
    By default, you can create up to 5 custom endpoints per project.

<a id="view-custom-endpoints"></a>
### View custom endpoints { #view-custom-endpoints }

You can view the list of endpoints that you have created on the **Custom Endpoint** tab. If you select an endpoint, the detailed information appears at the bottom, where you can view **Basic Information** (service name, resource type, target resource, maximum number of endpoints, and more), **Allowed Projects**, and **Usage**.

<a id="modify-a-custom-endpoint"></a>
### Modify a Custom Endpoint { #modify-a-custom-endpoint }

You can only change the **Name**, **Display Name**, **Maximum Creation Count**, and **Description**. The resource type and target resource cannot be changed.

1. On the **Custom Endpoint** tab, select the endpoint that you want to modify.
2. Click **Modify** and change the items that you want on the change screen.

!!! tip "Note"
    Even if you reduce the maximum creation count, service gateways that have already been created are retained. However, while the current count exceeds the maximum creation count, you cannot create additional service gateways.

<a id="delete-a-custom-endpoint"></a>
### Delete a Custom Endpoint { #delete-a-custom-endpoint }

On the **Custom Endpoint** tab, select the endpoint to delete and click the **Delete** button.

!!! danger "Caution"
    You cannot delete an endpoint if it is in use by any service gateway. Deleting an endpoint also deletes all registered allowed projects associated with it.

<a id="reissue-a-service-name"></a>
### Reissue a Service Name { #reissue-a-service-name }

You can reissue a service name if it needs to be changed — for example, if the shared service name has been leaked to outside parties.

1. On the **Custom Endpoint** tab, select an endpoint, and then click the **Reissue** button next to the service name in **Basic Information**.
2. In the confirmation dialog, click the **Reissue** button.

!!! danger "Caution"
    When reissued, the existing service name is immediately discarded and can no longer be found. Service gateways that were created using the existing service name will continue to work normally, but you must use the reissued service name to create new service gateways.

!!! tip "Note"
    Only a member (owner) of the project that created the endpoint can reissue a service name.

<a id="manage-allowed-projects"></a>
### Manage Allowed Projects { #manage-allowed-projects }

The allowed projects list manages the targets that are permitted to connect to this endpoint (by creating a service gateway).

1. Select an endpoint and go to the **Allowed Projects** tab in the details section.
2. Click **Add** and select the **Allowed Scope**.
    * **All Projects (\*)**: Allows connections from all projects.
    * **Specific Project**: Enter the **tenant ID** (32-digit hexadecimal) of the project to allow.
3. If needed, enter a **Description** and click **Confirm**.

!!! tip "Note"
    If both All Projects (\*) and a specific project are registered together, the narrower scope (specific project) takes effect. You can use this to switch the allowed scope without any connection interruption. For example, if you add a specific project while All Projects (\*) is active and then delete All Projects (\*), the configuration switches to allow only the specific project without interrupting any existing connections.

For existing allowed targets, only the **Description** can be modified; the allowed scope and tenant ID cannot be changed. To delete an allowed target, select the target from the list and click **Delete**.

<a id="check-usage-status"></a>
### Check Usage Status { #check-usage-status }

On the **Usage Status** tab of the endpoint details, you can check the list of service gateways currently connected to this endpoint. (Read-only)

<a id="use-a-service-gateway"></a>
## Use a Service Gateway { #use-a-service-gateway }

<a id="check-the-service-gateway-ip"></a>
### Check the Service Gateway IP { #check-the-service-gateway-ip }

1. Go to **Network > Service Gateway**.
2. Check the **IP address** in the list of service gateways.<br>
   When the VM Instance accesses this IP address, it is connected to the service that the service gateway is connected to.

<a id="connect-to-the-service-gateway"></a>
### Connect to the Service Gateway { #connect-to-the-service-gateway }

For example, if the IP address of the created service gateway is `192.168.1.42`, the service can be accessed in the following ways.

* If you connect to the service gateway IP from the VM Instance, you can connect to the service selected when creating the service gateway and use the service.
    * If you use the https protocol with an IP address, you may encounter certificate related errors.
    * If you need to use https, add the IP address and URL to `/etc/hosts` of the VM Instance.
    * Example: Downloading a file from object storage using an IP address

            ~# wget http://192.168.1.42/v1/AUTH_8222a22c22244badbf876dcd521f3f98/test-obs/test_file.txt

* URLs are not supported when accessing the service using a service gateway. If you need URL access, you need to add the URL to the `/etc/hosts` file as in the example below.
    * Example: Downloading a file from **object storage** using a URL<br>
      Add the IP address of the service gateway and the URL of the object storage to the `/etc/hosts` file as shown below.

            192.168.1.42    kr1-api-object-storage.nhncloudservice.com

        Connect to the URL added to `/etc/hosts` instead of the IP address

            ~# wget https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_8222a22c22244badbf876dcd521f3f98/test-obs/test_file.txt

<a id="example-of-using-object-storage-from-a-service-gateway"></a>
## Example of Using Object Storage from a Service Gateway { #example-of-using-object-storage-from-a-service-gateway }

Content related to **object storage** are described only at the level required for explaining the example. For details on how to use object storage, refer to **User Guide > Storage > Object Storage**.

<a id="example-of-using-object-storage-from-a-service-gateway-create-a-service-gateway"></a>
### Create a Service Gateway { #example-of-using-object-storage-from-a-service-gateway-create-a-service-gateway }

To use the **Object Storage API**, you must obtain an **authentication token**. To use object storage in a VPC in an isolated environment where internet is not available, you must obtain an authentication token also using the service gateway, and create the service gateway according to the following steps.

1. Choose the **Object Storage** service to create a service gateway.<br>
   A service gateway for accessing the Object Storage API.
2. Choose the **IaaS API Identity** service to create a service gateway.<br>
   A service gateway for obtaining the authentication token.
3. Check the IP addresses on the two service gateways that have been created.

<a id="edit-the-etchosts-file"></a>
### Edit the /etc/hosts File { #edit-the-etchosts-file }

For example, if the IP address of the service gateway created by selecting **Object Storage** is 192.168.1.42 and 192.168.1.57 is assigned as the IP address of the service gateway created by selecting **IaaS API Identity**, add the IP addresses and URLs to the `/etc/hosts` file of the VM Instance, as shown below.

!!! tip "Tip"
    You can check the API URL address of object storage by clicking the **Set API Endpoint** button in **Storage > Object Storage** on the console screen.

!!! danger "Caution"
    Since the URL address of the Object Storage API used by each region is different, make sure that you check the URL in **Set API Endpoint**.

```
192.168.1.42	api-identity-infrastructure.nhncloudservice.com
192.168.1.57	kr1-api-object-storage.nhncloudservice.com
```

<a id="obtain-the-authentication-token"></a>
### Obtain the Authentication Token { #obtain-the-authentication-token }

**Set the API password** for object storage and get an authentication token.

* Set API Password
    1. In **Storage > Object Storage**, click the **Set API Endpoint** button.
    2. Enter the password to use in **Set API Password** on the **API Endpoint settings** screen and click **Modify**.

!!! tip "Tip"
    For details on how to use it, refer to [User Guide > Storage > Object Storage > API Guide](https://docs.nhncloud.com/en/Storage/Object%20Storage/ko/api-guide/).

* Request for obtaining the Authentication token<br>
  Make a request to obtain the token to the URL of the service gateway created for the **IaaS API Identify** service using the **NHN Cloud login ID** and the password of **Set API Password** set previously.
    * Use NHN Cloud login ID for `auth.passwordCredentials.username`
    * Use the password entered in **Set API Password** for `auth.passwordCredentials.password`
  

            ~# curl -X POST -H 'Content-Type:application/json' https://api-identity-infrastructure.nhncloudservice.com/v2.0/tokens -d '{"auth": {"tenantId": "2fda9d4b88244a0a92ff23841198e2e6", "passwordCredentials": {"username": "example@nhn.com", "password": "example123"}}}'

* Response for obtaining the Authentication token<br>
  In the response below, the value of the `access.token.id` entry is the authentication token. The authentication token is valid until the time in `access.token.expires`.

            {"access":{"token":{"id":"gAAAAABiVnmCOJVJhh1W2eXGo3aL0eaZxXmd-SMDMIE3zmip2lXy6eH0BlZAlTZBG20dWEm7TF4zi4YIOTKnc6yKh_wqZsyxgMWKkpVNShzE-k6GaSThBP54QeUePSjC2t-R10X6G4xL_Wecl-V-lV-bnOfVo6Ccpz6rv9eLYJnbJw7KrIMSSiY","expires":"2022-04-13T19:19:30Z","tenant":{"id":"2fda9d4b8821111192ff23841198e2e6","name":"tTMgSSSF","groupId":"XXj2zkH7777modGU","description":"","enabled":true,"project_domain":"NORMAL","swift":true},"issued_at":"2022-04-13T07:32:14.000441"},"serviceCatalog":[{"endpoints":[{"region":"KR1","publicURL":"https://api-identity.infrastructure.cloud.toast.com/v2.0"}],"type":"identity","name":"keystone"},{"endpoints":[{"region":"KR2","publicURL":"https://kr2-api-storage.cloud.toast.com/v1/AUTH_2fda9d4b88244a0a92ff23841198e2e6"},{"region":"KR1","publicURL":"https://api-storage.cloud.toast.com/v1/AUTH_2fda9d4b88244a0a92ff23841198e2e6"}],"type":"object-store","name":"swift"}],"user":{"id":"80884888887b45dbaf9b815117130671","username":"5111111c-b111-4b11-b11b-01111f81111f","name":"5211122c-bfc4-4115-b11b-05b52f84

<a id="use-the-object-storage-api"></a>
### Use the Object Storage API { #use-the-object-storage-api }

When you have finished obtaining the authentication token, you can use the Object Storage API. Assuming that a container named example is created in the object storage and test_file.txt is uploaded to the container, you can query the file in the container by using the API as shown below.

* Request<br>
  Request by adding the authentication token to `X-Auth-Token`

        ~# curl -X GET -H 'X-Auth-Token:gAAAAABiVnmCOJVJhh1W2eXGo3aL0eaZxXmd-SMDMIE3zmip2lXy6eH0BlZAlTZBG20dWEm7TF4zi4YIOTKnc6yKh_wqZsyxgMWKkpVNShzE-k6GaSThBP54QeUePSjC2t-R10X6G4xL_Wecl-V-lV-bnOfVo6Ccpz6rv9eLYJnbJw7KrIMSSiY' https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2fda9d4b88244a0a92ff23841198e2e6/example

* Response<br>
  Check the list of files in the object storage container

        test_file.txt

