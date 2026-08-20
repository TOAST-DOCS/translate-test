<!-- machine_translated: true -->

<!-- pre-align:aligned sig=08050b417a83 -->

# NCS API Guide

**Container > NHN Container Service(NCS) > API Guide**

<a id="ncs-api-common-information"></a>
## NCS API Common Information { #ncs-api-common-information }

<a id="api-endpoint"></a>
### API Endpoint { #api-endpoint }

| Region | Domain |
| --- | --- |
| Korea (Pangyo) region | https://kr1-ncs.api.nhncloudservice.com |
| Korea (Gwangju) region | https://kr3-ncs.api.nhncloudservice.com |

<a id="authentication-and-permission"></a>
### Authentication and Permission { #authentication-and-permission }

NCS uses a User Access Key token for authentication/authorization when making API calls. A User Access Key token is a temporary, Bearer-type access token issued from a User Access Key, used for authentication and authorization when calling the API. For more information on issuing and using User Access Key tokens, please refer to the [User Access Key Token](/nhncloud/en/public-api/user-access-key-token).

<a id="common-response-information"></a>
### Common Response Information { #common-response-information }

Returns <strong>200 OK</strong> for all API requests. For more information on the response results, see Response Body Header.

<details>
  <summary><strong>Success Response</strong></summary>

```
{
  "header": {
    "isSuccessful": true,
    "resultCode": 200,
    "resultMessage": "SUCCESS"
  }
}

```

</details>

<details>
  <summary><strong>Failure Response</strong></summary>

```
{
  "header": {
    "isSuccessful": false,
    "resultCode": 10002,
    "resultMessage": "Bad Request."
  }
}
```

</details>

| Name | Type | Description |
| --- | --- | --- |
| header | Object | API response information |
| header.isSuccessful | Boolean | <li>true: Normal</li><li>false: Error</li> |
| header.resultCode | Integer | <li>200: Normal</li><li>10000 or higher: Error</li> |
| header.resultMessage | String | <li>SUCCESS: Normal</li><li>Other: Error cause message</li> |

---

> [Caution]
> In each API response, you may find fields that are not specified within this guide. Those fields are for NHN Cloud internal usage, and as such refrain from using them since they may be changed without prior notice.

<a id="template"></a>
## Template { #template }

<a id="view-template-list"></a>
### List Templates { #view-template-list }

Retrieves a list of templates.

```bash
GET /ncs/v1.0/appkeys/{appKey}/templates
x-nhn-authorization: Bearer {accessToken}
```

<a id="view-template-list-request"></a>
#### Request

This API does not require a request body.

| Name | Type | Format | Required | Description |
| --- | --- | --- | --- | --- |
| appKey | URL | String | O | Service Appkey |
| token | Header | String | O | NHN Cloud Token |
| page | Query | Integer | X | Page number to retrieve |
| size | Query | Integer | X | Page size to retrieve (default: 10) |
| disable\_containers | Query | Boolean | X | <li>true: Retrieve excluding containers</li><li>false: Retrieve including containers (default)</li> |

<a id="view-template-list-response"></a>
#### Response

| Name | Type | Format | Required | Description |
| --- | --- | --- | --- | --- |
| X-Total-Count | Header | Integer | O | Number of templates created in Appkey |
| templates | Body | Array | O | Template list |
| templates.id | Body | UUID | O | Template ID |
| templates.version | Body | String | O | Template version |
| templates.name | Body | String | O | Template name |
| templates.createdAt | Body | String | O | Creation time (UTC) |
| templates.description | Body | String | X | Template description |
| templates.versionDescription | Body | String | O | Template version description |
| templates.networks | Body | Array | O | Network information of the template |
| templates.networks.vpcId | Body | String | O | VPC ID of the template |
| templates.networks.subnetId | Body | String | O | Subnet ID of the template |
| templates.dnsConfig | Body | String List | X | DNS server information configured in the container |
| templates.hostAliases | Body | List | X | Information configured in the container's `/etc/hosts` |
| templates.hostAliases.ip | Body | String | O | IP of the hostnames configured in the container |
| templates.hostAliases.hostnames | Body | String List | O | Hostnames of the IP configured in the container |
| templates.versionCount | Body | Integer | O | Number of versions of the template |
| templates.workloadCount | Body | Integer | O | Number of workloads using the template |
| templates.containers | Body | Array | O | Container list of the template |
| templates.containers.name | Body | String | O | Container name |
| templates.containers.type | Body | String | O | Container Type<ul><li>normal: General</li><li>init: Initialization</li></ul>|
| templates.containers.image | Body | String | O | Container image |
| templates.containers.cpus | Body | Float | O | Number of CPUs allocated to the container |
| templates.containers.memoryLimit | Body | Object | O | Memory information allocated to the container |
| templates.containers.memoryLimit.hard | Body | Integer | O | Memory allocated to the container (MiB) |
| templates.containers.gpuFlavor | Body | String | X | GPU Flavor information<ul><li>ncs1.g1m5</li><li>ncs1.g2m10</li></ul> |
| templates.containers.ports | Body | Array | X | Port information used by the container |
| templates.containers.ports.containerPort | Body | Integer | O | Container port |
| templates.containers.ports.protocol | Body | String | O | Container protocol<ul><li>TCP</li><li>UDP</li><li>HTTP</li><li>HTTPS</li><li>TERMINATED\_HTTPS</li></ul> |
| templates.containers.command | Body | String List | X | Commands to run when the container starts |
| templates.containers.args | Body | String List | X | Arguments used when the container starts |
| templates.containers.workDirectory | Body | String | X | Working directory of the container |
| templates.containers.env | Body | Array | X | Container environment variables |
| templates.containers.env.name | Body | String | O | Container environment variable name |
| templates.containers.env.value | Body | String | O | Container environment variable value |
| templates.containers.postStart | Body | String List | X | Commands that run immediately after container creation |
| templates.containers.preStop | Body | String List | X | Commands that run immediately after container termination |
| templates.containers.configs | Body | List | X | ConfigMap information used by containers |
| templates.containers.configs.id | Body | Integer | O | ConfigMap ID |
| templates.containers.configs.type | Body | String | O | Service type for retrieving ConfigMap information<ul><li>obs: Object Storage</li></ul> |
| templates.containers.configs.value | Body | String | O | Object URL |
| templates.containers.configs.mountPath | Body | String | O | Container mount path |
| templates.containers.secrets | Body | List | X | Secret information used by the container |
| templates.containers.secrets.type | Body | String | O | Service type for retrieving Secret information<ul><li>skm: Secure Key Manager</li></ul> |
| templates.containers.secrets.value | Body | String | O | Key ID |
| templates.containers.secrets.mountPath | Body | String | O | Container mount path |
| templates.containers.volumes | Body | Array | X | NAS storage information used by the container |
| templates.containers.volumes.name | Body | String | O | Storage name |
| templates.containers.volumes.path | Body | String | O | NAS storage connection path |
| templates.containers.volumes.mountPath | body | String | X | Container connection path |
| templates.containers.probe | Body | List | X | Container Probe settings |
| templates.containers.probe.type | Body | String | O | Container Probe type<ul><li>startup</li><li>liveness</li></ul> |
| templates.containers.probe.failureThreshold | Body | Integer | O | Probe failure threshold |
| templates.containers.probe.initialDelaySeconds | Body | Integer | O | Probe initial delay time |
| templates.containers.probe.periodSeconds | Body | Integer | O | Probe execution interval |
| templates.containers.probe.timeoutSeconds | Body | Integer | O | Probe execution timeout |
| templates.containers.probe.exec | Body | String List | O | Probe execution commands |
| templates.containers.stopTimeout | Body | Integer | X | Initialization container execution timeout (seconds) |
| templates.containers.sharedMemory | Body | Object | X | Container shared memory settings |
| templates.containers.sharedMemory.changed | Body | Boolean | O | Whether the container shared memory settings were changed<ul><li>true: Changed</li><li>false: Not changed</li></ul> |
| templates.containers.sharedMemory.sizeLimit | Body | Boolean | O | Shared memory to set for the container (MiB) |

<details>
  <summary>Example</summary>

```json
{
  "header": {
    "resultCode": 200,
    "resultMessage": "SUCCESS",
    "isSuccessful": true
  },
  "templates": [
    {
      "createdAt": "2024-10-24T05:43:26.029Z",
      "updatedAt": "2024-10-24T05:43:26.029Z",
      "id": "bf095f99-1547-48f4-b57d-1124e853f6e2",
      "name": "nginx-template",
      "namespace": "abd7f92e-3353-4b45-944c-510a97ef89c9",
      "containers": [
        {
          "id": "51be9a5d-4737-4323-ae57-0ade225f4f4d",
          "name": "nginx",
          "image": "nginx:latest",
          "imageRegistry": "other",
          "imageRegistryType": "public",
          "cpus": 0.25,
          "memoryLimit": {
            "hard": 256
          },
          "ports": [
            {
              "hostPort": 80,
              "containerPort": 80,
              "protocol": "TCP"
            }
          ],
          "restartCount": 0,
          "type": "normal"
        }
      ],
      "networks": [
        {
          "vpcId": "aeeafe4e-287d-4dd4-b91a-294b87688457",
          "subnetId": "abd7f92e-3353-4b45-944c-510a97ef89c9"
        }
      ],
      "dnsConfig": [
        "223.255.201.241",
        "211.50.32.6"
      ],
      "versionCount": 2,
      "version": "second",
    },
    {
      "createdAt": "2024-10-24T05:44:25.292Z",
      "updatedAt": "2024-10-24T05:44:25.292Z",
      "id": "edfabd08-187b-4195-bed9-dad5d0b4d854",
      "name": "ubuntu",
      "namespace": "abd7f92e-3353-4b45-944c-510a97ef89c9",
      "containers": [
        {
          "id": "aeb71431-01b9-4b4b-8f2d-326b7863d0a9",
          "name": "ubuntu",
          "image": "ubuntu:latest",
          "imageRegistry": "other",
          "imageRegistryType": "public",
          "cpus": 1,
          "memoryLimit": {
            "hard": 256
          },
          "command": [
            "bash",
            "-c",
            "sleep infinity"
          ],
          "restartCount": 0,
          "type": "normal"
        }
      ],
      "networks": [
        {
          "vpcId": "aeeafe4e-287d-4dd4-b91a-294b87688457",
          "subnetId": "abd7f92e-3353-4b45-944c-510a97ef89c9"
        }
      ],
      "dnsConfig": [
        "223.255.201.241",
        "211.50.32.6"
      ],
      "versionCount": 1,
      "version": "1",
      "versionDescription": "ubuntu test"
    }
  ]
}
```

</details>

<a id="view-template"></a>

### View Template { #view-template }

Retrieves information about an individual template.

```bash
GET /ncs/v1.0/appkeys/{appKey}/templates/{templateId}
x-nhn-authorization: Bearer {accessToken}
```

<a id="view-template-request"></a>

#### Request

This API does not require a request body.

| Name | Type | Format | Required | Description |
| --- | --- | --- | --- | --- |
| appKey | URL | String | O | Service Appkey |
| templateId | URL | String | O | Template ID |
| token | Header | String | O | NHN Cloud Token |

<a id="view-template-response"></a>

#### Response

| Name | Type | Format | Required | Description |
| --- | --- | --- | --- | --- |
| template | Body | Object | O | Template information |
| template.id | Body | UUID | O | Template ID |
| template.version | Body | String | O | Template version |
| template.name | Body | String | O | Template name |
| template.createdAt | Body | String | O | Creation time (UTC) |
| template.description | Body | String | X | Template description |
| template.versionDescription | Body | String | X | Template version description |
| template.networks | Body | Array | O | Network information of the template |
| template.networks.vpcId | Body | String | O | VPC ID of the template |
| template.networks.subnetId | Body | String | O | Subnet ID of the template |
| template.dnsConfig | Body | String List | X | DNS server information configured in the container |
| template.hostAliases | Body | List | X | Information configured in the container's `/etc/hosts` |
| template.hostAliases.ip | Body | String | O | IP of the hostnames configured in the container |
| template.hostAliases.hostnames | Body | String List | O | Hostnames of the IP configured in the container |
| template.versionCount | Body | Integer | O | Number of versions of the template |
| template.workloadCount | Body | Integer | O | Number of workloads using the template |
| template.containers | Body | Array | O | List of containers in the template |
| template.containers.name | Body | String | O | Container name |
| template.containers.type | Body | String | O | Container Type<ul><li>normal: General</li><li>init: Initialization</li></ul> |
| template.containers.image | Body | String | O | Container image |
| template.containers.cpus | Body | Float | O | Number of CPUs allocated to the container |
| template.containers.memoryLimit | Body | Object | O | Memory information allocated to the container |
| template.containers.memoryLimit.hard | Body | Integer | O | Memory allocated to the container (MiB) |
| template.containers.gpuFlavor | Body | String | X | GPU Flavor information<ul><li>ncs1.g1m5</li><li>ncs1.g2m10</li></ul> |
| template.containers.ports | Body | Array | X | Port information used by the container |
| template.containers.ports.containerPort | Body | Integer | O | Container port |
| template.containers.ports.protocol | Body | String | O | Container protocol<ul><li>TCP</li><li>UDP</li><li>HTTP</li><li>HTTPS</li><li>TERMINATED\_HTTPS</li></ul> |
| template.containers.command | Body | String List | X | Command to run when the container starts |
| template.containers.args | Body | String List | X | Arguments used when the container starts |
| template.containers.workDirectory | Body | String | X | Working directory of the container |
| template.containers.env | Body | Array | X | Container environment variables |
| template.containers.env.name | Body | String | O | Container environment variable name |
| template.containers.env.value | Body | String | O | Container environment variable value |
| template.containers.postStart | Body | String List | X | Commands that run immediately after container creation |
| template.containers.preStop | Body | String List | X | Commands executed immediately before the container is stopped |
| template.containers.configs | Body | List | X | ConfigMap information used by the container |
| template.containers.configs.id | Body | Integer | O | ConfigMap ID |
| template.containers.configs.type | Body | String | O | Service type for retrieving ConfigMap information<ul><li>obs: Object Storage</li></ul> |
| template.containers.configs.value | Body | String | O | Object URL |
| template.containers.configs.mountPath | Body | String | O | Container mount path |
| template.containers.secrets | Body | List | X | Secret information used by the container |
| template.containers.secrets.type | Body | String | O | Service type for retrieving Secret information<ul><li>skm: Secure Key Manager</li></ul> |
| template.containers.secrets.value | Body | String | O | Key ID |
| template.containers.secrets.mountPath | Body | String | O | Container mount path |
| template.containers.volumes | Body | Array | X | NAS storage information used by the container |
| template.containers.volumes.name | Body | String | O | Storage name |
| template.containers.volumes.path | Body | String | O | NAS storage connection path |
| template.containers.volumes.mountPath | body | String | X | Container connection path |
| template.containers.probe | Body | List | X | Container Probe configuration |
| template.containers.probe.type | Body | String | O | Container Probe type<ul><li>startup</li><li>liveness</li></ul> |
| template.containers.probe.failureThreshold | Body | Integer | O | Probe failure criteria |
| template.containers.probe.initialDelaySeconds | Body | Integer | O | Probe startup latency |
| template.containers.probe.periodSeconds | Body | Integer | O | Probe execution interval |
| template.containers.probe.timeoutSeconds | Body | Integer | O | Probe execution timeout |
| template.containers.probe.exec | Body | String List | O | Command to run a probe |
| template.containers.stopTimeout | Body | Integer | X | Initialization container execution timeout (seconds) |
| template.containers.sharedMemory | Body | Object | X | Container shared memory settings information |
| template.containers.sharedMemory.changed | Body | Boolean | O | Whether the container shared memory settings have been changed<ul><li>true: Changed</li><li>false: Not changed</li></ul> |
| template.containers.sharedMemory.sizeLimit | Body | Boolean | O | Shared memory set for the container (MiB) |

<details>
  <summary>Example</summary>

```json
{
  "header": {
    "resultCode": 200,
    "resultMessage": "SUCCESS",
    "isSuccessful": true
  },
  "template": {
    "createdAt": "2024-10-24T05:43:26.029Z",
    "updatedAt": "2024-10-24T05:43:26.029Z",
    "id": "bf095f99-1547-48f4-b57d-1124e853f6e2",
    "name": "nginx-template",
    "namespace": "abd7f92e-3353-4b45-944c-510a97ef89c9",
    "containers": [
      {
        "id": "51be9a5d-4737-4323-ae57-0ade225f4f4d",
        "name": "nginx",
        "image": "nginx:latest",
        "imageRegistry": "other",
        "imageRegistryType": "public",
        "cpus": 0.25,
        "memoryLimit": {
          "hard": 256
        },
        "ports": [
          {
            "hostPort": 80,
            "containerPort": 80,
            "protocol": "TCP"
          }
        ],
        "restartCount": 0,
        "type": "normal"
      }
    ],
    "networks": [
      {
        "vpcId": "aeeafe4e-287d-4dd4-b91a-294b87688457",
        "subnetId": "abd7f92e-3353-4b45-944c-510a97ef89c9"
      }
    ],
    "dnsConfig": [
      "223.255.201.241",
      "211.50.32.6"
    ],
    "versionCount": 2,
    "version": "second",
  }
}
```

</details>

<a id="create-template"></a>

### Create Template { #create-template }

Creates a template.

```bash
POST /ncs/v1.0/appkeys/{appKey}/templates
Content-Type: application/json
x-nhn-authorization: Bearer {accessToken}
```

