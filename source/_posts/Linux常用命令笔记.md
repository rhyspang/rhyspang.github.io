title: Linux常用命令笔记
author: Rhys Pang
tags:
  - Linux
  - Tips
categories:
  - Linux
date: 2019-03-05 14:46:00
---


汇总工作中遇到的有用的Linux命令  

### 进程相关
- 已知PID获取进程的工作目录，可以通过以下三种方式获取
   ```shell
   $ pwdx <PID>
   $ lsof -p <PID> | grep cwd
   $ readlink -e /proc/<PID>/cwd
   ```
   
   
### Vim相关

- 很多时候用户使用vim打开文件，经过一番修复，准备保存的时候提示无写入权限，这时不得不放弃修改退出后用sudo重新打开该文件。可以使用以下命令保存无写入权限的文件（当有sudo权限时）。
```shell
$ w !sudo tee %
```
该命令解释可以参考 https://stackoverflow.com/a/7078429/10190375

### CUDA相关
- 查看cuda版本
```
/usr/local/cuda/bin/nvcc --version
```