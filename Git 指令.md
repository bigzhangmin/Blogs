## Git 常用指令

```shell
# 查看本地修改
git diff

# 撤销所有本地修改 '不可逆'
git checkout --
git checkout -- [fileName]

# 将工作区的文件标记为已暂存,保存在暂存区
git add .

# 查看暂存区的修改
git diff --staged

# 撤销暂存区修改
git reset .

# 将暂存区文件提交到本地仓库
git commit

# 查看历史提交
git log

# 切换到之前版本
git checkout <版本号>
```

