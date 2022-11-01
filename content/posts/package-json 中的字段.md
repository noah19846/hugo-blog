---
title: package.json 中的字段
date: 2022-10-29 12:45:14
categories:
  - 笔记
tags:
  - 前端
  - package.json
---

分三类

- 为 Node.js 所用的
- 为 npm 所用
- 为某些 package 所用的，比如 rollup、babel、webpack、typescript 等（npm 其实也可以归到这类，只不过像 npm 这样的 package 稍特殊些，人家是 package manager）

## 为 Node.js(v19.0.0) 所用

- name：package name
- main：指定 package 的默认入口 module
- packageManager：指定包管理器（是 npm、yarn 或是 pnpm），依赖 Corepack
- type：决定当前 package 的模块类型是 是 esm 还是 cjs
- exports：优先级高于并且可替代 main field，v12+ 可用
- imports：供 package 内部引入自身的 module 时使用，相当于 vue-cli 中的 path alias

## 为 npm(v8.19.2) 所用

- name
- version
- description
- keywords
- homepage
- bugs
- license
- author
- contributions
- funds

- files：发布时包含的文件（目录）列表，某些文件被默认忽略
- main：package 的入口文件，若无则默认为同级目录下的 index.js
- browsers: 用于告知（大多是那些 bundler）此 package 是在浏览器端运行。https://github.com/defunctzombie/package-browser-field-spec
- bin：全局安装时可用作命令行工具
- man：配合 man 命令提供手册
- repository：源码所在地
- scripts
- dependencies：Packages required by your application in production
- devDependencies：Packages that are only needed for local development and testing. 通过 npm install 安装 package A 依赖时，package A 的 devDependencies 不会被安装
- peerDependencies：比如 webpack 的某个插件依赖 webpack，这个插件将 webpack 列入 dependencies 和 devDependencies 似乎都不太合适，这样的依赖就列入 peerDependencies。v3 到 v6 不会自动安装，v7 之后默认自动安装
- peerDependenciesMeta：顾名思义，用于描述 peerDependencies 中的依赖，可以将某个依赖标记为 optional 为 false，此时当这个依赖没有被安装时 npm 就不会发出警告
- bundleDependencies：In cases where you need to preserve npm packages locally or have them available through a single file download, you can bundle the packages in a tarball file by specifying the package names in the bundleDependencies array and executing `npm pack`。
- optionalDependencies：安装失败也不会报错的 dependencies
- overrides
- engines：指定 node 或 npm 版本
- os：指定操作系统
- cpu：执行 cpu
- private：为 true 时不会被发布
- workspaces

## 为一些知名 package 所定义

比如 rollup 的 module，typescript 的 types、typing 以及 lint-staged 的 lint-staged 等

## 关于 browser、module、main、exports

browser 和 module 字段主要是由一些打包工具比如 webpack、rollup 等使用，用以告诉那些 bundler 当前 package 只在浏览器端运行，以及使用的模块类型是否是 esm。

main 和 exports 是 Node.js 标准引入，支持灵活配置的后者被推荐为在新项目中使用以代替前者。可以根据不同的运行环境（比如是通过 import 加载还是 require 加载）使用条件导出不同的代码；也可以定义 submodule 的导出，未被定义的 submodule 则不允许被其他 module 通过 module 路径导入，在支持 exports 的 Node.js 版本中，该字段的优先级大于 main 字段。

个人感觉 exports 字段应该可以取代 browser 字段在那些 bundler 中的作用。
