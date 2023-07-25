## hexo 博客使用说明

## 能力要求

自建博客需要一定的相关知识，在开始前，请务必确保：

已掌握 markdown 语法

已阅读 Hexo 官方文档

会使用终端（命令行），会使用 git

会阅读文档、搜索文档

为了更好地使用，还建议掌握以下知识：

规范地使用 GitHub Issues（解决文档中没有的问题）

GitHub Fork、Pull Request 操作（使主题保持更新）



## 1 网站图标

### 2 设置导航栏

![1595653359743](C:\Users\luyunxiao\AppData\Roaming\Typora\typora-user-images\1595653359743.png)

````javascript
 
menu:
    # The following can be written in `blog/source/_data/menu.yml`
    - name: lyx-博客
      icon: fas fa-rss
      url: https://www.baidu.com/?tn=62095104_19_oem_dg
   url空一格 加可以访问的地址。


````



新建导航栏： 

  里面只加 menu:  对象。 便可以修改

```
  menu:
    # The following can be written in `blog/source/_data/menu.yml`
    - name: lyx-博客
      icon: fas fa-rss
      url: /
```

### 可配置子页面， 但是要注意后退一格。



````javasc
    - name: lyx0博客
      icon: fas fa-compact-disc
      rows:
      - name: 博客的子页面
        url: https://github.com/volantis-x/hexo-theme-volantis/
    - name: 分类
      icon: fas fa-folder-open
      url: categories/
    - name: 标签
      icon: fas fa-tags
      url: tags/
    - name: 归档
      icon: fas fa-archive
      url: archives/
    - name: 友链
      icon: fas fa-link
      url: friends/
    - name: 关于
      icon: fas fa-info-circle
      url: about/
````



### 如何写页面：

模板就这一个

![1595664516412](C:\Users\luyunxiao\AppData\Roaming\Typora\typora-user-images\1595664516412.png)

hexo clean   清除了你之前生成的东西
hexo generate    生成静态文章  重新编译
hexo deploy   部署文章





hexo new post  使用baihexo写博客

命令行输入    hexo new post article