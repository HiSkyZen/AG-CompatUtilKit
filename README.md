# HiSkyZen's Compat'n'UtilKit — AdGuard Ready

Version: `2026.1109.0`  
Updated: `2026-11-09T14:02:00+00:00`  
Homepage: https://github.com/HiSkyZen/CompatUtilKit  
License: https://github.com/HiSkyZen/CompatUtilKit/blob/master/LICENSE

## 무엇을 어디에 적용해야 하나

| 파일 | 종류 | 적용 위치 | 메타데이터 |
|---|---|---|---|
| `mainfilter.txt` | AdGuard 일반 네트워크 필터 | 광고 차단 → 사용자 지정 필터로 TXT 가져오기 | `! Title/Description/Version/TimeUpdated/Expires/Homepage/License` |
| `fl.txt` | 별도 선택형 웹사이트 필터 | 지원되는 환경의 신뢰 가능한 사용자 지정 필터 (Windows/Android **사용 금지**) | 위와 동일 |
| `HTTPSexclusions.txt` | HTTPS 검사 예외 목록 | 앱 설정 → 네트워크 설정 → HTTPS 필터링 → 제외 목록 | `#` 주석으로 같은 7개 항목. 예외 입력란에서는 구독 필터 메타데이터처럼 UI에 표시되지 않음 |
| `dnsfilter.txt` | **DNS 필터**: 차단 예외 (allowlist) | DNS 보호 → DNS 필터 → 필터 가져오기 | `!` 메타데이터 7개 항목 |
| `DNSexclusions.txt` | **DNS 서버 우회**: 시스템 DNS로 전환 | 앱 설정 → 고급 설정 → DNS 제외 목록 | *파일 내부 메타데이터 없음* (순수 도메인 형식). `METADATA.json`에서 관리 |

**주의: `dnsfilter.txt`의 의미가 원본과 다릅니다.** 원본 `dnsfilter.txt`에는 도메인만 적혀 있어 DNS **필터**로 불러오면 도메인이 차단될 수 있었습니다. 따라서 여기서는 AdGuard DNS 예외 규칙 `@@||도메인^`으로 변환했습니다. 이 파일은 앱의 DNS 차단 규칙을 우회하지만, 시스템 DNS 리졸버로 전환하지 않습니다. 원본과 같은 DNS 서버 우회가 필요하면 `DNSexclusions.txt`만 DNS 제외 목록에 적용하세요. 두 기능은 대체 관계가 아닙니다.

## 메타데이터 설계

- AdGuard 일반/DNS 필터에는 `!` 주석 메타데이터를 사용합니다. `! Title`, `! Description`, `! Version`, `! TimeUpdated`, `! Expires`, `! Homepage`, `! License`를 동일한 순서로 넣었습니다.
- HTTPS 제외 목록은 AdGuard 공식 규격이 `#`을 주석으로 허용하므로 동일한 필드를 `#`으로 기록했습니다. 이것은 **설명용 주석**이며 필터 구독 메타데이터로 해석되지 않습니다.
- DNS 제외 목록은 일반 DNS 필터와 다른 **설정값 목록**이며, 주석이 안전하게 무시된다는 공식 보장이 없어 도메인만 두었습니다. 해당 파일의 일관된 메타데이터는 `METADATA.json`에 따로 있습니다.
- `Expires`는 구독 필터가 URL에서 자동 갱신될 때의 제안 값입니다. 로컬 파일을 직접 가져온다고 자동 갱신되는 것은 아닙니다.

## 호환성 및 위험

- `fl.txt`의 원본에는 **AdGuard for Windows / Android에서 사용하지 말라는 경고**가 있습니다. 본 패키지는 이를 유지하며 메인 필터에 병합하지 않았습니다. 일부 JavaScript/scriptlet 규칙에는 신뢰할 수 있는 필터 권한이 필요합니다.
- `mainfilter.txt`의 Microsoft 예외 범위는 넓습니다. DNS/HTTP 차단이나 추적 방지 규칙을 함께 우회해 텔레메트리·광고 요청도 허용할 수 있습니다. 필요할 때만 사용하세요.
- 메인 필터의 허용 규칙, 사이트별 수정 규칙 및 선택형 필터의 원본 규칙 본문은 수정하지 않았습니다.
- DNS/HTTPS 도메인 43개는 중복 제거 없이 원본 순서대로 유지했습니다. 원본의 하위 도메인 예외를 그대로 보존하기 위해서입니다.
- 원격 DNS 제공자나 Windows hosts, 브라우저의 자체 보안 정책 등 AdGuard 외부 차단은 이 목록만으로 해제할 수 없습니다.

## 공식 참고 문서

- AdGuard 필터 규칙: https://adguard.com/kb/general/ad-filtering/create-own-filters/
- AdGuard DNS 필터 규칙: https://adguard-dns.io/kb/general/dns-filtering-syntax/
- HTTPS 예외 목록 문법(`#` 주석): https://github.com/AdguardTeam/HttpsExclusions
- AdGuard for Windows 고급 설정 — DNS 제외: https://adguard.com/kb/adguard-for-windows/settings/app-settings/advanced-settings/
