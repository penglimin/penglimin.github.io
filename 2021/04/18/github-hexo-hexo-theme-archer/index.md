### 安装hexo

1.终端：
npm install -g hexo

2.找个目录放你的博客
eg：
/Users/xxx/blogs

3.cd  /Users/xxx/blogs
4.hexo init

生成文档
5. hexo g
部署dexo项目
6.   hexo s 

到此 hexo 已经本地部署

http://localhost:4000
看到默认的 主题


### 修改主题

下载你喜欢的主题
下载到 themes 文件夹下

eg：
git clone https://github.com/fi3ework/hexo-theme-archer.git themes/archer

去看项目依赖的  
`
npm i hexo-generator-json-content --save && npm i --save hexo-wordcount && git clone https://github.com/fi3ework/hexo-theme-archer.git themes/archer --depth=1
`

详细看 readme：
https://github.com/fi3ework/hexo-theme-archer


更换完主题
hexo clean
hexo g
hexo s

在访问 http://localhost:4000
你的主题就来了。。。


### github  上创建仓库 xxxx.github.io
自己研究一下先，回头我补一下博客。
不会的话 加 qq： 1463523968

### 将github上的 仓库地址，配置到。_config.xml
`
deploy:
  type: git
  repository: https://github.com/penglimin/penglimin.github.io.git
  branch: master
 `
 

### 将hexo 生成的blog 推送到 github上。
先安装插件：npm install hexo-deployer-git --save
终端：
hexo d