| Name | Type | Format | Required | Description |
| --- | --- | --- | --- | --- |
| appKey | URL | String | O | Service Appkey |
| token | Header | String | O | NHN Cloud Token |
| template | Body | Array | O | Template information |
| template.name | Body | String | O | Template name |
| template.version | Body | String | X | Template version |
| template.description | Body | String | X | Template description |
| template.versionDescription | Body | String | X | Template version description |
| template.networks | Body | Array | O | Network information of the template |
| template.networks.vpcId | Body | String | O | VPC ID of the template |
| template.networks.subnetId | Body | String | O | Subnet ID of the template |
| template.dnsConfig | Body | String List | X | DNS server information used by the container (up to three settings) |
| template.hostAliases | Body | List | X | Information to set in container `/etc/hosts` |
| template.hostAliases.ip | Body | String | O | IP information used by hostnames |
| template.hostAliases.hostnames | Body | String List | O | Host information used by hostnames |
| template.containers | Body | Array | O | Container list of the template |
| template.containers.name | Body | String | O | Container name |
| template.containers.type | Body | String | X | Container Type<ul><li>normal: General</li><li>init: Init</li></ul>|
| template.containers.image | Body | String | O | Container image |
| template.containers.imageRegistryCredentials | Body | Object | X | Information for accessing a private registry |
| template.containers.imageRegistryCredentials.username | Body | String | O | Private registry ID |
| template.containers.imageRegistryCredentials.password | Body | String | O | Private registry password |
| template.containers.cpus | Body | Float | O | Number of CPUs allocated to the container |
| template.containers.memoryLimit | Body | Object | O | Memory information allocated to the container |
| template.containers.memoryLimit.hard | Body | Integer | O | Memory allocated to the container (MiB) |
| template.containers.gpuFlavor | Body | String | X | GPU Flavor information<ul><li>ncs1.g1m5</li><li>ncs1.g2m10</li></ul> |
| template.containers.ports | Body | Array | X | Port information used by the container |
| template.containers.ports.containerPort | Body | Integer | O | Container port |
| template.containers.ports.protocol | Body | String | O | Container protocol<ul><li>TCP</li><li>UDP</li><li>HTTP</li><li>HTTPS</li><li>TERMINATED\_HTTPS</li></ul> |
| template.containers.command | Body | String List | X | Commands to run when the container starts |
| template.containers.args | Body | String List | X | Arguments used when the container starts |
| template.containers.workDirectory | Body | String | X | Working directory of the container |
| template.containers.env | Body | Array | X | Container environment variables |
| template.containers.env.name | Body | String | O | Container environment variable name |
| template.containers.env.value | Body | String | O | Container environment variable value |
| template.containers.postStart | Body | String List | X | Commands that run immediately after container creation |
| template.containers.preStop | Body | String List | X | Commands that run immediately before the container is stopped |
| template.containers.configs | Body | List | X | ConfigMap information used by the container (up to 10) |
| template.containers.configs.id | Body | Integer | O | ConfigMap ID |
| template.containers.configs.type | Body | String | O | Service type for retrieving ConfigMap information<ul><li>obs: Object Storage</li></ul> |
| template.containers.configs.appKey | Body | String | O | Object Storage AppKey |
| template.containers.configs.userAccessKeyId | Body | String | O | User Access Key for users accessing the Object Storage service |
| template.containers.configs.secretAccessKey | Body | String | O | Secret Access Key for users accessing the Object Storage service |
| template.containers.configs.value | Body | String | O | Object URL |
| template.containers.configs.mountPath | Body | String | O | Container mount path |
| template.containers.secrets | Body | List | X | Secret information used by the container (up to 10) |
| template.containers.secrets.type | Body | String | O | Service type for retrieving Secret information<ul><li>skm: Secure Key Manager</li></ul> |
| template.containers.secrets.value | Body | String | O | Key ID |
| template.containers.secrets.mountPath | Body | String | O | Container mount path |
| template.containers.volumes | Body | Array | X | NAS storage information used by the container |
| template.containers.volumes.name | Body | String | O | Storage name |
| template.containers.volumes.path | Body | String | O | NAS storage connection path |
| template.containers.volumes.mountPath | body | String | X | Container connection path (default: /mnt) |
| template.containers.probe | Body | List | X | Container Probe configuration |
| template.containers.probe.type | Body | String | O | Container Probe type<ul><li>startup</li><li>liveness</li></ul> |
| template.containers.probe.failureThreshold | Body | Integer | O | Probe failure threshold |
| template.containers.probe.initialDelaySeconds | Body | Integer | O | Probe startup latency |
| template.containers.probe.periodSeconds | Body | Integer | O | Probe execution interval<li>Must be set to a value smaller than timeoutSeconds.</li> |
| template.containers.probe.timeoutSeconds | Body | Integer | O | Probe execution timeout<li>A value greater than periodSeconds must be set.</li> |
| template.containers.probe.exec | Body | String List | O | Probe execution command |
| template.containers.stopTimeout | Body | Integer | X | Initialization container execution timeout (seconds)<ul><li>30 to 120 (default: 30)</li></ul>|
| template.containers.sharedMemory | Body | Object | X | Container shared memory settings |
| template.containers.sharedMemory.changed | Body | Boolean | O | Whether the container shared memory settings have changed<ul><li>true: Changed</li><li>false: Not changed</li></ul> |
| template.containers.sharedMemory.sizeLimit | Body | Boolean | O | Shared memory set for the container (MiB) |

<details>
  <summary>Example</summary>

```json
{
  "template": {
    "containers": [
      {
        "cpus": 0.25,
        "image": "nginx:latest",
        "memoryLimit": {
          "hard": 256
        },
        "name": "nginx",
        "ports": [
          {
            "containerPort": 80,
            "protocol": "tcp"
          }
        ]
      }
    ],
    "description": "api template",
    "name": "api-template",
    "networks": [
      {
        "subnetId": "abd7f92e-3353-4b45-944c-510a97ef89c9",
        "vpcId": "aeeafe4e-287d-4dd4-b91a-294b87688457"
      }
    ],
    "version": "api-1"
  }
}
```

</details>

<a id="create-template-response"></a>

#### Response

| Name | Type | Format | Required | Description |
| --- | --- | --- | --- | --- |
| template | Body | Object | O | Template information |
| template.id | Body | UUID | O | Template ID |
| template.name | Body | String | O | Template name |
| template.version | Body | String | O | Template version |
| template.createdAt | Body | String | O | Creation time (UTC) |
| template.description | Body | String | X | Template description |
| template.versionDescription | Body | String | X | Template version description |
| template.networks | Body | Array | O | Network information of the template |
| template.networks.vpcId | Body | String | O | VPC ID of the template |
| template.networks.subnetId | Body | String | O | Subnet ID of the template |
| template.dnsConfig | Body | String List | X | DNS server information set in the template |
| template.hostAliases | Body | List | X | Information set up in container `/etc/hosts` |
| template.hostAliases.ip | Body | String | O | IP of the hostnames set in the container |
| template.hostAliases.hostnames | Body | String List | O | hostnames of the IP set in the container |
| template.containers | Body | Array | O | List of containers in the template |
| template.containers.name | Body | String | O | Container name |
| template.containers.type | Body | String | O | Container Type<ul><li>normal: General</li><li>init: Initialization</li></ul>|
| template.containers.image | Body | String | O | Container image |
| template.containers.cpus | Body | Float | O | Number of CPU assigned to container |
| template.containers.memoryLimit | Body | Object | O | Information on memory assigned to container |
| template.containers.memoryLimit.hard | Body | Integer | O | Memory allocated to the container (MiB) |
| template.containers.gpuFlavor | Body | String | X | GPU Flavor information<ul><li>ncs1.g1m5</li><li>ncs1.g2m10</li></ul> |
| template.containers.ports | Body | Array | X | Port information used by the container |
| template.containers.ports.containerPort | Body | Integer | O | Container port |
| template.containers.ports.protocol | Body | String | O | Container protocol<ul><li>TCP</li><li>UDP</li><li>HTTP</li><li>HTTPS</li><li>TERMINATED\_HTTPS</li></ul> |
| template.containers.command | Body | String List | X | Command to run when the container starts |
| template.containers.args | Body | String List | X | Arguments used when the container starts |
| template.containers.workDirectory | Body | String | X | Working directory of the container |
| template.containers.env | Body | Array | X | Container environment variables |
| template.containers.env.name | Body | String | O | Container environment variable name |
| template.containers.env.value | Body | String | O | Container environment variable value |
| template.containers.postStart | Body | String List | X | Commands that run immediately after container creation |
| template.containers.preStop | Body | String List | X | Commands that run immediately before the container is stopped |
| template.containers.configs | Body | List | X | ConfigMap information used by the container |
| template.containers.configs.id | Body | Integer | O | ConfigMap ID |
| template.containers.configs.type | Body | String | O | Service type for retrieving ConfigMap information<ul><li>obs: Object Storage</li></ul> |
| template.containers.configs.value | Body | String | O | Object URL |
| template.containers.configs.mountPath | Body | String | O | Container mount path |
| template.containers.secrets | Body | List | X | Secret information used by the container |
| template.containers.secrets.type | Body | String | O | Service type for retrieving Secret information<ul><li>skm: Secure Key Manager</li></ul> |
| template.containers.secrets.value | Body | String | O | Key ID |
| template.containers.secrets.mountPath | Body | String | O | Container mount path |
| template.containers.volumes | Body | Array | X | Information on NAS storage used in containers |
| template.containers.volumes.name | Body | String | O | Storage name |
| template.containers.volumes.path | Body | String | O | NAS Storage Connection Path |
| template.containers.volumes.mountPath | body | String | X | Container connection path |
| template.containers.probe | Body | List | X | Container Probe settings |
| template.containers.probe.type | Body | String | O | Container Probe type<ul><li>startup</li><li>liveness</li></ul> |
| template.containers.probe.failureThreshold | Body | Integer | O | Probe failure threshold |
| template.containers.probe.initialDelaySeconds | Body | Integer | O | Probe startup latency |
| template.containers.probe.periodSeconds | Body | Integer | O | Probe execution interval |
| template.containers.probe.timeoutSeconds | Body | Integer | O | Probe execution timeout |
| template.containers.probe.exec | Body | String List | O | Probe execution commands |
| template.containers.stopTimeout | Body | Integer | X | Initialization container execution timeout (seconds) |
| template.containers.sharedMemory | Body | Object | X | Container shared memory settings |
| template.containers.sharedMemory.changed | Body | Boolean | O | Whether to change the container shared memory settings<ul><li>true: Changed</li><li>false: Not changed</li></ul> |
| template.containers.sharedMemory.sizeLimit | Body | Boolean | O | Shared memory to set for container (MiB) |

<details>
  <summary>Example</summary>

```json
{
  "header": {
    "resultCode": 200,
    "resultMessage": "SUCCESS",
    "isSuccessful": true
  },
  "template": {
    "createdAt": "2024-10-24T05:47:00.693Z",
    "updatedAt": "2024-10-24T05:47:00.693Z",
    "id": "89ab3d2f-385a-4322-8694-32cb7955f8de",
    "name": "api-template",
    "namespace": "abd7f92e-3353-4b45-944c-510a97ef89c9",
    "description": "api template",
    "containers": [
      {
        "id": "25f2753c-b7e3-42a3-ad8c-a0cfe4e6155f",
        "name": "nginx",
        "image": "nginx:latest",
        "imageRegistry": "other",
        "imageRegistryType": "public",
        "cpus": 0.25,
        "memoryLimit": {
          "hard": 256
        },
        "ports": [
          {
            "containerPort": 80,
            "protocol": "TCP"
          }
        ],
        "restartCount": 0,
        "type": "normal"
      }
    ],
    "networks": [
      {
        "vpcId": "aeeafe4e-287d-4dd4-b91a-294b87688457",
        "subnetId": "abd7f92e-3353-4b45-944c-510a97ef89c9"
      }
    ],
    "dnsConfig": [
      "223.255.201.241",
      "211.50.32.6"
    ],
    "version": "api-1"
  }
}
```

</details>

<a id="delete-template"></a>

### Delete Template { #delete-template }

Deletes a template.

```bash
DELETE /ncs/v1.0/appkeys/{appKey}/templates/{templateId}
x-nhn-authorization: Bearer {accessToken}
```

<a id="delete-template-request"></a>
#### Request

This API does not require a request body.

| Name | Type | Format | Required | Description |
| --- | --- | --- | --- | --- |
| appKey | URL | String | O | Service Appkey |
| templateId | URL | String | O | Template ID |
| token | Header | String | O | NHN Cloud Token |

<a id="delete-template-response"></a>
#### Response

This API responds with common information.

<a id="view-a-list-of-template-versions"></a>

### View a List of Template Versions { #view-a-list-of-template-versions }

```bash
GET /ncs/v1.0/appkeys/{appKey}/templates/{templateId}/versions
x-nhn-authorization: Bearer {accessToken}
```

<a id="view-a-list-of-template-versions-request"></a>

#### Request

This API does not require a request body.

| Name | Type | Format | Required | Description |
| --- | --- | --- | --- | --- |
| appKey | URL | String | O | Service Appkey |
| templateId | Path | String | O | Template ID |
| token | Header | String | O | NHN Cloud Token |
| q | Query | String | X | Search parameter |
| page | Query | Integer | X | Page number to retrieve |
| size | Query | Integer | X | Page size to retrieve (default: 10) |
| sort | Query | String | X | Field name to sort by<br>Prefix field names with `-` for reverse sorting<br>Example: `sort=-name` |

<a id="view-a-list-of-template-versions-response"></a>

#### Response

| Name | Type | Format | Required | Description |
| --- | --- | --- | --- | --- |
| X-Total-Count | Header | Integer | O | Number of template versions |
| templates | Body | Array | O | Template version list |
| templates.id | Body | UUID | O | Template ID |
| templates.version | Body | String | O | Template version |
| templates.name | Body | String | O | Template name |
| templates.createdAt | Body | String | O | Creation time (UTC) |
| templates.description | Body | String | X | Template description |
| templates.versionDescription | Body | String | X | Template version description |
| templates.networks | Body | Array | O | Network information of the template |
| templates.networks.vpcId | Body | String | O | VPC ID of the template |
| templates.networks.subnetId | Body | String | O | Subnet ID of the template |
| templates.dnsConfig | Body | String List | X | DNS server information configured in the container |
| templates.hostAliases | Body | List | X | Information configured in the container's `/etc/hosts` |
| templates.hostAliases.ip | Body | String | O | IP of the hostnames configured in the container |
| templates.hostAliases.hostnames | Body | String List | O | Hostnames of the IP configured in the container |
| templates.versionCount | Body | Integer | O | Number of versions of the template |
| templates.workloadCount | Body | Integer | O | Number of workloads using the template |
| templates.containers | Body | Array | O | Container list of the template |
| templates.containers.name | Body | String | O | Container name |
| templates.containers.type | Body | String | O | Container Type<ul><li>normal: General</li><li>init: Initialization</li></ul>|
| templates.containers.image | Body | String | O | Container image |
| templates.containers.cpus | Body | Float | O | Number of CPUs allocated to the container |
| templates.containers.memoryLimit | Body | Object | O | Memory information allocated to the container |
| templates.containers.memoryLimit.hard | Body | Integer | O | Memory allocated to the container (MiB) |
| templates.containers.gpuFlavor | Body | String | X | GPU Flavor information<ul><li>ncs1.g1m5</li><li>ncs1.g2m10</li></ul> |
| templates.containers.ports | Body | Array | X | Port information used by the container |
| templates.containers.ports.containerPort | Body | Integer | O | Container port |
| template.containers.ports.protocol | Body | String | O | Container protocol<ul><li>TCP</li><li>UDP</li><li>HTTP</li><li>HTTPS</li><li>TERMINATED\_HTTPS</li></ul> |
| templates.containers.command | Body | String List | X | Command to run when the container starts |
| templates.containers.args | Body | String List | X | Arguments used when the container starts |
| templates.containers.workDirectory | Body | String | X | Working directory of the container |
| templates.containers.env | Body | Array | X | Container environment variables |
| templates.containers.env.name | Body | String | O | Container environment variable name |
| templates.containers.env.value | Body | String | O | Container environment variable value |
| templates.containers.postStart | Body | String List | X | Commands that run immediately after container creation |
| templates.containers.preStop | Body | String List | X | Commands that run immediately after container termination |
| templates.containers.configs | Body | List | X | ConfigMap information used by containers |
| templates.containers.configs.id | Body | Integer | O | ConfigMap ID |
| templates.containers.configs.type | Body | String | O | Service type for retrieving ConfigMap information<ul><li>obs: Object Storage</li></ul> |
| templates.containers.configs.value | Body | String | O | Object URL |
| templates.containers.configs.mountPath | Body | String | O | Container mount path |
| templates.containers.secrets | Body | List | X | Secret information used by the container |
| templates.containers.secrets.type | Body | String | O | Service type for retrieving Secret information<ul><li>skm: Secure Key Manager</li></ul> |
| templates.containers.secrets.value | Body | String | O | Key ID |
| templates.containers.secrets.mountPath | Body | String | O | Container mount path |
| templates.containers.volumes | Body | Array | X | NAS storage information used by the container |
| templates.containers.volumes.name | Body | String | O | Storage name |
| templates.containers.volumes.path | Body | String | O | NAS storage connection path |
| templates.containers.volumes.mountPath | body | String | X | Container connection path |
| templates.containers.probe | Body | List | X | Container Probe settings |
| templates.containers.probe.type | Body | String | O | Container Probe type<ul><li>startup</li><li>liveness</li></ul> |
| templates.containers.probe.failureThreshold | Body | Integer | O | Probe failure criteria |
| templates.containers.probe.initialDelaySeconds | Body | Integer | O | Probe startup latency |
| templates.containers.probe.periodSeconds | Body | Integer | O | Probe execution interval |
| templates.containers.probe.timeoutSeconds | Body | Integer | O | Probe execution timeout |
| templates.containers.probe.exec | Body | String List | O | Command to run a probe |
| templates.containers.stopTimeout | Body | Integer | X | Initialization container execution timeout (seconds) |
| templates.containers.sharedMemory | Body | Object | X | Container shared memory settings |
| templates.containers.sharedMemory.changed | Body | Boolean | O | Whether to change the container shared memory settings<ul><li>true: Changed</li><li>false: Not changed</li></ul> |
| templates.containers.sharedMemory.sizeLimit | Body | Boolean | O | Shared memory set for the container (MiB) |

<details>
  <summary>Example</summary>

```json
{
  "header": {
    "resultCode": 200,
    "resultMessage": "SUCCESS",
    "isSuccessful": true
  },
  "templates": [
    {
      "createdAt": "2024-10-24T05:24:14.053Z",
      "updatedAt": "2024-10-24T05:24:14.053Z",
      "id": "bf095f99-1547-48f4-b57d-1124e853f6e2",
      "name": "nginx-template",
      "namespace": "abd7f92e-3353-4b45-944c-510a97ef89c9",
      "containers": [
        {
          "id": "51be9a5d-4737-4323-ae57-0ade225f4f4d",
          "name": "nginx",
          "image": "nginx:latest",
          "imageRegistry": "other",
          "imageRegistryType": "public",
          "cpus": 0.25,
          "memoryLimit": {
            "hard": 256
          },
          "ports": [
            {
              "hostPort": 80,
              "containerPort": 80,
              "protocol": "TCP"
            }
          ],
          "restartCount": 0,
          "probe": [
            {
              "type": "liveness",
              "exec": [
                "bash",
                "-c",
                "curl -f http://localhost || exit 1"
              ],
              "initialDelaySeconds": 5,
              "failureThreshold": 3,
              "timeoutSeconds": 1,
              "periodSeconds": 10
            },
            {
              "type": "startup",
              "exec": [
                "bash",
                "-c",
                "curl -f http://localhost || exit 1"
              ],
              "initialDelaySeconds": 5,
              "failureThreshold": 3,
              "timeoutSeconds": 1,
              "periodSeconds": 10
            }
          ],
          "type": "normal"
        }
      ],
      "networks": [
        {
          "vpcId": "aeeafe4e-287d-4dd4-b91a-294b87688457",
          "subnetId": "abd7f92e-3353-4b45-944c-510a97ef89c9"
        }
      ],
      "dnsConfig": [
        "223.255.201.241",
        "211.50.32.6"
      ],
      "versionCount": 2,
      "version": "first"
    },
    {
      "createdAt": "2024-10-24T05:43:26.029Z",
      "updatedAt": "2024-10-24T05:43:26.029Z",
      "id": "bf095f99-1547-48f4-b57d-1124e853f6e2",
      "name": "nginx-template",
      "namespace": "abd7f92e-3353-4b45-944c-510a97ef89c9",
      "containers": [
        {
          "id": "51be9a5d-4737-4323-ae57-0ade225f4f4d",
          "name": "nginx",
          "image": "nginx:latest",
          "imageRegistry": "other",
          "imageRegistryType": "public",
          "cpus": 0.25,
          "memoryLimit": {
            "hard": 256
          },
          "ports": [
            {
              "hostPort": 80,
              "containerPort": 80,
              "protocol": "TCP"
            }
          ],
          "restartCount": 0,
          "type": "normal"
        }
      ],
      "networks": [
        {
          "vpcId": "aeeafe4e-287d-4dd4-b91a-294b87688457",
          "subnetId": "abd7f92e-3353-4b45-944c-510a97ef89c9"
        }
      ],
      "dnsConfig": [
        "223.255.201.241",
        "211.50.32.6"
      ],
      "versionCount": 2,
      "version": "second",
    }
  ]
}
```

