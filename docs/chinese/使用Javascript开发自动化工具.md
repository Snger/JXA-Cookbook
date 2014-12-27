最简单的方式
---------------

直接打开脚本编辑器。（位于Application > Utilities中的Apple Script Editor程序）


在互动模式中运行
---------------------------

```javascript
osascript -il JavaScript
```

- `-i` 表示互动模式
- `-l JavaScript` 指定使用 javascript


创建指定脚本解释器的文件
-------------------------

```javascript
#!/usr/bin/env osascript -l JavaScript

function run(argv) {
  console.log(JSON.stringify(argv))
}
```


创建一个 Mac OS X 服务
---------------------------

`服务`是 Mac OS X 系统中便于使用的自动化工作流。当你创建一个服务，他将显示在菜单栏中的`服务`项中。例如，你可以在创建一个[使用 javascript 批量替换文件名的服务项](https://gist.github.com/dtinth/93e230152a771dcb1ec5)。

打开 __Automator.app__ 然后创建 "服务". 拖动 "Run JavaScript" 选项, 在编辑框中加入代码.

![](http://i.imgur.com/3HdAbIU.png)


从脚本中调用
-------------------------------

脚本可以使用 `osascript` 命令行任意调用 javascript 的自动化代码。

```bash
osascript -l JavaScript -e 'Application("iTunes").currentTrack.name()'
```

The result of the last statement will be printed out, similar to when you call `eval()`.
最后声明的结果将会被打印出来，就像使用 `eval()` 调用一样。
