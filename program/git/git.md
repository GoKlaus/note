[TOC]

## 

## git cache



## git rebase

git merge 操作合并分支会让两个分支的每一次提交都按照提交时间（并不是push时间）排序，并且会将两个分支的最新一次commit点进行合并成一个新的commit，最终的分支树呈现非整条线性直线的形式

git rebase操作实际上是将当前执行rebase分支的所有基于原分支提交点之后的commit打散成一个一个的patch，并重新生成一个新的commit hash值，再次基于原分支目前最新的commit点上进行提交，并不根据两个分支上实际的每次提交的时间点排序，rebase完成后，切到基分支进行合并另一个分支时也不会生成一个新的commit点，可以保持整个分支树的完美线性



## git merge



## git remote

更新远程仓分支变化

```bash
git remote update -p
git remote update --purge
```



```json
{"code":1,"message":"demoData","returnData":{"image":"demoData","uuid":"demoData"}}
```





```shell
git remote add origin xxxx
```



修改仓库地址

```
git remote set-url origin URL
```







## git global



## git reflog





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



## 





