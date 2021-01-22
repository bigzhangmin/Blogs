## 关于Puppeteer

> Puppeteer 是一个 Node 库，它提供了一个高级 API 来通过 [DevTools](https://zhaoqize.github.io/puppeteer-api-zh_CN/)) 协议控制 Chromium 或 Chrome。Puppeteer 默认以 [headless](https://developers.google.com/web/updates/2017/04/headless-chrome) 模式运行，但是可以通过修改配置文件运行“有头”模式。

Puppeteer 是 Node.js 工具引擎, 通过 Chrome DevTools Protocol 协议控制 Chromium/Chrome 浏览器的行为, 实现网页爬取, 自动化测试, 性能诊断等一系列的网页自动化的一些操作.

下面是一个简单的例子, 保存百度图片到本地.



## 安装

> 初始化package.json

在项目中使用 Puppeteer：

```bash
yarn add puppeteer
```



## 开始

目录结构

<ul>
	<li>
        product
        <ul>
            <li>node_modules</li>
            <li>
                src
                <ul>
                    <li>images</li>
                    <li>
                        utils
                    	<ul>
                            <li>saveimg.js</li>
                        </ul>
                    </li>
                    <li>app.js</li>
                </ul>
            </li>
            <li>package.json</li>
        </ul>
    </li>    
</ul>



## app.js

> app.js中的内容

```js
// 引入puppeteer
const puppeteer = require('puppeteer');
// 引入封装好的保存图片函数
const saveImg   = require('./utils/saveImg');
// 引入path模块
const path = require('path');

(async () => {
    // 创建浏览器实例
    const browser = await puppeteer.launch({
        // 关闭无头模式可以看到每一步执行的操作
        headless: false,
        // 每一步操作的延时
        slowMo: 500,
        // 打开浏览器控制台
        devtools: true
    });
    // 打开新的空白页
    const page = await browser.newPage();
    // 设置页面的宽高
    page.setViewport({
        width: 800,
        height: 600
    })
    // 跳转到页面
    await page.goto('https://image.baidu.com');
    // 将光标聚焦到输入框, 括号内是输入框的选择器, 和jQuery选择器同样用法
    await page.focus('#kw');
    // 在输入框种输入搜索内容
    await page.type('#kw', '蔡徐坤出道前');
    // 点击搜索按钮
    await page.click('.s_newBtn');
    // 页面加载完成后执行回调函数
    page.on('load', async function () {
        // page.evaluate(pageFunction) pageFunction函数可以在页面实例上下文中执行
        const source = await page.evaluate(async function() {
            // 在页面实例中就可以直接获取页面DOM元素
            const imgList = document.querySelectorAll('.main_img');
            // 获取图片data-imgurl 保存到数组中
            return [...imgList].map(el => el.getAttribute('data-imgurl'));
        })
        for(src of source){
            // 循环调用saveImg函数, 传入图片src和完整文件路径
            saveImg(src, path.resolve(__dirname, 'images'));
        }
        // 页面操作完成后关闭浏览器
        await browser.close();
    });
})();
```



## saveimg.js

```js
// 引入http和https模块
const http = require('http');
const https = require('https');
// 引入createWriteStream方法, 写入文件
const { createWriteStream } = require('fs');
const path = require('path');
// 初始图片数量
let qty = 0;

// 导出方法
module.exports = async function (url, dir) {
    qty+=1;
    await urlToImg(url, dir, qty);
}

// 定义保存图片的方法
const urlToImg = async (url, dir, qty) => {
    // 按图片地址分别使用http和https请求
    let mod = /^https:\/\//.test(url) ? https : http;
    // 使用path.extname方法获取图片格式后缀
    let ext = path.extname(url);
    // 图片保存路径加图片名, 使用时间戳加上文件数量作为图片名称
    let file = path.join(dir, `${Date.now()}-${qty}${ext}`);
    // 发送请求返回图片实例
    mod.get(url, res => {
        // 写入文件
        res.pipe(createWriteStream(file))
            // 写入完成后执行
            .on('finish', () => {
                console.log(`写入成功第${qty}张`);
            });
    });
}
```

## 运行代码

![image-20210122164431220](C:\Users\abc\AppData\Roaming\Typora\typora-user-images\image-20210122164431220.png)

异步请求所以保存顺序按写入顺序执行

![image-20210122164543995](C:\Users\abc\AppData\Roaming\Typora\typora-user-images\image-20210122164543995.png)

保存成功

![image-20210122164659303](C:\Users\abc\AppData\Roaming\Typora\typora-user-images\image-20210122164659303.png)