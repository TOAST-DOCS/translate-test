<!-- pre-align:aligned sig=c10e7e66fdb0 -->

# 키 회전을 이용한 보안 강화 가이드
**Security > Secure Key Manager > 키 회전을 이용한 보안 강화 가이드**

이 가이드는 Secure Key Manager(SKM)의 키 회전 기능을 활용하여 실제 서비스 환경에서 보안 수준을 향상시키는 방법을 설명합니다.

!!! tip "알아두기"
    이 가이드는 이미 Secure Key Manager 서비스를 사용 중인 분들을 대상으로 합니다. 처음 사용하는 경우 [Secure Key Manager 개요](./overview)를 먼저 확인하세요.

<a id="glossary"></a>
## 용어 정리 { #glossary }

이 가이드에서 사용하는 주요 용어를 먼저 이해하면 내용을 더 쉽게 파악할 수 있습니다.

| 용어 | 설명 |
| --- | --- |
| 키 회전(key rotation) | 보안을 강화하기 위해 암호화 키를 주기적으로 새 키로 교체하는 작업입니다. 마치 비밀번호를 정기적으로 변경하는 것과 같은 개념입니다. |
| 봉투 암호화(envelope encryption) | 데이터를 두 단계로 암호화하는 방법입니다. 중요한 문서를 봉투에 넣고, 그 봉투를 다시 금고에 보관하는 것처럼 데이터를 이중으로 보호합니다. |
| DEK(data encryption key, 데이터 암호화 키) | 실제 데이터를 암호화하는 데 사용하는 키입니다. 봉투 암호화에서 '봉투'의 역할을 합니다. |
| KEK(key encryption key, 키 암호화 키) | DEK를 암호화하는 데 사용하는 키입니다. Secure Key Manager에서 관리하는 대칭 키가 이 역할을 합니다. 봉투 암호화에서 '금고'의 역할을 합니다. |
| 키 분할(key segmentation) | 모든 데이터를 하나의 키로 암호화하지 않고, 여러 개의 키로 나누어 암호화하는 전략입니다. 시간별, 지역별, 사용자 그룹별 등 다양한 기준으로 나눌 수 있습니다. 계란을 한 바구니에 담지 않는 것과 같은 원리입니다. |

<a id="why-key-rotation-is-necessary"></a>
## 키 회전이 필요한 이유 { #why-key-rotation-is-necessary }

암호화 키를 장기간 사용할 경우 다음과 같은 보안 위험이 증가합니다.

* **키 노출 위험 증가**: 키를 사용하는 기간이 길어질수록 공격자에게 노출될 가능성이 높아집니다.
* **암호 분석 공격 위험**: 동일한 키로 암호화된 데이터가 많아질수록 패턴 분석을 통한 키 유추가 쉬워집니다.
* **보안 사고 영향 범위 확대**: 키가 유출될 경우 해당 키로 암호화된 모든 데이터가 위험에 노출됩니다.

Secure Key Manager의 키 회전 기능을 사용하면 키 ID를 변경하지 않고 키값만 갱신할 수 있어, 애플리케이션 코드 수정 없이 보안을 강화할 수 있습니다.

<a id="create-a-key-rotation-strategy"></a>
## 키 회전 전략 수립 { #create-a-key-rotation-strategy }

키 회전 전략은 서비스의 비즈니스 영향도와 보안 요구사항에 따라 적절히 수립해야 합니다.

<a id="considerations"></a>
### 고려 사항 { #considerations }

* **서비스 영향도**: 키 회전이 서비스에 미치는 영향을 최소화할 수 있는 전략을 수립합니다.
* **운영 복잡도**: 자동 회전 주기 설정 및 재암호화 전략 등 운영 가능한 범위를 고려합니다.

!!! tip "알아두기"
    최소 30일부터 자동 회전 주기를 설정할 수 있습니다.

<a id="key-rotation-in-an-envelope-encryption-environment"></a>
## 봉투 암호화 환경에서의 키 회전 { #key-rotation-in-an-envelope-encryption-environment }

봉투 암호화(envelope encryption)는 키 회전을 효율적으로 구현할 수 있는 암호화 패턴입니다.

<a id="what-is-envelope-encryption"></a>
### 봉투 암호화란? { #what-is-envelope-encryption }

