# react 프로젝트를 electron으로 띄우기

지금 진행중인 cowket 프로젝트에 electron을 적용해보려고 하는데,
일단 electron사용법을 익혀보고자 테스트프로젝트를 만들었음.

### 정리

1. loadURL (2021.11.21)

아래의 블로그를 보고 따라했는데, 따라하다가 에러가 난 부분이있어서 적어보겠당

블로그에서 electron.js파일에 아래와 같이 적으라고 나와있었다.

```js
// main.js
const { app, BrowserWindow } = require("electron");
app.whenReady().then(() => {
  const win = new BrowserWindow();
  win.loadFile("http://localhost:3000");
});
app.on("window-all-closed", () => {
  app.quit();
});
```

그런데 이 코드를 실행해보니 리액트프로젝트는 켜지지만 일렉트론실행시 에러가났다.

에러내용은 파일의 경로를 찾을수가없다는 내용이었다.

일렉트론을 처음 접해봐서 그냥 무작정 따라했는데, `win.loadFile`메서드에 파일경로가 아닌 링크를 넣어주는것이 틀린것같아 공식문서를 찾아보니 아래처럼 나와있었다.

```js
// In the main process.
const { BrowserWindow } = require("electron");

const win = new BrowserWindow({ width: 800, height: 600 });

// Load a remote URL
win.loadURL("https://github.com");

// Or load a local HTML file
win.loadFile("index.html");
```

내가 사용해야하는 메서드는 `loadFile`이 아니라 `loadURL`이었다.

그래서 메서드를 변경해서 실행해보니 일렉트론이 잘 실행되었다.

> 참고한 블로그
> https://pks2974.medium.com/electron-%EC%97%90-react-%EC%A0%81%EC%9A%A9%ED%95%B4-%EB%B3%B4%EA%B8%B0-ebcea2bbbd27
