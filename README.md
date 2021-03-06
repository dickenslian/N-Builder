N-Builder
============

## 什么是 N-Builder ?

N-Build 是一个基于nodejs 的 web 工程打包工具。提供了 js, css 压缩打包, png, jpg 图片压缩功能。支持 Windows 和 Linux 两大平台。N-Builder 亦支持多个工程同时打包压缩。使用时只需简单配置 config.js 文件即可。

## 用到哪些工具 ?

+ js 压缩使用 uglify-js

+ css 压缩使用 clean-css

+ 图片压缩使用 smushit

## 使用前需要准备什么 ?

由于 N-Build 是一个基于 nodejs 的打包工具，因此使用前必须具备 nodejs 环境，如果你没有 nodejs 环境，请到 http://www.nodejs.org/ 下载最新版本的 nodejs 再使用 N-Builder。

## 如何配置 config.js ?

### config.js 整体概述

config.js 内含一对象数组, 数组中每个对象对应一个工程（可同时配置多个对象，同时打包多个工程），
每个对象（数组项）中有 5 个可配置属性，如下图所示：

>     var config = config || [{
>         rootPath: ,
>         buildPath: ,
>         images: {
>             imagesBuildPath: [],
>             path: []
>         },
>         js: {
>             jsBuildPath: [],
>             jsDir: [],
>             copyOnly: [],
>             ignore: []
>         },
>         css: {
>             cssBuildPath: [],
>             cssDir: [],
>             copyOnly: [],
>             ignore: []
>         }
>     }];
> 
>     rootPath: 需要打包的工程的根目录路径，后面所有关于工程的路径均相对于该路径。(必填)
>     buildPath: 打包的目标目录路径。（即需要打包到的目录路径）(必填)
>     iamges: 图片配置项。(选填)
>     js: javascripts 配置项。(选填)
>     css: css 配置项。(选填)
>
>     注：在配置路径时，若配置文件夹，必须以斜杠结尾。

### images 项如何配置 ?

>     images: {
>         imagesBuildPath: [],
>         path: []
>     },
>
>     imagesBuildPath: 压缩后图片保存的目标路径，相对于 buildPath。（选填，若不配置，则默认为 buildPath 目录）
>         
>     path: 需要压缩的图片的路径集合（可多填），可配置 文件路径 以及 文件夹路径。
>           若配置的是文件夹路径，N-Builder 将压缩该文件夹下所有 jpg 和 png 图片。
>
>     注：在配置路径时，若配置文件夹，必须以斜杠结尾。

### js 项如何配置 ?

>     js: {
>         jsBuildPath: [],
>         jsDir: [],
>         copyOnly: [],
>         ignore: []
>     },
>     
>     jsBuildPath: 压缩后 js 保存的目标路径，相对于 buildPath。（选填，若不配置，则默认为 buildPath 目录）  
>
>     jsDir: 需要压缩的 js 文件的路径集合（可多填），可配置 文件路径 以及 文件夹路径。
>            若配置的是文件夹路径，N-Builder 将压缩该文件夹下所有除 copyOnly 和 ignore 之外的 js 文件。
>
>     copyOnly: 不需压缩只需复制的 js 文件的路径集合（可多填），可配置 文件路径 以及 文件夹路径。
>               若配置的是文件夹路径，N-Builder 将根据 js 文件夹原有目录结构，复制该文件夹下所有 js 文件。
>         
>     ignore：不需要做什么处理的 js 文件的路径集合（可多填），可配置 文件路径 以及 文件夹路径。 
>             若配置的是文件夹路径, N-Builder 将不处理该文件下的所有 js 文件。
>
>     注：在配置路径时，若配置文件夹，必须以斜杠结尾。

### css 项如何配置 ?

>     css: {
>         cssBuildPath: [],
>         cssDir: [],
>         copyOnly: [],
>         ignore: []
>     },
>       
>     cssBuildPath: 压缩后 css 保存的目标路径，相对于 buildPath。（选填，若不配置，则默认为 buildPath 目录）  
>  
>     cssDir: 需要压缩的 css 文件的路径集合（可多填），可配置 文件路径 以及 文件夹路径。
>             若配置的是文件夹路径，N-Builder 将压缩该文件夹下所有除 copyOnly 和 ignore 之外的 css 文件。
>
>     copyOnly: 不需压缩只需复制的 css 文件的路径集合（可多填），可配置 文件路径 以及 文件夹路径。
>               若配置的是文件夹路径，N-Builder 将根据 css 文件夹原有目录结构，复制该文件夹下所有 css 文件。
>         
>     ignore：不需要做什么处理的 css 文件的路径集合（可多填），可配置 文件路径 以及 文件夹路径。 
>             若配置的是文件夹路径, N-Builder 将不处理该文件下的所有 css 文件。
>
>     注：在配置路径时，若配置文件夹，必须以斜杠结尾。

## 用例

### 打包单个工程

>     var config = config || [{
>         rootPath: '../example/',
>         buildPath: '../example/production/',
>         images: {
>             imageBuildPath: ['img_min/'],
>             path: ['img/']
>         },
>         js: {
>             jsBuildPath: ['js_min/'],
>             jsDir: ['js/'],
>             copyOnly: ['js/systems/', 'js/doorlayer.js'],
>             ignore: ['js/components/']
>         },
>         css: {
>             cssBuildPath: ['css_min/'],
>             cssDir: ['css/'],
>             copyOnly: ['css/css1/', 'css/triangle1.css'],
>             ignore: ['css/css2/']
>         }
>     }];
>
>     module.exports = config;

### 打包多个工程

>     var config = config || [{
>         rootPath: '../example/',
>         buildPath: '../example/production/',
>         images: {
>             path: ['img/']
>         },
>         js: {
>             jsDir: ['js/'],
>         },
>         css: {
>             cssDir: ['css/'],
>             copyOnly: ['css/css1/', 'css/triangle1.css']
>         }
>     }, {
>         rootPath: '../dev/',
>         buildPath: '../production/',
>         images: {
>             path: ['images/']
>         },
>         js: {
>             jsDir: ['src/']
>         },
>         css: {
>             cssDir: ['css/']
>         }
>     }, {
>         rootPath: '../developent/',
>         buildPath: '../production/',
>         images: {
>             imageBuildPath: ['img/']
>             path: ['res/']
>         },
>         js: {
>             jsDir: ['javascript/', 'src/''],
>             copyOnly: ['javascript/core/gogo.js', 'javascript/a.js', 'javascript/b.js'],
>         }
>     }];
>
>     module.exports = config;

## 如何运行 ?

>     Windows 运行 build.bat

>     Linux 运行 build.sh