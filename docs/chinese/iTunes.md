播放暂停与停止
--------------------


```javascript
Application('iTunes').play()
Application('iTunes').pause()
Application('iTunes').stop()
```


获取当前曲目的播放到第几秒
-------------------------

```javascript
Application('iTunes').playerPosition()
//    => 12.345678993460083 (seconds)
```


获取当前播放曲目的数据
---------------------------------------------------------------------

__第一个例子：__

```javascript
var track = Application('iTunes').currentTrack
//    => Application("iTunes").currentTrack

track.name()
track.artist()
track.album()
track.duration()
```

__第二个例子：__

```javascript
var track = Application('iTunes').currentTrack()
//    => Application("iTunes").sources.byId(73).userPlaylists.byId(2090).fileTracks.byId(2093)

track.name()
track.artist()
track.album()
track.duration()
```

请注意 `currentTrack` 后面的 `()` 。两个例子都有效，那么（在行为上）有什么区别呢？

第一个例子把当前曲面存储在指定的 __对象字面量__ （变量）中；这相当于把这个变量指向正在播放的歌曲。这也意味着 `track.name()` 总会返回当前正在播放的歌曲名。

第二个例子实际上访问的是属性，于是将返回曲目的对象。即使切换歌曲后， `track` 变量依旧指向之前调用  `.currentTrack()` 时播放的歌曲。

同步已连接的设备(iPhone/iPod/iPad)
---------------------------------------------
在测试下面代码前，请先阅读 [[Security|System-Events#security]] 。因为有些步骤需要先操作才能确保下面这些代码能够成功执行。另外，请确定 iTunes 已经打开。

```javascript
var itunes = Application('iTunes')
itunes.activate()

var se = Application('System Events')
var proc = se.processes.byName('iTunes')
var fileMenu = proc.menuBars[0].menuBarItems.byName('File')
var devicesMenu = fileMenu.menus[0].menuItems.byName('Devices')
var items = devicesMenu.menus[0].menuItems()

// The menu item name here is dynamic, so using byName() will not work
// The menu item will only be enabled if a *single* device is plugged in and it is not busy
for (var i = 0, j < items.length; i < j; i++) {
    if (items[i].enabled() && /^Sync /.test(items[i].title())) {
        items[i].click()
    }
}
```
