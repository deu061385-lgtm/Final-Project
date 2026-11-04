# 배포 검증 기록

## 프로덕션 확인

- **확인 시각:** 2026-11-04 13:32:24 +09:00
- **프로덕션 URL:** https://runner-ai-coach.vercel.app
- **Vercel 배포 ID:** `dpl_AcvDYVYxtrXpPstMv2JzDjxkQyk7`
- **Vercel 배포 상태:** `Ready`
- **배포 URL:** https://runner-ai-coach-qvxq3fdbs-yeonseop.vercel.app
- **Git 커밋:** `b0ca1f4` (`chore: clarify AI-generated coaching notice`)

## HTTP 가용성 스모크 테스트

PowerShell에서 실행:

```powershell
curl.exe -sS -o NUL -w "HTTP %{http_code}; final URL %{url_effective}; content-type %{content_type}\n" https://runner-ai-coach.vercel.app
```

확인 결과:

```text
HTTP 200; final URL https://runner-ai-coach.vercel.app/; content-type text/html; charset=utf-8
```

Vercel 배포 확인:

```powershell
npx.cmd exec --yes -- vercel inspect https://runner-ai-coach.vercel.app
```

확인 결과: 배포 ID `dpl_AcvDYVYxtrXpPstMv2JzDjxkQyk7`가 `Ready` 상태이며 `https://runner-ai-coach.vercel.app` 프로덕션 별칭에 연결되어 있습니다.

## 로그인 코치 통합 스모크 테스트

- **확인 날짜:** 2026-11-04
- **실행 환경:** 프로덕션 사이트, 로그인 세션, 사용자 동의 체크 후 실행
- **질문 시나리오:** 최근 러닝 기록을 참고한 회복 방법과 운동 후 에너지·탄수화물·단백질·수분 가이드 요청
- **확인 결과:** 코치 응답이 생성되고 최근 운동 기록 조회 안내가 표시됨. 식단 참고 항목과 Better Health Channel 및 Mayo Clinic 출처 링크가 표시됨. 요청 화면에 오류가 나타나지 않음.
- **개인정보:** 계정 이메일이나 개인 기록의 구체적인 값은 이 문서에 기록하지 않음
- **화면 증거:** [RAG 코치 응답과 출처](evidence/rag-coach-response.png), [전체 코치 화면과 AI 고지](evidence/ai-disclosure.png)

## 검증 범위와 한계

확인한 항목은 공개 페이지의 HTTP 200 응답, Vercel 프로덕션 `Ready` 상태, 로그인된 사용자 1명의 수동 코치 통합 테스트입니다. RAG는 큐레이션 자료의 키워드 검색 방식이며 실시간 웹 검색은 아닙니다. 이 테스트는 외부 사용자 최소 5명 테스트를 대체하지 않으며, 사용자 테스트 및 피드백 반영 결과는 별도로 수집·기록해야 합니다.
