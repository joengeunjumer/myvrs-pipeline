# MYVRS Pipeline

**Claude · Gemini · Kie.ai(Nano Banana 2 / Seedance 2.0)를 오케스트레이션해 멀티프레임 XR 댄스 퍼포먼스 영상을 자동 생성하는 Next.js 풀스택 애플리케이션**입니다. Scale Virtual 인턴십에서 기획부터 프로덕션 배포(Vercel)까지 바이브 코딩(Claude Code)으로 구축했습니다.

> A production Next.js app that orchestrates Claude (prompt enhancement & scenario splitting), Gemini (scene planning), and Kie.ai — Nano Banana 2 for keyframes, Seedance 2.0 for video — to generate procedurally-consistent multi-frame XR dance videos, with Supabase storage and a Google Drive/Sheets/Gmail approval loop.

> 🔒 **전체 소스 코드는 private 저장소로 관리합니다.** 열람이 필요하시면 연락 주세요 — joengeunjumer@gmail.com

## 파이프라인 아키텍처

![Pipeline Architecture](assets/pipeline-architecture.png)

```
사용자 입력 (컨셉 / 레퍼런스 이미지)
  └─→ ① Claude — 프롬프트 강화 + 시나리오 분할 (vision)
        └─→ ② Gemini — 씬 플래닝
              └─→ ③ Kie.ai — Nano Banana 2 키프레임 → Seedance 2.0 영상 생성
                    └─→ ④ FFmpeg(브라우저) — 클립 결합 / 트랜스코딩
                          └─→ ⑤ Supabase 저장 + Google Drive 업로드 + Gmail 승인 요청
```

### 자동화 워크플로우

![Automation Diagram](assets/automation-diagram.png)

## 기술 스택

| 영역 | 기술 |
|---|---|
| Frontend / Backend | Next.js 16 (App Router) · React 19 · TypeScript · Tailwind CSS · Radix UI · React Flow |
| AI | Claude API (vision·구조화 출력) · Gemini API · Kie.ai (Nano Banana 2, Seedance 2.0) |
| 인프라 | Supabase (PostgreSQL·realtime) · Google Drive/Sheets/Gmail API · FFmpeg (브라우저 트랜스코딩) · Vercel |

## 핵심 설계 포인트

- **시스템 프롬프트의 버전 관리** — 프롬프트를 코드처럼 취급: 버전별 스냅샷(base v1.0–v1.1, theme v1.0–v1.1), 체인지로그, 롤백 절차, git 태그 기반 재현성
- **가변 시나리오 구조** — 시나리오 카드 2~5장 가변, 클립 길이 모드(8s/16s) 지원
- **브라우저 내 영상 처리** — 서버 비용 없이 FFmpeg WASM으로 클립 결합·트랜스코딩 (ProRes OOM 이슈 해결 포함)
- **이해관계자 승인 루프** — 생성 결과를 Drive에 정리하고 Gmail로 승인 요청을 자동 발송

## 🎬 데모

<!-- 데모 영상: GitHub 웹에서 이 README를 편집하며 영상 파일을 드래그하면 자동 업로드됩니다 -->
데모 영상 추가 예정

## 바이브 코딩 프로세스

전 과정을 Claude Code와의 페어 프로그래밍으로 개발했습니다. private 저장소의 커밋 히스토리(32 커밋)에 기능 단위 개발 과정 — `feat: B 모드 (8s/16s) + 시나리오 카드 가변 수 지원`, `fix: canvas compositor OOM on ProRes` — 이 그대로 남아 있습니다.
