# React_NextJSWithEcommerce

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
- 
