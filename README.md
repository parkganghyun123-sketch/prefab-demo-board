# 재실 감지 조명 보드 (REV2)

**2026 PNU AI 해커톤 창업트랙 C-06 · 팀 전전컴**이 만든 실측 보드입니다.
[Prefab](https://prefab-web.onrender.com) — 회로도와 펌웨어가 어긋난 곳을 찾는 도구 —
을 시연하려고 공개해 둡니다.

## 무엇이 들어 있나

```
hardware/board.net.xml   회로도 넷리스트 (KiCad kicadxml)
hardware/bom.csv         부품 목록
firmware/                Arduino 펌웨어
```

## 이 보드에 실제로 있었던 일

REV1 에서 **릴레이가 안 꺼졌습니다.**

> *"LED가 ON은 되는데 OFF가 안 되는 게 문제야"* — 2026-08-21

3.3V 로 도는 ESP32-C6 의 출력이 5V 릴레이(JQC-3FF-S-Z)의 입력 문턱에 못 미쳤습니다.
회로도 검사도 통과했고 코드도 컴파일됐지만, **문제는 둘 사이에 있었습니다.**

REV2 에서 2N3904 로 레벨 시프트를 넣어 고쳤고, 그 결함이 Prefab 의 규칙 **R15** 가 됐습니다.

## PR 마다 검사가 돕니다

`.github/workflows/prefab.yml` 이 붙어 있으면, 회로도나 펌웨어가 바뀐 PR 마다
Prefab 이 둘을 대조합니다. 치명 발견이 있으면 빨간불이 켜지고 머지가 막힙니다.

**직접 해 보시려면** — `firmware/` 의 `PRESENCE_PIN` 을 `D2` 에서 `D4` 로 바꿔
PR 을 올려 보세요. 회로도에 D4 가 없어서 잡힙니다.

## 라이선스

MIT. 저희가 그린 회로도이고 저희가 쓴 코드입니다.
