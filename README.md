# TOPIK Note — AI Solopreneur Submission

평가 기준: https://udpb.github.io/ai-solopreneur/criteria.html

## 3 Deliverables

| # | Deliverable | File(s) | Notes |
| - | ----------- | ------- | ----- |
| 1 | Landing Page (EN primary, KO sync) | `landing/index.html`, `landing/index.ko.html`, `landing/styles.css`, `landing/screenshots/*.png` | Persona + pain + 3 features (1:1) + before/after + testimonial + CTA. 자체 포함 (외부 의존성 없음). |
| 2 | 1-Page PRD | `PRD.md` | User flow / screen list / MVP scope / core assumptions & validation. Canonical copy가 Section 0. |
| 3 | MVP URL | https://topik-note.com + App Store / Play Store | 랜딩이 두 경로 CTA 모두 노출. 무설치 웹 데모는 backlog (PRD §3 "Out"). |

## Local preview

```bash
open landing/index.html
open landing/index.ko.html
```

GitHub/VS Code에서 `PRD.md`는 마크다운 프리뷰로 바로 확인 가능.

## Before submitting (TODO)

- [ ] `landing/index.html`과 `index.ko.html`의 **Testimonial 섹션**에 실제 베타 테스터 / App Store 리뷰 인용문 **최소 1개** 삽입. 현재 샘플 text는 placeholder 주석 위치에 있음.
- [ ] App Store / Google Play 최종 URL 확정 후 `index.html`과 `index.ko.html`의 `href`를 실제 URL로 치환 (현재 플레이스홀더 URL). grep으로 확인: `grep -n "apps.apple.com\|play.google.com" landing/*.html`.
- [ ] PRD §5 MVP URL 섹션의 iOS/Android 라인에 최종 URL 기입.
- [ ] (선택) 로컬 브라우저 모바일 뷰포트로 반응형 확인 (DevTools iPhone 14 프리셋).

## Consistency matrix

세 산출물이 **같은 persona / 같은 3 feature / 같은 positioning**을 공유함을 보장:

| 항목 | Landing (EN/KO) | PRD | App Store metadata |
| --- | --- | --- | --- |
| Persona | "Who this is for" | §0 Canonical, §4 Assumption 1 | (동일 타깃 — 영문/한국어/일본어/베트남어/중국어 5 언어 지원) |
| 3 core features | "Three things TOPIK Note does" | §0 · §3 In | `store-metadata/en.md` description 본문 |
| Positioning 1-liner | Hero subhead | §0 | Promo text |

## Source material

- 원 성장 전략 문서: `/Users/geonwoo/Documents/kil/topik-note-growth-strategy.md`
- 앱 스토어 카피: `/Users/geonwoo/Documents/kil/apps/mobile/store-metadata/en.md`
- 스크린샷 원본: `/Users/geonwoo/Documents/kil/apps/mobile/store-screenshots/` (이 폴더 `landing/screenshots/`로 복사됨)
