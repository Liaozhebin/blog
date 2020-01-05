---
layout:     post   				    # 使用的布局（不需要改）
title:      单个Github账号下添加多个 Github Pages				# 标题 
subtitle:   成功解决 #副标题
date:       2020-01-05 				# 时间
author:     Liaozhebin 						# 作者
header-img: img/post-bg-2015.jpg 	#这篇文章标题背景图片
catalog: true 						# 是否归档
tags:								#标签
    - Github
    -
---


## 这个项目页面是单个Github账号下添加多个 Github Pages 的相关尝试与结果。
#### 场景描述：   
- 当你在GitHub上已经有了一个和用户名同名的GitHub Pages项目当作个人主页(username.github.io)，还想尝试创建更多的Github Pages当个人主页，并且使用自定义域名。

#### 相关Github Pages的规则：

1. 个人主页必须要和用户的GitHub帐号同名，所以每个用户有且`只能有一个`repo作为个人主页，且必须是`<username>/<username>.github.io`的形式；
2. 项目主页的GitHub二级域名为`<username>.github.io/<projectname>`，这种有点类似于通过文件夹的方式进行索引进入的，它没有`<projectname>.<username>.github.io`这种方式，所以可以拥有的`数量为任意个`。

### 解决方法：
1. 在相关项目的repo里新建一个CNAME文件，并将不带协议名的裸域名写进去(`domain.com` 而不是 `https://domain.com`).
	> 这一步可以参考一下[官方文档](https://help.github.com/en/github/working-with-github-pages/managing-a-custom-domain-for-your-github-pages-site#configuring-an-apex-domain)
2. 到你域名的DNS服务商里给对应的二级域名添加CNAME解析到`<username>.github.io`(和个人主页的配置相同)
3. 等待DNS生效，具体时间和服务商有关（几分钟到几小时都有可能）
4. 然后打开`domain.com` ，就能进入你项目页的Github Page了
5. 创建多个项目，重复进行1-4步骤，进行自定义域名。这样每个项目都有了一个独立的域名。
**这里演示的是使用顶级域名，如果需要使用二级or三级域名，相应的进行修改和CNAME设置就行了。**

#### 后续
##### Project-name 与 个人主页 的冲突
- 在演示进行试验的过程中发现一个有趣的问题，个人主页下的文件夹是通过 `username.github.io/files/`来访问的，而项目页面也是通过`username.github.io/Project-name/`来访问的，这里就产生了一个冲突问题，当个人主页下的文件夹`files`**=**`Project-name`的时候，访问网址是一样的。
###### 结果
> 通过亲自测试，发现当 `files`**=**`Project-name`的时候，访问时，将会进入`Project-name`的项目页面，**即：`Project-Page`的优先级是高与个人主页的子文件夹**

### Ref：参考：
正所谓前人栽树后人乘凉，再此感谢以下文档提供的帮助。
1. [单个GitHub帐号下添加多个GitHub Pages的相关问题](http://chitanda.me/2015/11/03/multiple-git-pages-in-one-github-account/)
2. [Managing a custom domain for your GitHub Pages site --- Github官方文档](https://help.github.com/en/github/working-with-github-pages/managing-a-custom-domain-for-your-github-pages-site#about-custom-domain-configuration)
