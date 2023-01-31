---
title: 遇见的mac 和 linux Gemfile.lock 的系统依赖问题
tags: linux ruby macos
---

今天在搭建这个 blog 的时候, 发现在 mac 下bundle 了的话, 在 linux 拉代码, 再跑`bundle install`就会遇见这个典型的问题:


```
Your bundle only supports platforms ["x86_64-darwin-21"] but your local platform
  is x86_64-linux. Add the current platform to the lockfile with
  `bundle lock --add-platform x86_64-linux` and try again.
```
	
解决方案如字面所示:


`bundle lock --add-platform x86_64-linux`


此法会自动修改 gemfile.lock   在 platforms 中增加对应配置

```
PLATFORMS
  x86_64-darwin-21
  x86_64-linux
```

这是一篇测试文章, 用来测试 jekyll 的生成.
