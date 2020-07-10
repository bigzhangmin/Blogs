## Node.js 实现服务端图片上传

### 1. 安装依赖

```shell
npm i express -s
npm i fs -s
npm i multer -s
```

### 2. 路由代码

```javascript
var express = require('express');
var router = express.Router();
var multer = require('multer');
var fs = require('fs');

// 使用硬盘存储模式设置存放接收到的文件的路径以及文件名
var storage = multer.diskStorage({
    destination: function (req, file, cb) {
        // 接收到文件后输出的保存路径（若不存在则需要创建）
        cb(null, 'upload/images/');
    },
    filename: function (req, file, cb) {
        // 将保存文件名设置为 时间戳 + 文件原始名，比如 151342376785-123.jpg
        cb(null, Date.now() + "-" + file.originalname);
        // res.end({res_code:'500'})
    }
});

var createFolder = function (folder) {
    try {
        // 测试 path 指定的文件或目录的用户权限,我们用来检测文件是否存在
        // 如果文件路径不存在将会抛出错误"no such file or directory"
        fs.accessSync(folder);
    } catch (e) {
        // 文件夹不存在，以同步的方式创建文件目录。
        fs.mkdirSync(folder);
    }
};

var uploadFolder = './upload/images';
createFolder(uploadFolder);

// 创建 multer 对象
var upload = multer({ storage: storage });

/* GET users listing. */
router.post('/', upload.single('file'), function (req, res) {
    console.log(req.file)
    var file = req.file;
    console.log('文件类型：%s', file.mimetype);
    console.log('原始文件名：%s', file.originalname);
    console.log('文件大小：%s', file.size);
    console.log('文件保存路径：%s', file.path);
    // 接收文件成功后返回数据给前端
    res.json({ res_code: '0', name: file.originalname, url: file.path });
});

module.exports = router;
```

