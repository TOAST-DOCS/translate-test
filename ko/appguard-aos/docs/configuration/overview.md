# 통합 설정 파일

<a id="overview"></a>
## 개요 { #overview }

통합 설정 파일은 보호 작업에 적용할 기능별 설정을 하나로 모은 JSON 파일입니다.

보호 작업을 수행할 때 CLI의 `--config` 옵션으로 전달합니다. CLI 사용법은 [CLI를 이용한 보호 작업]({{ cli_page }})을 참고하세요.

```bash
--config /path/to/appguard.json
```

<a id="supported-version"></a>
## 지원 버전 { #supported-version }

통합 설정 파일은 다음 버전부터 사용할 수 있습니다.

{% if variant == 'onprem' %}

| 구분 | 최소 버전 |
|------|-----------|
| Protector | 1.14.0.0 |
| NHN AppGuard CLI | 1.0.3 |

{% else %}

| 구분 | 최소 버전 |
|------|-----------|
| NHN AppGuard | 1.14.0.0 |

{% endif %}

통합 설정 파일 버전별로 사용할 수 있는 기능은 다음과 같습니다.

| 기능 | 설정 이름 | 통합 설정 파일 버전 |
|------|-----------|--------------------|
| 리소스 문자열 난독화 | `resourceStringObfuscation` | 1.0 이상 |
| DEX 암호화 대상 지정 | `dexEncryption` | 1.0 이상 |

<a id="file-structure"></a>
## 파일 구조 { #file-structure }

설정 파일은 JSON으로 작성합니다. 최상위에 설정 파일의 버전을 나타내는 `version`과 기능별 설정을 담는 `configs`를 두고, `configs` 아래에 사용할 기능의 설정을 추가합니다.

```json
{
  "version": "1.0",
  "configs": {
    "resourceStringObfuscation": {
      "enabled": true,
      "include": ["secret_key", "secret_*", "*secret*"],
      "exclude": ["secret_debug_*"]
    },
    "dexEncryption": {
      "include": ["com.nhnent.appguard.*"],
      "exclude": ["com.nhnent.appguard.debug.*"]
    }
  }
}
```

| 필드 | 타입 | 필수 | 설명 |
|------|------|------|------|
| `version` | String | Y | 설정 파일의 버전 |
| `configs` | Object | Y | 기능별 설정 |

기능별 작성 방법과 설정을 생략했을 때의 동작은 [3.2 기능별 설정](sections.md)을 참고하세요.

<a id="invalid-configuration-file-handling"></a>
## 잘못된 설정 파일 처리 { #invalid-configuration-file-handling }

지정한 설정 파일의 내용이 정해진 형식과 다르면 보호 작업이 실패합니다.

| 상황 | 동작 |
|------|------|
| 설정 파일을 지정하지 않음 | 각 기능의 기본 동작에 따라 보호 작업 수행 |
| JSON 형식이 잘못됨 | 보호 작업 실패 |
| 지원하지 않는 `version` | 보호 작업 실패 |
| 해당 `version`에서 지원하지 않는 기능 이름을 작성함(오타 포함) | 보호 작업 실패 |
| 기능별 설정 형식이 잘못됨 | 보호 작업 실패 |

<a id="compatibility-with-existing-configuration-file"></a>
## 기존 설정 파일과의 호환성 { #compatibility-with-existing-configuration-file }

기존에는 리소스 문자열 난독화 설정 파일을 `--resource-obfuscate` 옵션으로 별도 전달했습니다. 1.14.0.0 이상에서는 이 설정을 통합 설정 파일의 `resourceStringObfuscation`에 작성하고 `--config` 옵션으로 전달하는 것을 권장합니다.

기존 설정 파일을 통합 설정 파일 형식으로 변경하는 방법은 [3.2 기능별 설정](sections.md)을 참고하세요.

1.14.0.0 미만에서는 `--resource-obfuscate`와 기존 설정 파일을 그대로 사용합니다.

```bash
# 1.14.0.0 이상
--config /path/to/appguard.json

# 1.14.0.0 미만
--resource-obfuscate /path/to/resource-obfuscation-rules.json
```

| 옵션 | 전달하는 설정 파일 | 비고 |
|------|--------------------|------|
| `--config` | 통합 설정 파일 | 1.14.0.0 이상에서 사용 |
| `--resource-obfuscate` | 리소스 문자열 난독화 설정 파일 | 기존 방식(지원 종료 예정) |

두 옵션을 함께 지정하면 `--config`로 전달한 통합 설정 파일을 사용합니다.

!!! warning "지원 종료 예정"
    1.14.0.0 이상에서도 `--resource-obfuscate`를 당분간 사용할 수 있습니다. 향후 지원을 종료할 예정이므로 통합 설정 파일(`--config`)로 전환하세요.

---
