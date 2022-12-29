---
layout: post
title: "git拉取合并代码提示refusing to merge unrelated histories"
categories: git
author:
- wuqi
meta: "git"
---

# git拉取合并代码提示refusing to merge unrelated histories

## 出现原因

远程git记录和本地记录无法匹配, 导致无法合并.

例如: 

1. 远程新建了git仓库, 并且同时创建了某些文件(.gitignore或者README.md之类的). 
2. 本地通过`git init`初始化一个代码仓库. 
3. 将本地仓库绑定到远程仓库.
4. 通过`git pull origin master`拉取代码, 此时本地和远程git提交记录无法匹配, 无法自动合并.

## 解决办法

通过在命令后面增加`--allow-unrelated-histories`参数, 运行未关联的历史记录合并, 接下来处理冲突即可.