</details>

<a id="view-template-versions"></a>

### View Template Versions { #view-template-versions }

Retrieves information on an individual template version.

```bash
GET /ncs/v1.0/appkeys/{appKey}/templates/{templateId}/versions/{version}
x-nhn-authorization: Bearer {accessToken}
```

<a id="view-template-versions-request"></a>

#### Request

This API does not require a request body.

| Name | Type | Format | Required | Description |
| --- | --- | --- | --- | --- |
| appKey | URL | String | O | Service Appkey |
| templateId | URL | String | O | Template ID |
| version | URL | String | O | Template version |
| token | Header | String | O | NHN Cloud Token |

<a id="view-template-versions-response"></a>

#### Response

* Same as retrieving template details

| Name | Type | Format | Required | Description |
| --- | --- | --- | --- | --- |
| template | Body | Object | O | Template version information |
| template.id | Body | UUID | O | Template ID |
| template.version | Body | String | O | Template version |
| template.name | Body | String | O | Template name |
| template.createdAt | Body | String | O | Creation time (UTC) |
| template.description | Body | String | X | Template description |
| template.versionDescription | Body | String | X | Template version description |
| template.networks | Body | Array | O | Network information of the template |
| template.networks.vpcId | Body | String | O | VPC ID of the template |
| template.networks.subnetId | Body | String | O | Subnet ID of the template |
| template.dnsConfig | Body | String List | X | DNS server information configured in the container |
| template.hostAliases | Body | List | X | Information configured in the container's `/etc/hosts` |
| template.hostAliases.ip | Body | String | O | IP of the hostnames configured in the container |
| template.hostAliases.hostnames | Body | String List | O | Hostnames of the IP configured in the container |
| template.versionCount | Body | Integer | O | Number of versions of the template |
| template.workloadCount | Body | Integer | O | Number of workloads using the template |
| template.containers | Body | Array | O | Container list of the template |
| template.containers.name | Body | String | O | Container name |
| template.containers.type | Body | String | O | Container Type<ul><li>normal: General</li><li>init: Initialization</li></ul>|
| template.containers.image | Body | String | O | Container image |
| template.containers.cpus | Body | Float | O | Number of CPUs allocated to the container |
| template.containers.memoryLimit | Body | Object | O | Memory information allocated to the container |
| template.containers.memoryLimit.hard | Body | Integer | O | Memory allocated to the container (MiB) |
| template.containers.gpuFlavor | Body | String | X | GPU Flavor information<ul><li>ncs1.g1m5</li><li>ncs1.g2m10</li></ul> |
| template.containers.ports | Body | Array | X | Port information used by the container |
| template.containers.ports.containerPort | Body | Integer | O | Container port |
| template.containers.ports.protocol | Body | String | O | Container protocol<ul><li>TCP</li><li>UDP</li><li>HTTP</li><li>HTTPS</li><li>TERMINATED\_HTTPS</li></ul> |
| template.containers.command | Body | String List | X | Commands to run when the container starts |
| template.containers.args | Body | String List | X | Arguments used when the container starts |
| template.containers.workDirectory | Body | String | X | Working directory of the container |
| template.containers.env | Body | Array | X | Container environment variables |
| template.containers.env.name | Body | String | O | Container environment variable name |
| template.containers.env.value | Body | String | O | Container environment variable value |
| template.containers.postStart | Body | String List | X | Commands that run immediately after container creation |
| template.containers.preStop | Body | String List | X | Commands that run immediately before the container terminates |
| template.containers.configs | Body | List | X | ConfigMap information used by the container |
| template.containers.configs.id | Body | Integer | O | ConfigMap ID |
| template.containers.configs.type | Body | String | O | Service type for retrieving ConfigMap information<ul><li>obs: Object Storage</li></ul> |
| template.containers.configs.value | Body | String | O | Object URL |
| template.containers.configs.mountPath | Body | String | O | Container mount path |
| template.containers.secrets | Body | List | X | Secret information used by the container |
| template.containers.secrets.type | Body | String | O | Service type for retrieving Secret information<ul><li>skm: Secure Key Manager</li></ul> |
| template.containers.secrets.value | Body | String | O | Key ID |
| template.containers.secrets.mountPath | Body | String | O | Container mount path |
| template.containers.volumes | Body | Array | X | NAS storage information used by the container |
| template.containers.volumes.name | Body | String | O | Storage name |
| template.containers.volumes.path | Body | String | O | NAS storage connection path |
| template.containers.volumes.mountPath | body | String | X | Container connection path |
| template.containers.probe | Body | List | X | Container Probe configuration |
| template.containers.probe.type | Body | String | O | Container Probe type<ul><li>startup</li><li>liveness</li></ul> |
| template.containers.probe.failureThreshold | Body | Integer | O | Probe failure criteria |
| template.containers.probe.initialDelaySeconds | Body | Integer | O | Probe startup latency |
| template.containers.probe.periodSeconds | Body | Integer | O | Probe execution interval |
| template.containers.probe.timeoutSeconds | Body | Integer | O | Probe execution timeout |
| template.containers.probe.exec | Body | String List | O | Command to run a probe |
| template.containers.stopTimeout | Body | Integer | X | Initialization container execution timeout (seconds) |
| template.containers.sharedMemory | Body | Object | X | Container shared memory settings |
| template.containers.sharedMemory.changed | Body | Boolean | O | Whether to change the container shared memory setting<ul><li>true: Changed</li><li>false: Not changed</li></ul> |
| template.containers.sharedMemory.sizeLimit | Body | Boolean | O | Shared memory to set for the container (MiB) |

<details>
  <summary>Example</summary>

```json
{
  "header": {
    "resultCode": 200,
    "resultMessage": "SUCCESS",
    "isSuccessful": true
  },
  "template": {
    "createdAt": "2024-10-24T05:24:14.053Z",
    "updatedAt": "2024-10-24T05:24:14.053Z",
    "id": "bf095f99-1547-48f4-b57d-1124e853f6e2",
    "name": "nginx-template",
    "namespace": "abd7f92e-3353-4b45-944c-510a97ef89c9",
    "containers": [
      {
        "id": "51be9a5d-4737-4323-ae57-0ade225f4f4d",
        "name": "nginx",
        "image": "nginx:latest",
        "imageRegistry": "other",
        "imageRegistryType": "public",
        "cpus": 0.25,
        "memoryLimit": {
          "hard": 256
        },
        "ports": [
          {
            "hostPort": 80,
            "containerPort": 80,
            "protocol": "TCP"
          }
        ],
        "restartCount": 0,
        "probe": [
          {
            "type": "liveness",
            "exec": [
              "bash",
              "-c",
              "curl -f http://localhost || exit 1"
            ],
            "initialDelaySeconds": 5,
            "failureThreshold": 3,
            "timeoutSeconds": 1,
            "periodSeconds": 10
          },
          {
            "type": "startup",
            "exec": [
              "bash",
              "-c",
              "curl -f http://localhost || exit 1"
            ],
            "initialDelaySeconds": 5,
            "failureThreshold": 3,
            "timeoutSeconds": 1,
            "periodSeconds": 10
          }
        ],
        "type": "normal"
      }
    ],
    "networks": [
      {
        "vpcId": "aeeafe4e-287d-4dd4-b91a-294b87688457",
        "subnetId": "abd7f92e-3353-4b45-944c-510a97ef89c9"
      }
    ],
    "dnsConfig": [
      "223.255.201.241",
      "211.50.32.6"
    ],
    "version": "first"
  }
}
```

</details>

<a id="create-template-version"></a>

### Create Template Version { #create-template-version }

Creates a version of the template.

```bash
POST /ncs/v1.0/appkeys/{appKey}/templates/{templateId}/versions
x-nhn-authorization: Bearer {accessToken}
```

| Name | Type | Format | Required | Description |
| --- | --- | --- | --- | --- |
| appKey | URL | String | O | Service Appkey |
| templateId | URL | String | O | Template ID |
| token | Header | String | O | NHN Cloud Token |
| template | Body | Object | O | Template version information |
| template.version | Body | String | O | Template version |
| template.sourceVersion | Body | String | O | Baseline template version |
| template.name | Body | String | O | Template name |
| template.versionDescription | Body | String | X | Template version description |
| template.dnsConfig | Body | String List | X | DNS server information configured in the container |
| template.hostAliases | Body | List | X | Information configured in the container's `/etc/hosts` |
| template.hostAliases.ip | Body | String | O | IP of the hostnames configured in the container |
| template.hostAliases.hostnames | Body | String List | O | Hostnames of the IP configured in the container |
| template.applyImmediately | Body | Boolean | X | true: Enable instant deployment, false: Disable instant deployment (default: false) |
| template.containers | Body | Array | O | List of containers in the template |
| template.containers.name | Body | String | O | Container name |
| template.containers.type | Body | String | O | Container Type<ul><li>normal: General</li><li>init: Initialization</li></ul>|
| template.containers.image | Body | String | O | Container image |
| template.containers.imageRegistryCredentials | Body | Object | X | Information for accessing a private registry |
| template.containers.imageRegistryCredentials.changed | Body | Boolean | X | Whether to use an existing account (default: false)<ul><li>false: Use existing account</li><li>true: Use a new account (username, password must be passed)</li></ul> |
| template.containers.imageRegistryCredentials.username | Body | String | O | Private registry ID |
| template.containers.imageRegistryCredentials.password | Body | String | O | Private registry password |
| template.containers.cpus | Body | Float | O | Number of CPUs allocated to the container |
| template.containers.memoryLimit | Body | Object | O | Memory information allocated to the container |
| template.containers.memoryLimit.hard | Body | Integer | O | Memory allocated to the container (MiB) |
| template.containers.gpuFlavor | Body | String | X | GPU Flavor information<ul><li>ncs1.g1m5</li><li>ncs1.g2m10</li></ul> |
| template.containers.ports | Body | Array | X | Port information used by the container |
| template.containers.ports.containerPort | Body | Integer | O | Container port |
| template.containers.ports.protocol | Body | String | O | Container protocol<ul><li>TCP</li><li>UDP</li><li>HTTP</li><li>HTTPS</li><li>TERMINATED\_HTTPS</li></ul> |
| template.containers.command | Body | String List | X | Commands to run when the container starts |
| template.containers.args | Body | String List | X | Arguments used when the container starts |
| template.containers.workDirectory | Body | String | X | Working directory of the container |
| template.containers.env | Body | Array | X | Container environment variables |
| template.containers.env.name | Body | String | O | Container environment variable name |
| template.containers.env.value | Body | String | O | Container environment variable value |
| template.containers.postStart | Body | String List | X | Commands that run immediately after container creation |
| template.containers.preStop | Body | String List | X | Commands executed immediately before the container is stopped |
| template.containers.configs | Body | List | X | ConfigMap information used by the container |
| template.containers.configs.id | Body | Integer | O | ConfigMap ID |
| template.containers.configs.type | Body | String | O | Service type for retrieving ConfigMap information<ul><li>obs: Object Storage</li></ul> |
| template.containers.configs.value | Body | String | O | Object URL |
| template.containers.configs.mountPath | Body | String | O | Container mount path |
| template.containers.configs.changedAppKey | Body | Boolean | X | Whether to use an existing AppKey (default: false)<ul><li>false: Use existing key</li><li>true: use new key (AppKey must be passed as required)</li></ul> |
| template.containers.configs.appKey | Body | String | X | Object Storage AppKey |
| template.containers.configs.changedUserAccessKeyId | Body | Boolean | X | Whether to use an existing UserAccessKeyId (default: false)<ul><li>false: Use existing key</li><li>true: Use new key (UserAccessKeyId must be passed as required)</li></ul> |
| template.containers.configs.userAccessKeyId | Body | String | X | User Access Key for users accessing the Object Storage service |
| template.containers.configs.changedSecretAccessKey | Body | Boolean | X | Whether to use an existing SecretAccessKey (default: false)<ul><li>false: Use existing key</li><li>true: use new key (SecretAccessKey must be passed)</li></ul> |
| template.containers.configs.secretAccessKey | Body | String | X | Secret Access Key for users accessing the Object Storage service |
| template.containers.secrets | Body | List | X | Secret information used by the container |
| template.containers.secrets.type | Body | String | O | Service type for retrieving Secret information<ul><li>skm: Secure Key Manager</li></ul> |
| template.containers.secrets.value | Body | String | O | Key ID |
| template.containers.secrets.mountPath | Body | String | O | Container mount path |
| template.containers.volumes | Body | Array | X | Information on NAS storage used in containers |
| template.containers.volumes.name | Body | String | O | Storage name |
| template.containers.volumes.path | Body | String | O | NAS Storage Connection Path |
| template.containers.volumes.mountPath | body | String | X | Container connection path |
| template.containers.probe | Body | List | X | Container Probe configuration |
| template.containers.probe.type | Body | String | O | Container Probe type<ul><li>startup</li><li>liveness</li></ul> |
| template.containers.probe.failureThreshold | Body | Integer | O | Probe failure threshold |
| template.containers.probe.initialDelaySeconds | Body | Integer | O | Probe startup latency |
| template.containers.probe.periodSeconds | Body | Integer | O | Probe execution interval |
| template.containers.probe.timeoutSeconds | Body | Integer | O | Probe execution timeout |
| template.containers.probe.exec | Body | String List | O | Probe execution command |
| template.containers.stopTimeout | Body | Integer | X | Initialization container execution timeout (seconds) |
| template.containers.sharedMemory | Body | Object | X | Container shared memory settings |
| template.containers.sharedMemory.changed | Body | Boolean | O | Whether the container shared memory setting was changed<ul><li>true: Changed</li><li>false: Not changed</li></ul> |
| template.containers.sharedMemory.sizeLimit | Body | Boolean | O | Shared memory to set for the container (MiB) |

<details>
  <summary>Example</summary>

```json
{
  "template": {
    "applyImmediately": false,
    "containers": [
      {
        "cpus": 1,
        "image": "nginx:latest",
        "imageRegistryType": "public",
        "memoryLimit": {
          "hard": 1024
        },
        "name": "nginx",
        "ports": [
          {
            "containerPort": 80,
            "protocol": "terminated-https"
          }
        ],
        "type": "normal"
      }
    ],
    "description": "new version",
    "name": "nginx-template",
    "version": "v3",
    "sourceVersion": "first"
  }
}
```

</details>

<a id="create-template-version-response"></a>

#### Response

| Name | Type | Format | Required | Description |
| --- | --- | --- | --- | --- |
| template | Body | Object | O | Template information |
| template.id | Body | UUID | O | Template ID |
| template.version | Body | String | O | Template version |
| template.name | Body | String | O | Template name |
| template.createdAt | Body | String | O | Creation time (UTC) |
| template.description | Body | String | X | Template description |
| template.versionDescription | Body | String | X | Template version description |
| template.networks | Body | Array | O | Network information of the template |
| template.networks.vpcId | Body | String | O | VPC ID of the template |
| template.networks.subnetId | Body | String | O | Subnet ID of the template |
| template.dnsConfig | Body | String List | X | DNS server information set in the template |
| template.hostAliases | Body | List | X | Information set up in container `/etc/hosts` |
| template.hostAliases.ip | Body | String | O | IP of the hostnames set in the container |
| template.hostAliases.hostnames | Body | String List | O | hostnames of the IP set in the container |
| template.containers | Body | Array | O | List of containers in the template |
| template.containers.name | Body | String | O | Container name |
| template.containers.type | Body | String | O | Container Type<ul><li>normal: General</li><li>init: Initialization</li></ul>|
| template.containers.image | Body | String | O | Container image |
| template.containers.cpus | Body | Float | O | Number of CPU assigned to container |
| template.containers.memoryLimit | Body | Object | O | Information on memory assigned to container |
| template.containers.memoryLimit.hard | Body | Integer | O | Memory allocated to the container (MiB) |
| template.containers.gpuFlavor | Body | String | X | GPU Flavor information<ul><li>ncs1.g1m5</li><li>ncs1.g2m10</li></ul> |
| template.containers.ports | Body | Array | X | Port information used by the container |
| template.containers.ports.containerPort | Body | Integer | O | Container port |
| template.containers.ports.protocol | Body | String | O | Container protocol<ul><li>TCP</li><li>UDP</li><li>HTTP</li><li>HTTPS</li><li>TERMINATED\_HTTPS</li></ul> |
| template.containers.command | Body | String List | X | Command to run when the container starts |
| template.containers.args | Body | String List | X | Arguments used when the container starts |
| template.containers.workDirectory | Body | String | X | Working directory of the container |
| template.containers.env | Body | Array | X | Container environment variables |
| template.containers.env.name | Body | String | O | Container environment variable name |
| template.containers.env.value | Body | String | O | Container environment variable value |
| template.containers.postStart | Body | String List | X | Commands that run immediately after container creation |
| template.containers.preStop | Body | String List | X | Commands executed just before container termination |
| template.containers.configs | Body | List | X | ConfigMap information used by containers |
| template.containers.configs.id | Body | Integer | O | ConfigMap ID |
| template.containers.configs.type | Body | String | O | Service type for retrieving ConfigMap information<ul><li>obs: Object Storage</li></ul> |
| template.containers.configs.value | Body | String | O | Object URL |
| template.containers.configs.mountPath | Body | String | O | Container mount path |
| template.containers.secrets | Body | List | X | Secret information used by containers |
| template.containers.secrets.type | Body | String | O | Service type for retrieving Secret information<ul><li>skm: Secure Key Manager</li></ul> |
| template.containers.secrets.value | Body | String | O | Key ID |
| template.containers.secrets.mountPath | Body | String | O | Container mount path |
| template.containers.volumes | Body | Array | X | Information on NAS storage used in containers |
| template.containers.volumes.name | Body | String | O | Storage name |
| template.containers.volumes.path | Body | String | O | NAS Storage Connection Path |
| template.containers.volumes.mountPath | body | String | X | Container connection path |
| template.containers.probe | Body | List | X | Container Probe configuration |
| template.containers.probe.type | Body | String | O | Container Probe type<ul><li>startup</li><li>liveness</li></ul> |
| template.containers.probe.failureThreshold | Body | Integer | O | Probe failure threshold |
| template.containers.probe.initialDelaySeconds | Body | Integer | O | Probe startup latency |
| template.containers.probe.periodSeconds | Body | Integer | O | Probe execution interval |
| template.containers.probe.timeoutSeconds | Body | Integer | O | Probe execution timeout |
| template.containers.probe.exec | Body | String List | O | Probe execution command |
| template.containers.stopTimeout | Body | Integer | X | Initialization container execution timeout (seconds) |
| template.containers.sharedMemory | Body | Object | X | Container shared memory settings |
| template.containers.sharedMemory.changed | Body | Boolean | O | Whether the container shared memory settings were changed<ul><li>true: Changed</li><li>false: Not changed</li></ul> |
| template.containers.sharedMemory.sizeLimit | Body | Boolean | O | Shared memory to set for the container (MiB) |

