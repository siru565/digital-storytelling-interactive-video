# Forkreel

웹 기반 **인터랙티브 비디오(분기형 영상 게임) 엔진** 프로토타입입니다.
영상을 넣고, 선택지로 장면을 이어서, 플레이어와 영상을 폴더째 내보낼 수 있습니다.

## 실행

`index.html`을 브라우저(Chrome·Edge 권장)로 열면 편집기가 실행됩니다.

## 구조

| 계층 | 위치 | 역할 |
|---|---|---|
| 엔진 코어 | `<script id="engine-src">` 의 `IVEngine` | 재생, 선택 타이밍, 제한 시간, 반복, 점수 변수, 되돌리기. UI를 모르고 이벤트만 발행 |
| 미디어 어댑터 | `VideoAdapter`, `PlaceholderAdapter`, `Media.resolve` | 실제 영상 / 글자 화면을 같은 인터페이스로 재생. `resolve`만 바꾸면 영상 출처 교체 |
| 스킨 | `Skins.register({id, name, mount})` | 영상 위 선택지 UI. 시네마형, 카드형 기본 제공 |
| 저장소 | `Store` (IndexedDB) | 영상 Blob과 프로젝트 JSON 저장. 같은 메서드로 다른 저장소 어댑터 교체 가능 |
| 편집기 | 두 번째 `<script>` | 장면 지도, 장면 편집, 영상 보관함, 내보내기/불러오기 |

### 엔진 이벤트

| 이벤트 | 데이터 |
|---|---|
| `scene` | `{scene, vars}` |
| `time` | `{t, d, scene, phase}` |
| `choices` | `{list, timeLimit, defaultId}` |
| `timer` | `{remain, total}` |
| `chosen` | `{choice, timeout}` |
| `end` | `{scene, vars, path}` |
| `state` | `{paused, muted}` |

## 내보내기 결과

```
프로젝트이름/
├─ index.html      ← 플레이어 (엔진 + 스킨 + 프로젝트 데이터)
├─ project.json    ← 편집기로 다시 불러오기용
├─ README.txt
└─ videos/
```

## 다음 작업 후보

- 영상 파일 키를 이름 대신 고유 ID로 (덮어쓰기 방지)
- 화면 속 영역을 누르는 핫스팟 선택지
- 긴 영상 하나를 구간으로 나눠 여러 장면에 사용
- 다음 분기 영상 미리 로딩
- Supabase / Google Drive 저장소 어댑터
