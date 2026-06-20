# 설치 매뉴얼 — Claude Code + MCP + 스킬 받아가기

이 문서는 강의에서 시연한 통합 워크플로우를 **여러분 컴퓨터에서 직접** 쓰기 위한 설치
안내입니다. 비개발자도 따라 할 수 있게 구성했습니다. 순서대로만 진행하세요.

> 결과적으로 여러분은 ① Claude Code를 IDE에 연결하고, ② 이 GitHub 스킬을 내려받고,
> ③ Semrush·Reddit 같은 도구를 MCP로 연결해, 강의의 리서치→전략→콘텐츠 과정을
> 명령어 하나로 실행하게 됩니다.

---

## 0. 미리 준비할 것

| 항목 | 용도 | 비고 |
|---|---|---|
| **Google Antigravity IDE** | Claude Code를 띄울 작업 공간 | 무료 |
| **Claude Code** | AI 에이전트(터미널/IDE에서 실행) | 구독 필요 |
| **Node.js** | 일부 MCP 실행 | nodejs.org에서 LTS 설치 |
| **Semrush 계정 (Pro 이상)** | 키워드·경쟁사 정량 분석 | MCP 기본 포함 |
| **Apify 계정 (무료)** | 레딧 정성 데이터 수집 | 월 $5 크레딧, 카드 불필요 |

> macOS 기준으로 설명합니다. Homebrew(brew)가 있으면 일부 단계가 더 쉽습니다.

---

## STEP 1 — Antigravity에 Claude Code 연동

1. Google Antigravity IDE를 설치하고 실행합니다.
2. 내장 **터미널**을 엽니다. (보기/View → Terminal)
3. 터미널에서 Claude Code를 설치하고 로그인합니다.
   ```
   npm install -g @anthropic-ai/claude-code
   claude            # 최초 실행 시 안내에 따라 로그인
   ```
4. 작업할 폴더를 하나 만들고 그 폴더에서 `claude`를 실행합니다.
   ```
   mkdir ~/branding-workspace && cd ~/branding-workspace
   claude
   ```

---

## STEP 2 — GitHub에서 스킬 내려받기

> ⚠️ **핵심:** Claude Code는 스킬을 **`.claude/skills/`** 폴더에서 자동으로 찾습니다.
> 그냥 `skills/`에 두면 인식되지 않으니, 반드시 `.claude/skills/` 위치로 넣어주세요.

**방법 A (가장 쉬움 — Claude Code에게 맡기기) ⭐**
Claude Code를 실행한 상태에서, 아래 한 문장을 그대로 입력하세요. (URL만 본인 레포 주소로)
```
https://github.com/paulsign-lab/global-ai-branding-skills 이 레포를 클론하고,
안의 skills 폴더를 .claude/skills/ 에 설치해줘.
그리고 mcp.json.template 을 .mcp.json 으로 복사해줘.
```
그러면 Claude Code가 `git clone`과 복사를 알아서 실행합니다.
설치 후 스킬이 목록에 뜨도록 **Claude Code를 한 번 재시작**하세요. 이게 가장 간단합니다.

**방법 B (다운로드 — 직접 복사):**
1. 이 저장소 페이지에서 **Code → Download ZIP**.
2. 압축을 풀고, `skills/` **안의 스킬 폴더들**을 작업 폴더의 **`.claude/skills/`** 아래로 복사합니다.
   ```
   mkdir -p ~/branding-workspace/.claude/skills
   cp -R 내려받은폴더/skills/* ~/branding-workspace/.claude/skills/
   ```
   - 위처럼 작업 폴더 안의 `.claude/skills/`에 두면 **그 폴더에서만** 스킬이 작동합니다.
   - 내 컴퓨터의 **모든 폴더에서** 항상 쓰고 싶으면 홈 폴더의 `~/.claude/skills/`로 복사하세요(전역 적용).

**방법 C (git 직접):**
```
cd ~/branding-workspace
git clone https://github.com/paulsign-lab/global-ai-branding-skills.git
mkdir -p .claude/skills
cp -R global-ai-branding-skills/skills/* .claude/skills/
cp global-ai-branding-skills/mcp.json.template ./.mcp.json
```