<details>
  <summary>Example</summary>

```json
{
  "header": {
    "resultCode": 200,
    "resultMessage": "SUCCESS",
    "isSuccessful": true
  },
  "template": {
    "createdAt": "2024-10-27T22:26:49.196Z",
    "updatedAt": "2024-10-27T22:26:49.196Z",
    "id": "bf095f99-1547-48f4-b57d-1124e853f6e2",
    "name": "nginx-template",
    "namespace": "abd7f92e-3353-4b45-944c-510a97ef89c9",
    "description": "new version",
    "containers": [
      {
        "id": "bf6bcdd7-6ef1-4f82-981a-c4fc4ebae16e",
        "name": "nginx",
        "image": "nginx:latest",
        "imageRegistry": "other",
        "imageRegistryType": "public",
        "cpus": 1,
        "memoryLimit": {
          "hard": 1024
        },
        "ports": [
          {
            "containerPort": 80,
            "protocol": "TERMINATED-HTTPS"
          }
        ],
        "restartCount": 0,
        "type": "normal"
      }
    ],
    "networks": [
      {
        "vpcId": "aeeafe4e-287d-4dd4-b91a-294b87688457",
        "subnetId": "abd7f92e-3353-4b45-944c-510a97ef89c9"
      }
    ],
    "dnsConfig": [
      "223.255.201.241",
      "211.50.32.6"
    ],
    "version": "v3",
  }
}
```

</details>

<a id="delete-template-version"></a>

### Delete Template Version { #delete-template-version }

```bash
DELETE /ncs/v1.0/appkeys/{appkey}/templates/{templateId}/versions/{version}
x-nhn-authorization: Bearer {accessToken}
```

<a id="delete-template-version-request"></a>
#### Request

This API does not require a request body.

| Name | Type | Format | Required | Description |
| --- | --- | --- | --- | --- |
| appKey | URL | String | O | Service Appkey |
| templateId | URL | String | O | Template ID |
| version | URL | String | O | Template version |
| token | Header | String | O | NHN Cloud Token |

<a id="delete-template-version-response"></a>
#### Response

This API responds with common information.

<a id="workload"></a>

## Workload { #workload }

<a id="list-workloads"></a>

### List Workloads { #list-workloads }

Retrieves a list of workloads.

```bash
GET /ncs/v1.0/appkeys/{appKey}/workloads
x-nhn-authorization: Bearer {accessToken}
```

<a id="list-workloads-request"></a>

#### Request

This API does not require a request body.

| Name | Type | Format | Required | Description |
| --- | --- | --- | --- | --- |
| appKey | URL | String | O | Service Appkey |
| token | Header | String | O | NHN Cloud Token |
| q | Query | String | X | Filter by workload name, template ID, and template version<ul>Examples:<li>q=templateId=${Template ID}</li><li>q=${Workload name)</li><li>q=templateId=${Template ID}\&version=${Template version}</li></ul> |
| page | Query | Integer | X | Page number to retrieve |
| size | Query | Integer | X | Page size to retrieve (default: 10) |

<a id="list-workloads-response"></a>

#### Response

| Name | Type | Format | Required | Description |
| --- | --- | --- | --- | --- |
| X-Total-Count | Header | Integer | O | Number of workloads created in Appkey |
| workloads | Body | Array | O | Workload list |
| workloads.id | Body | UUID | O | Workload ID |
| workloads.name | Body | String | O | Workload name |
| workloads.type | Body | String | O | Deployment controller<ul><li>deployment</li><li>statefulset</li></ul> |
| workloads.templateId | Body | String | O | Template ID of the workload |
| workloads.templateVersion | Body | String | O | Template version of the workload |
| workloads.createdAt | Body | String | O | Creation time (UTC) |
| workloads.desired | Body | Integer | O | Number of tasks requested for the workload |
| workloads.available | Body | Integer | O | Number of workload tasks running |
| workloads.internalLBTimeout | Body | Integer | X | Internal request response latency |
| workloads.status | Body | String | O | Workload status<ul><li>Pending: Workload creation/change in progress</li><li>Running: Workload creation/modification complete</li><li>Failed: Workload creation/modification failed</li><li>Terminated: Workload terminated</li><li>Paused: Workload paused</li><li>Active: Scheduled workload running</li><li>Suspend: Scheduled workload suspended</li></ul> |
| workloads.url | Body | String | X | Workload load balancer URL |
| workloads.loadBalancing | Body | Object | O | Workload load balancer information |
| workloads.loadBalancing.enabled | Body | Boolean | O | Whether to use workload load balancer |
| workloads.loadBalancing.floatingIp | Body | Boolean | O | Whether to use the workload load balancer floating IP |
| workloads.loadBalancing.ipAddress | Body | String | O | Load balancer IP information for the workload (vip, floating ip) |
| workloads.loadBalancing.vipAddress | Body | String | X | Specified IP of workload load balancer |
| workloads.loadBalancing.healthMonitor | Body | Object | X | About checking the health of the load balancer |
| workloads.loadBalancing.healthMonitor.delay | Body | Integer | O | Health check interval |
| workloads.loadBalancing.healthMonitor.timeout | Body | Integer | O | Maximum response wait time |
| workloads.loadBalancing.healthMonitor.maxRetries | Body | Integer | O | Maximum number of retries |
| workloads.loadBalancing.healthMonitor.httpMethod | Body | String | X | HTTP method<ul><li>GET</li></ul> |
| workloads.loadBalancing.healthMonitor.expectedCodes | Body | String | X | HTTP status code<ul><li>200</li><li>200,202</li><li>200-204</li></ul> |
| workloads.loadBalancing.healthMonitor.urlPath | Body | String | X | HTTP URL |
| workloads.loadBalancing.certificate | Body | String | X | Certificates used by the load balancer when using TERMINATED\_HTTPS |
| workloads.loadBalancing.privateKey | Body | String | X | Private key used by the load balancer when using TERMINATED\_HTTPS |
| workloads.loadBalancing.tlsVersion | Body | String | X | TLS version when using TERMINATED\_HTTPS<ul><li>SSLv3</li><li>TLSv1.0</li><li>TLSv1.0\_2016</li><li>TLSv1.1</li><li>TLSv1.2</li><li>TLSv1.3</li></ul> |
| workloads.loadBalancing.containerHref | Body | String | X | Secret container ID<li>If you separately registered a certificate and private key to use in TERMINATED\_HTTPS using the Load Balancer API, use it.</li> |
| workloads.loadBalancing.ipAclGroupsBinding | Body | List | X | List of IP access control groups to apply to the load balancer |
| workloads.loadBalancing.ipAclGroupsBinding.ipAclGroupId | Body | String | O | IP access control group ID |
| workloads.schedule | Body | Object | X | Scheduled execution configuration information |
| workloads.schedule.timeZone | Body | String | O | Base time for scheduled execution<ul><li>Examples: Asia/Seoul, UTC</li><li>[List of tz database time zones](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones)</li></ul> |
| workloads.schedule.cron | Body | String | O | Cron expression for scheduled execution |
| workloads.schedule.jobsHistoryLimit | Body | Integer | O | Number of scheduled execution histories to retain |
| workloads.schedule.concurrencyPolicy | Body | String | O | Concurrency policy<ul><li>Forbid</li><li>Replace</li></ul> |
| workloads.schedule.timeOffset | Body | String | O | Base time offset for scheduled execution |
| workloads.internalLoadBalancing | Body | Object | X | Internal load balancer information |
| workloads.internalLoadBalancing.enalbed | Body | Boolean | O | Whether the internal load balancer is enabled |
| workloads.internalLoadBalancing.type | Body | String | X | Internal load balancer IP allocation method<ul><li>dynamic: Automatic allocation</li><li>static: Specify IP</li></ul> |
| workloads.internalLoadBalancing.ip | Body | String | X | Designated IP for the internal load balancer |
| workloads.privateDns | Body | Object | X | Determinine whether to register workload working IPs with Private DNS |
| workloads.privateDns.ttl | Body | Integer | O | TTL value of a recordset |
| workloads.privateDns.zoneId | Body | String | O | The Private DNS Zone ID used by the workload |
| workloads.privateDns.domain | Body | String | O | About domains registered with Private DNS |
| workloads.activeDeadline | Body | Object | X | Information on workload scheduling end |
| workloads.activeDeadline.timeZone | Body | String | O | Scheduling end base time<li>Example: Asia/Seoul, UTC</li> |
| workloads.activeDeadline.timeOffset | Body | String | O | Offset the scheduling end base time |
| workloads.activeDeadline.time | Body | String | O | Scheduled termination time |
| workloads.autoScaler | Body | Object | X | AutoScaler configuration information |
| workloads.autoScaler.scaleOut | Body | Object | O | ScaleOut information |
| workloads.autoScaler.scaleOut.enabled | Body | Boolean | O | Whether ScaleOut is enabled |
| workloads.autoScaler.scaleOut.maxReplicas | Body | Integer | X | Maximum number of jobs for autoscaling |
| workloads.autoScaler.scaleOut.coolDownMinute | Body | Integer | X | Wait time after scaling out |
| workloads.autoScaler.scaleOut.condition | Body | List | X | Scale-out conditions |
| workloads.autoScaler.scaleOut.condition.resource | Body | String | X | Resource used as the scale-out condition basis<ul><li>cpu</li><li>memory</li><li>gpu</li><li>gpu-memory</li></ul> |
| workloads.autoScaler.scaleOut.condition.threshold | Body | Integer | X | Scale out condition resource usage (1-100) |
| workloads.autoScaler.scaleOut.condition.duration | Body | Integer | X | Scale out condition resource usage hold time (minutes) |
| workloads.autoScaler.scaleIn | Body | Object | X | ScaleIn information |
| workloads.autoScaler.scaleIn.enabled | Body | Boolean | O | Whether ScaleIn is enabled |
| workloads.autoScaler.scaleIn.minReplicas | Body | Integer | X | Minimum number of jobs for autoscaling |
| workloads.autoScaler.scaleIn.coolDownMinute | Body | Integer | X | Wait time after scaling in |
| workloads.autoScaler.scaleIn.condition | Body | List | X | Scale-in conditions |
| workloads.autoScaler.scaleIn.condition.resource | Body | String | X | Resource used as the scale-in condition basis<ul><li>cpu</li><li>memory</li><li>gpu</li><li>gpu-memory</li></ul> |
| workloads.autoScaler.scaleIn.condition.threshold | Body | Integer | X | Resource usage for scale-in condition (1–100) |
| workloads.autoScaler.scaleIn.condition.duration | Body | Integer | X | Duration for maintaining resource usage for scale-in condition (minutes) |
| workloads.securityGroups | Body | List | X | SecurityGroups information |
| workloads.securityGroups.id | Body | String | O | SecurityGroups ID |

<details>
  <summary>Example</summary>

```json
{
  "header": {
    "resultCode": 200,
    "resultMessage": "SUCCESS",
    "isSuccessful": true
  },
  "workloads": [
    {
      "createdAt": "2024-10-27T22:29:05.859Z",
      "updatedAt": "2024-10-27T22:29:05.859Z",
      "id": "08ef9e6e-5a57-49f3-8f52-7ce36b337a8a",
      "name": "nginx",
      "templateId": "bf095f99-1547-48f4-b57d-1124e853f6e2",
      "templateName": "nginx-template",
      "templateVersion": "first",
      "desired": 1,
      "available": 1,
      "status": "Running",
      "networks": [
        {
          "vpcId": "aeeafe4e-287d-4dd4-b91a-294b87688457",
          "subnetId": "abd7f92e-3353-4b45-944c-510a97ef89c9"
        }
      ],
      "loadBalancing": {
        "enabled": true,
        "floatingIp": false,
        "ipAddress": "192.168.0.102",
        "healthMonitor": {
          "delay": 30,
          "timeout": 5,
          "maxRetries": 2,
          "httpMethod": "GET",
          "expectedCodes": "200",
          "urlPath": "/"
        }
      },
      "type": "deployment",
      "internalLoadBalancing": {
        "enabled": false
      }
    }
  ]
}
```

</details>

<a id="view-workload"></a>

### View Workload { #view-workload }

Retrieves an individual workload.

```bash
GET /ncs/v1.0/appkeys/{appKey}/workloads/{workloadId}
x-nhn-authorization: Bearer {accessToken}
```

<a id="view-workload-request"></a>

#### Request

This API does not require a request body.

| Name | Type | Format | Required | Description |
| --- | --- | --- | --- | --- |
| appKey | URL | String | O | Service Appkey |
| workloadId | URL | String | O | Workload ID |
| token | Header | String | O | NHN Cloud Token |

<a id="view-workload-response"></a>

#### Response

| Name | Type | Format | Required | Description |
| --- | --- | --- | --- | --- |
| workload | Body | Array | O | Workload information |
| workload.id | Body | UUID | O | Workload ID |
| workload.name | Body | String | O | Workload name |
| workload.type | Body | String | O | Deployment controller<ul><li>deployment</li><li>statefulset</li></ul> |
| workload.templateId | Body | String | O | Template ID of the workload |
| workload.templateVersion | Body | String | O | Template version of the workload |
| workload.createdAt | Body | String | O | Creation time (UTC) |
| workload.desired | Body | Integer | O | Number of tasks requested for the workload |
| workload.available | Body | Integer | O | Number of workload tasks running |
| workload.internalLBTimeout | Body | Integer | X | Internal request response latency |
| workload.status | Body | String | O | Workload status<ul><li>Pending: Workload creation/change in progress</li><li>Running: Workload creation/modification complete</li><li>Failed: Workload creation/modification failed</li><li>Terminated: Workload terminated</li><li>Paused: Workload paused</li><li>Active: Scheduled workload running</li><li>Suspend: Scheduled workload suspended</li></ul> |
| workload.url | Body | String | X | Workload load balancer URL |
| workload.loadBalancing | Body | Object | O | Workload load balancer information |
| workload.loadBalancing.enabled | Body | Boolean | O | Whether to use workload load balancer |
| workload.loadBalancing.floatingIp | Body | Boolean | O | Whether to use the workload load balancer floating IP |
| workload.loadBalancing.ipAddress | Body | String | O | Workload load balancer IP information (vip, floating ip) |
| workload.loadBalancing.vipAddress | Body | String | X | Specify workload load balancer IP |
| workload.loadBalancing.healthMonitor | Body | Object | X | About checking the health of the load balancer |
| workload.loadBalancing.healthMonitor.delay | Body | Integer | O | Health check interval |
| workload.loadBalancing.healthMonitor.timeout | Body | Integer | O | Maximum response wait time |
| workload.loadBalancing.healthMonitor.maxRetries | Body | Integer | O | Maximum number of retries |
| workload.loadBalancing.healthMonitor.httpMethod | Body | String | X | HTTP method<ul><li>GET</li></ul> |
| workload.loadBalancing.healthMonitor.expectedCodes | Body | String | X | HTTP status code<ul><li>200</li><li>200,202</li><li>200-204</li></ul> |
| workload.loadBalancing.healthMonitor.urlPath | Body | String | X | HTTP URL |
| workload.loadBalancing.certificate | Body | String | X | Certificates used by the load balancer when using TERMINATED\_HTTPS |
| workload.loadBalancing.privateKey | Body | String | X | Private key used by the load balancer when using TERMINATED\_HTTPS |
| workload.loadBalancing.tlsVersion | Body | String | X | TLS version when using TERMINATED\_HTTPS<ul><li>SSLv3</li><li>TLSv1.0</li><li>TLSv1.0\_2016</li><li>TLSv1.1</li><li>TLSv1.2</li><li>TLSv1.3</li></ul> |
| workload.loadBalancing.containerHref | Body | String | X | Secret container ID<li>If you separately registered a certificate and private key to use in TERMINATED\_HTTPS using the Load Balancer API, use it.</li> |
| workload.loadBalancing.ipAclGroupsBinding | Body | List | X | List of IP access control groups to apply to the load balancer |
| workload.loadBalancing.ipAclGroupsBinding.ipAclGroupId | Body | String | O | IP access control group ID |
| workload.schedule | Body | Object | X | Scheduled execution configuration information |
| workload.schedule.timeZone | Body | String | O | Base time for scheduled execution<ul><li>Example: Asia/Seoul, UTC</li><li>[List of tz database time zones](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones)</li></ul> |
| workload.schedule.cron | Body | String | O | Cron expression for scheduled execution |
| workload.schedule.jobsHistoryLimit | Body | Integer | O | Number of scheduled execution history |
| workload.schedule.concurrencyPolicy | Body | String | O | Concurrency policy<ul><li>Forbid</li><li>Replace</li></ul> |
| workload.schedule.timeOffset | Body | String | O | Offset the scheduled execution base time |
| workload.internalLoadBalancing | Body | Object | X | Internal load balancer information |
| workload.internalLoadBalancing.enalbed | Body | Boolean | O | Whether to use an internal load balancer |
| workload.internalLoadBalancing.type | Body | String | X | How to assign internal load balancer IPs<ul><li>dynamic: Automatic allocation</li><li>static: Specify IP</li></ul> |
| workload.internalLoadBalancing.ip | Body | String | X | Specify internal load balancer IP |
| workload.privateDns | Body | Object | X | Determinine whether to register workload working IPs with Private DNS |
| workload.privateDns.ttl | Body | Integer | O | TTL value of the record set |
| workload.privateDns.zoneId | Body | String | O | The Private DNS Zone ID used by the workload |
| workload.privateDns.domain | Body | String | O | About domains registered with Private DNS |
| workload.activeDeadline | Body | Object | X | Information on workload scheduling end |
| workload.activeDeadline.timeZone | Body | String | O | Scheduling end base time<li>Example: Asia/Seoul, UTC</li> |
| workload.activeDeadline.timeOffset | Body | String | O | Offset the scheduling end base time |
| workload.activeDeadline.time | Body | String | O | Scheduled termination time |
| workload.autoScaler | Body | Object | X | AutoScaler configuration information |
| workload.autoScaler.scaleOut | Body | Object | O | ScaleOut information |
| workload.autoScaler.scaleOut.enabled | Body | Boolean | O | Whether ScaleOut is enabled |
| workload.autoScaler.scaleOut.maxReplicas | Body | Integer | X | Maximum number of jobs for autoscaling |
| workload.autoScaler.scaleOut.coolDownMinute | Body | Integer | X | Wait time after scaling out |
| workload.autoScaler.scaleOut.condition | Body | List | X | Scale-out conditions |
| workload.autoScaler.scaleOut.condition.resource | Body | String | X | Resource criteria for scale-out conditions<ul><li>cpu</li><li>memory</li><li>gpu</li><li>gpu-memory</li></ul> |
| workload.autoScaler.scaleOut.condition.threshold | Body | Integer | X | Scale out condition resource usage (1-100) |
| workload.autoScaler.scaleOut.condition.duration | Body | Integer | X | Scale out condition resource usage hold time (minutes) |
| workload.autoScaler.scaleIn | Body | Object | X | ScaleIn information |
| workload.autoScaler.scaleIn.enabled | Body | Boolean | O | Whether ScaleIn is enabled |
| workload.autoScaler.scaleIn.minReplicas | Body | Integer | X | Minimum number of jobs for autoscaling |
| workload.autoScaler.scaleIn.coolDownMinute | Body | Integer | X | Wait time after scale in |
| workload.autoScaler.scaleIn.condition | Body | List | X | Scale-in conditions |
| workload.autoScaler.scaleIn.condition.resource | Body | String | X | Resource for scale-in conditions<ul><li>cpu</li><li>memory</li><li>gpu</li><li>gpu-memory</li></ul> |
| workload.autoScaler.scaleIn.condition.threshold | Body | Integer | X | Resource usage for scale-in condition (1–100) |
| workload.autoScaler.scaleIn.condition.duration | Body | Integer | X | Duration for maintaining resource usage for scale-in condition (minutes) |
| workload.securityGroups | Body | List | X | SecurityGroups information |
| workload.securityGroups.id | Body | String | O | SecurityGroups ID |
| workload.tasks | Body | Array | O | List of tasks in the workload |
| workload.tasks.id | Body | UUID | O | Task ID |
| workload.tasks.containers | Body | Array | O | List of containers in the task |
| workload.tasks.containers.name | Body | String | O | Container name |
| workload.tasks.containers.type | Body | String | O | Container Type<ul><li>normal: general</li><li>init: init</li></ul>|
| workload.tasks.containers.image | Body | String | O | Container image |
| workload.tasks.containers.ip | Body | String | X | Container IP |
| workload.tasks.containers.cpus | Body | Float | O | Number of CPUs allocated to the container |
| workload.tasks.containers.memoryLimit | Body | Object | O | Memory information allocated to the container |
| workload.tasks.containers.memoryLimit.hard | Body | Integer | O | Memory allocated to the container (MiB) |
| workload.tasks.containers.gpuFlavor | Body | String | X | GPU Flavor information allocated to the container |
| workload.tasks.containers.ports | Body | Array | X | Port information of the container |
| workload.tasks.containers.ports.containerPort | Body | Integer | O | Container port |
| workload.tasks.containers.ports.protocol | Body | String | O | Container protocol<ul><li>TCP</li><li>UDP</li><li>HTTP</li><li>HTTPS</li><li>TERMINATED\_HTTPS</li></ul> |
| workload.tasks.containers.command | Body | String List | X | Commands to run when the container starts |
| workload.tasks.containers.args | Body | String List | X | Arguments used when the container is started |
| workload.tasks.containers.workDirectory | Body | String | X | Working directory of the container |
| workload.tasks.containers.env | Body | Array | X | Container environment variables |
| workload.tasks.containers.env.name | Body | String | O | Container environment variable name |
| workload.tasks.containers.env.value | Body | String | O | Container environment variable value |
| workload.tasks.containers.postStart | Body | String List | X | Commands that run immediately after container creation |
| workload.tasks.containers.preStop | Body | String List | X | Commands executed just before container termination |
| workload.tasks.containers.configs | Body | List | X | ConfigMap information used by containers |
| workload.tasks.containers.configs.id | Body | Integer | O | ConfigMap ID |
| workload.tasks.containers.configs.type | Body | String | O | Service type for retrieving ConfigMap information<ul><li>obs: Object Storage</li></ul> |
| workload.tasks.containers.configs.value | Body | String | O | Object URL |
| workload.tasks.containers.configs.mountPath | Body | String | O | Container mount path |
| workload.tasks.containers.secrets | Body | List | X | Secret information used by the container |
| workload.tasks.containers.secrets.type | Body | String | O | Service type for retrieving Secret information<ul><li>skm: Secure Key Manager</li></ul> |
| workload.tasks.containers.secrets.value | Body | String | O | Key ID |
| workload.tasks.containers.secrets.mountPath | Body | String | O | Container mount path |
| workload.tasks.containers.volumes | Body | Array | X | Storage information used by the container |
| workload.tasks.containers.volumes.name | Body | String | O | Storage name |
| workload.tasks.containers.volumes.path | Body | String | O | NAS storage connection path |
| workload.tasks.containers.volumes.mountPath | body | String | X | Container connection path (default: /mnt) |
| workload.tasks.containers.probe | Body | List | X | Container Probe configuration |
| workload.tasks.containers.probe.type | Body | String | O | Container Probe type<ul><li>startup</li><li>liveness</li></ul> |
| workload.tasks.containers.probe.failureThreshold | Body | Integer | O | Probe failure criteria |
| workload.tasks.containers.probe.initialDelaySeconds | Body | Integer | O | Probe startup latency |
| workload.tasks.containers.probe.periodSeconds | Body | String | O | Probe execution interval |
| workload.tasks.containers.probe.timeoutSeconds | Body | String | O | Probe execution timeout |
| workload.tasks.containers.probe.exec | Body | String List | O | Command to run a probe |
| workload.tasks.containers.stopTimeout | Body | Integer | X | Initialization container execution timeout (seconds) |
| workload.tasks.containers.sharedMemory | Body | Object | X | Container shared memory settings information |
| workload.tasks.containers.sharedMemory.changed | Body | Boolean | O | Whether the container shared memory settings have been changed<ul><li>true: Changed</li><li>false: Not changed</li></ul> |
| workload.tasks.containers.sharedMemory.sizeLimit | Body | Boolean | O | Shared memory set for the container (MiB) |
| workload.tasks.containers.state | Body | String | O | Container status |
| workload.tasks.containers.startedAt | Body | String | O | Container start time |
| workload.tasks.containers.finishedAt | Body | String | X | Initialization container completion time |
| workload.tasks.containers.restartCount | Body | String | O | Number of container restarts |

