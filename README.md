# 윤아 음성 사진첩

할머니의 목소리로 들려주는 윤아의 사진첩 웹앱입니다. 사진을 콕 누르면 자막이 뜨고 할머니 목소리가 나옵니다.

## 구성

```
index.html          앱 전체 (HTML + CSS + JS, 별도 빌드 불필요)
photos/p001.jpg …   사진 81장
voices/p001-*.mp3 … 할머니 목소리 81개
data/voices.json    사진 번호 → 목소리 파일 연결표, 수정한 자막
.nojekyll           GitHub Pages용 설정 파일
```

## 동작 방식

- 사진 번호(`p001` … `p081`)와 목소리 파일은 `data/voices.json`으로 연결됩니다.
- 녹음이 있는 사진은 항상 할머니 목소리로만 재생하며, 휴대폰 기계음(TTS)으로 대체하지 않습니다.
- 한 번에 한 목소리만 재생합니다. 다른 사진을 누르거나 넘기면 즉시 멈춥니다.
- 현재 사진과 앞뒤 사진의 목소리는 미리 내려받아 첫 터치도 바로 재생됩니다.

## 로컬에서 실행

브라우저가 `fetch`를 막으므로 `index.html`을 직접 열지 말고 간단한 서버로 실행하세요.

```bash
python3 -m http.server 8000
# http://localhost:8000 접속
```

## GitHub Pages로 배포

1. 저장소 생성 후 이 폴더의 내용을 올립니다.
2. Settings → Pages → Branch를 `main` / `/ (root)`로 지정합니다.
3. 안내된 주소를 폰에서 열고 홈 화면에 추가하면 앱처럼 쓸 수 있습니다.

```bash
git init
git add .
git commit -m "윤아 음성 사진첩"
git branch -M main
git remote add origin https://github.com/<계정>/<저장소>.git
git push -u origin main
```

## 목소리 교체

1. 새 녹음을 `voices/`에 넣습니다. 형식은 mp3를 권장합니다.
2. `data/voices.json`에서 해당 번호의 `path`를 새 파일명으로 바꿉니다.
3. 커밋 후 푸시합니다.

## 참고

- 앱 안의 할머니 모드 녹음/자막 저장 기능은 Claude 아티팩트 환경에서만 저장됩니다. GitHub Pages에서는 재생 전용이며, 목소리와 자막 변경은 위 방법으로 파일을 직접 수정하세요.
- 아이 사진과 가족 음성이 들어 있으므로 저장소를 **Private**으로 두는 것을 권장합니다. 무료 계정의 Private 저장소는 GitHub Pages가 지원되지 않을 수 있으니, 공개 배포 전 반드시 확인하세요.
