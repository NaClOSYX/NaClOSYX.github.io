
使用node版本 20

## 命令
```bash
hexo g   # 生成页面
hexo s   # 启动预览
hexo clean   # 清空打包文件
```
## 更新
```bash
# 全局安装更新检查工具
npm install -g npm-check-updates
# 检查可更新的依赖
ncu
# 更新 package.json 中的版本号
ncu -u
# 安装更新后的依赖
npm install
```
# 加密设置
文章顶部Front-matter 添加 password: xxxx