<details>
  <summary>Example</summary>

```json
{
  "header": {
    "resultCode": 200,
    "resultMessage": "SUCCESS",
    "isSuccessful": true
  },
  "workload": {
    "createdAt": "2024-10-27T22:29:05.859Z",
    "updatedAt": "2024-10-27T22:29:05.859Z",
    "id": "08ef9e6e-5a57-49f3-8f52-7ce36b337a8a",
    "name": "nginx",
    "namespace": "abd7f92e-3353-4b45-944c-510a97ef89c9",
    "templateId": "bf095f99-1547-48f4-b57d-1124e853f6e2",
    "templateName": "nginx-template",
    "templateVersion": "first",
    "desired": 1,
    "available": 1,
    "status": "Running",
    "tasks": [
      {
        "id": "e75d7945-62f4-4cd2-9a93-14e14edccb2b",
        "containers": [
          {
            "id": "51be9a5d-4737-4323-ae57-0ade225f4f4d",
            "name": "nginx",
            "ip": "192.168.0.76",
            "image": "nginx:latest",
            "imageRegistry": "other",
            "imageRegistryType": "public",
            "cpus": 0.25,
            "memoryLimit": {
              "hard": 256
            },
            "ports": [
              {
                "hostPort": 80,
                "containerPort": 80,
                "protocol": "TCP"
              }
            ],
            "state": "Running",
            "startedAt": "2024-10-27T22:29:23Z",
            "restartCount": 0,
            "probe": [
              {
                "type": "liveness",
                "exec": [
                  "bash",
                  "-c",
                  "curl -f http://localhost || exit 1"
                ],
                "initialDelaySeconds": 5,
                "failureThreshold": 3,
                "timeoutSeconds": 1,
                "periodSeconds": 10
              },
              {
                "type": "startup",
                "exec": [
                  "bash",
                  "-c",
                  "curl -f http://localhost || exit 1"
                ],
                "initialDelaySeconds": 5,
                "failureThreshold": 3,
                "timeoutSeconds": 1,
                "periodSeconds": 10
              }
            ],
            "type": "normal"
          }
        ]
      }
    ],
    "networks": [
      {
        "vpcId": "aeeafe4e-287d-4dd4-b91a-294b87688457",
        "subnetId": "abd7f92e-3353-4b45-944c-510a97ef89c9"
      }
    ],
    "securityGroups": [
      {
        "id": "b1b4a7b3-d35f-4676-857b-4f8997f9f3b8"
      }
    ],
    "loadBalancing": {
      "enabled": true,
      "floatingIp": false,
      "ipAddress": "192.168.0.102",
      "healthMonitor": {
        "delay": 30,
        "timeout": 5,
        "maxRetries": 2,
        "httpMethod": "GET",
        "expectedCodes": "200",
        "urlPath": "/"
      }
    },
    "type": "deployment",
    "internalLoadBalancing": {
      "enabled": false
    }
  }
}
```

</details>

<a id="view-workload-log"></a>

### View Workload Log { #view-workload-log }

Retrieves the container logs for your workload.

```bash
GET /ncs/v1.0/appkeys/{appKey}/workloads/{workloadId}/tasks/{taskId}/logs?container={ContainerName}&from={YYYY-MM-DDThh:mm:ssZ}&to={YYYY-MM-DDThh:mm:ssZ}
x-nhn-authorization: Bearer {accessToken}
```

<a id="view-workload-log-request"></a>
#### Request

This API does not require a request body.

| Name | Type | Format | Required | Description |
| --- | --- | --- | --- | --- |
| appKey | URL | String | O | Service Appkey |
| workloadId | URL | String | O | Workload ID |
| taskId | URL | String | O | Task ID |
| token | Header | String | O | NHN Cloud Token |
| containerName | Query | String | O | Container name |
| from | Query | String | X | Log start time (default: 5 minutes before current) |
| to | Query | String | X | Log end time (default: current time) |
| page | Query | String | X | Page to retrieve |
| size | Query | String | X | Page size (default: 100) |

<a id="view-workload-log-response"></a>
#### Response

| Name | Type | Format | Required | Description |
| --- | --- | --- | --- | --- |
| logs | Body | Array | O | List of container logs |
| log | Body | String | O | Log content |
| time | Body | String | O | Log occurrence time (UTC) |

<details>
  <summary>Example</summary>

```json
{
  "header": {
    "resultCode": 200,
    "resultMessage": "SUCCESS",
    "isSuccessful": true
  },
  "logs": [
    {
      "log": "/docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration",
      "time": "2024-10-27T22:29:23.546854524Z"
    },
    {
      "log": "/docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/",
      "time": "2024-10-27T22:29:23.548332152Z"
    }
  ]
}
```

</details>

<a id="view-workload-event"></a>

### View Workload Events { #view-workload-event }

Retrieves the events of a workload.

```bash
GET /ncs/v1.0/appkeys/{appKey}/workloads/{workloadId}/tasks/{taskId}/events
x-nhn-authorization: Bearer {accessToken}
```

<a id="view-workload-event-request"></a>
#### Request

This API does not require a request body.

| Name | Type | Format | Required | Description |
| --- | --- | --- | --- | --- |
| appKey | URL | String | O | Service Appkey |
| workloadId | URL | String | O | Workload ID |
| taskId | URL | String | O | Task ID |
| token | Header | String | O | NHN Cloud Token |
| type | Query | Integer | X | Event type<ul><li>Normal</li><li>Warning</li></ul> |
| q | Query | String | X | Filter by event content |
| page | Query | String | X | Page to retrieve |
| size | Query | String | X | Page size to retrieve (default: 10) |
| from | Query | String | X | Start time when the event last occurred (default: 1 hour before the current time) |
| to | Query | String | X | End time when the event last occurred (default: current time) |

<a id="view-workload-event-response"></a>
#### Response

| Name | Type | Format | Required | Description |
| --- | --- | --- | --- | --- |
| events | Body | Array | O | Event list |
| type | Body | String | O | Event type<ul><li>Normal</li><li>Warning</li></ul> |
| reason | Body | String | O | Cause of the event |
| message | Body | String | O | Event content |
| createTimestamp | Body | String | O | Date of first occurrence of event (UTC) |
| lastTimestamp | Body | String | O | Date of last occurrence of event (UTC) |
| count | Body | Integer | O | Number of times the event occurred |

<details>
  <summary>Example</summary>

```json
{
  "header": {
    "resultCode": 200,
    "resultMessage": "SUCCESS",
    "isSuccessful": true
  },
  "events": [
    {
      "type": "Normal",
      "reason": "Scheduled",
      "message": "Successfully assigned abd7f92e-3353-4b45-944c-510a97ef89c9/nginx-5b64d9d5d4-rkcr2 to ncsac1-kxzed5wj-0424fc5a",
      "createTimestamp": "2024-10-27T22:29:06Z",
      "lastTimestamp": "2024-10-27T22:29:06Z",
      "count": 1
    }
  ]
}
```

</details>

<a id="view-a-list-of-workload-run-history"></a>

### View a List of Workload Run History { #view-a-list-of-workload-run-history }

Retrieves a list of workload run history.

```bash
GET /ncs/v1.0/appkeys/{appKey}/workloads/{workloadId}/history
x-nhn-authorization: Bearer {accessToken}
```

<a id="view-a-list-of-workload-run-history-request"></a>
#### Request

This API does not require a request body.

| Name | Type | Format | Required | Description |
| --- | --- | --- | --- | --- |
| appKey | URL | String | O | Service Appkey |
| workloadId | URL | String | O | Workload ID |
| token | Header | String | O | NHN Cloud Token |
| page | Query | Integer | X | Page number to retrieve |
| size | Query | Integer | X | Page size to retrieve (default: 10) |
| sort | Query | String | X | Field name to sort by<br>Prefix the field name with `-` for reverse sorting<br>Example: `sort=-id` |

<a id="view-a-list-of-workload-run-history-response"></a>
#### Response

| Name | Type | Format | Required | Description |
| --- | --- | --- | --- | --- |
| history | Body | Array | O | History list |
| history.id | Body | Integer | O | History ID |
| history.createdAt | Body | String | O | Deployment time |
| history.deletedAt | Body | String | O | Termination time |
| history.templateId | Body | UUID | O | Template ID used by the workload |
| history.templateVersion | Body | UUID | O | Template version used by the workload |
| history.name | Body | String | O | Template name |
| history.status | Body | String | O | Status<ul><li>Succeeded</li><li>Terminated</li><li>Pending</li></ul> |

<details>
  <summary>Example</summary>

```json
{
  "header": {
    "resultCode": 200,
    "resultMessage": "SUCCESS",
    "isSuccessful": true
  },
  "id": "08ef9e6e-5a57-49f3-8f52-7ce36b337a8a",
  "history": [
    {
      "id": 1,
      "createdAt": "2024-10-27T22:29:05.996Z",
      "deletedAt": null,
      "templateId": "bf095f99-1547-48f4-b57d-1124e853f6e2",
      "templateVersion": "first",
      "name": "nginx-template",
      "status": "Succeeded"
    }
  ]
}
```

</details>

<a id="view-workload-run-history"></a>

### View Workload Run History { #view-workload-run-history }

Retrieves the run history of an individual workload.

```bash
GET /ncs/v1.0/appkeys/{appKey}/workloads/{workloadId}/history/{historyId}
x-nhn-authorization: Bearer {accessToken}
```

<a id="view-workload-run-history-request"></a>

#### Request

This API does not require a request body.

| Name | Type | Format | Required | Description |
| --- | --- | --- | --- | --- |
| appKey | URL | String | O | Service Appkey |
| workloadId | URL | String | O | Workload ID |
| historyId | URL | Integer | O | History ID |
| token | Header | String | O | NHN Cloud Token |

<a id="view-workload-run-history-response"></a>

#### Response

| Name | Type | Format | Required | Description |
| --- | --- | --- | --- | --- |
| history | Body | Object | O | History information |
| history.id | Body | Integer | O | History ID |
| history.createdAt | Body | String | O | Run time |
| history.deletedAt | Body | String | O | End time |
| history.templateId | Body | UUID | O | Template ID used by the workload |
| history.name | Body | String | O | Template name used by workloads |
| history.status | Body | String | O | Status<ul><li>Succeeded</li><li>Terminated</li><li>Pending</li></ul> |
| template | Body | Object | O | Template information |
| template.id | Body | UUID | O | Template ID |
| template.version | Body | String | O | Template version |
| template.name | Body | String | O | Template name |
| template.createdAt | Body | String | O | Creation time (UTC) |
| template.description | Body | String | X | Template description |
| template.versionDescription | Body | String | X | Template version description |
| template.networks | Body | Array | O | Network information of the template |
| template.networks.vpcId | Body | String | O | VPC ID of the template |
| template.networks.subnetId | Body | String | O | Subnet ID of the template |
| template.dnsConfig | Body | String List | X | DNS server information configured in the container |
| template.hostAliases | Body | List | X | Information configured in the container's `/etc/hosts` |
| template.hostAliases.ip | Body | String | O | IP of the hostnames configured in the container |
| template.hostAliases.hostnames | Body | String List | O | Hostnames of the IP configured in the container |
| template.containers | Body | Array | O | List of containers in the template |
| template.containers.name | Body | String | O | Container name |
| template.containers.type | Body | String | O | Container Type<ul><li>normal: General</li><li>init: Initialization</li></ul>|
| template.containers.image | Body | String | O | Container image |
| template.containers.cpus | Body | Float | O | Number of CPUs allocated to the container |
| template.containers.memoryLimit | Body | Object | O | Memory information allocated to the container |
| template.containers.memoryLimit.hard | Body | Integer | O | Memory allocated to the container (MiB) |
| template.containers.gpuFlavor | Body | String | X | GPU Flavor information<ul><li>ncs1.g1m5</li><li>ncs1.g2m10</li></ul> |
| template.containers.ports | Body | Array | X | Port information used by the container |
| template.containers.ports.containerPort | Body | Integer | O | Container port |
| template.containers.ports.protocol | Body | String | O | Container protocol<ul><li>TCP</li><li>UDP</li><li>HTTP</li><li>HTTPS</li><li>TERMINATED\_HTTPS</li></ul> |
| template.containers.command | Body | String List | X | Command to run when container starts |
| template.containers.args | Body | String List | X | Arguments used when the container is started |
| template.containers.workDirectory | Body | String | X | Working directory of the container |
| template.containers.env | Body | Array | X | Container environment variables |
| template.containers.env.name | Body | String | O | Container environment variable name |
| template.containers.env.value | Body | String | O | Container environment variable value |
| template.containers.postStart | Body | String List | X | Commands that run immediately after container creation |
| template.containers.preStop | Body | String List | X | Commands executed just before container termination |
| template.containers.configs | Body | List | X | ConfigMap information used by the container |
| template.containers.configs.id | Body | Integer | O | ConfigMap ID |
| template.containers.configs.type | Body | String | O | Service type for retrieving ConfigMap information<ul><li>obs: Object Storage</li></ul> |
| template.containers.configs.value | Body | String | O | Object URL |
| template.containers.configs.mountPath | Body | String | O | Container mount path |
| template.containers.secrets | Body | List | X | Secret information used by the container |
| template.containers.secrets.type | Body | String | O | Service type for retrieving Secret information<ul><li>skm: Secure Key Manager</li></ul> |
| template.containers.secrets.value | Body | String | O | Key ID |
| template.containers.secrets.mountPath | Body | String | O | Container mount path |
| template.containers.volumes | Body | Array | X | NAS storage information used by the container |
| template.containers.volumes.name | Body | String | O | Storage name |
| template.containers.volumes.path | Body | String | O | NAS Storage Connection Path |
| template.containers.volumes.mountPath | body | String | X | Container connection path |
| template.containers.probe | Body | List | X | Container Probe settings |
| template.containers.probe.type | Body | String | O | Container Probe type<ul><li>startup</li><li>liveness</li></ul> |
| template.containers.probe.failureThreshold | Body | Integer | O | Probe failure threshold |
| template.containers.probe.initialDelaySeconds | Body | Integer | O | Probe startup latency |
| template.containers.probe.periodSeconds | Body | Integer | O | Probe execution interval |
| template.containers.probe.timeoutSeconds | Body | Integer | O | Probe execution timeout |
| template.containers.probe.exec | Body | String List | O | Probe execution command |
| template.containers.stopTimeout | Body | Integer | X | Initialization container execution timeout (seconds) |
| template.containers.sharedMemory | Body | Object | X | Container shared memory settings |
| template.containers.sharedMemory.changed | Body | Boolean | O | Whether to change the container shared memory settings<ul><li>true: Changed</li><li>false: Not changed</li></ul> |
| template.containers.sharedMemory.sizeLimit | Body | Boolean | O | Shared memory set for the container (MiB) |

