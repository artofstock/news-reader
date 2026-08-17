# 영어 리더 — 문장별 영/한 대역 읽기

긴 영문 글(기사, 칼럼 등)을 붙여넣으면 문장 단위로 잘라 자동 번역하고,
유튜브처럼 영어 문장 → 한글 해석을 번갈아 보여주거나 읽어주는 PWA입니다.

## 주요 기능

- 영문 붙여넣기 또는 .txt 파일 업로드 → 문장 자동 분리 → 무료 API로 자동 번역
- **자동 재생 모드**: 영어 낭독 → 한글 낭독 → 다음 문장, 계속 자동으로 넘어감 (TTS)
- **수동 모드**: 카드를 탭하면 영어 ↔ 한글 전환, 좌우 스와이프로 문장 이동
- 번역이 이상하거나 문장이 잘못 나뉜 경우 연필 아이콘으로 직접 수정/삭제/다음 문장과 합치기 가능
- 읽던 위치 자동 저장(북마크), 여러 글을 목록에 저장해두고 이어 읽기
- 오프라인에서도 앱 자체는 열림(번역은 온라인 필요)

## 번역에 대해 꼭 알아두세요

- 번역은 **MyMemory**라는 무료 번역 API를 사용합니다(키 필요 없음).
- 품질은 구글 번역보다는 떨어질 수 있고, 하루 요청량이 넘으면(개인 사용으론 거의 안 넘습니다) 일시적으로 실패할 수 있어요.
- 실패한 문장은 카드에 "⚠️ 번역 실패"로 표시되고, 연필 아이콘을 눌러 직접 입력할 수 있습니다.
- 더 좋은 번역이 필요하면: 미리 Claude 등으로 번역해서 영문 옆에 준비해둔 뒤, 이 화면의 연필 아이콘으로 각 문장에 붙여넣는 방식도 가능합니다.

## 문장 분리 관련 참고

- 마침표 기준으로 자동 분리하는데, "D.C.", "U.S.A." 같은 복잡한 약어가 있으면 가끔 문장이 이상하게 나뉠 수 있어요.
- 이럴 땐 편집 화면에서 "다음 문장과 합치기" 버튼으로 붙이거나, 직접 텍스트를 수정하면 됩니다.

## 폴더 구성

```
news-reader/
├── index.html
├── manifest.json
├── sw.js
└── icons/
    ├── icon-192.png
    ├── icon-512.png
    ├── icon-512-maskable.png
    └── apple-touch-icon.png
```

## GitHub Pages로 배포하기

영어카드 앱과 똑같은 방식입니다. 별도 저장소로 만드는 걸 권장합니다.

1. GitHub에서 **New repository** → 이름 예: `news-reader` → Public → Create repository
2. 저장소 페이지 → **Add file → Upload files** → 이 폴더 안의 파일/폴더 전체를 그대로 업로드
   (또는 git 사용 시)
   ```bash
   cd news-reader
   git init
   git add .
   git commit -m "첫 배포"
   git branch -M main
   git remote add origin https://github.com/사용자명/news-reader.git
   git push -u origin main
   ```
3. 저장소 → **Settings → Pages** → Source: **Deploy from a branch** → Branch: `main`, 폴더: `/ (root)` → Save
4. 1~2분 후 `https://사용자명.github.io/news-reader/` 접속 → 홈 화면에 추가하면 설치 완료

## 업데이트

파일 수정 후 다시 업로드(또는 `git push`)하면 됩니다. 캐시가 안 바뀌면 `sw.js`의 `CACHE_VERSION`을 올려서 재업로드하세요.

## 데이터

모든 글과 번역, 학습 진행 상황은 기기(브라우저)에만 저장됩니다. 설정 화면에서 "전체 백업 내보내기"로 JSON 파일을 저장해둘 수 있어요.
