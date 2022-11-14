### 调试Vue项目

@vue/cli创建的webpack做为构建工具项目

#### 安装@vue/cli

```
  yarn global add @vue/cli
```

Vue3模版

调整webpack的devtool配置

```
  const { defineConfig } = require('@vue/cli-service')
  module.exports = defineConfig({
    configureWebpack(config) {
      config.devtool = 'source-map'
    }
  })
```

Vue2模版

.vscode的launch.json配置调整

```
  {
    "type": "chrome",
    ...
    "sourceMapPathOverrides" : {
      "webpack://vue-demo/src/*" : "${workspaceFolder}/src/*"
    }
  }

```

#### 调试create vue创建的vite项目

调整.vscode的launch.json配置

```
  {
    "type": "chrome",
    "request": "launch",
    "name": "调试 vite 项目",
    "runtimeExecutable": "canary",
    "runtimeArgs": [
        "--auto-open-devtools-for-tabs"
    ],
    "userDataDir": false,
    "url": "http://localhost:5174",
    "webRoot": "${workspaceFolder}/aaa"
}
```