설치 후 폴더 구조가 이렇게 되면 됩니다:
```
~/branding-workspace/
  .claude/
    skills/
      competitor-quant/SKILL.md
      reddit-voc/SKILL.md
      ...
  .mcp.json            ← mcp.json.template 을 이 이름으로
```

설치가 끝나면 Claude Code에서 `/help` 또는 스킬 목록에서 8개 스킬이 보이는지 확인하세요.

---

## STEP 3 — MCP 도구 연결

### 3-1. Semrush (OAuth — 키 입력 없이 로그인)
작업 폴더에서:
```
claude mcp add semrush https://mcp.semrush.com/v1/mcp -t http -s project
```
Claude Code에서 `/mcp` 입력 → **semrush** 선택 → **Authenticate** → 브라우저로 본인
Semrush 계정 로그인. 끝.

### 3-2. Apify Reddit (무료 토큰)
1. apify.com 무료 가입 → **Console → Settings → API & Integrations**에서 API 토큰 복사
   (`apify_api_...`).
2. 토큰을 환경변수로 등록(비밀값을 코드에 직접 넣지 않기 위함):
   ```
   echo 'export APIFY_TOKEN=여기에_본인_토큰' >> ~/.zshrc
   source ~/.zshrc
   ```
3. MCP 추가:
   ```
   claude mcp add apify https://mcp.apify.com -t http -s project --header "Authorization: Bearer ${APIFY_TOKEN}"
   ```

### 3-3. 연결 확인
Claude Code에서 `/mcp` 입력 → **semrush**, **apify**가 모두 `connected`이면 성공입니다.

> 위 두 줄을 직접 입력하는 대신, 저장소의 **`mcp.json.template`** 파일을 작업 폴더에 두고
> 파일명을 **`.mcp.json`**으로 바꾸면 설정이 미리 들어가 있습니다.
> (비밀값은 `${APIFY_TOKEN}` 환경변수로만 참조하므로 안전하게 공유됩니다.)

---

## STEP 4 — 스킬 사용하기

작업 폴더에서 `claude`를 실행한 뒤, 스킬은 **세 가지 방법**으로 부를 수 있습니다.

1. **자동 (권장)** — 그냥 하고 싶은 일을 말하면 Claude Code가 맞는 스킬을 알아서 실행합니다.
   ```
   cosrx.com과 beautyofjoseon.com의 키워드 갭을 분석해줘.      → competitor-quant 자동 실행
   r/AsianBeauty에서 COSRX 페인포인트를 분석해줘.              → reddit-voc 자동 실행
   ```
2. **슬래시 명령** — 콕 집어 부르기: `/reddit-voc`, `/brand-mission` …
3. **이름 지정** — "reddit-voc 스킬로 ~ 해줘"

권장 순서는 `skills/README.md`의 흐름도(정량→정성→전략→콘텐츠)와 같습니다.
**앞 스킬의 결과를 다음 스킬 입력으로 이어주면** 가장 좋은 결과가 나옵니다.

---

## 트러블슈팅

**`Executable not found in $PATH: "uvx"` (일부 MCP)**
파이썬 도구 `uv`가 없을 때 발생합니다.
```
brew install uv          # 또는: curl -LsSf https://astral.sh/uv/install.sh | sh
```
설치 후 **IDE를 완전히 종료했다 재실행**하세요. 그래도 안 되면 `which uvx`로 절대경로를
확인해, MCP 설정의 `uvx`를 그 절대경로(예: `/opt/homebrew/bin/uvx`)로 바꿉니다.

**`/mcp`에서 `Needs Auth` 표시**
해당 MCP 카드에서 Authenticate를 눌러 로그인하세요(Semrush 등 OAuth 방식).

**MCP가 데이터를 안 가져옴**
해당 도구의 유료/무료 한도(크레딧·API 유닛)를 확인하세요. Apify는 무료 $5 크레딧,
Semrush는 플랜의 API 유닛을 사용합니다.

---

## ⚠️ 보안 주의
- API 토큰·비밀번호는 **절대 GitHub에 그대로 올리지 마세요.** 이 저장소의 `.mcp.json`은
  토큰을 `${APIFY_TOKEN}` 환경변수로만 참조합니다.
- `.env` 등 비밀 파일은 `.gitignore`에 포함되어 있습니다.