<details>
  <summary>Example</summary>

```json
{
  "header": {
    "resultCode": 200,
    "resultMessage": "SUCCESS",
    "isSuccessful": true
  },
  "history": {
    "id": 1,
    "createdAt": "2024-10-27T22:29:05.996Z",
    "deletedAt": null,
    "templateId": "bf095f99-1547-48f4-b57d-1124e853f6e2",
    "templateVersion": "first",
    "name": "nginx-template",
    "status": "Succeeded"
  },
  "template": {
    "createdAt": "2024-10-24T05:24:14.053Z",
    "updatedAt": "2024-10-24T05:24:14.053Z",
    "id": "bf095f99-1547-48f4-b57d-1124e853f6e2",
    "name": "nginx-template",
    "namespace": "abd7f92e-3353-4b45-944c-510a97ef89c9",
    "containers": [
      {
        "id": "51be9a5d-4737-4323-ae57-0ade225f4f4d",
        "name": "nginx",
        "image": "nginx:latest",
        "imageRegistry": "other",
        "imageRegistryType": "public",
        "cpus": 0.25,
        "memoryLimit": {
          "hard": 256
        },
        "ports": [
          {
            "hostPort": 80,
            "containerPort": 80,
            "protocol": "TCP"
          }
        ],
        "restartCount": 0,
        "probe": [
          {
            "type": "liveness",
            "exec": [
              "bash",
              "-c",
              "curl -f http://localhost || exit 1"
            ],
            "initialDelaySeconds": 5,
            "failureThreshold": 3,
            "timeoutSeconds": 1,
            "periodSeconds": 10
          },
          {
            "type": "startup",
            "exec": [
              "bash",
              "-c",
              "curl -f http://localhost || exit 1"
            ],
            "initialDelaySeconds": 5,
            "failureThreshold": 3,
            "timeoutSeconds": 1,
            "periodSeconds": 10
          }
        ],
        "type": "normal"
      }
    ],
    "networks": [
      {
        "vpcId": "aeeafe4e-287d-4dd4-b91a-294b87688457",
        "subnetId": "abd7f92e-3353-4b45-944c-510a97ef89c9"
      }
    ],
    "dnsConfig": [
      "223.255.201.241",
      "211.50.32.6"
    ],
    "version": "first"
  }
}
```

</details>

<a id="view-workload-scheduled-run-history"></a>

### View workload scheduled run history { #view-workload-scheduled-run-history }

Views the history of a scheduled run.

```bash
GET /ncs/v1.0/appkeys/{appKey}/workloads/{workloadId}/schedulehistory
x-nhn-authorization: Bearer {accessToken}
```

<a id="view-workload-scheduled-run-history-request"></a>
#### Request

This API does not require a request body.

| Name | Type | Format | Required | Description |
| --- | --- | --- | --- | --- |
| appKey | URL | String | O | Service Appkey |
| workloadId | URL | String | O | Workload ID |
| token | Header | String | O | NHN Cloud Token |
| page | Query | Integer | X | Page number to retrieve |
| size | Query | Integer | X | Page size to retrieve (default: 10) |

<a id="view-workload-scheduled-run-history-response"></a>
#### Response

| Name | Type | Format | Required | Description |
| --- | --- | --- | --- | --- |
| schedulehistory | Body | List | O | Scheduled Execution History |
| schedulehistory.id | Body | String | O | Task ID |
| schedulehistory.createdAt | Body | String | O | Start time |
| schedulehistory.finishedAt | Body | Object | O | End time |
| schedulehistory.status | Body | String | O | Scheduled task status<ul><li>Error</li><li>Completed</li><li>Waiting</li><li>Running</li></ul> |

<details>
  <summary>Example</summary>

```json
{
  "header": {
    "resultCode": 200,
    "resultMessage": "SUCCESS",
    "isSuccessful": true
  },
  "schedulehistory": [
    {
      "id": "6a8241f7-13ba-468b-ae03-dc1e7a35ccb8",
      "createdAt": "2024-10-27T22:48:00Z",
      "finishedAt": "2024-10-27T22:48:45Z",
      "status": "Completed"
    }
  ]
}

```

</details>

<a id="create-workload"></a>

### Create a Workload { #create-workload }

Creates a workload.

```bash
POST /ncs/v1.0/appkeys/{appKey}/workloads
Content-Type: application/json
x-nhn-authorization: Bearer {accessToken}
```

<a id="create-workload-request"></a>

#### Request

| Name | Type | Format | Required | Description |
| --- | --- | --- | --- | --- |
| appKey | URL | String | O | Service Appkey |
| token | Header | String | O | NHN Cloud Token |
| workload | Body | Object | O | Workload information |
| workload.name | Body | String | O | Workload name |
| workload.type | Body | String | X | Deployment controller (default:deployment)<ul><li>deployment</li><li>statefulset</li></ul> |
| workload.templateId | Body | String | O | Template ID of the workload |
| workload.templateVersion | Body | String | X | Template version of the workload (default: latest version) |
| workload.desired | Body | Integer | O | Number of tasks requested for the workload |
| workload.internalLBTimeout | Body | Integer | X | Internal request response latency |
| workload.loadBalancing | Body | Object | O | Workload load balancer information |
| workload.loadBalancing.enabled | Body | Boolean | O | Whether to use workload load balancer |
| workload.loadBalancing.floatingIp | Body | Boolean | O | Whether to use the workload load balancer floating IP |
| workload.loadBalancing.vipAddress | Body | String | X | Specify internal load balancer IP |
| workload.loadBalancing.healthMonitor | Body | Object | X | Health check information for the load balancer |
| workload.loadBalancing.healthMonitor.delay | Body | Integer | O | Health check interval |
| workload.loadBalancing.healthMonitor.timeout | Body | Integer | O | Maximum response wait time |
| workload.loadBalancing.healthMonitor.maxRetries | Body | Integer | O | Maximum number of retries |
| workload.loadBalancing.healthMonitor.httpMethod | Body | String | X | HTTP method<ul><li>GET</li></ul> |
| workload.loadBalancing.healthMonitor.expectedCodes | Body | String | X | HTTP status code<ul><li>200</li><li>200,202</li><li>200-204</li></ul> |
| workload.loadBalancing.healthMonitor.urlPath | Body | String | X | HTTP URL |
| workload.loadBalancing.certificate | Body | String | X | Certificates used by the load balancer when using TERMINATED\_HTTPS |
| workload.loadBalancing.privateKey | Body | String | X | Private key used by the load balancer when using TERMINATED\_HTTPS |
| workload.loadBalancing.tlsVersion | Body | String | X | TLS version when using TERMINATED\_HTTPS<ul><li>SSLv3</li><li>TLSv1.0</li><li>TLSv1.0\_2016</li><li>TLSv1.1</li><li>TLSv1.2</li><li>TLSv1.3</li></ul> |
| workload.loadBalancing.containerHref | Body | String | X | Secret container ID<li>If you separately registered a certificate and private key to use in TERMINATED\_HTTPS using the Load Balancer API, use it.</li> |
| workload.loadBalancing.ipAclGroupsBinding | Body | List | X | List of IP access control groups to apply to the load balancer |
| workload.loadBalancing.ipAclGroupsBinding.ipAclGroupId | Body | String | O | IP access control group ID |
| workload.schedule | Body | Object | X | Scheduled execution configuration information |
| workload.schedule.timeZone | Body | String | O | Base time for scheduled execution<ul><li>Example: Asia/Seoul, UTC</li><li>[List of tz database time zones](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones)</li></ul> |
| workload.schedule.cron | Body | String | O | Cron expression for scheduled execution |
| workload.schedule.jobsHistoryLimit | Body | Integer | O | Number of scheduled execution histories |
| workload.schedule.concurrencyPolicy | Body | String | O | Concurrency policy<ul><li>Forbid</li><li>Replace</li></ul> |
| workload.internalLoadBalancing | Body | Object | X | Internal load balancer information |
| workload.internalLoadBalancing.enalbed | Body | Boolean | O | Whether to use an internal load balancer |
| workload.internalLoadBalancing.type | Body | String | X | How to assign internal load balancer IPs<ul><li>dynamic: Automatic allocation</li><li>static: Specify IP</li></ul> |
| workload.internalLoadBalancing.ip | Body | String | X | Specify internal load balancer IP |
| workload.privateDns | Body | Object | X | Determinine whether to register workload working IPs with Private DNS |
| workload.privateDns.ttl | Body | Integer | O | TTL value of the record set |
| workload.privateDns.zoneId | Body | String | O | The Private DNS Zone ID used by the workload |
| workload.privateDns.domain | Body | String | O | About domains registered with Private DNS |
| workload.activeDeadline | Body | Object | X | Workload scheduled termination information |
| workload.activeDeadline.timeZone | Body | String | O | Base time for scheduled termination<li>Example: Asia/Seoul, UTC</li> |
| workload.activeDeadline.timeOffset | Body | String | O | Offset the scheduling end base time |
| workload.activeDeadline.time | Body | String | O | Scheduled termination time |
| workload.autoScaler | Body | Object | X | AutoScaler configuration information |
| workload.autoScaler.scaleOut | Body | Object | O | ScaleOut information |
| workload.autoScaler.scaleOut.enabled | Body | Boolean | O | Whether to use ScaleOut |
| workload.autoScaler.scaleOut.maxReplicas | Body | Integer | X | Maximum number of jobs for autoscaling |
| workload.autoScaler.scaleOut.coolDownMinute | Body | Integer | X | Wait time after scaling up |
| workload.autoScaler.scaleOut.condition | Body | List | X | Scale-out conditions |
| workload.autoScaler.scaleOut.condition.resource | Body | String | X | Resources based on scale out conditions<ul><li>cpu</li><li>memory</li><li>gpu</li><li>gpu-memory</li></ul> |
| workload.autoScaler.scaleOut.condition.threshold | Body | Integer | X | Scale out condition resource usage (1-100) |
| workload.autoScaler.scaleOut.condition.duration | Body | Integer | X | Scale out condition resource usage hold time (minutes) |
| workload.autoScaler.scaleIn | Body | Object | X | ScaleIn information |
| workload.autoScaler.scaleIn.enabled | Body | Boolean | O | Whether ScaleIn is enabled |
| workload.autoScaler.scaleIn.minReplicas | Body | Integer | X | Minimum number of jobs for autoscaling |
| workload.autoScaler.scaleIn.coolDownMinute | Body | Integer | X | Wait time after scale in |
| workload.autoScaler.scaleIn.condition | Body | List | X | Scale-in conditions |
| workload.autoScaler.scaleIn.condition.resource | Body | String | X | Resources based on scale in conditions<ul><li>cpu</li><li>memory</li><li>gpu</li><li>gpu-memory</li></ul> |
| workload.autoScaler.scaleIn.condition.threshold | Body | Integer | X | Scale in condition resource usage (1-100) |
| workload.autoScaler.scaleIn.condition.duration | Body | Integer | X | Scale in condition resource usage hold time (minutes) |
| workload.securityGroups | Body | List | X | SecurityGroups information |
| workload.securityGroups.id | Body | String | O | SecurityGroups ID |

<details>
  <summary>Example</summary>

```json
{
  "workload": {
    "description": "api workload",
    "desired": 1,
    "loadBalancing": {
      "enabled": false,
      "floatingIp": false
    },
    "name": "ncs-workload",
    "templateId": "bf095f99-1547-48f4-b57d-1124e853f6e2",
    "templateVersion": "first",
    "type": "deployment"
  }
}
```

</details>

<a id="create-workload-response"></a>

#### Response

| Name | Type | Format | Required | Description |
| --- | --- | --- | --- | --- |
| workload | Body | Object | O | Workload information |
| workload.id | Body | UUID | O | Workload ID |
| workload.name | Body | String | O | Workload name |
| workload.type | Body | String | O | Deployment controller<ul><li>deployment</li><li>statefulset</li></ul> |
| workload.templateId | Body | String | O | Template ID of the workload |
| workload.templateVersion | Body | String | O | Template version of the workload |
| workload.createdAt | Body | String | O | Creation time (UTC) |
| workload.desired | Body | Integer | O | Number of tasks requested for the workload |
| workload.internalLBTimeout | Body | Integer | X | Internal request response latency |
| workload.loadBalancing | Body | Object | O | Workload load balancer information |
| workload.loadBalancing.enabled | Body | Boolean | O | Whether to use workload load balancer |
| workload.loadBalancing.floatingIp | Body | Boolean | O | Whether to use the workload load balancer floating IP |
| workload.loadBalancing.vipAddress | Body | String | X | Specify workload load balancer IP |
| workload.loadBalancing.healthMonitor | Body | Object | X | Health check information for the load balancer |
| workload.loadBalancing.healthMonitor.delay | Body | Integer | O | Health check interval |
| workload.loadBalancing.healthMonitor.timeout | Body | Integer | O | Maximum response wait time |
| workload.loadBalancing.healthMonitor.maxRetries | Body | Integer | O | Maximum number of retries |
| workload.loadBalancing.healthMonitor.httpMethod | Body | String | X | HTTP method<ul><li>GET</li></ul> |
| workload.loadBalancing.healthMonitor.expectedCodes | Body | String | X | HTTP status code<ul><li>200</li><li>200,202</li><li>200-204</li></ul> |
| workload.loadBalancing.healthMonitor.urlPath | Body | String | X | HTTP URL |
| workload.loadBalancing.certificate | Body | String | X | Certificates used by the load balancer when using TERMINATED\_HTTPS |
| workload.loadBalancing.privateKey | Body | String | X | Private key used by the load balancer when using TERMINATED\_HTTPS |
| workload.loadBalancing.tlsVersion | Body | String | X | TLS version when using TERMINATED\_HTTPS<ul><li>SSLv3</li><li>TLSv1.0</li><li>TLSv1.0\_2016</li><li>TLSv1.1</li><li>TLSv1.2</li><li>TLSv1.3</li></ul> |
| workload.loadBalancing.containerHref | Body | String | X | Secret container ID<li>If you separately registered a certificate and private key to use in TERMINATED\_HTTPS using the Load Balancer API, use it.</li> |
| workload.loadBalancing.ipAclGroupsBinding | Body | List | X | List of IP access control groups to apply to the load balancer |
| workload.loadBalancing.ipAclGroupsBinding.ipAclGroupId | Body | String | O | IP access control group ID |
| workload.schedule | Body | Object | X | Scheduled execution configuration information |
| workload.schedule.timeZone | Body | String | O | Base time for scheduled execution<ul><li>Example: Asia/Seoul, UTC</li><li>[List of tz database time zones](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones)</li></ul> |
| workload.schedule.cron | Body | String | O | Cron expression for scheduled execution |
| workload.schedule.jobsHistoryLimit | Body | Integer | O | Number of scheduled execution histories |
| workload.schedule.concurrencyPolicy | Body | String | O | Concurrency policy<ul><li>Forbid</li><li>Replace</li></ul> |
| workload.schedule.timeOffset | Body | String | O | Offset the scheduled execution base time |
| workload.internalLoadBalancing | Body | Object | X | Internal load balancer information |
| workload.internalLoadBalancing.enalbed | Body | Boolean | O | Whether to use an internal load balancer |
| workload.internalLoadBalancing.type | Body | String | X | How to assign internal load balancer IPs<ul><li>dynamic: Automatic allocation</li><li>static: Specify IP</li></ul> |
| workload.internalLoadBalancing.ip | Body | String | X | Specify internal load balancer IP |
| workload.privateDns | Body | Object | X | Determinine whether to register workload working IPs with Private DNS |
| workload.privateDns.ttl | Body | Integer | O | TTL value of the record set |
| workload.privateDns.zoneId | Body | String | O | The Private DNS Zone ID used by the workload |
| workload.privateDns.domain | Body | String | O | About domains registered with Private DNS |
| workload.activeDeadline | Body | Object | X | Workload scheduled termination information |
| workload.activeDeadline.timeZone | Body | String | O | Scheduling end base time<li>Example: Asia/Seoul, UTC</li> |
| workload.activeDeadline.timeOffset | Body | String | O | Offset the scheduling end base time |
| workload.activeDeadline.time | Body | String | O | Scheduled termination time |
| workload.autoScaler | Body | Object | X | AutoScaler configuration information |
| workload.autoScaler.scaleOut | Body | Object | O | ScaleOut information |
| workload.autoScaler.scaleOut.enabled | Body | Boolean | O | Whether ScaleOut is enabled |
| workload.autoScaler.scaleOut.maxReplicas | Body | Integer | X | Maximum number of jobs for autoscaling |
| workload.autoScaler.scaleOut.coolDownMinute | Body | Integer | X | Wait time after scaling up |
| workload.autoScaler.scaleOut.condition | Body | List | X | Scale-out conditions |
| workload.autoScaler.scaleOut.condition.resource | Body | String | X | Resources based on scale out conditions<ul><li>cpu</li><li>memory</li><li>gpu</li><li>gpu-memory</li></ul> |
| workload.autoScaler.scaleOut.condition.threshold | Body | Integer | X | Scale out condition resource usage (1-100) |
| workload.autoScaler.scaleOut.condition.duration | Body | Integer | X | Scale out condition resource usage hold time (minutes) |
| workload.autoScaler.scaleIn | Body | Object | X | ScaleIn information |
| workload.autoScaler.scaleIn.enabled | Body | Boolean | O | Whether ScaleIn is enabled |
| workload.autoScaler.scaleIn.minReplicas | Body | Integer | X | Minimum number of jobs for autoscaling |
| workload.autoScaler.scaleIn.coolDownMinute | Body | Integer | X | Wait time after scale in |
| workload.autoScaler.scaleIn.condition | Body | List | X | Scale-in conditions |
| workload.autoScaler.scaleIn.condition.resource | Body | String | X | Resources based on scale in conditions<ul><li>cpu</li><li>memory</li><li>gpu</li><li>gpu-memory</li></ul> |
| workload.autoScaler.scaleIn.condition.threshold | Body | Integer | X | Scale in condition resource usage (1-100) |
| workload.autoScaler.scaleIn.condition.duration | Body | Integer | X | Scale in condition resource usage hold time (minutes) |
| workload.securityGroups | Body | List | X | SecurityGroups information |
| workload.securityGroups.id | Body | String | O | SecurityGroups ID |

