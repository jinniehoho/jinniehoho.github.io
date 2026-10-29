# 포트폴리오 직접 수정하기

## 파일별 역할

- `index.html`: 홈페이지의 Hero, 프로젝트 카드, About, Contact 구조와 기본 영문 문구.
- `steam.html`: Steam 상세 페이지와 기술 활용 근거.
- `site.css`: 두 페이지의 공통 디자인과 모바일 대응.
- `site.js`: 영어(en), 독일어(de), 한국어(ko) 문구와 연락처 설정.
- `reports/`: 공개할 PDF만 보관.
- `assets/`: 보고서 이미지.

## 이메일·LinkedIn·CV 추가하기

1. GitHub 저장소에서 `site.js`를 열고 연필(Edit) 버튼을 누릅니다.
2. `const contact`를 찾습니다. 현재 세 값은 모두 빈 문자열이므로 화면에 표시되지 않습니다.
3. `email`의 따옴표 안에 공개할 이메일 주소를 입력합니다.
4. `linkedin`에는 본인의 전체 `https://www.linkedin.com/...` 주소를 입력합니다.
5. 공개용 CV는 먼저 `reports` 폴더에서 **Add file → Upload files**로 올립니다. 예를 들어 파일명이 `cv.pdf`라면 `cv` 값은 `reports/cv.pdf`로 입력합니다. 영문·숫자·하이픈·밑줄로 된 파일명을 사용하세요.
6. **Commit changes**를 눌러 저장합니다. 정보가 들어간 항목만 표시됩니다. 다시 숨기려면 값을 빈 따옴표로 바꾸세요.

연락처 구조는 `index.html`의 `id="contact"` 영역입니다. 공개하지 않을 개인정보가 포함된 CV는 올리지 마세요.

## 문구 수정하기

`site.js`의 `translations` 아래 `en`, `de`, `ko`가 있습니다.

- `headline`, `intro`: 첫 화면 제목과 소개.
- `bio`, `degree`, `training`: 경력 소개와 교육.
- `connect`, `contactText`: 연락 영역 제목과 설명.
- `email`, `linkedin`, `cv`: 연락 버튼 이름.
- `meta`, `title`: 페이지 설명과 제목.

원하는 언어의 따옴표 안 문구만 바꾸세요. 쉼표와 중괄호는 유지합니다. 영어 기본 화면과 검색 설명도 일치시키려면 `index.html`과 `steam.html`의 같은 `data-i18n` 항목 및 description 메타 태그를 함께 수정합니다.

## 프로젝트 추가하기

`index.html`의 `<div class="projects">` 안에서 `<article class="card">`부터 대응하는 `</article>`까지가 카드 한 개입니다. 이를 복사해 같은 영역에 추가하고 제목·이미지·질문·결과·링크를 바꿉니다. 새 문구에는 새 `data-i18n` 이름을 붙이고 `site.js`의 세 언어에 같은 이름을 추가합니다. 실제 공개할 프로젝트만 추가하세요.

## 공개 사이트에 반영하기

1. 변경을 `main` 브랜치에 **Commit changes**로 저장합니다.
2. 저장소 **Actions**에서 최신 `pages build and deployment` 작업이 녹색 체크가 될 때까지 기다립니다.
3. https://jinniehoho.github.io/ 를 새로고침합니다. 이전 화면이 보이면 Ctrl+F5를 누릅니다.
4. EN/DE/KO 전환, 프로젝트 상세, PDF와 새 연락 링크를 눌러 확인합니다.

수정 전 내용은 GitHub의 파일 History에서 확인할 수 있습니다. 이번 변경 이전 홈페이지는 로컬의 `output/portfolio-before-redesign/index.html`에도 보존되어 있습니다.

## 현재 공개 범위

영문 보고서와 출력 제거한 노트북을 공개합니다. 독일어 PDF는 마지막 페이지 잘림으로 보류 중입니다. 노트북 전체 재실행과 SQL → Power BI 전체 재현은 검증하지 않았으며 SQL 정의는 아직 공개되지 않았습니다. CSV, .venv, practice, 시험 파일, PBIX는 업로드하지 않습니다.
