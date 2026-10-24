# mzr6.com 博客（Hugo + LoveIt + Cloudflare Pages）

主题：LoveIt（dillonzq/LoveIt），需 Hugo extended + Dart Sass。

## 本地预览

```bash
export PATH="$HOME/workspace/blog/tools/dart-sass:$PATH"
hugo server -D
```

## Cloudflare Pages 接入（上线时）

1. 把本目录推到 GitHub 仓库
2. Cloudflare Dashboard → Workers & Pages → Create → Pages → Connect to Git
3. 构建设置：
   - Framework preset: Hugo
   - Build command（LoveIt 需要 Dart Sass，Pages 镜像里没有，先下载再构建）：
     `curl -sL -o ds.tar.gz https://github.com/sass/dart-sass/releases/download/1.106.1/dart-sass-1.106.1-linux-x64.tar.gz && tar xzf ds.tar.gz && export PATH="$PWD/dart-sass:$PATH" && hugo --minify`
   - Build output directory: `public`
   - 环境变量：`HUGO_VERSION = 0.168.0`
4. 预览阶段先用 Pages 自带的 `*.pages.dev` 域名访问；
   DNS 从 Porkbun 迁到 Cloudflare 后，再在 Pages 里绑定自定义域名 `mzr6.com`。

## 写文章

在 `content/posts/` 下新建 Markdown 文件，front matter 参考 `welcome.md`。
提交并 push 后，Pages 自动构建上线。
