登录和退回帐号
---------------------------

使用提定服务（或进程）对象的 `logIn()` 和 `logOut()` 方法。（以登录或退出 `Messages` 作为例子的）具体的实现是：在 `Application('Messages')` 实例中反复使用 `services` 属性的 `name()` 方法进行判断。需要注意的是：如果如果系统服务用相同的 `name`，将不能如预期般执行。

This is a shell script that can log in or out of a service name. Usage: `./thescript 'Service Name' out` or `in` to log in.
下面的代码的作用是登录和退出系统服务。使用方法：执行 `./thescript 'Service Name' out` 或者 `in`

```javascript
#!/usr/bin/osascript -l JavaScript
ObjC.import('stdlib')
ObjC.import('Foundation')

var i, len
var args = $.NSProcessInfo.processInfo.arguments // NSArray
var lastArg = ObjC.unwrap(args.lastObject).toLowerCase() // -[args lastObject]
var serviceName = ObjC.unwrap(args.objectAtIndex(args.count - 2)) // -[args objectAtindex:[args count] - 2]

// There should always be at least 5 arguments: osascript, -l, JavaScript, NAME_OF_SERVICE, out/in
if (args.count < 5 || (lastArg !== 'out' && lastArg !== 'in')) {
    console.log('Usage: ' + ObjC.unwrap(args.firstObject) + ' NAME_OF_SERVICE "out|in"')
    $.exit(1)
}

var app = Application('Messages')
var service
for (i = 0, len = app.services.length; i < len; i++) {
    if (app.services[i].name() === serviceName) {
        service = app.services[i]
        break
    }
}

if (!service) {
    console.log('Service with name "' + serviceName + '" not found')
    $.exit(1)
}
if (lastArg === 'out') {
    service.logOut()
}
else {
    service.logIn()
}

// Suppress last result output
$.exit(0)
```
