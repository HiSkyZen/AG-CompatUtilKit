# HiSkyZen's Compat 'n' UtilKit

**Version:** `2026.1109.1`  
**Rule content last updated:** `2026-11-09T14:02:00+00:00`  
**Project:** https://github.com/HiSkyZen/AG-CompatUtilKit  
**License:** [MIT](LICENSE)

AdGuard 호환성·사용자 수정 필터와 Microsoft 관련 HTTPS/DNS 예외 목록입니다.
이번 정리에서는 **규칙·도메인·활성화 여부·UUID를 변경하지 않았습니다.**
메타데이터와 문서, 파일 배치만 통일했습니다.

## 가져오기 파일

| 파일 | 실제 형식 | 적용 위치 | 보존 여부 |
|---|---|---|---|
| `mainfilter.txt` | AdGuard 네트워크 필터 | 광고 차단 → 사용자 지정 필터 | 규칙 100개 동일 |
| `dnsfilter.txt` | AdGuard DNS 허용 필터 | DNS 보호 → DNS 필터 | 규칙 43개 동일 |
| `fl.txt` | 선택형 AdGuard 네트워크 필터 | 지원 환경의 신뢰 가능한 사용자 지정 필터 | 규칙 15개 동일 |
| `HTTPSexclusions.adgdomains` | **AdGuard for Windows 네이티브 HTTPS 제외 목록** | 네트워크 설정 → HTTPS 필터링 → 제외 목록 → 가져오기 | 원본 바이너리(텍스트) 바이트 동일, 항목 43개 동일 |
| `DNSexclusions.txt` | **DNS 서버 우회용 순수 도메인 목록** | Windows 앱 설정 → 고급 설정 → DNS 제외 목록 | 원본 바이트 동일, 도메인 43개 동일 |

**중요:** `HTTPSexclusions.adgdomains`는 43개 도메인만 포함하는 파일입니다. 이미 설정되어 있는
HTTPS 제외 목록을 유지하려면 **먼저 기존 목록을 내보내 백업**하세요. 가져오기 과정에서 기존
항목이 대체될 수 있으므로 추가·병합 동작을 전제로 사용하지 마세요. 기존 제외 목록 전체를
자동 병합한 파일이 아닙니다.

`fl.txt`의 원래 경고를 그대로 따르세요. **AdGuard for Windows 또는 Android에서는 활성화하지 마세요.**
`dnsfilter.txt`는 DNS 차단 허용 규칙이며, `DNSexclusions.txt`의 시스템 DNS 우회 기능을
대신하지 않습니다. `mainfilter.txt` 또한 HTTPS 검사 예외를 대신하지 않습니다.

## 메타데이터 정리 원칙

- 네트워크/DNS 필터는 AdGuard의 필터 메타데이터 형식인 `! Title`, `! Description`,
  `! Version`, `! TimeUpdated`, `! Expires`, `! Homepage`, `! License`를 사용합니다.
- `! Expires: 1 day`는 구독 필터의 갱신 간격입니다. DNS/HTTPS 제외 설정 목록의 만료일을 의미하지 않습니다.
- 프로젝트 URL을 원본 Git 설정 및 README의 `HiSkyZen/AG-CompatUtilKit`으로 통일했습니다.
- 버전은 기존 README에 적힌 `2026.1109.1`으로 통일하고, **실제 규칙 변경 일시는 원본 필터의
  `TimeUpdated` 값을 유지**했습니다.
- `.adgdomains` 파일의 최상위 JSON 및 문자열 형태의 `Payload` 구조에는 메타데이터를 임의로
  삽입하지 않았습니다. **원본 파일 자체를 바이트 단위로 그대로 보존**했습니다.
- `DNSexclusions.txt` 역시 호환성 보호를 위해 주석 없이 도메인만 유지했습니다.
- 두 예외 목록의 설명/버전/해시/개수는 별도의 `METADATA.json`에서 관리합니다.

## 보조 자료

- `docs/HTTPSexclusions-reference.txt`: 43개 HTTPS 제외 도메인의 읽기 전용 참조 목록.
  이것은 **네이티브 가져오기 파일이 아닙니다**.
- `METADATA.json`: 각 파일의 형식·규칙 수·SHA-256·원본 보존 검증값.
- `archive/old/`: 원본 ZIP의 이전 버전 파일들을 바이트 단위로 보존한 기록.

## 검증 범위

세 개의 필터에서 **주석/메타데이터를 제외한 모든 유효 규칙**이 원본과 같은지,
HTTPS 네이티브 파일의 JSON과 `Payload`가 유지되는지, HTTPS·DNS 도메인 순서가 43개
동일한지 검사했습니다. **실제 AdGuard UI에서 가져오기 성공까지 실행 검증하지는 않았습니다.**

## 공식 문서

- [AdGuard 필터 문법](https://adguard.com/kb/general/ad-filtering/create-own-filters/)
- [AdGuard HTTPS 예외 문법](https://github.com/AdguardTeam/HttpsExclusions)
- [AdGuard DNS 필터 문법](https://adguard-dns.io/kb/general/dns-filtering-syntax/)
