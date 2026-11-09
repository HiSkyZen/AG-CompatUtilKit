# HiSkyZen's Compat 'n' UtilKit

Version: `2026.1109.1`  
Updated: `2026-11-09T14:26:00+00:00`  
Homepage: https://github.com/HiSkyZen/AG-CompatUtilKit  
License: https://github.com/HiSkyZen/AG-CompatUtilKit/blob/master/LICENSE

## 무엇을 어디에 적용해야 하나

| 파일 | 종류 | 적용 위치 |
|---|---|---|---|
| `mainfilter.txt` | AdGuard 일반 네트워크 필터 | 광고 차단 → 사용자 지정 필터로 TXT 가져오기 |
| `fl.txt` | 별도 선택형 웹사이트 필터 | 지원되는 환경의 신뢰 가능한 사용자 지정 필터 (Windows/Android **사용 금지**) |
| `HTTPSexclusions.txt` | HTTPS 검사 예외 목록 | 앱 설정 → 네트워크 설정 → HTTPS 필터링 → 제외 목록 |
| `dnsfilter.txt` | **DNS 필터**: 차단 예외 (allowlist) | DNS 보호 → DNS 필터 → 필터 가져오기 |
| `DNSexclusions.txt` | **DNS 서버 우회**: 시스템 DNS로 전환 | 앱 설정 → 고급 설정 → DNS 제외 목록 |

## 호환성 및 위험

- `mainfilter.txt`의 Microsoft 예외 범위는 넓습니다. DNS/HTTP 차단이나 추적 방지 규칙을 함께 우회해 텔레메트리·광고 요청도 허용할 수 있습니다. 필요할 때만 사용하세요.
- 메인 필터의 허용 규칙, 사이트별 수정 규칙 및 선택형 필터의 원본 규칙 본문은 수정하지 않았습니다.
- DNS/HTTPS 도메인 43개는 중복 제거 없이 원본 순서대로 유지했습니다. 원본의 하위 도메인 예외를 그대로 보존하기 위해서입니다.
- 원격 DNS 제공자나 Windows hosts, 브라우저의 자체 보안 정책 등 AdGuard 외부 차단은 이 목록만으로 해제할 수 없습니다.

## 공식 참고 문서

- AdGuard 필터 규칙: https://adguard.com/kb/general/ad-filtering/create-own-filters/
- AdGuard DNS 필터 규칙: https://adguard-dns.io/kb/general/dns-filtering-syntax/
- HTTPS 예외 목록 문법(`#` 주석): https://github.com/AdguardTeam/HttpsExclusions
- AdGuard for Windows 고급 설정 — DNS 제외: https://adguard.com/kb/adguard-for-windows/settings/app-settings/advanced-settings/
