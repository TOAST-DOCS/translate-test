<!-- pre-align:aligned sig=24c6566066ad -->

# 객체

**Security > Cloud Access > 콘솔 사용 가이드 > 객체**

**객체** 탭에서는 ACL 정책을 생성할 때 사용할 IP와 포트를 관리합니다.

<br>

<a id="manage-ip"></a>
## IP 관리하기 { #manage-ip }

<a id="add"></a>
### 추가 { #add }

![object_add_1.PNG](../../static/images/2025.06.24/object_add_1.png)

필수 항목을 입력하여 객체를 생성합니다.

<a id="modify"></a>
### 수정 { #modify }

**수정**을 클릭해 객체를 수정할 수 있습니다.

<a id="delete"></a>
### 삭제 { #delete }

**삭제**를 클릭해 객체를 삭제할 수 있습니다.

<a id="additional-features"></a>
### 부가 기능 { #additional-features }

* 사용자 객체 추가: 추가된 사용자를 기반으로 객체를 추가할 수 있습니다.
* 템플릿 내려받기: 일괄 등록 시 필요한 템플릿 파일을 다운로드합니다.
* 객체 일괄 등록: 다운로드한 템플릿을 사용하여 한 번에 객체를 등록할 수 있습니다.
* 객체 일괄 내려받기: **객체** 탭에 생성되어 있는 IP 객체 전체를 한 번에 다운로드할 수 있습니다.

<br>

!!! tip "알아두기"
    * 그룹 객체 생성 시 그룹 객체는 추가할 수 없습니다(단일이나 범위 객체만 선택하여 추가 가능합니다.).
    * IP 객체 수정 시 타입은 수정이 불가능합니다.
    * Cloud Access 생성 시 있었던 IP 객체는 수정하거나 삭제할 수 없습니다.

!!! danger "주의"
    정책에서 사용 중인 객체를 삭제할 경우 삭제 후 ALL 객체로 변경됩니다. 삭제 시 유의하세요.

<br>

<a id="manage-port"></a>
## 포트 관리하기 { #manage-port }

<a id="manage-port-add"></a>
### 추가 { #manage-port-add }

![object_add_2.PNG](../../static/images/2025.06.24/object_add_2.png)

필수 항목을 입력하여 객체를 생성합니다.

<a id="manage-port-modify"></a>
### 수정 { #manage-port-modify }

**수정**을 클릭해 객체를 수정할 수 있습니다.

<a id="manage-port-delete"></a>
### 삭제 { #manage-port-delete }

**삭제**를 클릭해 객체를 삭제할 수 있습니다.

<a id="manage-port-additional-features"></a>
### 부가 기능 { #manage-port-additional-features }

* 템플릿 내려받기: 일괄 등록 시 필요한 템플릿 파일을 다운로드합니다.
* 객체 일괄 등록: 다운로드한 템플릿을 사용하여 일괄적으로 객체를 등록할 수 있습니다.
* 객체 일괄 내려받기: **객체** 탭에 생성되어 있는 포트 객체 전체를 각각 한 번에 다운로드할 수 있습니다.


!!! tip "알아두기"
    * 그룹 객체 생성 시 그룹 객체는 추가할 수 없습니다(단일이나 범위 객체만 선택하여 추가 가능합니다.).
    * 포트 객체 수정 시 타입은 수정이 불가능합니다.
    * Cloud Access 생성 시 있었던 포트 객체는 수정하거나 삭제할 수 없습니다.

!!! danger "주의"
    정책에서 사용 중인 객체를 삭제할 경우 삭제 후 ALL 객체로 변경됩니다. 삭제 시 유의하세요.