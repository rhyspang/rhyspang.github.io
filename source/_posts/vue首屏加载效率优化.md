---
title: vue首屏加载效率优化
date: 2019-10-24 10:00:30
tags:
---

- nginx 静态文件压缩
  ```
    gzip on;   # 打开gzip开关，默认为on
    gzip_min_length 1k; # 需要压缩的最小文件大小， 小于这个值的文件不压缩
    gzip_buffers 4 16k;
    gzip_types text/plain application/x-javascript text/css application/xml text/javascript application/x-httpd-php application/javascript;  # 需要压缩的文件类型， gzip 压缩文本文件效率较高
    gzip_vary off;
  ```
  **gzip** 
  是否启用zip压缩
  **gzip_min_length**
  需要压缩的最小文件大小， 小于这个值的文件不压缩以减小压缩时占用的资源
  **gzip buffers**
  设置response响应的缓冲区大小。4 16k代表以16k为单位将响应数据以16k的4倍(64k)的大小申请内存。如果没有设置，缓冲区的大小默认为整个响应页面的大小。
  **zip_types**
  指定哪些类型的相应才启用gzip压缩，多个用空格分隔。通配符`*`可以匹配任意类型。不管是否指定`text/html`类型，该类型的响应总是启用压缩。一般js、css等文本文件都启用压缩。gzip对文本文件压缩比较高，对图像文件压缩比较低
  
  **gzip_comp_level**
  gzip的压缩级别，可接受的范围是从1到9，数字越大压缩率越高，但更消耗CPU，一般设置6即可。
    
- 项目编译压缩
  ```
  module.exports = {
      configureWebpack: (config) => {
            if (process.env.NODE_ENV === 'production') {
                config.optimization.minimizer[0].options.terserOptions.compress.drop_console = true;
            }
        },
  }
  ```
- 第三方库导入优化
    使用懒加载导入组件和第三方库，减少首屏加载压力
   