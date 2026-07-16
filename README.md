# 🐾 ClaudePet

화면 위를 떠다니는 클로드 도트 마스코트 — macOS 데스크톱 펫입니다.
Claude Code와 연동되어 실제 작업 상태에 반응합니다: 일하면 같이 분주해지고, 끝나면 축하해주고, Claude가 부르면 달려와 알려줍니다.

*(English below)*

## 기능

- 화면을 천천히 떠다니고, 눈동자가 커서를 따라옵니다
- **Claude Code 연동** — 작업 중 표시, 완료 시 "끝! 🎉", Claude가 부르면 달려와서 ❗
- **더블클릭** — 구독 사용량(주간/세션)을 말풍선으로
- 클릭하면 폴짝 + 하트, 던지면 관성 비행, 마우스가 오래 멈추면 콕콕 찌르러 옵니다
- 이름·대사 편집, 크기 조절(기본/2배/3배), 효과음, 로그인 시 자동 실행, 한국어/영어
- 새 버전이 나오면 펫이 직접 알려줍니다
- **클립보드 보안 감시** — API 키·토큰을 복사하면 조심하라고 알려줍니다 (검사는 전부 로컬에서만, 저장·전송 없음)
- **메세지 자동 생성** — 메뉴에서 누르면 Claude가 펫의 대사 4종을 전부 새로 지어줍니다 (Claude Code CLI 사용, 별도 API 키 불필요)

## 설치

1. [최신 릴리스](https://github.com/jihoon85/claudepet/releases/latest)에서 `ClaudePet-x.x.dmg` 다운로드
2. dmg를 열고 **ClaudePet을 Applications 폴더로 드래그**
3. 미서명 앱이라 첫 실행은 **우클릭 → 열기**
4. 펫이 Claude Code 연동을 물어보면 **연동하기** 클릭 — 끝!

연동을 나중에 하려면 메뉴바 🐾 → **Claude Code 연동 설정**. 종료·설정도 모두 메뉴바 🐾에서.

---

# 🐾 ClaudePet (English)

A tiny pixel-art Claude mascot that floats around your macOS screen.
It syncs with Claude Code and reacts to what's actually happening: gets busy when Claude works, celebrates when a task finishes, and runs over when Claude needs you.

## Features

- Drifts around your screen, pupils follow your cursor
- **Claude Code sync** — shows working state, cheers "Done! 🎉", dashes over with ❗ when Claude needs you
- **Double-click** — subscription usage (weekly/session) in a speech bubble
- Click for hops & hearts, throw it for inertial flight, and it pokes you if your mouse sits idle
- Rename, edit its phrases, resize (1×/2×/3×), toggle sounds, launch at login, Korean/English
- Tells you itself when a new version is out
- **Clipboard secret guard** — warns you when you copy an API key or token (all checks run locally; nothing is stored or sent)
- **Auto-generated chatter** — one click and Claude rewrites all of your pet's lines (via the Claude Code CLI, no API key needed)

## Install

1. Download `ClaudePet-x.x.dmg` from the [latest release](https://github.com/jihoon85/claudepet/releases/latest)
2. Open the dmg and **drag ClaudePet into the Applications folder**
3. Unsigned app — **right-click → Open** on first launch
4. When the pet offers Claude Code sync, click **Set Up** — done!

To set up later: menubar 🐾 → **Set Up Claude Code Sync**. Quit and all settings live in the menubar 🐾 too.
