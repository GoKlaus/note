# git

[TOC]

## 常用指令

## 暂存区，仓库等概念



## 解决Git换行符问题

### 1.Git设置

 [设置的意义](https://blog.csdn.net/xuewuzhijin2012/article/details/50117181)

windows

git config --global core.autocrlf false

git config --global core.safecrlf true

linux

git config --global core.autocrlf input

git config --global core.safecrlf true

含义：

AutoCRLF

\#提交时转换为LF，检出时转换为CRLF

git config --global core.autocrlf true

 

\#提交时转换为LF，检出时不转换

git config --global core.autocrlf input

 

\#提交检出均不转换

git config --global core.autocrlf false

SafeCRLF

\#拒绝提交包含混合换行符的文件

git config --global core.safecrlf true

 

\#允许提交包含混合换行符的文件

git config --global core.safecrlf false

 

\#提交包含混合换行符的文件时给出警告

git config --global core.safecrlf warn



## 常见问题解决

| 报错类型                                     | 解决方案                                           |      |
| -------------------------------------------- | -------------------------------------------------- | ---- |
| fatal: refusing to merge unrelated histories | git pull origin master --allow-unrelated-histories |      |
|                                              |                                                    |      |
|                                              |                                                    |      |

