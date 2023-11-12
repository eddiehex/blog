---
title: hexo博客pure主题安装记录
categories: code
tag： hexo
toc: true
---

## hexo插件安装

其实在dockerfile定制安装了一部分插件，但由于当时使用的教程和目前使用的主题不一致故导致部分插件未能安装。

- hexo-wordcount 文章数字计算
- hexo-generator-json-content 内部搜索

安装代码：

```shell
npm install hexo-wordcount --save
npm install hexo-generator-json-content --save
```

> 需要注意的是安装路径需在博客文件根目录下即～/blog/hexo（这个坑一开始我没注意）

## 修改icon和avatar 图像地址

主题中图像都从本地路径加载。

因上传麻烦且占用服务器资源故直接选择图传连接

`avatar: https://od.xxxx.cf/api/raw/?path=/picture/Icon/fish.png`

## 将Links（友链）改为service（服务）

- 处理主题文件夹下的_config.yml文件

```yaml
menu:
  Home: .
  #Archives: archives  # 归档
  Categories: categories  # 分类
  #Tags: tags  # 标签
  #Repository: repository  # github repositories
  #Books: books  # 豆瓣书单
  Services: links  # Links 改成Service
  About: about  # 关于

# Enable/Disable menu icons
menu_icons:
  enable: true  # 是否启用导航菜单图标
  home: icon-home-fill
  archives: icon-archives-fill
  categories: icon-folder
  tags: icon-tags
  repository: icon-project
  #books: icon-book-fill
  services: icon-project
  about: icon-book-fill
```

- 修改links index.md 路径：～/blog/hexo/source/links/index.md

```markdown
---
title: 服务
layout: links
comments: true
sidebar: none
---
```

- 修改语言文件

```yaml
Services: 服务
links-desc: 服务描述
```

## 删除文章版权信息

修改layout/_partial/post/copyright.ejs 文件

- 添加 `style="display: none;"`
- 修改条件判断`if(theme.profile && theme.profile.articleSelfBlock)`

```ejs
<blockquote class="mt-2x" style="display: none;">
  <ul class="post-copyright list-unstyled">
    <% if (post.permalink) { %>
    <li class="post-copyright-link hidden-xs">
      <strong>本文链接：</strong>
      <a href="<%- post.permalink %>" title="<%= post.title %>" target="_blank" rel="external"><%- decodeURIComponent(post.permalink) %></a>
    </li>
    <% } %>
    <li class="post-copyright-license">
      <strong>版权声明： </strong> 本博客所有文章除特别声明外，均采用 <a href="http://creativecommons.org/licenses/by/4.0/deed.zh" target="_blank" rel="external">CC BY 4.0 CN协议</a> 许可协议。转载请注明出处！
    </li>
  </ul>
</blockquote>
<% if(theme.profile && theme.profile.articleSelfBlock) { %>
<% var profile = theme.profile; %>
<div class="panel panel-default panel-badger">
  <div class="panel-body">
    <figure class="media">
      <div class="media-left">
        <a href="<%= profile.follow %>" target="_blank" class="img-burn thumb-sm visible-lg">
          <img src="<%= ( profile.gravatar ? gravatar(profile.gravatar, 128) : url_for(profile.avatar)) %>" class="img-rounded w-full" alt="">
        </a>
      </div>
      <div class="media-body">
        <h3 class="media-heading"><a href="<%= profile.follow %>" target="_blank"><span class="text-dark"><%= profile.author %></span><small class="ml-1x"><%= profile.author_title %></small></a></h3>
        <div><%= profile.author_description %></div>
      </div>
    </figure>
  </div>
</div>
<% } %>
```

## 关闭评论板块

修改_config.yml文件 将type 改成 false

```yaml
comment:
  type: false  # 启用哪种评论系统
```

## 文章目录开启

根据sidebar.ejs的判断语句:

```ejs
<% if (!index && theme.config.toc && post.toc) { %>
  <aside class="sidebar sidebar-toc collapse <% if(theme.config.autoUnfold){%>  in  <%}%>" id="collapseToc" itemscope itemtype="http://schema.org/WPSideBar">
  <div class="slimContent">
    <nav id="toc" class="article-toc">
      <h3 class="toc-title"><%= __('article.catalogue') %></h3>
      <%- toc(post.content) %>
    </nav>
  </div>
</aside>
<% } %>
```

我们可以看出需要满足三个条件:

- 不是index文件

- 主题config toc 需要开启为true

- post toc 需为true 即需要在每篇文章开头

  ``` markdown
  ---
  title: hexo博客pure主题安装记录
  categories: code
  tag： hexo
  toc: true #这个
  ---
  ```

## 添加服务

在source/_data/links.yml中按照格式添加即可

```yaml
Jupyter:
  link: https://hexo.kygoho.win/py
  avatar: /images/favatar/chuangzaoshi-logo.png
  desc: jupyter-notebook

Monitor:
  link: https://cloud.kygoho.win/
  avatar: https://od.wadaho.cf/api/raw/?path=/picture/Icon/star.png
  desc: service monitor panel

RSS:
  link: https://rss.009100.xyz
  avatar: https://od.wadaho.cf/api/raw/?path=/picture/Icon/read.png
  desc: RSS online reader
```



