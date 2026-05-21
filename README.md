# 저현고등학교 부서별 홍보 사이트 (2026)

자율형 공립고 저현고등학교의 2026학년도 부서별 행사·프로그램을 안내하는 정적 웹사이트입니다.

**라이브 사이트:** https://gimseuli-cmd.github.io/jeohyeon-homepage/

---

## 폴더 구조

```
.
├── index.html              ← 메인 페이지 (부서 카드 6개)
├── pages/                  ← 부서별 상세 페이지
│   ├── 창의인문부.html
│   ├── 과학정보부.html
│   ├── 예술체육부.html
│   ├── 진로상담부.html
│   ├── 학년부.html
│   └── 대외협력부.html
├── assets/
│   └── img/
│       ├── logo.png
│       └── posters/        ← 모든 행사 포스터
└── css/
    └── styles.css          ← 백업용 (실제 스타일은 각 HTML의 <style>에 인라인)
```

> CSS는 각 HTML 파일의 `<style>` 블록에 인라인으로 작성되어 있습니다. `css/styles.css`는 백업이며 사이트는 이를 사용하지 않습니다.

---

## 부서 페이지 구성

| 부서 | data-dept | 컬러 | 주요 프로그램 |
|---|---|---|---|
| 창의인문부 | changin | 코발트 블루 | 학생 주도 독서교육 / 국제교류·다문화 / 지역연계·세계시민 |
| 과학정보부 | science | 그린 | G-bio Link · 창의융합 STEAM(S.P.A.R.K) · 학교 숲 환경교육 |
| 예술체육부 | arts | 황토 | 아침운동 · 학교스포츠클럽 리그전 · 생활체육 · 체육축제 |
| 진로상담부 | counseling | 보라 | 학부모 진로진학 아카데미 / 해양 미세플라스틱 / 1:1 컨설팅 / 학과 멘토링 / 기업가정신 / 학습 코칭 |
| 학년부 | grade | 와인 | 체험학습 · 창업 아이디어 공모전 · 재능 기부 · 문화다양성 · SDGs · 미래포럼 |
| 대외협력부 | partnership | 청록 | 3D 바이오프린팅 캠프 · 2026 크루인증제 |

---

## 포스터 관련

### 네이밍 규칙
- 형식: `poster-<영문-케밥-케이스>.png`
- 예시: `poster-glocal-leader.png`, `poster-bio-convergence.png`

### 원본 파일 보관 위치
구글 드라이브의 `15. 홍보물/6.웹사이트 제작/` 폴더에 모든 원본 포스터(PNG/JPG)와 가정통신문(HWPX/PDF/ODT)이 함께 들어 있습니다.

### 새 포스터 추가 절차
1. 원본 폴더에서 파일을 찾아 `poster-XXX.png` 형식으로 이름 변경
2. `assets/img/posters/`로 복사
3. HTML의 해당 섹션에 `<figure class="poster">` 추가
4. 1열용 `.poster-row--1`, 3열용 `.poster-row--3`, 5열용 `.poster-row--5` 사용

### 라이트박스 (확대 모달)
모든 `.poster img`는 클릭 시 자동으로 확대 모달을 열도록 모든 부서 페이지에 인라인 JS가 포함되어 있습니다. 닫기 버튼(우상단 ×), 모달 바깥 클릭, ESC 키 모두 지원.

---

## 반응형 디자인

| 브레이크포인트 | 변경 사항 |
|---|---|
| ≤ 1100px | 네비게이션 간격 축소 |
| ≤ 1024px | 부서 카드 3열 → 2열 |
| ≤ 900px | block__head 그리드 단일 컬럼 |
| ≤ 880px | 상단 네비게이션 숨김 |
| ≤ 640px | 부서 카드 1열, 모바일 전용 패딩/폰트, 표 auto-layout |

모바일에서 표 첫 컬럼의 긴 텍스트는 명시적 `<br />`로 줄바꿈 처리되어 있습니다 (예: 과학정보부의 `G-kim<br />(고양시 지킴이)`).

---

## 로컬 미리보기

Python이 설치되어 있다면:

```bash
cd 홈페이지폴더
python -m http.server 8000
```

브라우저에서 http://localhost:8000/ 접속.

---

## 수정 → 배포 흐름

GitHub Pages가 `main` 브랜치 루트를 자동 배포합니다.

```bash
# 1. 파일 수정 (HTML/CSS/이미지)
# 2. 변경 확인
git status

# 3. 커밋 + 푸시
git add .
git commit -m "수정 내용 요약"
git push

# 4. 1~3분 후 https://gimseuli-cmd.github.io/jeohyeon-homepage/ 에 반영
```

---

## Claude Code로 작업 이어가기

다른 환경/계정의 Claude Code에서 이어서 작업하려면:

```bash
git clone https://github.com/gimseuli-cmd/jeohyeon-homepage.git
cd jeohyeon-homepage
claude
```

이 README가 프로젝트 맥락을 모두 담고 있으므로 Claude가 즉시 작업에 합류할 수 있습니다.

### 사용자 작업 선호도
- 파일 이동·복사·이름 변경: 사용자가 직접 처리하는 것을 선호 (필요 파일을 표로 안내)
- 단, 명시적으로 "자동으로 처리해줘"라고 하면 스크립트로 일괄 처리
- PDF → PNG 변환 필요 시 PyMuPDF(`fitz`), JPG → PNG 변환은 Pillow 사용

---

## 기술 스택

- 순수 HTML5 + CSS3 + Vanilla JS (빌드 단계 없음)
- 폰트: Pretendard (CDN 로드)
- 호스팅: GitHub Pages
