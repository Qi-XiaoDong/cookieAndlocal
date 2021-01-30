# cookieAndlocal

cookie 存储 和本地存储

## cookie

> 1. 关联同一地址多次请求(**请求自动携带，不要滥用**)
> 2. set-cookie: 服务器设置
> 3. 不可跨域，**domain可以**
> 4. 数量(50条)和大小(4kb)的限制
> 5. 存储时间特别灵活
> 6. 前端可以设置cookie(**document.cookie**) key=value, 每次只能设置一个
> 7. **基于http协议**生效

- 为什么需要cookie？

1. http：上下文无关，无状态的协议(**同一个地址多次的请求是没有关联的**)

- cookie 属性

> 1. name: cookie的名字，具有唯一性

> 2. value: cookie的值

> 3. domain: 设置cookie在那个域名下生效

> 4. path: cookie有效路径(指定的url下使用改cookie)

> 5. expires: 过期时间(**默认为会话期**传递的时刻)

```js
  // cookie日期存储格式 GMT: 格林威治 new Date();
  // 设置过期的时间可以删除该条cookie
```

> 6. max-age: cookie过期时间(传递的时间)

```js
  // -1: 过期的cookie
  // 0： 结束的cookie
  // 正数： 存过的时间段
```
> 其他三个属性

```js
  // 1. httpOnly: 有这个标记的cookie，前端无法获取
  // 2. Secure: 这是cookie 只可以通过https协议传输
  // SameSite： 跨域请求时cookie不被发送
```
