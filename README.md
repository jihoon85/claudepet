# 🐾 ClaudePet

화면 위를 떠다니는 클로드 도트 마스코트 — macOS 데스크톱 펫입니다.
Claude Code와 연동되어 **실제 작업 상태**에 반응합니다: 일하면 같이 분주해지고, 끝나면 축하해주고, Claude가 부르면 달려와 알려줍니다.

*(English guide below — [English](#-claudepet-english))*

## 기능

- **화면 방랑** — 천천히 둥둥 떠다니며 눈동자가 커서를 따라옵니다
- **Claude Code 연동** (훅 기반)
  - 작업 중: 활발히 움직이고 메뉴바 아이콘에 배지 표시
  - 작업 완료: 폭죽 + "끝! 🎉" (프로젝트명 포함)
  - Claude가 주의를 요청하면: 화면 중앙으로 달려와 크게 점프 + ❗
- **더블클릭** — 구독 사용량(주간/세션 리미트)을 말풍선으로 표시
- **클릭** — 폴짝 뛰며 하트 분출 / **드래그 후 던지기** — 관성 비행 + 벽 튕김
- **커서 정지 감지** — 3분간 마우스가 안 움직이면 걱정돼서 콕콕 찌르러 옵니다
- **커스터마이즈** — 이름 바꾸기, 상태별 대사 편집, 효과음 on/off, 로그인 시 자동 실행
- **한국어/영어** — 시스템 언어를 자동으로 따라가고, 메뉴에서 직접 바꿀 수도 있습니다
- **업데이트 알림** — 새 버전이 나오면 펫이 말풍선으로 알려주고, 메뉴에서 바로 받을 수 있습니다

## 요구 사항

- macOS 11+ (Apple Silicon)
- Python 3 + [PyObjC](https://pypi.org/project/pyobjc/)

```bash
pip3 install pyobjc
```

## 실행

```bash
python3 claude_pet.py
```

앱 번들로 빌드하려면 (py2app):

```bash
pip3 install py2app
python3 setup.py py2app        # → dist/ClaudePet.app
```

종료는 메뉴바 🐾 아이콘 → 종료.

## Claude Code 연동 설정

**첫 실행 때 펫이 알아서 물어봅니다.** "연동하기"를 누르면 `~/.claude/settings.json`에
훅과 statusline이 자동으로 추가돼요 (기존 설정은 보존, 백업 파일 생성).
나중에 하려면 메뉴바 🐾 → **Claude Code 연동 설정**을 누르면 됩니다.

연동하면 펫이 실제 턴 진행 상태를 정확히 알게 됩니다
(연동하지 않으면 `pgrep` 폴백으로 대략적인 감지만 합니다).

<details>
<summary>수동으로 설정하려면 (JSON 예시)</summary>

훅 스크립트는 앱 안에 들어 있습니다: `ClaudePet.app/Contents/Resources/pet_hook.py`

```json
{
  "hooks": {
    "UserPromptSubmit": [{"hooks": [{"type": "command", "command": "python3 ~/Applications/ClaudePet.app/Contents/Resources/pet_hook.py start"}]}],
    "PreToolUse":       [{"hooks": [{"type": "command", "command": "python3 ~/Applications/ClaudePet.app/Contents/Resources/pet_hook.py start", "async": true}]}],
    "PostToolUse":      [{"hooks": [{"type": "command", "command": "python3 ~/Applications/ClaudePet.app/Contents/Resources/pet_hook.py start", "async": true}]}],
    "Stop":             [{"hooks": [{"type": "command", "command": "python3 ~/Applications/ClaudePet.app/Contents/Resources/pet_hook.py stop"}]}],
    "SessionEnd":       [{"hooks": [{"type": "command", "command": "python3 ~/Applications/ClaudePet.app/Contents/Resources/pet_hook.py stop"}]}],
    "Notification":     [{"hooks": [{"type": "command", "command": "python3 ~/Applications/ClaudePet.app/Contents/Resources/pet_hook.py alert"}]}]
  },
  "statusLine": {"type": "command", "command": "python3 ~/Applications/ClaudePet.app/Contents/Resources/pet_statusline.py"}
}
```

statusline은 더블클릭 사용량 표시에 필요합니다. 이미 쓰는 statusline이 있다면 자동 설치가 건드리지 않으니, 사용량 표시가 필요하면 직접 연결하세요.
</details>

## 파일 구성

| 파일 | 역할 |
|---|---|
| `claude_pet.py` | 펫 본체 (창·애니메이션·메뉴바) |
| `pattern.py` | 도트 패턴 데이터 |
| `strings.py` | ko/en 문자열 테이블 (시스템 언어 자동 감지) |
| `pet_hook.py` | Claude Code 훅 → 세션 마커 브리지 |
| `pet_statusline.py` | statusline → 사용량 캐시 브리지 |
| `setup.py` | py2app 빌드 설정 |

---

# 🐾 ClaudePet (English)

A tiny pixel-art Claude mascot that floats around your macOS screen.
It hooks into **Claude Code** and reacts to what's actually happening: gets busy when Claude works, celebrates when a task finishes, and runs over to grab your attention when Claude needs you.

## Features

- **Wanders your screen** — drifts around slowly, pupils follow your cursor
- **Claude Code integration** (hook-based)
  - Working: moves busily, menubar icon shows a badge
  - Task done: fireworks + "Done! 🎉" (with the project name)
  - When Claude requests attention: dashes to screen center, big jumps + ❗
- **Double-click** — shows your subscription usage (weekly / session limits) in a speech bubble
- **Click** — hops with hearts / **drag & throw** — inertial flight with wall bounces
- **Idle-cursor detection** — if your mouse hasn't moved for 3 minutes, it comes over to poke you
- **Customizable** — rename your pet, edit its phrases per state, toggle sounds, launch at login
- **Korean/English** — follows your system language automatically, or pick one from the menu
- **Update alerts** — when a new release is out, the pet tells you in a speech bubble and you can grab it from the menu

## Requirements

- macOS 11+ (Apple Silicon)
- Python 3 + [PyObjC](https://pypi.org/project/pyobjc/)

```bash
pip3 install pyobjc
```

## Run

```bash
python3 claude_pet.py
```

To build an app bundle (py2app):

```bash
pip3 install py2app
python3 setup.py py2app        # → dist/ClaudePet.app
```

Quit via the menubar 🐾 icon → Quit.

## Claude Code setup

**The pet offers to set this up on first launch.** Click "Set Up" and it adds the hooks
and statusline to `~/.claude/settings.json` automatically (existing settings are kept,
with a backup file). You can also do it later via menubar 🐾 → **Set Up Claude Code Sync**.

With the hooks in place the pet knows the real turn state; without them it falls back
to a rough `pgrep` check. For manual setup, see the JSON example in the Korean section
above — the hook scripts ship inside the app at `ClaudePet.app/Contents/Resources/`.

## Files

| File | Role |
|---|---|
| `claude_pet.py` | The pet itself (window, animation, menubar) |
| `pattern.py` | Pixel pattern data |
| `strings.py` | ko/en string table (auto language detection) |
| `pet_hook.py` | Claude Code hooks → session marker bridge |
| `pet_statusline.py` | statusline → usage cache bridge |
| `setup.py` | py2app build config |
