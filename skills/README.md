# 글로벌 AI 브랜딩 — Claude Code 스킬 패키지

「AI 시대에 살아남는 디지털 브랜딩 실무」 강의의 전 과정을 **Claude Code 스킬**로 박제한
패키지입니다. 강의에서는 각 작업을 *나눠서* 보여드리지만, 이 스킬들을 쓰면 **Claude Code +
MCP 하나에서 통합 리서치 → 전략 설계 → 콘텐츠 생성**까지 흐르게 됩니다.

> 워크플로우를 직접 만들어 각 단계를 편집하셔도 좋고, 이 스킬로 편하게 결과물을 받아보셔도 됩니다.
> **AI는 반복 작업을 실행하고, 사람은 본질적 판단과 전략 설계에 집중합니다.**

## 전체 흐름 (데이터 핸드오프 체인)

```
[정량]  competitor-quant ─(페인포인트 키워드+검색량)─┐
        (Semrush MCP)                                │
                                                     ▼
[정성]  reddit-voc ─(페르소나 원형 + FGI 질문지)→ persona-fgi ─(FGI 결과)─┐
        (Apify Reddit MCP)                          (AskRally)            │
                                                                          ▼
[전략]  brand-mission ──→ brand-positioning ──→ brand-story ──→ brand-voice
        (미션·비전)        (포지셔닝·2x2맵)      (스토리·메시지)   (보이스 엔진)
                                                                          │
[콘텐츠] seo-content ◀───(기회 키워드 / 브랜드 보이스)────────────────────┘
        (Semrush MCP, Opal 워크플로우 박제)
```

핵심: **앞 스킬의 출력이 뒤 스킬의 입력**이 됩니다. 그래서 미션·포지셔닝이 직감이 아니라,
앞에서 MCP로 실제 수집·검증한 데이터 위에 섭니다.

## 스킬 목록 (강의 Part 매핑)

| 스킬 | 강의 | 하는 일 | 필요 MCP |
|---|---|---|---|
| `competitor-quant` | Part 3 | 경쟁사 키워드 갭·페인포인트 키워드(검색량) | Semrush |
| `reddit-voc` | Part 3 | 레딧 정성 5종 + 페르소나 원형 + FGI 질문지 | Apify Reddit |
| `persona-fgi` | Part 3 | 가상 FGI 페르소나·4축 20문항 설계 | (AskRally) |
| `brand-mission` | Part 4 | 미션·비전 후보 3개 + 검증 | — |
| `brand-positioning` | Part 4 | 포지셔닝 스테이트먼트 + 2x2 맵 | — |
| `brand-story` | Part 4 | 오리진 스토리 3버전 + 메시지 체계 + 검증 | — |
| `brand-voice` | Part 4 | 브랜드 일관 콘텐츠 엔진(예전 Gemini Gems 역할) | — |
| `seo-content` | Part 5 | SEO·GEO 블로그 콘텐츠 자동 생성 | Semrush |

## 사전 준비 (MCP 연결)
- **Semrush MCP** — `competitor-quant`, `seo-content`용 (Pro 플랜이면 충분)
- **Apify Reddit MCP** — `reddit-voc`용 (무료 $5 크레딧)
- 연결 명령어·설치 매뉴얼은 별도 설치 가이드 참조.

## 사용법
Claude Code에서 해당 스킬을 호출하면 SKILL.md의 절차대로 진행됩니다. 권장 순서는 위
흐름도와 같습니다(정량→정성→전략→콘텐츠). 각 스킬은 단독으로도 쓸 수 있지만, 체인으로
이어서 쓸 때 앞 단계 산출물을 입력하면 가장 좋은 결과가 나옵니다.

---
*최종 판단은 언제나 사람의 몫입니다. 이 스킬들은 직감을 데이터로, 데이터를 전략으로 바꾸는
과정을 10배 빠르게 해주는 도구입니다.*
