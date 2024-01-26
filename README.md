# React_NextJSWithEcommerce

## Infos
- example code: https://github.com/techoi/fastcampus-commerce

## Url을 바꾸는 3가지 방식
- location.replace("url"): 로컬 state 유지 안됨(리랜더), url 바뀜
- router.push(url): 로컬 state유지 / data fetching은 일어남, getServerSideProps는 호출됨, url 바뀜
- router.push(url, as, {shallow: true}): 로컬 state는 유지 / data fetching은 일어나지 않음, getServerSideProps는 호출 되지 않음, url 바뀜, url이 동일할 경우에만 shallow로 동작
```
<button onClick=(() => {
  alert('edit');
  setClicked(true);
  location.replace('/settings/my/info?status=editing')
});


<button onClick=(() => {
  alert('edit');
  setClicked(true);
  router.push('/settings/my/info?status=editing')
});

<button onClick=(() => {
  alert('edit');
  setClicked(true);
  router.push('/settings/my/info?status=editing', undefined, {shallow: true)

```


## Blog Example
- create
```
% yarn create next-app blog --example "https://github.com/vercel/next-learn/tree/master/basics/learn-starter"
% yarn add -D prettier

```

### Adding metadata loader
- yaml파일 형식으로된 메타데이터를 파일 상단에서 읽어오는 것
- install
```bash
% yarn add gray-matter

### MD file analyze tools
```bash
% yarn add remark remark-html
```

### date formatting package
```bash
% yarn add date-fns
```

### SSG(Static Site Generation)
- fallback
    + false: show errors
    + 'Blocking': show after generation
    + true: Show loading first and show the generated page


### 블로그 테마 저장소
- https://jamstackthemes.dev/ : 여러가지 블로그에 대한 예제가 있음

### 예제에서 사용하는 블로그
- https://github.com/timlrx/tailwind-nextjs-starter-blog


### Install tailwind css
- How to install Tailwind on NextJS project
- https://tailwindcss.com/docs/guides/nextjs
```
% yarn add -D tailwindcss postcss autoprefixer
% npx tailwindcss init -p
```
- 위의 두가지 명령어를 실행하면 **tainwind.config.js** 파일이 생성된다
- 해당 파일의 내용에 contents부분을 아래와 같이 바꿔준다.
```
/** @type {import('tailwindcss').Config} */
module.exports = {
  darkMode: 'class',
  content: [
    "./app/**/*.{js,ts,jsx,tsx,mdx}",
    "./pages/**/*.{js,ts,jsx,tsx,mdx}",
    "./components/**/*.{js,ts,jsx,tsx,mdx}",
  ],
  theme: {
    extend: {},
  },
  plugins: [],
}
```
- 이후 styles/global.css파일의 상단에 아래의 내용을 추가해 준다.
```
@tailwind base;
@tailwind components;
@tailwind utilities;
```
- 이후 *** yarn dev**로 프로젝트를 실행하면 된다

## MD 파일이 jsx파일을 포함 할 수 있도록 변경
- 패키지 설치
```
% yarn add next-mdx-remote react-syntax-highlighter
```


## SEO를 위한 도구
- robots.txt: 검색엔진이나 크롤러 등이 이 사이트의 내용을 수집해가도 되는지 권한 체크를 하는 페이지
- sitemap: 도메인 내의 페이지 목록
   + xml로 만들어진 페이지 목록
 
- 라이브러리 추가
   + next-sitemap
   + https://www.npmjs.com/package/next-sitemap
```
% yarn add -D next-sitemap
```
- build하고 나서 post-build에서 실행하는 식
- sitemap을 생성하고 나서 robots.txt까지 같이 생성 할 수 있음
- 패키지 설치 이후 프로젝트 루트에서 **next-sitemap.config.js**파일을 만들어 줌
- 설정 파일 내부에 url을 설정해 줌.
```
/** @type {import('next-sitemap').IConfig} */
module.exports = {
  siteUrl: process.env.SITE_URL || 'https://example.com',
  generateRobotsTxt: true, // (optional)
  // ...other options
}
```
- package.json에 script 추가
```
'postbuild': 'next-sitemap'
```


## ESLint
- 설치
```
% yarn add -D eslint
```
- 초기화
```
% yarn eslint -init
```
- tainwind-css용 eslint 추가
```
% yarn add -D eslint-plugin-tainwindcss
```
- nextjs용 eslint 추가
```
% yarn add -D @next/eslint-plugin-next
```

### _app.js
- 공통된 데이터

### _document.js
- 좀더 정적인것, 메타태그등의 헤더

### Web Performance 측정
- https://web.dev/vitals/
    + 웹개발에서 유의해야할 사항에 대하여 정리해놓은 사이트
 
- https://developers.google.com/speed
    + page speed 분석 사이트
- Chrome 브라우저를 이용한 Performence 측정
    + Performence, Performence Insight, Lighthouse를 통한 측정
- _app.js에 webvitals추가
    + 아래의 코드를 _app.js에 추가, 아래의 코드는 브라우저 로그로 바로 보여주지만, ga등에 보내서 수집, 사용자의 로그 수집
```
export function reportWebVitals(metric) {
  console.log(metric)
}
```

## Error Handling
- https://nextjs.org/docs/pages/building-your-application/configuring/error-handling
- yarn dev로 했을 경우에는 화면에 바로 표시된다
- _error.js만들어서 커스텀 가능
    + 만약 404.js가 있다면 먼저 보여주고 없다면 커스텀 페이지(_error.js)를 보여준다
    + 예시
```
function Error({ statusCode }) {
  return (
    <p>
      {statusCode
        ? `An error ${statusCode} occurred on server`
        : 'An error occurred on client'}
    </p>
  )
}
 
