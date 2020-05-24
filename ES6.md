## ES6语法记录

### Object.assign：实现拷贝继承

```js
//Object.assign 就是进行对象的浅拷贝
    var source={ age:18,height:170,className:"3年2班" }

    //克隆一个新对象出来
    var newObj=Object.assign({},source);
    console.log(newObj);

    var newObj2={};
    Object.assign(newObj2,source);
    console.log(newObj2);
```

上面可以实现浅拷贝，但是代码有点多，es6这个对象扩展，牛掰的一个方法，解决浅拷贝的问题，

```
var car={ brand:"BMW",price:"368000",length:"3米" }

    //克隆一个跟car完全一样的对象出来：
    var car2={ ...car }  
    console.log(car2); 

    //新车子，跟car的长度不同，其他相同
    var car3={ ...car,length:"4米" }  
    console.log(car3);

    var car4={ ...car,type:"SUV"}
    console.log(car4);

    var car5={...car4,price:"69800",brand:"BYD"};
    console.log(car5);
```

对象扩展，简单方便，代码更加简介，更少的代码实现更强大的功能。

### **Promise**

> Promise是异步编程一种解决方案(回调地狱)

```
在没有promise都是这样写的回调，一层一层的写，$.get("/getUser",function(res){
        $.get("/getUserDetail",function(){
            $.get("/getCart",function(){
                $.get("/getBooks",function(){
                    //...
                })
            })
        })
    })
```

promise的基本用法

```
var promise=new Promise((resolve,reject)=>{
        //b 把需要执行的异步操作放在这里
        $.get("/getUser",res=>{
            //获取数据的异步操作已经执行完毕了，等待下一步的执行，通过执行resolve函数，告诉外界你可以执行下一步操作了
            //c、
            resolve(res)
            //而执行的下一步操作，其实就是写在then的回调函数中的
        })
    })
    //a、
    promise.then(res=>{
        //d、执行后续的操作
        console.log(
        res);
    })
```

promise实现多层回调

```
new Promise((resolve,reject)=>{
        $.get("/getUser",res=>{
            resolve(res)
        })
    }).then(res=>{
        //用户基本信息
        return new Promise(resolve=>{
            $.get("/getUserDetail",res=>{
                resolve(res)
            })
        })
    }).then(res=>{
        //用户详情
        return new Promise(resolve=>{
            $.get("/getCart",res=>{
                resolve(res)
            })
        })
    }).then(res=>{
        //购物车信息
    })
```

promise实现错误处理

```
new Promise((resolve,reject)=>{
        $.ajax({
            url:"/getUser",
            type:"GET",
            success:res=>{
                resolve(res);
            },
            error:res=>{
                reject(res)
            }
        })
    }).then(resSuccess=>{
        //成功的返回值
    },resError=>{
        //失败的返回值
    })
```