---
title: 将hexo配置到github上
date: 2017-12-10 01:17:31
updated:
tags:
- Hexo
- 配置
thumbnail: /images/将hexo配置到github上/bg.jpg
---
>  可以参考[这篇文章](https://www.cnblogs.com/liuxianan/p/build-blog-website-by-hexo-github.html)

## github

1.  在github上面建一个和你的账号一样的项目，比如账号是【caozihao】，项目名为【caozihao.github.io】

2.  配置SSH，获取权限
    
        ssh-keygen -t rsa -C "[email]"

>   这个邮箱是你在github上注册的邮箱

3.  找到并打开 id_rsa.pub 文件，地址是
    
        C:\Users\Skull\.ssh

4.  将内容复制到github上的ssh里的key内容框里，目录为
    
        头像/SSH and GPG keys

5.  检测是否成功，控制台输入指令
    
        ssh -T git@github.com
    
    如果显示

        Hi caozihao! You've successfully authenticated, but GitHub does not provide shell access.
    
    说明配置成功

6.  为了方便不要每次push都要输入账号密码，有两种做法，一种是走SSH,配置key,就是上面这种不;另外一种是用https的，配credential helper，指令如下
    
        git config --global credential.helper store

##  Hexo项目
1.  在_config.yml文件中，找到deploy,将 repository 属性配置为 你的那个访问页面项目的地址
    
        deploy:
          type: git
          repository: https://github.com/caozihao/caozihao.github.io.git
          branch: master

2.  安装 hexo-deployer-git  自动部署发布工具
    
         npm install hexo-deployer-git  --save

3.  部署发布
    
        hexo g -d
    
    如果最后出现

        INFO Deploy done:git
        
    说明部署成功
    
4.  访问网站 https://caozihao.github.io/ 看看部署好了没有
    

##  绑定域名

1.  看[这篇](http://blog.csdn.net/u011976726/article/details/78217467)

2.  注意：添加完CNAME文件后，要重新部署一下
        
        hexo g -d

3.  注意：域名解析时要添加两个（ANAME和A）