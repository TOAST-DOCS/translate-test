{% include-markdown '../_nas-for-big-data-vars.md' %}

<!-- pre-align:aligned sig=d48e0cc2304b -->

<a id="storage-nas-for-bigdata-console-user-guide"></a>
## Storage > NAS for BigData > 콘솔 사용 가이드 { #storage-nas-for-bigdata-console-user-guide }

이 문서는 NHN Cloud 콘솔에서 NAS for BigData의 볼륨과 스냅숏을 관리하고 인스턴스에 연결하는 방법을 설명합니다.

<a id="volume"></a>
## 볼륨 { #volume }
볼륨은 NAS의 논리적인 저장 공간으로, 인스턴스에 마운트하여 데이터를 저장하거나 읽을 수 있습니다.

<a id="create_volume"></a>
### 볼륨 생성 { #create_volume }

새로운 볼륨을 생성합니다. 생성된 볼륨은 NFS(network file system, 네트워크 파일 시스템) 프로토콜을 사용하여 인스턴스에서 접근할 수 있습니다.

| 항목 | 설명 |
| --- | --- |
| 이름 | 생성할 볼륨의 이름입니다. 볼륨 이름으로 NFS의 접근 경로를 만듭니다. 이름은 100자 이내의 영문자와 숫자, 일부 기호('-', '_')만 입력할 수 있습니다. |
| 설명 | 볼륨의 설명입니다. |
| VPC | 볼륨에 접근할 VPC(virtual private cloud, 가상 사설 클라우드)입니다. |
| 서브넷 | 볼륨에 접근할 서브넷입니다. 선택한 VPC의 서브넷만 선택할 수 있습니다. |
| 크기 | 생성할 볼륨의 크기입니다. 최소 $[ min_size ]$부터 최대 $[ max_size ]$까지 입력할 수 있습니다. |
| 접근 제어 목록(ACL) | Network ACL 서비스에서 접근 제어 목록(ACL)을 설정할 수 있습니다. 자세한 내용은 [Network ACL 서비스 사용자 가이드]($[ network_acl_guide_url ]$)를 참고합니다. |
| 스냅숏 자동 생성 | 설정한 주기에 따라 스냅숏을 자동으로 생성합니다. 설정한 개수를 초과하면 가장 오래된 스냅숏부터 순차적으로 삭제됩니다. |

<a id="delete_volume"></a>
### 볼륨 삭제 { #delete_volume }

볼륨을 삭제합니다.

!!! danger "주의"
    연결된 인스턴스에서 마운트 해제 후 삭제할 것을 권장합니다. 마운트 상태에서 볼륨을 삭제하면 사용자 시스템에 문제가 생길 수 있습니다.

    볼륨을 삭제할 경우 스냅숏을 포함한 모든 데이터가 삭제됩니다. 삭제 후에는 데이터를 복구할 수 없습니다.

<a id="change_volume_size"></a>
### 볼륨 크기 변경 { #change_volume_size }

볼륨의 크기를 변경합니다. 볼륨 사용 중에도 크기를 변경할 수 있습니다.

<a id="change_acl"></a>
### 접근 제어 설정 변경 { #change_acl }

Network ACL 서비스에서 접근 제어 목록(ACL)을 설정할 수 있습니다. 자세한 내용은 [Network ACL 서비스 사용자 가이드]($[ network_acl_guide_url ]$)를 참고합니다.

<a id="snapshots"></a>
## 스냅숏 { #snapshots }
스냅숏은 볼륨의 특정 시점 상태를 저장한 읽기 전용 복사본입니다. 스냅숏을 사용해 볼륨을 스냅숏 생성 시점의 상태로 복원할 수 있습니다.

| 항목 | 설명 |
| --- | --- |
| 이름 | 스냅숏의 이름입니다. 시스템이 생성한 경우 지정된 규칙에 따라 이름이 정해집니다. |
| 생성일 | 스냅숏을 생성한 일시입니다. |

<a id="snapshots.create"></a>
### 스냅숏 즉시 생성 { #snapshots.create }

스냅숏을 즉시 생성합니다. 이름은 32자 이내의 영문자와 숫자, 일부 기호('-', '\_', '.')만 입력할 수 있습니다. 각 스냅숏은 볼륨에서 고유한 이름을 가져야 합니다.

<a id="snapshots.restore"></a>
### 스냅숏 복원 { #snapshots.restore }

볼륨을 스냅숏이 생성된 시점으로 복원합니다. 스냅숏을 복원하려면 [고객지원]($[ support_url ]$)에 문의하세요.

<a id="snapshots.delete"></a>
### 스냅숏 삭제 { #snapshots.delete }

지정한 스냅숏을 삭제합니다. 삭제한 스냅숏은 복구할 수 없습니다.

<a id="connect_volume"></a>
## 볼륨 연결 { #connect_volume }

생성된 볼륨의 연결 정보를 사용하여 인스턴스에 마운트할 수 있습니다. 단, 마운트할 인스턴스는 볼륨과 같은 서브넷에 연결되어야 합니다.

<a id="connect_volume.nfs"></a>
### NFS 패키지 설치 { #connect_volume.nfs }

<a id="connect_volume.nfs-debian-ubuntu"></a>
#### Debian, Ubuntu

```
sudo apt-get install nfs-common rpcbind
```

<br>

<a id="connect_volume.nfs-rocky"></a>
#### Rocky

```
sudo dnf install nfs-utils rpcbind
```

<br>

<a id="connect_volume.rpcbind"></a>
### rpcbind 서비스 실행 { #connect_volume.rpcbind }

```
sudo service rpcbind start
```

<br>

<a id="connect_volume.mount"></a>
### 볼륨 마운트 { #connect_volume.mount }

```
sudo mount -t nfs <nas-source> <mount-point>
```

| 항목 | 설명 |
| --- | --- |
| &lt;nas-source&gt; | 볼륨의 연결 경로(`NFS 서버 주소:내보내기 경로`)<br>예: 192.168.0.11:/GJ\_SHARE\_FS8/bacb62d4-f271-44ad-a5d2-505d21037b45 |
| &lt;mount-point&gt; | 볼륨을 마운트할 디렉터리<br>예: /mnt |
