## Service > Table Compare Test > 콘솔 사용 가이드

<a id='section-a'></a>
## 섹션 A — 일부 행 누락 케이스

| 파라미터 | 설명 |
|---|---|
| name | 이름 |
| size | 크기 |
| region | 리전 |

<a id='section-b'></a>
## 섹션 B — 행 추가 케이스

| 필드 | 타입 |
|---|---|
| id | string |
| count | int |
| enabled | bool |
| tags | list |

<a id='section-c'></a>
## 섹션 C — ja에 섹션 자체가 없음

| 코드 | 의미 |
|---|---|
| 200 | 성공 |
| 404 | 없음 |

<a id='section-d'></a>
## 섹션 D — en에만 표가 추가됨

설명 문단만 있고 ko에는 표가 없습니다.