Error.getInitialProps = ({ res, err }) => {
  const statusCode = res ? res.statusCode : err ? err.statusCode : 404
  return { statusCode }
}
 
export default Error
```

- Server side error와 같은 경우에는 404.js, 500.js와 같은 파일들을 통하여 에러 핸들링이 가능하다. Client side error와 같은 경우에는 Error Boundary설정을 통하여 가능하다
- Error Boundary - class component, fallback처럼 UI에서 에러를 먼저 만들어서 보여줄 수 있다

### React 심화 - 18version streaming
- 먼저 새 프로젝트 제작
```
% yarn create next-app server-components --example "https://github.com/vercel/next-react-server-components"
```
- 스켈레톤을 먼저 그리고 데이터를 불러오는 streaming 방식에 대한 예제
- 이전에는 컴포넌트 별로 서버사이드랑 클라이언트 사이드 각각 안되던 부분을 따로 된다는 내용


### Data Fetching API
1. getServerSideProps
    + return props, redirect, notfound
    + request할때마다 페이지가 pre-render된다
2. getStaticProps
    + return props, redirect, notfound, revalidate
3. getInitialProps
    + legacy
4. getStaticPaths
    + return paths or fallback(false, true, 'blocking')
    + preview / revalidate / process.cwd() - 파일 읽을때 사용

### Next Rounter
- https://nextjs.org/docs/pages/api-reference/functions/use-router
- router object
    + isReady가 true일때 query값을 가지고 있다고 할 수 있다
- router.push(url, as, options): 히스토리가 쌓이는 이동
- router.replace(url, as, options): 히스토리가 쌓이지 않는 이동
- router.prefetch: 미리 fetch해오기, yarn dev에서는 동작하지 않음, useEffect등에서 등록해놓으면 링크 클릭시 불러오지 않음
- router.back: 뒤로가기
- router.reload: 새로고침

## NextJS Configuration
- next.config.js파일을 만들어 놓고 여기서 설정
- document: https://nextjs.org/docs/app/api-reference/next-config-js
- Webpack, Babel, Typescript로 파싱이 되지 않으니 최신 js문법을 쓰면 안된다
- 어떤 설정이 없어도 nextjs는 잘 동작한다. 설정이 필수는 아니다
- 환경변수 설정이 가능
```
module.exports = {
  env: {
    customKey: 'my-value',
  },
}
```
- 페이지에서 이렇게 쓸 수 있다
```
function Page() {
  return <h1>The value of customKey is: {process.env.customKey}</h1>
}
 
export default Page
```
- basePath: export path를 수정할때 사용
```
module.exports = {
  basePath: '/docs',
}
```
- rewrites: source와 destination을 설정하여 path는 destination의 것을 보여주는데, 실제 내용은 source의 것을 보여준다
- redirect: source와 destination을 설정하여 path는 destination으로 이동


## E-Commerce project
- 프로젝트 생성
   + ESLint : yes
   + Tailwind CSS: yes
   + 'src' directory: no
   + App Router: no
   + customize the default import alias(@/*): no
```
% yarn create next-app react_commerce --typescript
```
- tsconfig.json 수정: compilerOptions에 추가
   + baseUrl
   + paths
```
  "compilerOptions": {
    "baseUrl": ".",
    "paths": {
      "@components/*": ["components/*"]
    }
  },
```
