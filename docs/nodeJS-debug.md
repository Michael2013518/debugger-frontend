### 调试NodeJS项目

启动调试模式

方法一：Chrome DevTools调试nodejs项目

```
  node --inspect-brk ./index.js

  // node --inspect-brk=8888 ./index.js
```
--inspect: 调试模式启动

--inspect-brk: 调试模式启动并首行断住


打开chrome://inspect/#devices, 找到ws服务端, inspect后，断点调试；

方法二： VSCode Debug调试nodejs项目

.vscode添加launch.json调试配置

```
  {
      "name": "Launch Program",
      "program": "${workspaceFolder}/app.js",
      "request": "launch",
      "skipFiles": [
        "<node_internals>/**"
      ],
      "stopOnEntry": true,
      "type": "node"
    }
```