봉투 암호화는 데이터를 두 단계로 암호화하는 방법입니다. 일반적인 암호화 방식과 어떻게 다른지 비교해 보겠습니다.

<a id="what-is-envelope-encryption-common-encryption-method"></a>
#### 일반적인 암호화 방식

```
[사용자 데이터] → [암호화 키로 직접 암호화] → [암호화된 데이터] (DB 저장)
```

이 방식의 문제점은 키가 유출되면 모든 데이터가 위험에 노출되고, 키를 변경하려면 모든 데이터를 다시 암호화해야 합니다.

<a id="what-is-envelope-encryption-envelope-encryption-method"></a>
#### 봉투 암호화 방식

```
[사용자 데이터] → [DEK로 암호화] → [암호화된 데이터]   (DB 저장)
[DEK] → [KEK로 암호화] → [DEK 암호문]            (KEK는 Secure Key Manager에 저장, DEK 암호문은 DB 또는 Secure Key Manager에 저장)
```

봉투 암호화는 일반 암호화 방식에 비해 다음과 같은 보안상 이점이 있습니다.

* **키 노출 범위 최소화**: KEK는 Secure Key Manager에서 안전하게 보관되며 사용자의 코드로 노출되지 않습니다.
* **키 관리 집중화**: 중요한 KEK는 Secure Key Manager에서 중앙 집중 관리되고, DEK는 각 데이터마다 다르게 생성할 수 있어 피해 범위를 최소화할 수 있습니다.
* **감사 추적 강화**: Secure Key Manager가 모든 KEK 사용 내역을 기록하므로, 키 사용에 대한 감사 추적이 용이합니다.

<a id="what-is-envelope-encryption-understanding-with-analogies"></a>
#### 비유로 이해하기

아파트 현관 비밀번호를 정기적으로 변경해야 하는 상황을 생각해 봅시다.

* **일반 방식**: 현관문(데이터)에 직접 비밀번호(키)를 걸어둠 → 비밀번호를 바꾸려면 100개 세대의 문 비밀번호를 모두 재설정해야 함
* **봉투 방식**: 현관문(데이터)은 고정된 열쇠(DEK)로 잠그고, 열쇠는 작은 보관함에 넣어 비밀번호(KEK)로 보관 → 비밀번호를 바꾸려면 보관함 비밀번호만 변경하면 됨

<a id="why-envelope-encryption-favors-key-rotation"></a>
### 봉투 암호화가 키 회전에 유리한 이유 { #why-envelope-encryption-favors-key-rotation }

<a id="why-envelope-encryption-favors-key-rotation-problems-with-traditional-single-key-encryption"></a>
#### 전통적인 단일 키 암호화의 문제점

* 단일 키로 직접 모든 데이터를 암호화하면, 키 회전 시 전체 데이터를 재암호화해야 합니다.
* 100만 건의 데이터가 있다면, 키 회전 시 100만 건 모두 재암호화가 필요합니다.

<a id="why-envelope-encryption-favors-key-rotation-workarounds-for-envelope-encryption"></a>
#### 봉투 암호화의 해결 방법

* **2단계 암호화 구조**: 데이터는 DEK(data encryption key)로 암호화하고, DEK만 KEK(key encryption key)로 암호화합니다.
* **KEK 회전의 장점**: KEK를 회전해도 실제 사용자 데이터는 그대로이며, DEK 암호문만 처리하면 됩니다.
* **이전 버전 호환**: Secure Key Manager는 여러 버전의 KEK를 동시에 관리하므로, 이전 버전 KEK로 암호화된 DEK 암호문도 자동으로 복호화할 수 있습니다.

<a id="why-envelope-encryption-favors-key-rotation-real-world-impact"></a>
#### 실제 효과

```
단일 키 방식
키 회전 시 → 100만 건의 데이터 재암호화 필요(매우 긴 시간 소요)

봉투 암호화 방식
키 회전 시 → 실제 사용자 데이터는 그대로, 재암호화 불필요
         → DEK 암호문만 새 KEK 버전으로 재암호화
         → 애플리케이션 코드 변경 없이 자동으로 새 KEK 버전 사용
```

이러한 구조 덕분에 봉투 암호화는 **키 회전의 운영 부담을 최소화**하면서도 **보안 수준을 유지**할 수 있습니다.

<a id="implementation-example"></a>
### 봉투 암호화 구현 예시 { #implementation-example }

