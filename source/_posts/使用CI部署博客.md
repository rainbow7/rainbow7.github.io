---
title: 使用CI部署博客
date: 2021-02-23 00:25:46
tags:
---

工欲善其事，必先利其器。

<!-- more -->

使用持续集成系统部署博客，会省去不少工作，也方便在没有hexo的环境下对博客内容进行修改。

[Xpote](https://keep.xpoet.cn/2020/11/%E4%BD%BF%E7%94%A8-Travis-CI-%E8%87%AA%E5%8A%A8%E9%83%A8%E7%BD%B2-Hexo-%E9%9D%99%E6%80%81%E5%8D%9A%E5%AE%A2/)老哥（应该不会是小姐姐吧）已经写了非常详细的教程了。这里就不再重复了。本博客的主题也是使用他（她）的。非常简洁、美观、实用。真的非常感谢！

最后提一点要注意`.travis.yml`配置文件中`token`变量的值是，是Tarvis系统上面配置的`Environment Variables`的name。可能是我比较傻，当时用token值把这个替换了。结果部署的时候提示没权限.....

![](/assets/blogImage/travis_config.png)

```yaml
deploy:
  on:
    branch: xxx         				# 工作分支（博客源码的分支）
  strategy: git
  provider: pages
  skip_cleanup: true            # 跳过清理
  token: $GH_TOKEN              # GitHub Token 变量
  keep_history: true            # 保持推送记录，以增量提交的方式
  local_dir: public             # 需要推送到 gh-pages 分支的静态文件目录
  target_branch: xxx            # 构建好的博客分支，也就是对外提供静态页面的分支
```



