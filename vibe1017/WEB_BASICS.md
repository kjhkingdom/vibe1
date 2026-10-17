# 기본 웹페이지 제작을 위한 지식 정리

이 문서는 처음 웹페이지를 만드는 사람이 알아야 할 개념과 작업 순서를 정리한 입문 가이드입니다. 목표는 제목, 소개 글, 이미지, 링크, 간단한 버튼이 있는 반응형 페이지를 직접 만들고 배포하는 것입니다.

## 1. 웹페이지가 동작하는 방식

브라우저는 서버에 파일을 요청한 뒤 HTML, CSS, JavaScript를 해석해 화면을 보여 줍니다.

- **HTML**: 제목, 문단, 링크 같은 콘텐츠와 구조를 정의합니다.
- **CSS**: 색상, 글꼴, 간격, 배치, 화면 크기에 따른 디자인을 정의합니다.
- **JavaScript**: 버튼 클릭, 입력 처리, 화면 내용 변경 등 동작을 구현합니다.
- **서버와 호스팅**: 파일을 보관하고 인터넷을 통해 전달합니다.
- **도메인과 HTTPS**: 사람이 읽는 주소와 암호화된 연결을 제공합니다.

소개 페이지처럼 파일만 제공하면 되는 사이트는 **정적 웹사이트**로 만들 수 있습니다. 로그인, 데이터 저장, 결제 등은 보통 백엔드나 외부 서비스가 추가로 필요합니다.

## 2. 필요한 도구와 파일 구조

처음에는 코드 편집기, 웹 브라우저, 로컬 서버만 있으면 됩니다. React 같은 프레임워크나 Node.js 패키지는 기본 페이지의 필수 조건이 아닙니다.

```text
my-page/
├── index.html
├── style.css
├── script.js
└── images/
    └── profile.webp
```

- `index.html`: 첫 화면의 진입 파일입니다.
- `style.css`: 화면 스타일을 모읍니다.
- `script.js`: 필요한 상호작용을 구현합니다.
- `images/`: 사용할 이미지를 보관합니다. 실제 사용하는 파일만 추가합니다.

파일명은 소문자와 하이픈을 사용하면 관리하기 편합니다. 배포 서버에서는 대소문자를 구분할 수 있으므로 파일명과 참조 경로를 정확히 맞춥니다.

## 3. HTML: 의미 있는 구조 만들기

HTML은 태그로 콘텐츠의 역할을 표시합니다.

| 태그 | 용도 |
| --- | --- |
| `h1`–`h6` | 제목과 하위 제목 |
| `p` | 문단 |
| `a` | 다른 페이지나 위치로 이동 |
| `img` | 이미지 |
| `ul`, `ol`, `li` | 목록 |
| `header`, `nav`, `main`, `section`, `footer` | 문서의 주요 영역 |
| `button` | 클릭으로 실행하는 동작 |
| `form`, `label`, `input` | 사용자 입력 |

페이지의 대표 제목은 보통 `h1` 하나로 두고 하위 제목은 내용의 계층에 맞게 사용합니다. 이동에는 링크를, 동작에는 버튼을 사용합니다. 의미 있는 태그는 접근성과 검색엔진의 내용 이해에 도움이 됩니다.

### 기본 HTML 예제

아래 코드를 `index.html`에 저장합니다. 뒤의 CSS와 JavaScript 예제는 이 HTML과 함께 사용합니다.

```html
<!doctype html>
<html lang="ko">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta name="description" content="웹 개발을 배우며 만든 첫 소개 페이지입니다." />
    <title>나의 첫 웹페이지</title>
    <link rel="stylesheet" href="./style.css" />
    <script src="./script.js" defer></script>
  </head>
  <body>
    <header class="container">
      <h1>안녕하세요, 나의 첫 웹페이지입니다</h1>
      <nav aria-label="주요 메뉴">
        <a href="#about">소개</a>
      </nav>
    </header>

    <main class="container">
      <section id="about" aria-labelledby="about-title">
        <h2 id="about-title">소개</h2>
        <p>HTML, CSS, JavaScript를 배우고 있습니다.</p>
        <button id="greet-button" type="button">인사하기</button>
        <p id="message" role="status"></p>
      </section>
    </main>

    <footer class="container">
      <p>직접 만든 소개 페이지</p>
    </footer>
  </body>
</html>
```

