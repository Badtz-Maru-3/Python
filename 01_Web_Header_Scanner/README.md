# 🛡️ Web Header Security Checker

> **제작 목적**  
> 모의해킹 진단 시 누락되기 쉬운 HTTP 보안 헤더 설정(CSP, HSTS 등)을 자동으로 점검하여 **인적 오류(Human Error)를 줄이기 위해** 제작한 학습용 도구입니다.

---

## 📌 개요

웹 애플리케이션 모의해킹을 수행할 때, HTTP 응답 헤더의 보안 설정 누락은 체크리스트가 길어질수록 놓치기 쉬운 항목 중 하나입니다.  
이 도구는 수동 점검 과정을 보조하는 목적으로 제작되었으며, 주요 보안 헤더의 존재 여부와 설정값을 자동으로 분석합니다.

---

## 🔍 점검 항목

| 헤더 | 설명 |
|---|---|
| `Content-Security-Policy (CSP)` | XSS 및 데이터 인젝션 공격 방지를 위한 콘텐츠 로드 정책 |
| `Strict-Transport-Security (HSTS)` | HTTPS 강제 전송 설정, 다운그레이드 공격 방지 |
| `X-Content-Type-Options` | MIME 타입 스니핑 방지 (`nosniff`) |
| `X-Frame-Options` | 클릭재킹(Clickjacking) 방지 |
| `X-XSS-Protection` | 구형 브라우저 XSS 필터 활성화 여부 |
| `Referrer-Policy` | 리퍼러 정보 노출 범위 제어 |
| `Permissions-Policy` | 브라우저 기능(카메라, 마이크 등) 접근 제어 |

---

## 🚀 사용법

```bash
python header_checker.py -u https://example.com
```

```bash
# 복수 URL 일괄 점검
python header_checker.py -f urls.txt

# 결과를 JSON으로 저장
python header_checker.py -u https://example.com -o result.json
```

---

## 📊 결과 예시

```
[+] Target: https://example.com
======================================
[✓] Strict-Transport-Security : max-age=31536000; includeSubDomains
[✗] Content-Security-Policy   : 누락
[✗] X-Frame-Options           : 누락
[✓] X-Content-Type-Options    : nosniff
[!] X-XSS-Protection          : 설정값 검토 필요 (1; mode=block)
======================================
[결과] 5개 항목 중 2개 누락, 1개 검토 필요
```

---

## 💡 학습 포인트

- HTTP 응답 헤더가 실제 보안에 미치는 영향 이해
- 각 헤더의 올바른 설정값과 잘못된 설정값의 차이 분석
- 자동화 스크립트를 통한 반복 점검 작업 효율화
- OWASP Secure Headers Project 기준 적용 방법 학습

---

## ⚠️ 주의사항

> 이 도구는 **학습 및 보안 진단 역량 향상을 위한 목적**으로 제작되었습니다.  
> 반드시 **본인 소유 또는 명시적 허가를 받은 시스템**에 대해서만 사용하십시오.  
> 무단 사용 시 관련 법령(정보통신망법 등)에 따른 처벌을 받을 수 있습니다.

---

## 📚 참고 자료

- [OWASP Secure Headers Project](https://owasp.org/www-project-secure-headers/)
- [MDN Web Docs - HTTP Headers](https://developer.mozilla.org/ko/docs/Web/HTTP/Headers)
- [Mozilla Observatory](https://observatory.mozilla.org/)
