### 使用Charles调试https

[Charles官网下载](https://www.charlesproxy.com/)

安装根证书

1. 点击 help > SSL Proxying > Install Charles Root Certificate，安装到系统的钥匙串中，改为：始终信任

2. 在请求的URL地址上，右键，勾选breakpoints，开启断点，刷新页面，断电会生效；

3. 对请求内容和响应(URL, Headers, Cookies, Text)进行编辑，点击 "Execute"

对请求更细粒度的控制可以使用 SwitchyOmega 插件（chrome）

SwitchyOmega 插件

proxy - 情景模式

```
  代理协议  代理服务器    代理端口
  https    127.0.0.1    8888
```

auto switch - 情景模式

```
  条件类型    条件设置    情景模式
  域名通配符  *juejin*    proxy
```

方法一：

在报错的脚本右键，“Add source map”，添加sourcemap的URL地址， 地址可以通过""npx http-server"启动dist目录web服务。

方法二：

Charles: Proxy > Breakpoint Setrings,添加对test.com的dist/index.js响应的断点，强制刷新页面，Charles断住；

在“Edit Response” 添加soucemap的关联，如：//#sourceMappingURL=http://test.com:8888/dist/index.js.map

VS Code通过添加.vscode/launch.json的调试的源码处断住；