**1、super 是干嘛用的？在 Python2 和 Python3 使用，有什么区别？为什么要使用 super？请举例说明。**

答：

super 用于继承父类的方法、属性。
super 是新式类中才有的，所以 Python2 中使用时，要在类名的参数中写 Object。Python3 默认是新式类，不用写，直接可用。
使用 super 可以提高代码的复用性、可维护性。修改代码时，只需修改一处。
代码举例：
```python
class baseClass:
 def test1(self, num):
 print(num)

class sonClass(baseClass):
 def test2(self):
 super().test1(num)

son = sonClass()
son.test1(11)
``` 
**2、阅读以下代码，推导最后结果：**

```python
def add(n, i):
 return n+i

def test():
 for i in range(4):
 yield i

g = test()

for n in [1, 10, 5]:
    g = (add(n, i) for i in g)

print(list(g)) # 结果是 [15, 16, 17, 18] 
```
**答： 所有的结果都是生成器表达式，不调用它，不从里面取值，就不干活。附上我的推导过程：**

``` python
n = 1
g = (add(n,i) for i in test())
# print(list(g))    # [1, 2, 3, 4]

n = 10
g = (add(n,i) for i in (add(n,i) for i in test()))
# print(list(g))    # [20, 21, 22, 23]

n = 5
g = (add(n,i) for i in (add(n,i) for i in (add(n,i) for i in test())))
g = (add(n,i) for i in (add(n,i) for i in (5,6,7,8)))
g = (add(n,i) for i in (10,11,12,13))

g = (15,16,17,18)
print(list(g)) # [15, 16, 17, 18] 
```
**3、快速编写前端 HTML、JavaScript、Vue 代码**。

答：
```javascript
HTML、JavaScript 代码:
<!DOCTYPE html>
<html lang="en">
<head>
 <meta charset="utf-8">
</head>
<body>
 <h1 id="title">xxx公司</h1>
 <p>xxx公司是一家......</p>

 <div id="mybox">
 <h1>{{a}}</h1>
 <input type="button" value="按我" v-on:click="add()">
 </div>
 <script type="text/javascript" src="public/bundle.js"></script>
</body>
</html>
<script>
 var title =  document.getElementById("title");
    title.onclick = function() {
        alert('我爱xxx公司，祝我面试成功');
 }
</script>
```

Vue 代码编写：
```javascript
import Vue from "vue";
new Vue({
    el : "#mybox",
    data : {
        a : 100
 },
    methods : {
        add : function(){
        this.a ++;
      }
   }
}); 
```
**4、L = [1, 2, 3, 11, 2, 5, 3, 2, 5, 3]，用一行代码得出 [11, 1, 2, 3, 5]**

**答： list(set(L))**


**5、L = [1, 2, 3, 4, 5]，L[10:]的结果是？**

答： 空列表(当时有点紧张，一直在“空列表”和“索引超出范围”两个答案之间徘徊）。

**6、L = [1, 2, 3, 5, 6]，如何得出 '12356'？**

答： 注意，个人觉得这个题有坑，列表的元素不是字符串，所以不能 ''.join(L)。以下是过程：

```python
s = '' 
for i in L: 
    s = s + str(i)
print(s) # 12356
print(type(s)) # <class 'str'>
 ```
**7、列表和字典有什么区别？**

答： 一般都是问列表和元组有什么不同。   
（1）获取元素的方式不同。列表通过索引值获取，字典通过键获取。   
（2）数据结构和算法不同。字典是 hash 算法，搜索的速度特别快。   
（3）占用的内存不同。

**8、如何结束一个进程？**

答：（1）调用 terminate 方法。   
（2）使用 subProcess 模块的 Popen 方法。

**9、进程、线程有什么区别？什么情况下用进程？什么情况下用线程？**

答：  
（1）区别：

① 地址空间和其它资源（如打开文件）：进程之间相互独立，同一进程的各线程之间共享。某进程内的线程在其它进程不可见。
② 通信：进程间通信 IPC，线程间可以直接读写进程数据段（如全局变量）来进行通信——需要进程同步和互斥手段的辅助，以保证数据的一致性。
③ 调度和切换：线程上下文切换比进程上下文切换要快得多。
④ 在多线程操作系统中，进程不是一个可执行的实体。
（2）使用场景：同时操作一个对象的时候，比如操作的是一个全局变量，我用线程，因为全局变量是所有线程共享的。

**10、什么是ORM？为什么要用ORM？不用ORM会带来什么影响？**

答：

ORM 框架可以将类和数据表进行对应，只需要通过类和对象就可以对数据表进行操作。
通过类和对象操作对应的数据表，类的静态属性名和数据表的字段名一一对应，不需要写 SQL 语句。
ORM 另外一个作用，是根据设计的类生成数据库中的表。
**11、写一段代码，ping 一个 ip 地址，并返回成功、失败的信息。**

答： 使用 subProcess 模块的 Popen 方法(使用简单，具体用法，这里不展开)。

**12、说说接口测试的流程，介绍一下request有哪些内容。**

答：（1）流程：获取接口文档，依据文档设计接口参数，获取响应，解析响应，校验结果，判断测试是否通过。 （2）request 内容：

封装了各种请求类型，get、post 等；
以关键字参数的方式，封装了各种请求参数，params、data、headers、token 等；
封装了响应内容，status_code、json()、cookies、url 等；
session 会话对象，可以跨请求。
**13、UI 自动化，如何做集群？**

答： Selenium Grid。

**14、移动端 UI 自动化，经常会自动安装 2 个程序，你知道那两个程序是什么东西不？**

答： 守护精灵，和 Python 并发编程中的 daemon 原理一样，父进程/父线程的代码执行完毕，它就终止，要写在 start 方法前面。另外，要找到配置文件，注释掉两行代码。

**15、说5个以上 Linux 命令。**

答：一口气，劈里啪啦说了 10 多个 。

**16、介绍一下你在这个项目中是如何使用 Jenkins 的。**

答：用的不深入，说了基本操作，比如定时构建执行代码。

**17、说说你对敏捷模式的认识。**

答：小步快跑，拥抱变化。测试中，可以通过行为驱动测试，有个框架 lettuce 可以用。