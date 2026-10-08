<!-- pre-align:aligned sig=c2c525b018f2 -->

<a id="ai-service-ocr-document-ai-release-notes"></a>
## AI Service > OCR > Document AI > 릴리스 노트 { #ai-service-ocr-document-ai-release-notes }

<a id="august-11-2026"></a>
### 2026. 08. 11. { #august-11-2026 }

- API 엔드포인트 도메인 변경
  - 신규 엔드포인트 `https://api-ocr.nhncloudservice.com`이 추가되었습니다.
  - 기존 엔드포인트 `https://ocr.api.nhncloudservice.com`은 2027년 7월 31일까지 유지된 후 지원이 종료됩니다.
  - 신규 엔드포인트로 전환하세요. 자세한 내용은 [API 가이드](./document-ai-api-guide-v1.1.md)를 참고하세요.
- 요청 파일 최대 용량 확대
  - 요청 파일 최대 용량이 5MB에서 20MB로 확대되었습니다.

<a id="march-10-2026"></a>
### 2026. 03. 10. { #march-10-2026 }

- API v1.1 출시
  - User Access Key 토큰 인증을 사용하는 API가 추가되었습니다.
  - User Access Key 토큰 발급 및 사용에 대한 자세한 내용은 [User Access Key 토큰](/nhncloud/ko/public-api/user-access-key-token)을 참고하세요.

<a id="november-12-2024"></a>
### 2024. 11. 12. { #november-12-2024 }

- Document AI 서비스 출시
  - OCR을 통해 이미지에서 문자를 추출하고, 추출한 정보를 기반으로 LLM 모델과 연동하여 내용에 대한 요약, 정보 추출 등 질의응답을 제공하는 서비스입니다.
