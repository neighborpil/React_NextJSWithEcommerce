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
 


