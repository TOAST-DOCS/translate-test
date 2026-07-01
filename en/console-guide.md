## Network > Service Gateway > Console User Guide

This guides describes how to use the **Service Gateway** service from the console.

## Service Gateway

### Create a Service Gateway

To create a service gateway, use the following steps:

1. Go to **Network > Service Gateway**.
2. Click **Create Service Gateway**, and the screen for creation appears.
3. Enter the **Name** to use for the service gateway.
4. Select the **Service**. When accessing the IP assigned to the service gateway, you will be connected to the selected service.
5. Select the **VPC**. A service gateway dependent on the selected VPC is created.
6. Select the **Subnet**. An IP address for the service gateway is assigned from the selected subnet.
7. Select how to assign the **Private IP**.
    * Auto assignment: automatically assign within the CIDR range of the selected subnet.
    * Custom: enter the IP address you want to use.
    > [Note] The IP address you enter must be within the CIDR range of the selected subnet.
8. Select whether to use **Fix NAT IP**.
    * Normally, you don't need to select it. You only need to select it if the selected **Service** requires access control settings.
    * Selection is only possible at creation time, and changes are not supported.
    > [Note] It is only enabled on services that allow selection.

### View a Service Gateway

You can check the created service gateway on the **Network > Service Gateway** page. If you select a service gateway, the service gateway information appears at the bottom.

### Modify a Service Gateway

A service gateway can be modified as follows. You can only change the **Name** and **Description**.

1. Go to **Network > Service Gateway**.
2. Click **Change Service Gateway** and change items on the change screen.

### Delete a Service Gateway

To delete a service gateway, select the service gateway you want to delete in the **Network > Service Gateway** page and click the **Delete Service Gateway** button.

## Use a Service Gateway

### Check the Service Gateway IP

1. Go to **Network > Service Gateway**.
2. Check the **IP address** in the list of service gateways.<br>
   When the VM Instance accesses this IP address, it is connected to the service that the service gateway is connected to.

### Connect to the Service Gateway

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

## Example of Using Object Storage from a Service Gateway

Content related to **object storage** are described only at the level required for explaining the example. For details on how to use object storage, refer to **User Guide > Storage > Object Storage**.

### Create a Service Gateway

To use the **Object Storage API**, you must obtain an **authentication token**. To use object storage in a VPC in an isolated environment where internet is not available, you must obtain an authentication token also using the service gateway, and create the service gateway according to the following steps.

1. Choose the **Object Storage** service to create a service gateway.<br>
   A service gateway for accessing the Object Storage API.
2. Choose the **IaaS API Identity** service to create a service gateway.<br>
   A service gateway for obtaining the authentication token.
3. Check the IP addresses on the two service gateways that have been created.

### Edit the /etc/hosts File

For example, if the IP address of the service gateway created by selecting **Object Storage** is 192.168.1.42 and 192.168.1.57 is assigned as the IP address of the service gateway created by selecting **IaaS API Identity**, add the IP addresses and URLs to the `/etc/hosts` file of the VM Instance, as shown below.

> [Note] You can check the API URL address of object storage by clicking the **Set API Endpoint** button in **Storage > Object Storage** on the console screen.<br>
> [Caution] Since the URL address of the Object Storage API used by each region is different, make sure that you check the URL in the **Set API Endpoint**.

```
192.168.1.42	api-identity-infrastructure.nhncloudservice.com
192.168.1.57	kr1-api-object-storage.nhncloudservice.com
```

### Obtain the Authentication Token

**Set the API password** for object storage and get an authentication token.

* Set the API password
    1. In **Storage > Object Storage**, click the **Set API Endpoint** button.
    2. Enter the password to use in **Set API Password** on the **API Endpoint settings** screen and click **Modify**.
    > [Note] For details on how to use it, refer to [User Guide > Storage > Object Storage > API Guide](https://docs.nhncloud.com/en/Storage/Object%20Storage/en/api-guide/).

* Request for obtaining the Authentication token<br>
  Make a request to obtain the token to the URL of the service gateway created for the **IaaS API Identify** service using the **NHN Cloud login ID** and the password of **Set API Password** set previously.
    * Use NHN Cloud login ID for `auth.passwordCredentials.username`
    * Use the password entered in **Set API Password** for `auth.passwordCredentials.password`
  

            ~# curl -X POST -H 'Content-Type:application/json' https://api-identity-infrastructure.nhncloudservice.com/v2.0/tokens -d '{"auth": {"tenantId": "2fda9d4b88244a0a92ff23841198e2e6", "passwordCredentials": {"username": "example@nhn.com", "password": "example123"}}}'

* Response for obtaining the Authentication token<br>
  In the response below, the value of the `access.token.id` entry is the authentication token. The authentication token is valid until the time in `access.token.expires`.

            {"access":{"token":{"id":"gAAAAABiVnmCOJVJhh1W2eXGo3aL0eaZxXmd-SMDMIE3zmip2lXy6eH0BlZAlTZBG20dWEm7TF4zi4YIOTKnc6yKh_wqZsyxgMWKkpVNShzE-k6GaSThBP54QeUePSjC2t-R10X6G4xL_Wecl-V-lV-bnOfVo6Ccpz6rv9eLYJnbJw7KrIMSSiY","expires":"2022-04-13T19:19:30Z","tenant":{"id":"2fda9d4b8821111192ff23841198e2e6","name":"tTMgSSSF","groupId":"XXj2zkH7777modGU","description":"","enabled":true,"project_domain":"NORMAL","swift":true},"issued_at":"2022-04-13T07:32:14.000441"},"serviceCatalog":[{"endpoints":[{"region":"KR1","publicURL":"https://api-identity.infrastructure.cloud.toast.com/v2.0"}],"type":"identity","name":"keystone"},{"endpoints":[{"region":"KR2","publicURL":"https://kr2-api-storage.cloud.toast.com/v1/AUTH_2fda9d4b88244a0a92ff23841198e2e6"},{"region":"KR1","publicURL":"https://api-storage.cloud.toast.com/v1/AUTH_2fda9d4b88244a0a92ff23841198e2e6"}],"type":"object-store","name":"swift"}],"user":{"id":"80884888887b45dbaf9b815117130671","username":"5111111c-b111-4b11-b11b-01111f81111f","name":"5211122c-bfc4-4115-b11b-05b52f84

### Use the Object Storage API

When you have finished obtaining the authentication token, you can use the Object Storage API. Assuming that a container named example is created in the object storage and test_file.txt is uploaded to the container, you can query the file in the container by using the API as shown below.

* Request<br>
  Request by adding the authentication token to `X-Auth-Token`

        ~# curl -X GET -H 'X-Auth-Token:gAAAAABiVnmCOJVJhh1W2eXGo3aL0eaZxXmd-SMDMIE3zmip2lXy6eH0BlZAlTZBG20dWEm7TF4zi4YIOTKnc6yKh_wqZsyxgMWKkpVNShzE-k6GaSThBP54QeUePSjC2t-R10X6G4xL_Wecl-V-lV-bnOfVo6Ccpz6rv9eLYJnbJw7KrIMSSiY' https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2fda9d4b88244a0a92ff23841198e2e6/example

* Response<br>
  Check the list of files in the object storage container

        test_file.txt

