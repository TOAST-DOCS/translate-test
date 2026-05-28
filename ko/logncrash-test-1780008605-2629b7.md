## Log & Crash 보고 테스트

이 문서는 번역 파이프라인이 작업 완료 후 Log & Crash Search에 로그를 정상적으로 전송하는지 확인하기 위한 짧은 한국어 샘플입니다.

번역 결과의 품질이 아니라, 잡(job)이 끝났을 때 `jobId`, `sourcePrUrl`, `translationPrUrl`, `longDurationSec` 같은 필드를 포함한 한 줄짜리 로그가 수집 서버에 도달했는지를 검증합니다.