<details>
  <summary>Example</summary>

```json
{
  "header": {
    "resultCode": 200,
    "resultMessage": "SUCCESS",
    "isSuccessful": true
  },
  "workload": {
    "createdAt": "2024-10-27T22:51:32.305Z",
    "updatedAt": "2024-10-27T22:51:32.305Z",
    "id": "6c6201b5-5b68-4035-adf7-40cd5f9402e5",
    "name": "ncs-workload",
    "namespace": "abd7f92e-3353-4b45-944c-510a97ef89c9",
    "description": "api workload",
    "templateId": "bf095f99-1547-48f4-b57d-1124e853f6e2",
    "templateName": "nginx-template",
    "templateVersion": "first",
    "desired": 1,
    "available": 0,
    "status": "",
    "loadBalancing": {
      "enabled": false,
      "floatingIp": false
    },
    "type": "deployment"
  }
}
```

</details>

<a id="change-workload"></a>

### Change Workload { #change-workload }

Changes a workload.

```bash
PUT /ncs/v1.0/appkeys/{appKey}/workloads/{workloadId}
Content-Type: application/json
x-nhn-authorization: Bearer {accessToken}
```

<a id="change-workload-request"></a>

#### Request

| Name | Type | Format | Required | Description |
| --- | --- | --- | --- | --- |
| appKey | URL | String | O | Service Appkey |
| workloadId | URL | String | O | Workload ID |
| token | Header | String | O | NHN Cloud Token |
| workload | Body | Object | O | Workload information |
| workload.name | Body | String | O | Workload name |
| workload.templateId | Body | String | O | Template ID of the workload |
| workload.templateVersion | Body | String | O | Template version of the workload |
| workload.desired | Body | Integer | O | Number of tasks requested for the workload |
| workload.internalLBTimeout | Body | Integer | X | Internal request response latency |
| workload.loadBalancing | Body | Object | O | Workload load balancer information |
| workload.loadBalancing.enabled | Body | Boolean | O | Whether to use workload load balancer |
| workload.loadBalancing.floatingIp | Body | Boolean | O | Whether to use the workload load balancer floating IP |
| workload.loadBalancing.vipAddress | Body | String | X | Specified IP address of the workload load balancer |
| workload.loadBalancing.healthMonitor | Body | Object | X | Health check information for the load balancer |
| workload.loadBalancing.healthMonitor.delay | Body | Integer | O | Health check interval |
| workload.loadBalancing.healthMonitor.timeout | Body | Integer | O | Maximum response wait time |
| workload.loadBalancing.healthMonitor.maxRetries | Body | Integer | O | Maximum number of retries |
| workload.loadBalancing.healthMonitor.httpMethod | Body | String | X | HTTP method<ul><li>GET</li></ul> |
| workload.loadBalancing.healthMonitor.expectedCodes | Body | String | X | HTTP status code<ul><li>200</li><li>200,202</li><li>200-204</li></ul> |
| workload.loadBalancing.healthMonitor.urlPath | Body | String | X | HTTP URL |
| workload.loadBalancing.certificate | Body | String | X | Certificates used by the load balancer when using TERMINATED\_HTTPS |
| workload.loadBalancing.privateKey | Body | String | X | Private key used by the load balancer when using TERMINATED\_HTTPS |
| workload.loadBalancing.tlsVersion | Body | String | X | TLS version when using TERMINATED\_HTTPS<ul><li>SSLv3</li><li>TLSv1.0</li><li>TLSv1.0\_2016</li><li>TLSv1.1</li><li>TLSv1.2</li><li>TLSv1.3</li></ul> |
| workload.loadBalancing.containerHref | Body | String | X | Secret container ID<li>If you separately registered a certificate and private key to use in TERMINATED\_HTTPS using the Load Balancer API, use it.</li> |
| workload.loadBalancing.ipAclGroupsBinding | Body | List | X | List of IP access control groups to apply to the load balancer |
| workload.loadBalancing.ipAclGroupsBinding.ipAclGroupId | Body | String | O | IP access control group ID |
| workload.schedule | Body | Object | X | Scheduled execution configuration information |
| workload.schedule.timeZone | Body | String | O | Base time for scheduled execution<ul><li>Example: Asia/Seoul, UTC</li><li>[List of tz database time zones](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones)</li></ul> |
| workload.schedule.cron | Body | String | O | Cron expression for scheduled execution |
| workload.schedule.jobsHistoryLimit | Body | Integer | O | Number of scheduled execution histories |
| workload.schedule.concurrencyPolicy | Body | String | O | Concurrency policy<ul><li>Forbid</li><li>Replace</li></ul> |
| workload.internalLoadBalancing | Body | Object | X | Internal load balancer information |
| workload.internalLoadBalancing.enalbed | Body | Boolean | O | Whether to use an internal load balancer |
| workload.internalLoadBalancing.type | Body | String | X | How to assign internal load balancer IPs<ul><li>dynamic: Automatic allocation</li><li>static: Specify IP</li></ul> |
| workload.internalLoadBalancing.ip | Body | String | X | Specify internal load balancer IP |
| workload.activeDeadline | Body | Object | X | Workload scheduled termination information |
| workload.activeDeadline.timeZone | Body | String | O | Base time for scheduled termination<li>Example: Asia/Seoul, UTC</li> |
| workload.activeDeadline.timeOffset | Body | String | O | Offset the scheduling end base time |
| workload.activeDeadline.time | Body | String | O | Scheduled termination time |
| workload.autoScaler | Body | Object | X | AutoScaler configuration information |
| workload.autoScaler.scaleOut | Body | Object | O | ScaleOut information |
| workload.autoScaler.scaleOut.enabled | Body | Boolean | O | Whether ScaleOut is enabled |
| workload.autoScaler.scaleOut.maxReplicas | Body | Integer | X | Maximum number of jobs for autoscaling |
| workload.autoScaler.scaleOut.coolDownMinute | Body | Integer | X | Wait time after scaling up |
| workload.autoScaler.scaleOut.condition | Body | List | X | Scale-out conditions |
| workload.autoScaler.scaleOut.condition.resource | Body | String | X | Resources based on scale out conditions<ul><li>cpu</li><li>memory</li><li>gpu</li><li>gpu-memory</li></ul> |
| workload.autoScaler.scaleOut.condition.threshold | Body | Integer | X | Scale out condition resource usage (1-100) |
| workload.autoScaler.scaleOut.condition.duration | Body | Integer | X | Scale out condition resource usage hold time (minutes) |
| workload.autoScaler.scaleIn | Body | Object | X | ScaleIn information |
| workload.autoScaler.scaleIn.enabled | Body | Boolean | O | Whether ScaleIn is enabled |
| workload.autoScaler.scaleIn.minReplicas | Body | Integer | X | Minimum number of jobs for autoscaling |
| workload.autoScaler.scaleIn.coolDownMinute | Body | Integer | X | Wait time after scale in |
| workload.autoScaler.scaleIn.condition | Body | List | X | Scale-in conditions |
| workload.autoScaler.scaleIn.condition.resource | Body | String | X | Resources based on scale in conditions<ul><li>cpu</li><li>memory</li><li>gpu</li><li>gpu-memory</li></ul> |
| workload.autoScaler.scaleIn.condition.threshold | Body | Integer | X | Scale in condition resource usage (1-100) |
| workload.autoScaler.scaleIn.condition.duration | Body | Integer | X | Scale in condition resource usage hold time (minutes) |
| workload.securityGroups | Body | List | X | SecurityGroups information |
| workload.securityGroups.id | Body | String | O | SecurityGroups ID |

<details>
  <summary>Example</summary>

```json
{
  "workload": {
    "description": "api workload",
    "desired": 2,
    "loadBalancing": {
      "enabled": true,
      "floatingIp": false
    },
    "name": "ncs-workload",
    "templateId": "bf095f99-1547-48f4-b57d-1124e853f6e2",
    "templateVersion": "first",
    "type": "deployment"
  }
}
```

</details>

<a id="change-workload-response"></a>

#### Response

| Name | Type | Format | Required | Description |
| --- | --- | --- | --- | --- |
| workloads | Body | Object | O | Workload information |
| workload.id | Body | UUID | O | Workload ID |
| workload.name | Body | String | O | Workload name |
| workload.type | Body | String | O | Deployment controller<ul><li>deployment</li><li>statefulset</li></ul> |
| workload.templateId | Body | String | O | Template ID of the workload |
| workload.templateVersion | Body | String | O | Template version of the workload |
| workload.createdAt | Body | String | O | Creation time (UTC) |
| workload.desired | Body | Integer | O | Number of tasks requested for the workload |
| workload.internalLBTimeout | Body | Integer | X | Internal request response latency |
| workload.loadBalancing | Body | Object | O | Workload load balancer information |
| workload.loadBalancing.enabled | Body | Boolean | O | Whether to use workload load balancer |
| workload.loadBalancing.floatingIp | Body | Boolean | O | Whether to use the workload load balancer floating IP |
| workload.loadBalancing.vipAddress | Body | String | X | Specify IP address of workload load balancer |
| workload.loadBalancing.healthMonitor | Body | Object | X | Health check information for the load balancer |
| workload.loadBalancing.healthMonitor.delay | Body | Integer | O | Health check interval |
| workload.loadBalancing.healthMonitor.timeout | Body | Integer | O | Maximum response wait time |
| workload.loadBalancing.healthMonitor.maxRetries | Body | Integer | O | Maximum number of retries |
| workload.loadBalancing.healthMonitor.httpMethod | Body | String | X | HTTP method<ul><li>GET</li></ul> |
| workload.loadBalancing.healthMonitor.expectedCodes | Body | String | X | HTTP status code<ul><li>200</li><li>200,202</li><li>200-204</li></ul> |
| workload.loadBalancing.healthMonitor.urlPath | Body | String | X | HTTP URL |
| workload.loadBalancing.certificate | Body | String | X | Certificates used by the load balancer when using TERMINATED\_HTTPS |
| workload.loadBalancing.privateKey | Body | String | X | Private key used by the load balancer when using TERMINATED\_HTTPS |
| workload.loadBalancing.tlsVersion | Body | String | X | TLS version when using TERMINATED\_HTTPS<ul><li>SSLv3</li><li>TLSv1.0</li><li>TLSv1.0\_2016</li><li>TLSv1.1</li><li>TLSv1.2</li><li>TLSv1.3</li></ul> |
| workload.loadBalancing.containerHref | Body | String | X | Secret container ID<li>If you separately registered a certificate and private key to use in TERMINATED\_HTTPS using the Load Balancer API, use it.</li> |
| workload.loadBalancing.ipAclGroupsBinding | Body | List | X | List of IP access control groups to apply to the load balancer |
| workload.loadBalancing.ipAclGroupsBinding.ipAclGroupId | Body | String | O | IP access control group ID |
| workload.schedule | Body | Object | X | Scheduled execution configuration information |
| workload.schedule.timeZone | Body | String | O | Base time for scheduled execution<ul><li>Example: Asia/Seoul, UTC</li><li>[List of tz database time zones](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones)</li></ul> |
| workload.schedule.cron | Body | String | O | Cron expression for scheduled execution |
| workload.schedule.jobsHistoryLimit | Body | Integer | O | Number of scheduled execution histories |
| workload.schedule.concurrencyPolicy | Body | String | O | Concurrency policy<ul><li>Forbid</li><li>Replace</li></ul> |
| workload.schedule.timeOffset | Body | String | O | Offset the scheduled execution base time |
| workload.internalLoadBalancing | Body | Object | X | Internal load balancer information |
| workload.internalLoadBalancing.enalbed | Body | Boolean | O | Whether to use an internal load balancer |
| workload.internalLoadBalancing.type | Body | String | X | How to assign internal load balancer IPs<ul><li>dynamic: Automatic allocation</li><li>static: Specify IP</li></ul> |
| workload.internalLoadBalancing.ip | Body | String | X | Specify internal load balancer IP |
| workload.privateDns | Body | Object | X | Determinine whether to register workload working IPs with Private DNS |
| workload.privateDns.ttl | Body | Integer | O | TTL value of the record set |
| workload.privateDns.zoneId | Body | String | O | The Private DNS Zone ID used by the workload |
| workload.privateDns.domain | Body | String | O | About domains registered with Private DNS |
| workload.activeDeadline | Body | Object | X | Workload scheduled termination information |
| workload.activeDeadline.timeZone | Body | String | O | Scheduling end base time<li>Example: Asia/Seoul, UTC</li> |
| workload.activeDeadline.timeOffset | Body | String | O | Offset the scheduling end base time |
| workload.activeDeadline.time | Body | String | O | Scheduled termination time |
| workload.autoScaler | Body | Object | X | AutoScaler configuration information |
| workload.autoScaler.scaleOut | Body | Object | O | ScaleOut information |
| workload.autoScaler.scaleOut.enabled | Body | Boolean | O | Whether ScaleOut is enabled |
| workload.autoScaler.scaleOut.maxReplicas | Body | Integer | X | Maximum number of jobs for autoscaling |
| workload.autoScaler.scaleOut.coolDownMinute | Body | Integer | X | Wait time after scaling up |
| workload.autoScaler.scaleOut.condition | Body | List | X | Scale-out conditions |
| workload.autoScaler.scaleOut.condition.resource | Body | String | X | Resources based on scale out conditions<ul><li>cpu</li><li>memory</li><li>gpu</li><li>gpu-memory</li></ul> |
| workload.autoScaler.scaleOut.condition.threshold | Body | Integer | X | Scale out condition resource usage (1-100) |
| workload.autoScaler.scaleOut.condition.duration | Body | Integer | X | Scale out condition resource usage hold time (minutes) |
| workload.autoScaler.scaleIn | Body | Object | X | ScaleIn information |
| workload.autoScaler.scaleIn.enabled | Body | Boolean | O | Whether ScaleIn is enabled |
| workload.autoScaler.scaleIn.minReplicas | Body | Integer | X | Minimum number of jobs for autoscaling |
| workload.autoScaler.scaleIn.coolDownMinute | Body | Integer | X | Wait time after scale in |
| workload.autoScaler.scaleIn.condition | Body | List | X | Scale-in conditions |
| workload.autoScaler.scaleIn.condition.resource | Body | String | X | Resources based on scale in conditions<ul><li>cpu</li><li>memory</li><li>gpu</li><li>gpu-memory</li></ul> |
| workload.autoScaler.scaleIn.condition.threshold | Body | Integer | X | Scale in condition resource usage (1-100) |
| workload.autoScaler.scaleIn.condition.duration | Body | Integer | X | Scale in condition resource usage hold time (minutes) |
| workload.securityGroups | Body | List | X | SecurityGroups information |
| workload.securityGroups.id | Body | String | O | SecurityGroups ID |

<details>
  <summary>Example</summary>

```json
{
  "header": {
    "resultCode": 200,
    "resultMessage": "SUCCESS",
    "isSuccessful": true
  },
  "workload": {
    "createdAt": "2024-10-27T22:51:32.305Z",
    "updatedAt": "2024-10-27T22:54:30.734Z",
    "id": "6c6201b5-5b68-4035-adf7-40cd5f9402e5",
    "name": "ncs-workload",
    "namespace": "abd7f92e-3353-4b45-944c-510a97ef89c9",
    "description": "api workload",
    "templateId": "bf095f99-1547-48f4-b57d-1124e853f6e2",
    "templateName": "nginx-template",
    "templateVersion": "first",
    "desired": 2,
    "available": 0,
    "status": "",
    "networks": [
      {
        "vpcId": "aeeafe4e-287d-4dd4-b91a-294b87688457",
        "subnetId": "abd7f92e-3353-4b45-944c-510a97ef89c9"
      }
    ],
    "loadBalancing": {
      "enabled": true,
      "floatingIp": false
    },
    "type": "deployment"
  }
}
```

</details>

<a id="changing-workload-parts"></a>

### Change Workload Parts { #changing-workload-parts }

You can modify only part of a workload.

<a id="changing-workload-parts-request"></a>

#### Request

* When using this API, the Content-Type must be set to application/json-patch+json.

```bash
PATCH /ncs/v1.0/appkeys/{appKey}/workloads/{workloadId}
Content-Type: application/json-patch+json
x-nhn-authorization: Bearer {accessToken}
```

| Name | Type | Format | Required | Description |
| --- | --- | --- | --- | --- |
| appKey | URL | String | O | Service Appkey |
| workloadId | URL | String | O | Workload ID |
| token | Header | String | O | NHN Cloud Token |
| op | Body | String | O | Operation<ul><li>Add</li><li>Remove</li><li>Replace</li><li>Copy</li><li>Move</li><li>Test</li></ul> |
| path | Body | String | O | Path of the data to change |
| value | Body | String | X | Changed value |
| from | Body | String | X | Path of the existing data |

<details>
   <summary>Example</summary>

```json
[
  {
    "op": "replace",
    "path": "/workload/desired",
    "value": 1
  }
]
```

</details>

<a id="changing-workload-parts-response"></a>

#### Response

