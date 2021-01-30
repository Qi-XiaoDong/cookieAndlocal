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

### cookie 封装

```js
   <script>
    /**
     * 封装cookie增删改查
     */
    var cookieApi = {
      /**
       * 设置cookie
       */
      setCookie(name, value, date){
        /**
         * expires:设置的是一个时刻 GTML格式
        */
        // var endDate = new Date(); // 当前的时刻
        // endDate.setDate(endDate.getDate() + date);
        // document.cookie = name + "=" + value + "; expires=" + endDate;
        /**
         * max-age : 设置的是一个时间段毫秒为单位
         * **/
        document.cookie = name + "=" + value + "; max-age=" + date;
      },
      /**
       * 删除cookie
      */
      removeCookie(name){
        this.setCookie(name, "", 0);
      },
      /***
       * 获取cookie
      */
      getCookie(name){
        var cookieStr = document.cookie;
        var cookieArr = cookieStr.split("; ");
        const cookieObj = {};
        for (var i = 0; i < cookieArr.length; i++){
          const cookie = cookieArr[i].split("=");
          // 不传递name：表示获取所有的cookie
          if (!name) {
            cookieObj[cookie[0]] = cookie[1];
          }
          // 获取某一个cookie
          if (name === cookie[0]) {
            cookieObj[name] = cookie[1];
            break;
          }
        }
        return cookieObj;
      },
      /**
        * 获取全部cookie
      */
        getAllCookie(){
          return this.getCookie();
        }
    }
  </script>

````

## 存储 (Storeage内置对象**不依赖于http协议**)

- 优势

> 1. 存储量大
> 2. 不会随请求发送，节省资源
> 3. 有原生的Api进行怎删改查
> 4. 不能跨域**和cookie一样**
> 5. 无痕模式可删除本地存储

- LocalStorage: 本地的存储，域名下所有的页面有效

- sessionStore: 会话存储，仅在当前窗口有效

- 属性和方法

- - length：本地数据存储的数量

- - key(): 通过索引去找到存储的数据

- - getItem(): 通过键名取到存储的数据

- - setItem(): 设置一个本地存储数据

- - removeItem()： 删除指定键名的本地数据

- - clear(): 清空本地数据

### 存储注意

> 会将引用值转换为字符串存储

```js
  var colorArr = ["red", "green"]

  var colorObj = {"red" : "#f00", "block": "#000"};

  localStorage.setItem("color", JSON.stringify(colorObj));

  localStorage.getItem("color");

```
