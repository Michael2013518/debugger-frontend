## Webpack的sourcemap配置

soucemap的配置：

. eval-nosources-cheap-module-source-map

. hidden-source-map

webpack通过正则(如下)，组合为不同的配置项

```
^(inline-|hidden-|eval-)?(nosources-)?(cheap-(module-)?)?source-map$
```

eval的特性(如下)，浏览器已支持该特性，eval代码的最后加上//# sourceURL=xxx，会以 xxx 为名字把这段代码加到 sources 里，以此可以打断点;sourceMappingUrl可以关联源码

```
eval(`
  function getURLParameters(url) {
  return (url.match(/([^?=&]+)(=([^&]*))/g) || []).reduce(
    (a, v) => (
      (a[v.slice(0, v.indexOf('='))] = v.slice(v.indexOf('=') + 1)), a
    ),
    {}
  )};
  console.log(getURLParameters(location.href));
  //# sourceURL=michael.js
  //# sourceMappingURL=xxx
`)
```

如果要高度定制option、module、noSource，可以使用SourceMapDevToolPlugin插件

说明：

eval：浏览器 devtool 支持通过 sourceUrl 来把 eval 的内容单独生成文件，还可以进一步通过 sourceMappingUrl 来映射回源码，webpack 利用这个特性来简化了 sourcemap 的处理，可以直接从模块开始映射，不用从 bundle 级别。

cheap：只映射到源代码的某一行，不精确到列，可以提升 sourcemap 生成速度

source-map：生成 sourcemap 文件，可以配置 inline，会以 dataURL 的方式内联，可以配置 hidden，只生成 sourcemap，不和生成的文件关联

nosources：不生成 sourceContent 内容，可以减小 sourcemap 文件的大小

module： sourcemap 生成时会关联每一步 loader 生成的 sourcemap，可以映射回最初的源码