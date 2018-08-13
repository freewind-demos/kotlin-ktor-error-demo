Kotlin Ktor Responds 404 for Exception Issue Demo
=================================================

发现在[ktor](http://ktor.io)中<s>有一个bug</s>:

当Server端发生了Exception时，它返回给客户端的居然是`404`，而不是`500`。

Run `Hello.kt` in your IDE to start the server, then:

```
$ curl -I http://localhost:8080/
HTTP/1.1 404 Not Found
Content-Length: 0
```

显然是不合适的。已经提了Issue: <https://github.com/ktorio/ktor/issues/512>，等修复。

---

Update:

感谢@cy6erGn0m指出是我的用法有问题，因为`curl -I`发送的是`HEAD`请求，而不是`GET`，当然是`404`。

正确写法是：

```
curl -D - http://localhost:8080/
```

详情请看: https://github.com/ktorio/ktor/issues/512

我觉得还是[httpie](https://httpie.org/)更友好一点：

```
$ brew install httpie
$ http http://localhost:8080/
HTTP/1.1 500 Internal Server Error
Connection: keep-alive
Content-Length: 0
```

同时服务器端会提示错误：

```
ERROR ktor.application - Unhandled: GET - /
java.lang.Exception: test
	at example.HelloKt$main$server$1$1$1.doResume(Hello.kt:12)
```

说明ktor的处理是正常的。