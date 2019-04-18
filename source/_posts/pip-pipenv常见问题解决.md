title: pip & pipenv使用常见问题及解决办法(持续更新)
author: Rhys Pang
date: 2019-02-28 11:59:15
tags:
---
### 使用pipenv 安装第三包失败

**环境**  
- os: mac os  
- python: 3.7
- pip: 18.1

**错误提示**
```shell
lib/python3.7/site-packages/pipenv/utils.py", line 402, in resolve_deps
    req_dir=req_dir
  File "/usr/local/Cellar/pipenv/2018.7.1/libexec/lib/python3.7/site-packages/pipenv/utils.py", line 250, in actually_resolve_deps
    req = Requirement.from_line(dep)
  File "/usr/local/Cellar/pipenv/2018.7.1/libexec/lib/python3.7/site-packages/pipenv/vendor/requirementslib/models/requirements.py", line 704, in from_line
    line, extras = _strip_extras(line)
TypeError: 'module' object is not callable
```
**原因**  
使用的pip版本过高，可能为开发版本    


**解决方案**  
降级pip至18.0版本
```
pip install pipenv
pipenv run pip install pip==18.0
pipenv install
```
**参考**  
- https://github.com/pypa/pipenv/issues/2871

### pip install提示locale.Error
**环境** 
- os: Mac
- python: 3

**错误提示**
```shell
➜  ~ pip install virtualenv
Traceback (most recent call last):
  File "/usr/bin/pip", line 11, in <module>
    sys.exit(main())
  File "/usr/lib/python3.4/site-packages/pip/__init__.py", line 215, in main
    locale.setlocale(locale.LC_ALL, '')
  File "/usr/lib64/python3.4/locale.py", line 592, in setlocale
    return _setlocale(category, locale)
locale.Error: unsupported locale setting
```
**原因**   
环境变量`LC_ALL`缺失或非法   
   
   
**解决方案**   
运行以下命令
```shell
$ export LC_ALL=C
```
如果在新的shell中仍然报错，可以将命令写入到~/.bash_rc(bash)或者~/.zshrc(zsh)  

**参考**   
- https://stackoverflow.com/a/36394262/10190375