`lang`은 문서 언어, `charset`은 문자 인코딩을 지정합니다. `viewport`는 모바일 화면에 맞는 표시를 돕고, `defer`는 HTML 분석이 끝난 뒤 스크립트를 실행하게 합니다.

이미지를 추가할 때는 실제 이미지 파일과 함께 `<img src="./images/profile.webp" alt="작업 중인 나의 모습" width="640" height="480" />`처럼 사용합니다. `alt`에는 이미지의 목적을 전달하는 설명을 적고, 순수 장식 이미지는 `alt=""`로 둡니다. 너비와 높이는 실제 이미지 비율에 맞춥니다.

## 4. CSS: 디자인과 배치

CSS는 선택자로 요소를 고르고 속성과 값으로 스타일을 지정합니다.

```css
/* style.css */
* {
  box-sizing: border-box;
}

body {
  margin: 0;
  font-family: system-ui, sans-serif;
  line-height: 1.6;
  color: #1f2937;
  background: #f8fafc;
}

.container {
  width: min(100% - 2rem, 60rem);
  margin-inline: auto;
  padding-block: 1.5rem;
}

h1 {
  font-size: clamp(1.75rem, 5vw, 2.5rem);
}

a {
  color: #1d4ed8;
}

button {
  padding: 0.75rem 1rem;
  border: 0;
  border-radius: 0.5rem;
  color: #fff;
  background: #1d4ed8;
  font: inherit;
  cursor: pointer;
}

button:hover {
  background: #1e40af;
}

a:focus-visible,
button:focus-visible {
  outline: 3px solid #0f172a;
  outline-offset: 4px;
}

img {
  display: block;
  max-width: 100%;
  height: auto;
}

@media (min-width: 48rem) {
  header.container {
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 2rem;
  }
}
```

### 먼저 익힐 개념

- **선택자**: `p`는 태그, `.container`는 클래스, `#message`는 ID를 선택합니다.
- **박스 모델**: 콘텐츠 주변에 `padding`, `border`, `margin`이 있습니다. `border-box`는 지정한 크기에 안쪽 여백과 테두리를 포함합니다.
- **캐스케이드와 우선순위**: 여러 규칙이 겹치면 중요도, 선택자 구체성, 선언 순서 등에 따라 적용 결과가 결정됩니다. 개발자 도구에서 실제 적용 규칙을 확인합니다.
- **단위**: `rem`은 루트 글자 크기 기준, `%`는 속성에 따른 기준 크기의 비율, `px`는 CSS 픽셀입니다.
- **Flexbox**: 메뉴처럼 한 방향으로 정렬하는 배치에 편리합니다.
- **Grid**: 카드 목록처럼 행과 열을 함께 다루는 배치에 편리합니다.
- **반응형 디자인**: 작은 화면부터 구성하고 필요한 지점에 미디어 쿼리를 추가합니다. 특정 기기 이름보다 콘텐츠가 불편해지는 너비를 기준으로 판단합니다.

고정 너비를 과하게 지정하면 모바일에서 가로 스크롤이 생기기 쉽습니다. 유연한 너비와 최대 너비를 함께 사용합니다.

## 5. JavaScript: 사용자 동작 처리

처음에는 변수, 함수, 조건문, 배열과 객체를 배우고, DOM과 이벤트로 화면에 연결합니다. DOM은 JavaScript에서 HTML 요소를 읽고 수정할 수 있는 문서 표현입니다.

