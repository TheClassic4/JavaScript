### hash模式

hash模式下，当url发生变化时，浏览器会记录下来，因此前进后退按钮都可以使用

因此在该模式下，即使浏览器没有请求服务器，页面也会和url一一对应起来
需要注意的是hash模式下修改的是#后面的内容，使用 URL 的 hash 来模拟一个完整的 URL，于是当 URL 改变时，页面不会重新加载。

```
            window.onhashchange = function() {

                document.getElementById("demo").innerHTML = x;    //更新页面内容

                ......

            };
```
### history模式

history 利用了 html5 history interface 中新增的 `pushState()` 和 `replaceState()` 方法。这两个方法应用于浏览器记录栈

在当前已有的 back、forward、go 基础之上，它们提供了对历史记录 修改的功能（pushState将传入url直接压入历史记录栈，replaceState将传入url替换当前历史记录栈）。

只是当它们执行修改时，虽然改变了当前的 URL ，但浏览器不会立即向后端发送请求

```
 pushState()、replaceState() 方法接收三个参数：stateObj、title、url

                history.pushState({color: "red"}, "red", "red")；//设置状态

                window.onpopstate = function(event) {  //监听状态

                     if(event.state && event.state.color === "red") {

                         document.body.style.color = "red";    //更新页面内容

                      }

                }

                // 改变状态  *在使用history API改变浏览器的url时，仍需要额外的步骤去触发 popstate 事件，例如调用 history.back() 和 history.forward() 等方法

                history.back();

                history.forward();
```

`history.go(-2);`

`history.go(2);`

`history.back();`

`history.forward();`

### history 对比  hash 

优势：

pushState 设置的 url 可以是同源下的任意 url ；而 hash 只能修改 # 后面的部分，因此只能设置当前 url 同文档的 url。

pushState 设置的新的 url 可以与当前 url 一样，这样也会把记录添加到栈中；hash 设置的新值不能与原来的一样，一样的值不会触发动作将记录添加到栈中。

pushState 通过 stateObject 参数可以将任何数据类型添加到记录中；hash 只能添加短字符串。

pushState 可以设置额外的 title 属性供后续使用。



劣势：

history 在刷新页面时，如果服务器中没有相应的响应或资源，就会出现404。因此，如果 URL 匹配不到任何静态资源，则应该返回同一个 index.html 页面，这个页面就是你 app 依赖的页面。

hash 模式下，仅 # 之前的内容包含在 http 请求中，对后端来说，即使没有对路由做到全面覆盖，也不会报 404。


[参考：](https://www.jianshu.com/p/3b4abc20ae0f)

