# 포켓 단어장 AI 버전

Vercel Serverless Function과 Gemini API를 연동한 모바일 단어장입니다. API 키는 브라우저 코드가 아니라 서버 함수에서만 읽습니다.

## 파일 구성

- `api/vocab.js`: Gemini 단어 정보 생성 및 이미지 분석 서버 함수
- `index.html`, `style.css`, `app.js`: 모바일 웹 앱
- `package.json`, `package-lock.json`: Vercel이 설치할 서버 의존성
- `.env.example`: 환경 변수 이름 예시

## Vercel 배포

1. 이 폴더의 **내용 전체**를 GitHub 저장소 루트에 올립니다. `api` 폴더도 반드시 포함하세요.
2. Vercel에서 저장소를 Import합니다. Framework Preset은 `Other`, Root Directory는 이 파일들이 있는 폴더로 설정합니다.
3. Project Settings → Environment Variables에 `GEMINI_API_KEY`를 추가합니다.
4. 사용할 배포 환경(Production, Preview)에 체크하고 저장합니다.
5. 환경 변수를 추가하거나 바꾼 뒤에는 반드시 새로 Deploy/Redeploy합니다.

GitHub 저장소 첫 화면에는 `vocab.js`가 아니라 `api` 폴더가 보여야 합니다. `api` 폴더를 열었을 때 `vocab.js`가 있어야 합니다.

선택적으로 `GEMINI_MODEL`을 지정할 수 있으며, 미설정 시 `gemini-3.6-flash`를 사용합니다. 이전 배포본을 유지한다면 Vercel 환경 변수에 `GEMINI_MODEL=gemini-3.6-flash`를 추가하고 재배포해도 됩니다.

## 오류 확인

배포 후 `https://내주소.vercel.app/api/vocab`을 브라우저에서 열었을 때 `POST 요청만 허용됩니다.`가 보이면 서버 함수가 정상 배포된 것입니다. `404`라면 `api/vocab.js`가 저장소 루트 아래에 없거나 Vercel Root Directory가 잘못된 것입니다.

자동 채우기나 이미지 분석 실패 시 화면에 서버 오류 메시지가 표시됩니다. Vercel의 해당 Deployment → Functions 로그에서도 자세한 오류를 확인할 수 있습니다.