봉투 암호화 형태로 Secure Key Manager를 이용할 경우 다음과 같은 흐름을 갖는 것을 추천합니다.

![key-rotation.png](http://static.toastoven.net/prod_kms/2026-02-06/NHN%20Cloud_SKM_key-rotation_ko_900.png)

!!! danger "주의"
    키가 필요한 모든 요청에 대하여 Secure Key Manager API를 직접 호출하면 응답 지연이 발생할 수 있습니다. 성능 최적화를 위해 적절히 캐싱하여 사용하세요.

<a id="minimize-the-damage-with-a-key-splitting-strategy"></a>
## 키 분할 전략으로 피해 범위 최소화 { #minimize-the-damage-with-a-key-splitting-strategy }

전체 데이터를 단일 키로 암호화할 경우, 키 유출 시 모든 데이터가 위험에 노출됩니다. 이를 방지하기 위해 키 분할(key segmentation) 전략을 사용하여 피해 범위를 최소화할 수 있습니다.

<a id="the-need-for-key-segmentation"></a>
### 1. 키 분할의 필요성 { #the-need-for-key-segmentation }

<a id="the-need-for-key-segmentation-problems-with-using-a-single-key"></a>
#### 단일 키 사용 시 문제점

```
[전체 고객 데이터 100만 건]
    ↓
[단일 DEK로 암호화]
    ↓
키 유출 시 → 100만 건 전체 위험 노출
```

<a id="the-need-for-key-segmentation-when-applying-key-splitting"></a>
#### 키 분할 적용 시

```
[고객 데이터 100만 건]
    ↓
[지역별/기간별/고객등급별로 여러 DEK 사용]
    ↓
DEK 1개 유출 시 → 10만 건만 위험 노출(피해 90% 감소)
```

<a id="key-split-strategy-types"></a>
### 2. 키 분할 전략 유형 { #key-split-strategy-types }

<a id="key-split-strategy-types-is-time-based-segmentation"></a>
#### 가. 시간 기반 분할(time-based segmentation)

데이터 생성 시점에 따라 다른 키를 사용하는 방식입니다.

**구현 방법**

1. 데이터 생성 시점(년월)별로 Secure Key Manager에서 대칭 키를 생성하고 자동 회전을 설정합니다.
2. 애플리케이션에서 시점별 키 ID 매핑 정보를 관리합니다(예: `2026-01 → 키 ID: abc123...`, `2026-02 → 키 ID: def456...`).
3. 데이터 암호화 시 해당 월에 매핑된 키 ID와 현재 키 버전으로 봉투 암호화를 수행합니다.
4. 암호화된 데이터와 함께 사용한 키 ID와 키 버전 정보를 저장합니다(예: `keyId: abc123..., version: 0`).
5. 복호화 시에는 저장된 키 ID와 버전 정보를 사용하여 데이터를 복호화합니다.

!!! tip "알아두기"
    Secure Key Manager의 키는 UUID 형식의 키 ID와 0부터 시작하는 버전으로 관리됩니다. 키 회전 시 버전이 0 → 1 → 2로 증가하므로, 어느 버전으로 암호화했는지 애플리케이션에서 반드시 기록해야 합니다.

**장점**

* 키 유출 시 해당 기간 데이터만 영향
* 오래된 데이터는 키 삭제로 완전한 데이터 파기 가능
* 규제 준수: 데이터 보관 기간 만료 시 키 삭제로 암호학적으로 파기 가능

**적용 예시**

```
2026년 1월 데이터: 키 ID abc123...(10만 건)
2026년 2월 데이터: 키 ID def456...(10만 건)
2026년 3월 데이터: 키 ID ghi789...(10만 건)

→ 1월 키(abc123...) 유출 시: 1월 데이터 10만 건만 영향
```

<a id="key-split-strategy-types-b-user-group-segmentation"></a>
#### 나. 사용자 그룹 기반 분할(user group segmentation)

사용자 속성에 따라 다른 키를 사용하는 방식입니다.

**구현 방법**

**방법 1: 해시 기반 분할**

1. Secure Key Manager에서 여러 개의 대칭 키를 생성합니다(예: 10개).

!!! tip "알아두기"
    해시 함수는 입력값을 고정된 길이의 고유한 값으로 변환하는 함수입니다. 같은 입력값은 항상 같은 결과를 만들어내므로, 사용자별로 일관된 키를 할당할 수 있습니다.

2. 사용자 ID를 해시 함수로 변환하고, 해시값을 키 개수로 나눈 나머지를 구해 키 번호를 결정합니다(예: 0~9).
3. 애플리케이션에서 키 번호별 키 ID 매핑 정보를 관리합니다(예: `0 → 키 ID: abc123...`, `1 → 키 ID: def456...`).
4. 암호화된 데이터와 함께 사용한 키 ID와 키 버전 정보를 저장합니다.
5. 복호화 시에는 저장된 키 ID와 버전 정보를 사용하여 데이터를 복호화합니다.

**방법 2: 고객 등급별 분할**

1. 고객 등급별로 Secure Key Manager에서 대칭 키를 생성합니다(예: VIP용, PREMIUM용, STANDARD용).
2. 애플리케이션에서 고객 등급별 키 ID 매핑 정보를 관리합니다(예: `VIP → 키 ID: abc123...`, `PREMIUM → 키 ID: def456...`).
3. 암호화된 데이터와 함께 사용한 키 ID와 키 버전 정보를 저장합니다.
4. 복호화 시에는 저장된 키 ID와 버전 정보를 사용하여 데이터를 복호화합니다.

**장점**

* 사용자 그룹별 보안 정책 차등 적용 가능
* 특정 사용자 그룹 키 유출 시 다른 그룹 데이터는 안전
* 고객 등급별 키 회전 주기 차별화(VIP: 30일, 일반: 90일)

<a id="key-split-operation-scenario"></a>
### 3. 키 분할 운영 시나리오 { #key-split-operation-scenario }

**시나리오: 100만 고객 데이터를 10개 키로 분할**

```
초기 상태
- 10개 키 ID(abc123..., def456..., ghi789... 등), 각 10만 건씩 데이터 보유
- 각 키별 독립적으로 관리

사고 발생
→ 키 ID ghi789... 유출 의심

대응 조치
1. 키 ID ghi789... 즉시 회전
2. 해당 키로 암호화된 10만 건의 데이터만 재암호화
3. 다른 9개 키는 영향 없음

결과
✅ 피해 범위: 10만 건(전체의 10%)
✅ 재암호화 시간: 약 1시간(전체 재암호화 시 10시간 → 90% 절감)
✅ 서비스 영향: 최소화
```

<a id="key-partitioning-considerations"></a>
### 4. 키 분할 시 주의사항 { #key-partitioning-considerations }

<a id="key-partitioning-considerations-a-increased-management-complexity"></a>
#### 가. 키 관리 복잡도 증가

분할된 키가 많아질수록 관리가 복잡해집니다.

**키 목록 추적 방법**

1. Secure Key Manager API를 사용하여 현재 활성화된 모든 키 목록을 조회합니다.
2. 애플리케이션의 키 매핑 테이블을 기준으로 그룹화합니다(예: 시간별, 서비스별, 고객등급별).
3. 각 키 ID에 대해 데이터베이스에서 암호화된 데이터 개수를 조회합니다.
4. 키별 생성일, 다음 회전 예정일, 사용 데이터 개수를 정기적으로 감사합니다.

<a id="key-partitioning-considerations-b-stale-key-cleanup-policy"></a>
#### 나. 오래된 키 정리 정책

사용하지 않는 키를 정리하는 정책이 필요합니다. 생성된 지 일정 기간이 지난 키를 조회하여, 해당 키로 암호화된 데이터가 없다면 삭제 대상으로 분류하고 정기적으로 정리 작업을 수행합니다.

<a id="tips-for-choosing-a-key-partitioning-strategy"></a>
### 5. 키 분할 전략 선택 팁 { #tips-for-choosing-a-key-partitioning-strategy }

처음 시작한다면 **시간 기반 분할(월별)**로 시작하는 것을 추천합니다. 서비스 규모가 커지고 데이터가 중요해지면 **해시 기반 분할**을 추가로 적용하여 보안을 강화할 수 있습니다.

<a id="setting-up-automatic-key-rotation"></a>
## 자동 키 회전 설정 { #setting-up-automatic-key-rotation }

<a id="enabling-auto-rotation-in-the-console"></a>
### 1. 콘솔에서 자동 회전 활성화 { #enabling-auto-rotation-in-the-console }

**단계별 설정 방법**

1. Secure Key Manager 콘솔에서 키 저장소를 선택합니다.
2. **키 관리** 메뉴를 클릭합니다.
3. 회전할 대칭 키 또는 비대칭 키를 선택합니다.
4. 상세 정보 창에서 **자동 회전 주기**를 설정합니다.

![console-guide-24](http://static.toastoven.net/prod_kms/2023-03-28-ko/console-guide-24.png)

<a id="how-auto-rotation-works"></a>
### 2. 자동 회전 동작 방식 { #how-auto-rotation-works }

* 설정한 주기가 도래하면 **자동으로 새 키 버전 생성**
* 기존 키 ID는 유지되며 키 버전만 증가(0 → 1 → 2 ...)
* **최신 버전이 자동으로 기본 키로 설정**되어 암호화에 사용됨
* 이전 버전 키는 복호화 용도로 계속 사용 가능

!!! danger "주의"
    * 회전 주기를 '0'으로 설정하면 자동 회전이 비활성화됩니다.
    * 최소 회전 주기는 30일입니다.

<a id="operating-manual-key-rotation"></a>
## 수동 키 회전 운영 { #operating-manual-key-rotation }

자동 회전 외에 다음과 같은 상황에서는 즉시 수동 회전이 필요합니다.

<a id="scenarios-requiring-emergency-key-rotation"></a>
### 1. 긴급 키 회전이 필요한 경우 { #scenarios-requiring-emergency-key-rotation }

* KEK 유출 의심 시
* DEK 암호문 유출 의심 시
* 퇴사자 등 내부 인력 변동 발생 시
* 보안 취약점 발견 시
* 시스템 침입 탐지 시

!!! danger "주의"
    평문 DEK가 메모리나 애플리케이션 레벨에서 유출된 경우, 키 회전만으로는 불충분합니다. 이미 유출된 평문 키로 암호화된 데이터는 여전히 복호화 가능하므로, 반드시 데이터 재암호화(re-encryption)를 함께 수행해야 합니다.

<a id="how-to-execute-immediate-rotation"></a>
### 2. 즉시 회전 실행 방법 { #how-to-execute-immediate-rotation }

1. 키 저장소에서 대상 키를 선택합니다.
2. **키 상세 정보** 창에서 **즉시 회전**을 클릭합니다.

![console-guide-26](http://static.toastoven.net/prod_kms/2023-03-28-ko/console-guide-26.png)

3. 회전 완료 후 키 버전 목록에서 새 버전을 확인합니다.

![console-guide-27](http://static.toastoven.net/prod_kms/2023-03-28-ko/console-guide-27.png)

<a id="monitoring-key-rotation-via-api"></a>
### 3. API로 키 회전 모니터링 { #monitoring-key-rotation-via-api }

키 회전 후 변경 사항을 API로 확인할 수 있습니다.

```bash
curl -X GET \
  'https://api-keymanager.nhncloudservice.com/keymanager/v1.2/appkey/{appkey}/keystores/{keyStoreId}/keys/{keyId}' \
  -H 'X-TC-AUTHENTICATION-ID: {User Access Key ID}' \
  -H 'X-TC-AUTHENTICATION-SECRET: {Secret Access Key}'
```

**응답 예시**

```json
{
  "header": {
    "resultCode": 0,
    "resultMessage": "success",
    "isSuccessful": true
  },
  "body": {
    "keyId": "035a0ffa16a64bbf8171c4bdcea37bbf",
    ...중략...
    "currentKeyValueVersion": 2,
    "autoRotationPeriod": 0,
    "nextAutoRotationDate": null,
    ...후략...
  }
}
```

<a id="cautions"></a>
## 주의 사항 { #cautions }

<a id="pre-rotation-checklist"></a>
### 키 회전 적용 전 유의 사항 { #pre-rotation-checklist }

현재 Secure Key Manager의 대칭 키를 **데이터를 직접 암호화하는 용도**로 사용 중이라면, **키 회전을 적용하기 전에 반드시 봉투 암호화로 전환**해야 합니다.

<a id="pre-rotation-checklist-if-data-was-encrypted-directly-with-a-single-key"></a>
#### 단일 키로 데이터를 직접 암호화한 경우

```
사용자 데이터 → Secure Key Manager의 대칭 키로 직접 암호화 → 암호화된 데이터 저장
```

이 상태에서 키 회전을 적용하면 다음과 같은 문제가 발생합니다.

1. 키 버전이 0 → 1로 변경됨
2. 기존 데이터는 이전 키 버전으로 암호화되었지만, 새로운 키 버전으로 복호화를 시도하게 됨
3. 모든 기존 데이터 복호화 실패 → 서비스 전체 장애

<a id="pre-rotation-checklist-safe-implementation-methods"></a>
#### 안전한 적용 방법

**방법 1: 봉투 암호화로 마이그레이션(권장)**

1. 봉투 암호화 구조로 시스템을 재설계합니다.
2. 기존 데이터를 새로운 구조로 마이그레이션합니다.
3. 마이그레이션 완료 후 키 회전을 적용합니다.

**방법 2: 현재 구조 유지(비권장)**

단일 키 암호화를 유지하면서 키 회전을 적용할 경우 다음과 같은 문제가 발생합니다.

* 키 회전 시마다 **모든 데이터를 재암호화**해야 함
* 대량 데이터의 경우 재암호화에 수십 시간 소요
* 재암호화 중 서비스 중단 또는 성능 저하 발생

<a id="pre-rotation-checklist-checklist"></a>
#### 체크리스트

키 회전 적용 전 꼭 다음 사항을 확인하세요.

* 현재 봉투 암호화 방식을 사용하고 있는가?
* 키 ID와 키 버전 정보를 데이터와 함께 저장하고 있는가?
* 테스트 환경에서 키 회전 시나리오를 검증했는가?
* 키 회전 후 기존 데이터 복호화가 정상 동작하는지 확인했는가?

!!! danger "주의"
    프로덕션 환경에 키 회전을 적용하기 전에 반드시 테스트 환경에서 전체 시나리오를 검증해야 합니다. 한 번의 잘못으로 큰 장애가 발생할 수 있습니다.

<a id="conclusion"></a>
## 결론 { #conclusion }

높아지는 보안 요구사항에 대응하기 위해, 이 가이드에서는 Secure Key Manager의 키 회전 기능을 활용한 두 가지 보안 강화 전략을 소개했습니다. 서비스 환경과 데이터 특성에 따라 다음과 같이 필수 또는 선택적으로 적용할 수 있습니다.

<a id="recommended-approach"></a>
### 권장 적용 방식 { #recommended-approach }

<a id="recommended-approach-envelope-encryption-mandatory"></a>
#### 1. 봉투 암호화(필수)

봉투 암호화는 키 회전의 기본이 되는 패턴입니다. 단일 키로 직접 데이터를 암호화하는 방식보다 키 회전이 훨씬 쉽고, 대량의 데이터를 재암호화할 필요가 없습니다. 처음 시스템을 설계할 때부터 봉투 암호화 방식을 적용하는 것을 강력히 권장합니다.

<a id="recommended-approach-key-partitioning-optional"></a>
#### 2. 키 분할(선택)

키 분할은 보안 수준을 한 단계 더 높이는 전략입니다. 하지만 관리 복잡도가 증가하므로, 서비스 특성에 따라 선택적으로 적용할 수 있습니다.

* **적용 시 이점**: 개인정보나 금융 데이터 등 민감한 정보 보호 강화, 키 유출 시 피해 범위 최소화
* **적용 고려사항**: 관리 복잡도 증가, 키 추적 및 정리 정책 필요

<a id="expected-benefits"></a>
### 기대 효과 { #expected-benefits }

Secure Key Manager의 키 회전 기능을 적절히 활용하면 다음과 같은 효과를 얻을 수 있습니다.

* 애플리케이션 코드 변경 없이 보안 수준 향상
* 자동화된 키 관리로 운영 부담 감소
* 보안 컴플라이언스 요구사항 충족
* 보안 사고 발생 시 피해 범위 최소화

키 회전은 일회성 작업이 아닌 지속적인 보안 프로세스입니다. 서비스 규모와 보안 요구사항에 맞게 전략을 선택하고, 정기적인 검토와 개선을 통해 보안 수준을 꾸준히 향상시킬 수 있습니다.

<a id="references"></a>
## 참고 자료 { #references }

* [Secure Key Manager 콘솔 가이드](./console-guide)
* [Secure Key Manager API v1.2 가이드](./api-guide-v1.2)
* [대칭 키 관리 기능을 활용한 봉투 암호화](./overview/#envelope-encryption-with-symmetric-key-management-of-secure-key-manager)