```javascript
// script.js
const button = document.querySelector('#greet-button');
const message = document.querySelector('#message');

if (button && message) {
  button.addEventListener('click', () => {
    message.textContent = '방문해 주셔서 감사합니다!';
  });
}
```

`querySelector`는 요소를 찾고, `addEventListener`는 이벤트가 발생했을 때 실행할 함수를 등록합니다. `textContent`는 내용을 일반 텍스트로 넣습니다. 사용자 입력을 `innerHTML`에 그대로 넣으면 스크립트 삽입 등 보안 문제가 생길 수 있습니다.

추가로 익힐 항목은 폼 입력과 검증, `fetch`를 통한 HTTP 요청, `async`/`await`, 오류 처리입니다. 외부 API 호출에는 네트워크 장애와 브라우저의 CORS 제한도 고려해야 합니다.

## 6. 접근성과 사용성

- 키보드의 Tab, Enter, Space로 주요 기능을 사용할 수 있게 합니다.
- 포커스 표시를 보이게 유지합니다.
- 글자와 배경의 대비를 확보하고, 색상만으로 상태를 구분하지 않습니다.
- 입력 필드에는 연결된 `label`을 제공합니다. placeholder는 label을 대신하지 않습니다.
- 링크 문구는 목적을 설명하게 적습니다. 예: “프로젝트 소개 보기”.
- 작은 화면과 브라우저 확대 상태에서도 내용을 읽고 조작할 수 있게 합니다.
- 기본 HTML 요소의 기능을 먼저 활용하고, 필요한 경우에만 ARIA 속성을 보완합니다.

폼을 화면에 만드는 것만으로 문의 내용이 전송되거나 저장되지는 않습니다. 실제 제출 대상과 서버 처리가 필요하며, 브라우저 입력 검증 외에 서버에서도 검증해야 합니다.

## 7. 로컬에서 실행하고 확인하기

위 세 파일을 저장한 디렉터리에서 다음 명령을 실행합니다. Python이 설치되어 있어야 합니다.

```bash
python3 -m http.server 8000 --bind 127.0.0.1
```

자신의 컴퓨터에서 실행했다면 브라우저 주소창에 `http://127.0.0.1:8000`을 입력합니다. 서버 종료는 터미널에서 `Ctrl+C`를 누릅니다. 원격 클라우드 환경에서는 실행 환경이 제공하는 포트 접근 기능이 있어야 자신의 브라우저로 볼 수 있습니다. 단순 HTTP 서버는 개발 확인용으로 사용합니다.

HTML 파일을 직접 열 수도 있지만, HTTP 서버를 사용하면 경로와 요청 동작을 실제 서비스 방식에 가깝게 확인할 수 있습니다.

### 개발자 도구 활용

브라우저의 개발자 도구에서 다음을 확인합니다.

| 기능 | 확인할 내용 |
| --- | --- |
| Elements / Inspector | HTML 구조와 실제 적용된 CSS |
| Console | JavaScript 오류 |
| Network | HTML, CSS, JS, 이미지 요청의 성공 여부와 404 오류 |
| 화면 크기 조절 / 기기 모드 | 작은 화면에서 배치와 가로 넘침 |
| Accessibility | 요소 이름, 역할, 접근성 정보 |

수정 결과가 반영되지 않으면 파일 저장 여부, 경로, 캐시를 확인합니다. 요청이 성공했더라도 올바른 파일 내용이 전달되었는지 확인해야 합니다.

## 8. 버전 관리와 배포

Git은 변경 이력을 기록하는 도구입니다. 작은 작업 단위로 차이를 확인하고 커밋하면 되돌리기와 협업이 쉬워집니다.

```bash
git status
git diff
git add index.html style.css script.js
git commit -m "Add basic introduction page"
```

위 명령은 해당 파일들이 있는 Git 저장소에서 실행하는 예시입니다. 커밋 전에 비밀번호, API 키, 불필요한 생성 파일이 포함되지 않았는지 확인합니다.

