# npm

#### 常见命令

```
# 更新npm到最新
npm install npm@latest -g

# 更新到下一预览版本
npm install npm@next -g

# 本地安装
npm install lodash

# 安装到 package.json 文件中 dependencies
npm install lodash --save

# 安装到 package.json 文件中 devDependencies
npm install lodash --save-dev

# 全局安装
npm install -g express

# 更新依赖包
npm update lodash

# 更新全局依赖包
npm update -g express

# 删除依赖
npm uninstall lodash

# 删除全局依赖
npm uninstall -g express

# 从 package.json 文件中删除
npm uninstall --save lodash

# 搜索模块
npm search express

# 找模块文档
npm docs express

# 查看项目bug
npm bugs express

# 阅读源代码 必须在项目文件夹的根目录下运行，而且该模块必须已经被下载到了node_modules文件夹中
npm edit express

# 发布你的包
npm publish ccc

# 创建包标签
npm publish --tag beta

# 查看当前的配置信息
npm profile get
─────────────────┬───────────────────────────────────┐
│ name            │ masterton                         │
├─────────────────┼───────────────────────────────────┤
│ email           │ zhengcloud@foxmail.com (verified) │
├─────────────────┼───────────────────────────────────┤
│ two-factor auth │ disabled                          │
├─────────────────┼───────────────────────────────────┤
│ fullname        │ Masterton                         │
├─────────────────┼───────────────────────────────────┤
│ homepage        │                                   │
├─────────────────┼───────────────────────────────────┤
│ freenode        │                                   │
├─────────────────┼───────────────────────────────────┤
│ twitter         │                                   │
├─────────────────┼───────────────────────────────────┤
│ github          │ Masterton                         │
├─────────────────┼───────────────────────────────────┤
│ created         │ 2017-06-28T08:01:04.327Z          │
├─────────────────┼───────────────────────────────────┤
│ updated         │ 2019-09-20T10:25:16.669Z          │
└─────────────────┴───────────────────────────────────┘

# 设置配置信息
npm profile set name masterton
```

#### package.json 管理Node.js模块

```
# 初始化 package.json 文件
npm init
npm init --yes

# 设置配置选项
npm set init.author.email "wombat@npmjs.com"
npm set init.author.name "ag_dubs"
npm set init.license "MIT"

# 最小的package.json
{
    "name": "example01",
    "version": "0.1.1",
    "dependencies": {
        "underscore": "~1.2.1"
    }
}
```