| Name | Type | Format | Required | Description |
| --- | --- | --- | --- | --- |
| workloads | Body | Object | O | Workload information |
| workload.id | Body | UUID | O | Workload ID |
| workload.name | Body | String | O | Workload name |
| workload.type | Body | String | O | Deployment controller<ul><li>deployment</li><li>statefulset</li></ul> |
| workload.templateId | Body | String | O | Template ID of the workload |
| workload.templateVersion | Body | String | O | Template version of the workload |
| workload.createdAt | Body | String | O | Creation time (UTC) |
| workload.desired | Body | Integer | O | Number of tasks requested for the workload |
| workload.internalLBTimeout | Body | Integer | X | Internal request response latency |
| workload.loadBalancing | Body | Object | O | Workload load balancer information |
| workload.loadBalancing.enabled | Body | Boolean | O | Whether to use workload load balancer |
| workload.loadBalancing.floatingIp | Body | Boolean | O | Whether to use the workload load balancer floating IP |
| workload.loadBalancing.vipAddress | Body | String | X | Specify IP address for workload load balancer |
| workload.loadBalancing.healthMonitor | Body | Object | X | Health check information for the load balancer |
| workload.loadBalancing.healthMonitor.delay | Body | Integer | X | Health check interval |
| workload.loadBalancing.healthMonitor.timeout | Body | Integer | X | Maximum response wait time |
| workload.loadBalancing.healthMonitor.maxRetries | Body | Integer | X | Maximum number of retries |
| workload.loadBalancing.healthMonitor.httpMethod | Body | String | X | HTTP method<ul><li>GET</li></ul> |
| workload.loadBalancing.healthMonitor.expectedCodes | Body | String | X | HTTP status code<ul><li>200</li><li>200,202</li><li>200-204</li></ul> |
| workload.loadBalancing.healthMonitor.urlPath | Body | String | X | HTTP URL |
| workload.loadBalancing.certificate | Body | String | X | Certificates used by the load balancer when using TERMINATED\_HTTPS |
| workload.loadBalancing.privateKey | Body | String | X | Private key used by the load balancer when using TERMINATED\_HTTPS |
| workload.loadBalancing.tlsVersion | Body | String | X | TLS version when using TERMINATED\_HTTPS<ul><li>SSLv3</li><li>TLSv1.0</li><li>TLSv1.0\_2016</li><li>TLSv1.1</li><li>TLSv1.2</li><li>TLSv1.3</li></ul> |
| workload.loadBalancing.containerHref | Body | String | X | Secret container ID<li>If you separately registered a certificate and private key to use in TERMINATED\_HTTPS using the Load Balancer API, use it.</li> |
| workload.loadBalancing.ipAclGroupsBinding | Body | List | X | List of IP access control groups to apply to the load balancer |
| workload.loadBalancing.ipAclGroupsBinding.ipAclGroupId | Body | String | O | IP access control group ID |
| workload.schedule | Body | Object | X | Scheduled execution configuration information |
| workload.schedule.timeZone | Body | String | O | Base time for scheduled execution<ul><li>Example: Asia/Seoul, UTC</li><li>[List of tz database time zones](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones)</li></ul> |
| workload.schedule.cron | Body | String | O | Cron expression for scheduled execution |
| workload.schedule.jobsHistoryLimit | Body | Integer | O | Number of scheduled execution histories |
| workload.schedule.concurrencyPolicy | Body | String | O | Concurrency policy<ul><li>Forbid</li><li>Replace</li></ul> |
| workload.schedule.timeOffset | Body | String | O | Offset the scheduled execution base time |
| workload.internalLoadBalancing | Body | Object | X | Internal load balancer information |
| workload.internalLoadBalancing.enalbed | Body | Boolean | O | Whether to use an internal load balancer |
| workload.internalLoadBalancing.type | Body | String | X | How to assign internal load balancer IPs<ul><li>dynamic: Automatic allocation</li><li>static: Specify IP</li></ul> |
| workload.internalLoadBalancing.ip | Body | String | X | Specify internal load balancer IP |
| workload.privateDns | Body | Object | X | Determinine whether to register workload working IPs with Private DNS |
| workload.privateDns.ttl | Body | Integer | O | TTL value of the record set |
| workload.privateDns.zoneId | Body | String | O | The Private DNS Zone ID used by the workload |
| workload.privateDns.domain | Body | String | O | About domains registered with Private DNS |
| workload.activeDeadline | Body | Object | X | Workload scheduled termination information |
| workload.activeDeadline.timeZone | Body | String | O | Scheduling end base time<li>Example: Asia/Seoul, UTC</li> |
| workload.activeDeadline.timeOffset | Body | String | O | Offset the scheduling end base time |
| workload.activeDeadline.time | Body | String | O | Scheduled termination time |
| workload.autoScaler | Body | Object | X | AutoScaler configuration information |
| workload.autoScaler.scaleOut | Body | Object | O | ScaleOut information |
| workload.autoScaler.scaleOut.enabled | Body | Boolean | O | Whether ScaleOut is enabled |
| workload.autoScaler.scaleOut.maxReplicas | Body | Integer | X | Maximum number of jobs for autoscaling |
| workload.autoScaler.scaleOut.coolDownMinute | Body | Integer | X | Wait time after scaling up |
| workload.autoScaler.scaleOut.condition | Body | List | X | Scale-out conditions |
| workload.autoScaler.scaleOut.condition.resource | Body | String | X | Resources based on scale out conditions<ul><li>cpu</li><li>memory</li><li>gpu</li><li>gpu-memory</li></ul> |
| workload.autoScaler.scaleOut.condition.threshold | Body | Integer | X | Scale out condition resource usage (1-100) |
| workload.autoScaler.scaleOut.condition.duration | Body | Integer | X | Scale out condition resource usage hold time (minutes) |
| workload.autoScaler.scaleIn | Body | Object | X | ScaleIn information |
| workload.autoScaler.scaleIn.enabled | Body | Boolean | O | Whether ScaleIn is enabled |
| workload.autoScaler.scaleIn.minReplicas | Body | Integer | X | Minimum number of jobs for autoscaling |
| workload.autoScaler.scaleIn.coolDownMinute | Body | Integer | X | Wait time after scale in |
| workload.autoScaler.scaleIn.condition | Body | List | X | Scale-in conditions |
| workload.autoScaler.scaleIn.condition.resource | Body | String | X | Resources based on scale in conditions<ul><li>cpu</li><li>memory</li><li>gpu</li><li>gpu-memory</li></ul> |
| workload.autoScaler.scaleIn.condition.threshold | Body | Integer | X | Scale in condition resource usage (1-100) |
| workload.autoScaler.scaleIn.condition.duration | Body | Integer | X | Scale in condition resource usage hold time (minutes) |
| workload.securityGroups | Body | List | X | SecurityGroups information |
| workload.securityGroups.id | Body | String | O | SecurityGroups ID |

<details>
  <summary>Example</summary>

```json
{
  "header": {
    "resultCode": 200,
    "resultMessage": "SUCCESS",
    "isSuccessful": true
  },
  "workload": {
    "createdAt": "2024-10-27T22:51:32.305Z",
    "updatedAt": "2024-10-27T22:57:00.663Z",
    "id": "6c6201b5-5b68-4035-adf7-40cd5f9402e5",
    "name": "ncs-workload",
    "namespace": "abd7f92e-3353-4b45-944c-510a97ef89c9",
    "description": "api workload",
    "templateId": "bf095f99-1547-48f4-b57d-1124e853f6e2",
    "templateName": "nginx-template",
    "templateVersion": "first",
    "desired": 1,
    "available": 0,
    "status": "",
    "networks": [
      {
        "vpcId": "aeeafe4e-287d-4dd4-b91a-294b87688457",
        "subnetId": "abd7f92e-3353-4b45-944c-510a97ef89c9"
      }
    ],
    "loadBalancing": {
      "enabled": true,
      "floatingIp": false
    },
    "type": "deployment"
  }
}
```

</details>

<a id="stop-workload"></a>

### Stop Workload { #stop-workload }
Stops a workload.

```bash
POST /ncs/v1.0/appkeys/{appKey}/workloads/{workloadId}/pause
x-nhn-authorization: Bearer {accessToken}
```

<a id="stop-workload-request"></a>
#### Request

This API does not require a request body.

| Name | Type | Format | Required | Description |
| --- | --- | --- | --- | --- |
| appKey | URL | String | O | Service Appkey |
| workloadId | URL | String | O | Template ID |
| token | Header | String | O | NHN Cloud Token |

<a id="stop-workload-response"></a>
#### Response
This API responds with common information.

<a id="restart-workload"></a>

### Restart Workload { #restart-workload }
Restarts a workload that is stopped.

```bash
POST /ncs/v1.0/appkeys/{appKey}/workloads/{workloadId}/resume
x-nhn-authorization: Bearer {accessToken}
```

<a id="restart-workload-request"></a>
#### Request

This API does not require a request body.

| Name | Type | Format | Required | Description |
| --- | --- | --- | --- | --- |
| appKey | URL | String | O | Service Appkey |
| workloadId | URL | String | O | Workload ID |
| token | Header | String | O | NHN Cloud Token |

<a id="restart-workload-response"></a>
#### Response
This API responds with common information.

<a id="delete-workload"></a>

### Restart Workload Task { #delete-workload }
Restarts a task in the workload.

```bash
POST /ncs/v1.0/appkeys/{appKey}/workloads/{workloadId}/tasks/{taskId}/restart
x-nhn-authorization: Bearer {accessToken}
```

<a id="delete-workload-request"></a>
#### Request

This API does not require a request body.

| Name | Type | Format | Required | Description |
| --- | --- | --- | --- | --- |
| appKey | URL | String | O | Service Appkey |
| workloadId | URL | String | O | Workload ID |
| taskId | URL | String | O | Task ID |
| token | Header | String | O | NHN Cloud Token |

<a id="delete-workload-response"></a>
#### Response
This API responds with common information.

<a id="workload-1"></a>

### Delete Workload { #workload-1 }

Deletes a workload.

```bash
DELETE /ncs/v1.0/appkeys/{appKey}/workloads/{workloadId}
x-nhn-authorization: Bearer {accessToken}
```

<a id="workload-1-1"></a>
#### Request

This API does not require a request body.

| Name | Type | Format | Required | Description |
| --- | --- | --- | --- | --- |
| appKey | URL | String | O | Service Appkey |
| workloadId | URL | String | O | Workload ID |
| token | Header | String | O | NHN Cloud Token |

<a id="workload-1-2"></a>
#### Response

This API responds with common information.

<a id="view-malware-scan-settings"></a>

### View Malware Scan Settings { #view-malware-scan-settings }
Retrieves the configured malware scan settings.

```bash
GET /ncs/v1.0/appkeys/{appKey}/malware/config
x-nhn-authorization: Bearer {accessToken}
```

<a id="view-malware-scan-settings-request"></a>
#### Request

This API does not require a request body.

| Name | Type | Format | Required | Description |
| --- | --- | --- | --- | --- |
| appKey | URL | String | O | Service Appkey |
| token | Header | String | O | NHN Cloud Token |


<a id="view-malware-scan-settings-respose"></a>
#### Response

| Name | Type | Format | Required | Description |
| --- | --- | --- | --- | --- |
| enabled | Body | String | O | Malware scan settings result<ul><li>true: Enabled</li><li>false: Disabled</li></ul>|

<details>
  <summary>Example</summary>

```json
{
  "header": {
    "resultCode": 200,
    "resultMessage": "SUCCESS",
    "isSuccessful": true
  },
  "enabled": true 
}
```
</details>

<a id="configure-malware-scan"></a>

### Configure Malware Scan { #configure-malware-scan }
Configures the malware scan settings.

```bash
POST /ncs/v1.0/appkeys/{appKey}/malware/config
x-nhn-authorization: Bearer {accessToken}
```

<a id="configure-malware-scan-request"></a>
#### Request
| Name | Type | Format | Required | Description |
| --- | --- | --- | --- | --- |
| appKey | URL | String | O | Service Appkey |
| token | Header | String | O | NHN Cloud Token |
| enabled | Body | String | O | Malware scan settings<ul><li>true: Enable</li><li>false: Disable</li></ul>|

<details>
  <summary>Example</summary>

```json
{
  "enabled": true 
}
```
</details>

<a id="configure-malware-scan-response"></a>
#### Response

| Name | Type | Format | Required | Description |
| --- | --- | --- | --- | --- |
| enabled | Body | String | O | Malware scan settings result<ul><li>true: Enabled</li><li>false: Disabled</li></ul>|

<details>
  <summary>Example</summary>

```json
{
  "header": {
    "resultCode": 200,
    "resultMessage": "SUCCESS",
    "isSuccessful": true
  },
  "enabled": true 
}
```
</details>

<a id="view-malware-scan-result"></a>

### View Malware Scan Result { #view-malware-scan-result }

Retrieves the malware scan result.

```bash
GET /ncs/v1.0/appkeys/{appKey}/workloads/{workloadId}/history/{historyId}/malware
x-nhn-authorization: Bearer {accessToken}
```

<a id="view-malware-scan-result-request"></a>
#### Request

This API does not require a request body.

| Name | Type | Format | Required | Description |
| --- | --- | --- | --- | --- |
| appKey | URL | String | O | Service Appkey |
| token | Header | String | O | NHN Cloud Token |
| workloadId | URL | String | O | Workload ID |


<a id="view-malware-scan-result-response"></a>
#### Response

| Name | Type | Format | Required | Description |
| --- | --- | --- | --- | --- |
| X-Total-Count | Header | Integer | O | Number of workload scan results |
| scannedAt | Body | String | X | Scan completion time |
| infectedFiles | Body | String | X | Number of detected malware |
| scannedDirectories | Body | String | X | Number of scanned directories |
| scannedFiles | Body | String | X | Number of scanned files |
| reports | Body | Array | X | Number of reports |
| reports.image | Body | String | O | Image name:tag |
| reports.digest | Body | String | O | Image digest |
| reports.layer | Body | String | O | Image layer |
| reports.detection | Body | String | O | Detection item |
| reports.result | Body | String | O | Result<br><ul><li>Clean</li><li>Infected</li></ul> |

<details>
  <summary>Example</summary>

```json
{
  "header": {
    "resultCode": 200,
    "resultMessage": "SUCCESS",
    "isSuccessful": true
  },
  "scannedAt": "2025-10-28T00:00:00Z",
  "infectedFiles": 0,
  "scannedDirectories": 689,
  "scannedFiles": 4210,
  "reports": [
    {
      "image": "nginx:latest",
      "digest": "sha256:d5f28ef21aabddd098f3dbc21fe5b7a7d7a184720bc07da0b6c9b9820e97f25e",
      "layer": "sha256:36f5f951f60a9fa1d51878e76fc16ba7b752f4d464a21b758a8ac88f0992c488",
      "detection": "-",
      "result": "Clean"
    },
    {
      "image": "nginx:latest",
      "digest": "sha256:d5f28ef21aabddd098f3dbc21fe5b7a7d7a184720bc07da0b6c9b9820e97f25e",
      "layer": "sha256:c855abf10cdcf792853d61ec842e41c85cb82a5cb926c86217a7fa632dfc56c4",
      "detection": "-",
      "result": "Clean"
    },
    {
      "image": "nginx:latest",
      "digest": "sha256:d5f28ef21aabddd098f3dbc21fe5b7a7d7a184720bc07da0b6c9b9820e97f25e",
      "layer": "sha256:8e7d6b51107830934d3dcdcf0883f193250d22b3d0dc7a2d7d57e4403d1a3489",
      "detection": "-",
      "result": "Clean"
    },
    {
      "image": "nginx:latest",
      "digest": "sha256:d5f28ef21aabddd098f3dbc21fe5b7a7d7a184720bc07da0b6c9b9820e97f25e",
      "layer": "sha256:50da593f622278859c89ed290484a8cafa3ddb1fef0090530fff63c9de06845f",
      "detection": "-",
      "result": "Clean"
    },
    {
      "image": "nginx:latest",
      "digest": "sha256:d5f28ef21aabddd098f3dbc21fe5b7a7d7a184720bc07da0b6c9b9820e97f25e",
      "layer": "sha256:72fa904a482c9806187aeb804837f58f54da8aeb564f0ce4ef01426e08f68a01",
      "detection": "-",
      "result": "Clean"
    },
    {
      "image": "nginx:latest",
      "digest": "sha256:d5f28ef21aabddd098f3dbc21fe5b7a7d7a184720bc07da0b6c9b9820e97f25e",
      "layer": "sha256:7d95a4a72e110d4fe6bab4059f2d2968058c8006d0f3976ea7065186acc49fbd",
      "detection": "-",
      "result": "Clean"
    },
    {
      "image": "nginx:latest",
      "digest": "sha256:d5f28ef21aabddd098f3dbc21fe5b7a7d7a184720bc07da0b6c9b9820e97f25e",
      "layer": "sha256:3ce214e9ebc59367731dc352744c8392822aceddcee0a3806537dfd9fa984268",
      "detection": "-",
      "result": "Clean"
    }
  ]
}
```
</details>

<a id="response-code"></a>

## Response Codes { #response-code }
| resultCode | resultMessage | Description |
| --- | --- | --- |
| 200 | SUCCESS | Request successful |
| 10001 | Authentication error. | The AppKey is invalid. |
| 10002 | Bad Request. | An invalid value was requested. |
| 10003 | An error occurred while parsing the request body. | An error occurred while parsing the request body. |
| 10004 | Internal server error. | Internal server error. |
| 10005 | No permissions. | You do not have permission. |
| 10006 | You have exceeded the maximum number of {{.Resource}} that can be created. Please contact the Customer Center to increase the limit. | The maximum number of {{.Resource}} that can be created has been exceeded. |
| 10041 | Could not find the template. | The template was not found. |
| 10042 | Could not use the ECR. | Images from ECR cannot be used. |
| 10043 | The network information does not exist. | The network information does not exist. |
| 10044 | The template in use by the workload cannot be deleted. | A template in use by a workload cannot be deleted. |
| 10045 | Duplicate container port exists in the template. | A duplicate container port exists in the template. |
| 10046 | Template with the same name already exists. | A template with the same name already exists. |
| 10047 | Resource {{.gpuFlavor}} is not available. If you want to use, please contact the Customer Center. | The {{.gpuFlavor}} resource is not available. |
| 10048 | Failed to download ConfigMaps. | Failed to download ConfigMaps. |
| 10049 | ConfigMaps can only use the object storage from the same organization. | Configmaps can only use Object Storage from the same organization. |
| 10050 | The total size of the template's ConfigMap cannot exceed 1 MiB. | The total size of the template's ConfigMap cannot exceed 1 MiB. |
| 10051 | Failed to download secrets from Secure Key Manager. | Failed to download secrets from Secure Key Manager. |
| 10052 | Could not create a template that consists only of init containers. | A template that consists only of init containers cannot be created. |
| 10053 | The {{.Resource}} of an init container must be less than the sum of the normal containers. | The {{.Resource}} of an init container must be less than the sum of the regular containers. |
| 10054 | Could not set the GPU type of an init container differently than a regular container. | Could not set the GPU type of an init container differently than a regular container. |
| 10061 | Could not find the workload. | The workload was not found. |
| 10062 | Task does not exist. | The task does not exist. |
| 10063 | You cannot use the load balancer because the container port is not specified in the template. | You cannot use the load balancer because the container port is not specified in the template. |
| 10064 | A workload with the same name already exists. | A workload with the same name already exists. |
| 10065 | Invalid container specifications in the template. | The container specifications in the template are invalid. |
| 10066 | Could not create a workload due to insufficient resources. | The workload could not be created due to insufficient resources. |
| 10067 | You cannot change the workload name. | The workload name cannot be changed. |
| 10068 | You cannot change to the template that uses a different network. | You cannot change to a template that uses a different network. |
| 10069 | In the template, you must set the same container port as the port used by the load balancer. | In the template, you must set the same container port as the port used by the load balancer. |
| 10070 | You cannot use the load balancer in legacy network environments. | The load balancer cannot be used in legacy network environments. |
| 10071 | UDP protocol cannot use load balancer. | The UDP protocol cannot use the load balancer. |
| 10072 | If the workload runs less than {{.Minutes}} minutes, you cannot use the load balancer. | If the workload execution interval is {{.Minutes}} minutes or less, the load balancer is not available. |
| 10073 | Invalid cron expression. | The cron expression is invalid. |
| 10074 | Invalid time zone. | The time zone is invalid. |
| 10075 | You cannot change the load balancer to Use while the workload is stopped. | You cannot change the load balancer to Enabled while the workload is stopped. |
| 10076 | The certificate and private key are invalid. To use TERMINATED_HTTPS, you must register a valid certificate and private key. | The certificate and private key are invalid. You must enroll for a valid certificate and private key to use TERMINATED_HTTPS. |
| 10077 | Only one security group can be used. | Only one security group can be used. |
| 10078 | The actions of all groups must be the same. | The actions of all groups must be the same. |
| 10079 | Invalid Private DNS zone. | The Private DNS zone is invalid. |
| 10080 | Could not change the load balancer to Enabled while the workload is terminated. | You cannot change the load balancer to Enabled while the workload is terminated. |
| 10081 | The task is not in a restartable state. | The task is not in a restartable state. |