정적 웹사이트는 GitHub Pages 같은 정적 호스팅에 배포할 수 있습니다. 일반적인 순서는 다음과 같습니다.

1. 페이지 파일을 저장소에 올립니다.
2. 호스팅 서비스에서 배포할 저장소와 폴더 또는 빌드 결과물을 지정합니다.
3. 배포가 끝나면 HTTPS 주소로 접속합니다.
4. 하위 경로에서 CSS, JS, 이미지가 정상 로드되는지 확인합니다.
5. 수정 후 다시 배포해 반영 결과를 확인합니다.

기본 정적 페이지는 별도 빌드 없이 파일을 제공할 수 있습니다. 프레임워크를 사용하면 의존성 설치와 빌드 과정이 추가될 수 있습니다. 브라우저로 전달되는 코드와 파일은 공개된다고 가정하고, 비밀 키는 넣지 않습니다. `.env`라는 파일명만으로 비밀이 보호되지는 않습니다.

## 9. 성능과 기본 보안

- 이미지는 표시 크기에 맞게 줄이고 적절한 형식으로 압축합니다.
- 첫 화면에 필요하지 않은 이미지에는 상황에 따라 `loading="lazy"`를 사용합니다.
- 사용하지 않는 라이브러리와 과도하게 큰 파일은 제외합니다.
- 외부 스크립트와 패키지는 출처와 필요성을 확인합니다.
- 입력값을 신뢰하지 않고, 화면 출력과 서버 처리 양쪽에서 적절하게 다룹니다.
- 개인정보를 수집한다면 수집 목적, 보관, 접근 권한을 먼저 설계합니다.
- 실제 서비스에는 HTTPS를 사용합니다.

## 10. 완성 전 체크리스트

- [ ] 페이지 제목, 설명, 언어가 설정되어 있다.
- [ ] 제목 계층과 주요 영역이 의미 있게 구성되어 있다.
- [ ] 링크와 이미지 경로가 맞고 파일 요청에 오류가 없다.
- [ ] 버튼 클릭 시 예상한 내용이 표시된다.
- [ ] 키보드로 이동하고 기능을 실행할 수 있다.
- [ ] 작은 화면과 확대 상태에서 내용이 잘리지 않는다.
- [ ] Console에 해결되지 않은 오류가 없다.
- [ ] 비밀 키와 개인정보가 공개 파일에 포함되지 않았다.
- [ ] 배포한 주소에서도 주요 기능과 파일 경로가 정상이다.

이 체크리스트는 기초 점검용이며, 접근성이나 보안 전반에 대한 인증을 대신하지 않습니다.

## 11. 권장 학습 순서와 참고 자료

1. HTML로 소개 글과 링크를 구성합니다.
2. CSS로 글꼴, 색상, 간격을 조정합니다.
3. Flexbox와 Grid로 배치를 연습합니다.
4. 모바일 화면에서도 읽기 편하게 수정합니다.
5. JavaScript로 버튼 동작을 추가합니다.
6. 개발자 도구와 키보드로 동작을 점검합니다.
7. Git으로 변경을 기록하고 정적 호스팅에 배포합니다.

기본기를 익힌 뒤에 여러 페이지, 폼, API 연동, 프레임워크 순으로 범위를 넓히면 됩니다.

- [MDN 웹 개발 학습](https://developer.mozilla.org/ko/docs/Learn_web_development)
- [MDN HTML](https://developer.mozilla.org/ko/docs/Web/HTML)
- [MDN CSS](https://developer.mozilla.org/ko/docs/Web/CSS)
- [MDN JavaScript](https://developer.mozilla.org/ko/docs/Web/JavaScript)
- [W3C 접근성 기초](https://www.w3.org/WAI/fundamentals/accessibility-intro/)
- [GitHub Pages 문서](https://docs.github.com/ko/pages)

문서의 코드는 학습용 예시입니다. 이 문서를 생성하면서 실제 웹페이지 파일을 만들거나 배포하지는 않았습니다.
