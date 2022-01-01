# VSCode Extensions 정리

## 1. ``SynthWave '94`` 스타일 커스터마이징

``SynthWave '94`` 는 ``VSCode Theme`` 입니다.

``Neon`` 효과를 가지는 유일한 테마지만, ``VSCode API`` 를 사용한 테마 커스터마이징이 적용되지 않는 문제가 있습니다.

문제가 되는 스타일 커스터마이징은 ``줄번호 영역 배경색`` 입니다.

* ``editorGutter.background``

<br />

아래의 코드는 ``VSCode settings.js`` 파일에서 ``SynthWave '94`` 테마를 커스터마이징 한 예시 입니다.

그리고 ``editorGutter.background`` 가 적용되지 않는 상태 입니다.

```json
// .vscode/settings.json

{
  // ... 생략

  "workbench.colorCustomizations": {
    // Synthwave 84 테마 커스텀
    "[SynthWave '84]": {
      // 줄번호 영역 배경색❌
      "editorGutter.background": "#ff1493",
      
      // 에디터 배경색⭕
      "editor.background": "#000",
      // 좌측 Hierarchy 영역 배경색⭕
      "sideBar.background": "#000",
      // 터미널 영역 배경색⭕
      "panel.background": "#000",
      // 상단 메뉴, 우클릭 메뉴 배경색⭕
      "menu.background": "#000000f0",
      // 상단탭 (파일명) 의 빈공간 배경색⭕
      "editorGroupHeader.tabsBackground": "#ffffff07",

      // 커서가 있는 줄번호 폰트색⭕
      "editorLineNumber.activeForeground": "#ffff00"
    }
  }
}
```

이슈가 발생한 버전은 다음과 같습니다.
* ``v0.1.10``

<img src="./readmeAssets/image%201.png"><br />

<br />

위의 ``editorGutter.background`` 를 커스터마이징 하기 위해서는, ``.AppData`` 의 ``VSCode`` 확장 파일을 수정해야 합니다.

수정할 파일경로는 다음과 같습니다.

```bash
C:\Users\{사용자명}\AppData\Local\Programs\Microsoft VS Code\resources\app\out\vs\code\electron-browser\workbench\neondreams.js
```

<br />

위의 파일에서 수정할 것은 다음과 같습니다.

* ``background-color`` 검색 (``1개 존재``)
* ``background-color`` 색상 변경
* 바로 아래줄에 있는 ``background-image`` 삭제

<br/>

위와같이 수정하면 ``background-color`` 에 지정한 색상이 ``줄번호 영역 배경색`` 에 반영됩니다.

하지만, ``VSCode`` 의 ``settings.json`` 에서 ``editorGutter.background`` 는 여전히 적용되지 않으므로, 위의 방법으로 수정해야 합니다.

아래코드는 ``neondreams.js`` 의 커스터마이징 코드 입니다.

```javascript
// C:\Users\{사용자명}\AppData\Local\Programs\Microsoft VS Code\resources\app\out\vs\code\electron-browser\workbench\neondreams.js

// ... 생략 ...

/* Add the subtle gradient to the editor background */
.monaco-editor {
  /* 
   * editorGutter 색상 커스터마이징
   * - background-color 변경
   * - background-image 삭제
   * 
   * 원본
   * - 아래의 원본이 없으면, 다른 테마에서 ``줄번호 영역`` 색상반영❌
  background-color: transparent !important;
  background-image: linear-gradient(to bottom, #2a2139 75%, #34294f);
   */
  background-color: #101010 !important;
  background-size: auto 100vh;
  background-position: top;
  background-repeat: no-repeat;
}

// ... 생략 ...
```

<br />

커스터마이징을 한 후, VSCode 를 ``재시작`` 하면 커스터마이징이 반영된 것을 확인할 수 있습니다.

<img src="./readmeAssets/image%203.png"><br />

<br />

* 참고: https://github.com/robb0wen/synthwave-vscode/issues/199

<img src="./readmeAssets/image%204.png" width="700px"><br />

<img src="./readmeAssets/image%205.png" width="700px"><br />
