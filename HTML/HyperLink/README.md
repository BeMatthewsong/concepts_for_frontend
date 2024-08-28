## a 태그는 속성들
```html
<!DOCTYPE html>
<html>
  <body>
    <a href="http://www.google.com">Visit google.com!</a>
  </body>
</html>
```
### href (경로)
1. 절대 URL:	웹사이트 URL (href=”http://www.example.com/default.html”)
2. 상대 URL:	자신의 위치를 기준으로한 대상의 URL (href=”html/default.html”)
3. fragment identifier:	페이지 내의 특정 id를 갖는 요소에의 링크 (`href=”#top”`)
4. 메일:	`mailto:`
5. script:	href=”javascript:alert(‘Hello’);”

```html
<!DOCTYPE html>
<html>
  <body>
    <a href="http://www.google.com">URL</a><br>
    <a href="html/my.html">Local file</a><br>
    <a href="file/my.pdf" download>Download file</a><br>
    <a href="#">fragment identifier</a><br>
    <a href="mailto:someone@example.com?Subject=Hello again">Send Mail</a><br>
    <a href="javascript:alert('Hello');">Javascript</a>
  </body>
</html>
```

### target (target 어트리뷰트는 링크를 클릭했을 때 윈도우를 어떻게 오픈할 지를 지정한다)
1. _self	링크를 클릭했을 때 연결문서를 현재 윈도우에서 오픈한다 (기본값)
2. _blank	링크를 클릭했을 때 연결문서를 새로운 윈도우나 탭에서 오픈한다

```html
<!DOCTYPE html>
<html>
  <body>
    <a href="http://www.google.com" target="_blank" rel="noopener noreferrer">Visit google.com!</a>
  </body>
</html>
```
