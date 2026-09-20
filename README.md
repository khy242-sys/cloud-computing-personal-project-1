# 개인 소개 페이지 + 지출 관리 API

## 프로젝트 소개

김한룡의 개인 소개 페이지와, 그 페이지에서 호출하는 FastAPI 백엔드 API를 만든 클라우드컴퓨팅 개인과제입니다.
소개 페이지의 "API 호출하기" 버튼을 누르면 브라우저가 Render에 배포된 백엔드 서버의 `/health` 엔드포인트를 호출하고, 응답 결과를 화면에 보여줍니다.
프론트엔드는 Vercel, 백엔드는 Render에 각각 배포했고, 소스 코드는 GitHub 한 저장소에서 관리합니다.

## 주요 구성

```
personal_project_1/
├─ backend/                # FastAPI 백엔드 (Render 배포)
│   ├─ app/
│   │   ├─ main.py         # 앱 진입점, CORS 설정, /, /health
│   │   ├─ models.py       # Pydantic 모델
│   │   └─ routers/
│   │       └─ transactions.py   # 지출 내역 API
│   └─ requirements.txt
└─ frontend/               # 정적 웹페이지 (Vercel 배포)
    ├─ index.html          # 자기소개 카드 + API 연동 영역
    ├─ script.js           # 다크모드 전환
    └─ style.css
```

| 구분 | 사용 기술 | 배포 |
|---|---|---|
| 프론트엔드 | HTML, CSS, JavaScript (fetch) | Vercel |
| 백엔드 | Python, FastAPI, Uvicorn | Render |
| 소스 관리 | Git, GitHub | GitHub |

- 백엔드는 `CORSMiddleware`를 적용해서 다른 주소(Vercel)의 브라우저에서 호출할 수 있습니다.
- Render 무료 플랜은 15분간 요청이 없으면 잠들기 때문에, 오래 쉬었다가 처음 호출하면 응답에 30~60초 정도 걸릴 수 있습니다.

## 배포 주소

| 항목 | 주소 |
|---|---|
| GitHub 저장소 | https://github.com/khy242-sys/cloud-computing-personal-project-1 |
| 프론트엔드 (Vercel) | https://cloud-computing-personal-project-1.vercel.app |
| 백엔드 API (Render) | https://cloud-computing-personal-project-1.onrender.com |
| Swagger UI (API 문서) | https://cloud-computing-personal-project-1.onrender.com/docs |

## 로컬 실행 방법

```bash
cd backend
python -m venv .venv
.venv\Scripts\activate
pip install -r requirements.txt
fastapi dev app/main.py
```

서버가 켜지면 http://127.0.0.1:8000/docs 에서 API 문서를 확인할 수 있습니다.
프론트엔드는 `frontend/index.html`을 VS Code Live Server로 열면 됩니다.