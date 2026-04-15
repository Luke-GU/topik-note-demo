# TOPIK Note — AI Solopreneur Submission

평가 기준: https://udpb.github.io/ai-solopreneur/criteria.html

**Live URL**: https://luke-gu.github.io/topik-note-demo/
**Repo**: https://github.com/Luke-GU/topik-note-demo
**Creator**: GEONWOO JUNG · codelue01@gmail.com

## 3 Deliverables

| # | Deliverable | File(s) | Notes |
| - | ----------- | ------- | ----- |
| 1 | Landing Page (EN primary, KO sync) | `index.html`, `index.ko.html`, `styles.css`, `screenshots/*.png` | Persona + pain + 3 features (1:1) + before/after + testimonial + CTA. 자체 포함. |
| 2 | 1-Page PRD | `PRD.md` | User flow / screen list / MVP scope / core assumptions & validation. Canonical copy가 Section 0. |
| 3 | MVP URL | https://luke-gu.github.io/topik-note-demo/ + App Store / Play Store | 랜딩에 두 경로 CTA 노출. 무설치 웹 데모는 backlog (PRD §3 "Out"). |

## Local preview

```bash
open index.html
open index.ko.html
```

GitHub/VS Code에서 `PRD.md`는 마크다운 프리뷰로 바로 확인.

## Differentiation (핵심 차별점)

> **모든 단어와 뜻풀이를 한국인 원어민이 직접 검수**하여 TOPIK 응시에 최적화. 외국인 제작진이 만든 기존 TOPIK 앱들에서 흔한 오기입·잘못된 정답·어색한 번역이 없음.

이 메시지가 landing(EN/KO) hero · feature 3 · PRD §0 canonical copy 3곳에서 동일한 톤으로 반복됨.

## Demo lead form

CTA가 App Store / Play Store 다운로드 → **데모 신청 이메일 폼**으로 변경됨. 양 페이지 hero + final CTA 두 위치에 동일 폼 (Formsubmit 사용, 백엔드 불필요).

**최초 1회 활성화 필요**:
1. 라이브 사이트(https://luke-gu.github.io/topik-note-demo/)에서 폼에 본인 이메일을 한 번 제출
2. `codelue01@gmail.com` 받은편지함에서 **Formsubmit confirmation 메일** 클릭 (스팸함 확인)
3. 활성화 완료 후 모든 데모 신청이 codelue01@gmail.com으로 자동 배달됨

폼 메타데이터:
- `_subject` — 메일 제목 (페이지/위치별로 구분: EN hero / EN final / KO hero / KO final)
- `source` — 분석용 hidden field (어느 폼에서 들어온 lead인지)
- `_template=table` — 메일 본문이 테이블 형태로 정리됨
- `_captcha=false` — 캡차 비활성 (스팸 시 켜기)
- `_next` — 제출 후 `#thanks` 앵커로 리디렉트

## Before submitting (TODO)

- [ ] **Testimonial 실제 인용문** — `index.html`·`index.ko.html`의 testimonial 섹션 placeholder를 베타 테스터 인용문(최소 1개)로 교체.
- [ ] **Formsubmit 활성화** (위 절차).
- [ ] (선택) 모바일 뷰포트 반응형 확인 (DevTools iPhone 14 프리셋).

## Consistency matrix

| 항목 | Landing (EN/KO) | PRD |
| --- | --- | --- |
| Persona | "Who this is for" 섹션 | §0 Canonical, §4 Assumption 1 |
| 3 core features | "Three things TOPIK Note does" | §0 · §3 In |
| Positioning 1-liner | Hero subhead | §0 |
| Korean-native verification 차별점 | Hero · Feature 3 | §0 feature 3 · §4 Assumption 1 |

## Deploying updates

```bash
cd ~/Documents/topik-note-submission
git add -A
git commit -m "<message>"
git push
```

GitHub Pages 자동 재빌드 (~1분).
