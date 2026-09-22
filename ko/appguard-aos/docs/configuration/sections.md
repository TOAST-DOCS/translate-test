# 기능별 설정

통합 설정 파일의 `configs`에 작성할 수 있는 기능별 설정을 설명합니다.

| 기능 | 설정 이름 | 작성하지 않았을 때 |
|------|-----------|--------------------|
| 리소스 문자열 난독화 | `resourceStringObfuscation` | 난독화하지 않음 |
| DEX 암호화 대상 지정 | `dexEncryption` | DEX 암호화가 활성화된 경우 전체 DEX 암호화 |

<a id="resource-string-obfuscation-section"></a>
## 리소스 문자열 난독화 { #resource-string-obfuscation-section }

`resourceStringObfuscation` 설정에 난독화할 문자열 리소스 이름 패턴을 지정합니다. 기능 설명은 [7. 리소스 문자열 난독화](../resource-string-obfuscation/overview.md)를 참고하세요.

```json
{
  "version": "1.0",
  "configs": {
    "resourceStringObfuscation": {
      "enabled": true,
      "include": ["secret_key", "secret_*", "*secret*"],
      "exclude": ["secret_debug_*"]
    }
  }
}
```

| 필드 | 타입 | 필수 | 설명 |
|------|------|------|------|
| `enabled` | Boolean | N | 기능 활성화 여부(기본값: `true`) |
| `include` | String[] | Y | 난독화 대상 리소스 이름 패턴 |
| `exclude` | String[] | N | 난독화 제외 리소스 이름 패턴(기본값: `[]`) |

리소스 이름이 `include`에 매칭되고 `exclude`에 매칭되지 않는 경우에만 난독화됩니다. `resourceStringObfuscation` 설정을 작성하지 않으면 리소스 문자열 난독화를 수행하지 않습니다.

패턴 규칙과 주의 사항은 [7.2 설정 파일 작성 방법](../resource-string-obfuscation/config.md)을 참고하세요.

<a id="dex-encryption-section"></a>
## DEX 암호화 대상 지정 { #dex-encryption-section }

DEX 암호화는 Enterprise 플랜에서 기본으로 동작합니다. 암호화 대상을 제한하려면 `dexEncryption` 설정에 패키지나 클래스를 지정합니다. 지정한 대상만 암호화하고 나머지는 암호화하지 않습니다.

!!! warning "ANR 주의"
    암호화 대상 DEX가 크면 복호화 시간이 길어져 ANR이 발생할 수 있습니다. `dexEncryption` 설정으로 암호화 대상을 좁히면 복호화 시간을 줄일 수 있습니다.

```json
{
  "version": "1.0",
  "configs": {
    "dexEncryption": {
      "include": ["com.nhnent.appguard.*"],
      "exclude": ["com.nhnent.appguard.debug.*"]
    }
  }
}
```

| 필드 | 타입 | 필수 | 설명 |
|------|------|------|------|
| `include` | String[] | Y | 암호화 대상 클래스 패턴(비어 있으면 오류) |
| `exclude` | String[] | N | 암호화 제외 클래스 패턴(기본값: `[]`) |

클래스가 `include`에 매칭되고 `exclude`에 매칭되지 않는 경우에만 암호화됩니다. `dexEncryption` 설정을 작성했다면 `include`에 대상을 하나 이상 지정해야 합니다. 전체를 암호화하려면 `include`에 `["*"]`를 지정합니다.

<a id="pattern-rules"></a>
### 패턴 규칙 { #pattern-rules }

`dexEncryption`에는 패키지 이름 또는 클래스 이름만 지정할 수 있습니다. 리소스 문자열 난독화의 패턴 규칙과 다릅니다.

| 패턴 | 설명 | 예시 |
|------|------|------|
| `*` | 전체 매칭 | 모든 클래스 |
| `com.example.*` | 패키지 매칭 | `com.example` 패키지와 모든 하위 패키지의 클래스 |
| `com.example.TestClass` | 클래스 매칭 | `com.example.TestClass`만 매칭 |

`*`는 단독으로 사용하거나 `com.example.*`처럼 패키지 이름 끝에 붙일 수 있습니다. `com.*.sample`, `com.exa*`처럼 다른 위치에 사용하면 보호 작업이 실패합니다.

클래스를 지정하면 내부 클래스도 함께 암호화하거나 제외합니다. 예를 들어 `com.example.TestClass`를 지정하면 `com.example.TestClass$InnerClass`도 동일하게 처리합니다.

<a id="behavior-by-configuration"></a>
### 설정별 동작 { #behavior-by-configuration }

DEX 암호화를 수행할 때 설정에 따른 동작은 다음과 같습니다.

| 상황 | 동작 |
|------|------|
| 통합 설정 파일을 지정하지 않음 | 전체 DEX 암호화 |
| `dexEncryption` 설정을 작성하지 않음 | 전체 DEX 암호화 |
| `include`에 `["*"]`만 지정 | 전체 DEX 암호화 |
| `include`, `exclude`로 대상을 지정 | 지정한 클래스만 부분 암호화 |
| `include`가 비어 있음 | 보호 작업 실패 |
| 지정한 패턴에 매칭되는 클래스가 없음 | 보호 작업 실패 |
| `dexEncryption`의 설정 형식이 잘못됨 | 보호 작업 실패 |

<a id="proguard-guide"></a>
### ProGuard(R8) 사용 시 주의 사항 { #proguard-guide }

이 주의 사항은 **부분 암호화**(`include`/`exclude`로 대상을 지정한 경우)에만 해당합니다. 전체 암호화는 패키지·클래스 이름과 무관하므로 영향받지 않습니다.

부분 암호화는 `include`/`exclude`에 지정한 **패키지·클래스 이름**으로 암호화 대상을 찾습니다. 앱에 ProGuard(R8) 난독화를 함께 적용하면 패키지·클래스 이름이 바뀌어 암호화 대상에서 제외될 수 있습니다.

```text
예) com.example.Sample  ──(ProGuard 적용)──▶  a.a.A
```

예를 들어 `include`에 `com.example.*`를 지정했더라도 ProGuard가 `com.example` 패키지 이름을 바꾸면, 해당 클래스는 더 이상 `com.example.*`에 매칭되지 않아 암호화되지 않습니다.

암호화 대상 패키지 이름이 난독화 후에도 유지되도록 `proguard-rules.pro`에 다음을 추가합니다.

```proguard
-keeppackagenames com.example.**
```

예시의 `com.example`은 실제 부분 암호화 대상 패키지 이름으로 변경하세요. `include`에 `com.example.TestClass`처럼 클래스를 지정한 경우에는 `-keep class com.example.TestClass`를 추가하여 클래스가 제거되거나 이름이 변경되지 않도록 합니다.

설정을 적용한 뒤 대상 클래스가 실제로 암호화되는지 확인하세요.

ProGuard 설정에 관한 자세한 내용은 [9.2 ProGuard 적용 시 확인 사항](../testing/proguard.md)도 참고하세요.

---
