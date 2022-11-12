## 前端调试

示例：launch

```
{
  "configurations": [
    {
      "name": "Launch Chrome",
      "request": "launch",
      "type": "chrome",
      "url": "http://localhost:8080",
      "webRoot": "${workspaceFolder}",
      "runtimeExecutable": "canary",
      // "--incogninto" :无痕模式启动，不加载插件
      "runtimeArgs": ["--auto-open-devtools-for-tabs"],
      "sourceMapPathOverrides": {
        "webpack://?:*/*": "${workspaceFolder}/*"
      },
      "file": "${worksspaceFolder}/index.html",
      "userDataDir": "/Users/michael/code"
    }

  ]
}
```

示例： attach

```
{
  "configurations": [
    {
      "name": "attach to Chrome",
      "request": "attach",
      "type": "chrome",
      "webRoot": "${workspaceFolder}"
    }

  ]
}
```
说明：

. launch：调试模式启动浏览器，访问某个 url，然后连上进行调试
. attach：连接某个已经在调试模式启动的 url 进行调试
. userDataDir： user data dir 是保存用户数据的地方，比如浏览历史、cookie 等，一个数据目录只能跑一个 chrome，所以默认会创建临时用户数据目录，想用默认的目录可以把这个配置设为 false
. runtimeExecutable：切换调试用的浏览器，可以是 stable、canary 或者自定义的
. runtimeArgs：启动浏览器的时候传递的启动参数
. sourceMapPathOverrides：对 sourcemap 到的文件路径做一次映射，映射到 VSCode workspace 下的文件，这样调试的文件就可以修改了
. file：可以直接指定某个文件，然后启动调试

### SourceMap

sourcemap格式：
```
{
　　　　version : 3,
　　　　file: "out.js",
　　　　sourceRoot : "",
　　　　sources: ["foo.js", "bar.js"],
　　　　names: ["a", "b"],
　　　　mappings: "AAgBC,SAAQ,CAAEA;AAAEA",
      sourcesContent: ['const a = 1; console.log(a)', 'const b = 2; console.log(b)']
}
```
version：sourcemap 的版本，一般为 3

file：编译后的文件名

sourceRoot：源码根目录

names：转换前的变量名

sources：源码文件名

sourcesContent：每个 sources 对应的源码的内容

mappings：一个个位置映射

这种编码叫VLQ编码，可参考：https://www.ruanyifeng.com/blog/2013/01/javascript_source_map.html

[Webpack的soucemap配置](./docs/webpack-config.md)