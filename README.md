Kotlin Ktor Responds 404 for Exception Issue Demo
=================================================

发现在[ktor](http://ktor.io)中有一个bug:

当Server端发生了Exception时，它返回给客户端的居然是`404`，而不是`500`。

Run `Hello.kt` in your IDE to start the server, then:

```
$ curl -I http://localhost:8080/
HTTP/1.1 404 Not Found
Content-Length: 0
```

显然是不合适的。已经提了Issue: <https://github.com/ktorio/ktor/issues/512>，等修复。
