<!-- pre-align:aligned sig=d558666785f8 -->

<a id="logs"></a>
## 로그 { #logs }

**Security > Network Firewall > 콘솔 사용 가이드 > 로그**

**로그** 탭에서는 Network Firewall에서 생성된 로그를 검색할 수 있습니다.

<br>

<a id="search-logs"></a>
## 로그 검색하기 { #search-logs }

<a id="traffic"></a>
### 트래픽 { #traffic }

* Network Firewall을 통과할 때 허용 또는 차단 정책에 의해 생성된 트래픽 로그를 검색합니다.
    * 조회는 1개월 단위로 최대 3개월까지의 과거 데이터만 검색 가능합니다.
        * 최대 저장 로그 개수는 800만 개이며, 트래픽의 양에 따라 저장되는 로그의 양이 달라지므로 과거의 데이터가 조회되지 않을 수 있습니다.
    * 별도의 데이터 저장이 필요한 경우 **옵션** 탭의 **로그 원격 전송 설정**을 참고하세요.

<a id="audit"></a>
### Audit { #audit }

* 정책 생성 및 삭제 등 Network Firewall의 변경 사항에 대한 로그를 검색합니다.
    * 조회는 최대 1개월 단위로 검색 가능하며, 조직 서비스인 CloudTrail에서도 검색할 수 있습니다.

<br>

<a id="download-excel"></a>
## 엑셀 내려받기 { #download-excel }

* **엑셀 내려받기**를 클릭해 트래픽과 Audit 로그의 검색 결과를 다운로드할 수 있습니다.
    * 트래픽 로그의 최대 다운로드 개수는 30만 건입니다.