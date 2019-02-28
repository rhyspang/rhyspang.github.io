title: pip & pipenv使用常见问题及解决办法(持续更新)
author: Rhys Pang
date: 2019-02-28 11:59:15
tags:
---
#### 使用pipenv 安装第三包失败

**环境**  
- os: mac os  
- python: 3.7
- pip: 18.1

**错误提示**
```
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
