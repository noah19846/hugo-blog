---
title: eslintrc 配置笔记
date: 2022-11-05 11:45:14
categories:
  - 笔记
tags:
  - 前端
  - eslint
---

- parser：定义文件的 parser，比如引入 TypeScript 时就要使用特定的 parser
- parserOptions：定义关键字、语法的解析规则（不定义全局变量）
- env： 可以看成某组 global 变量组成的 preset
- globals: 定义全局变量，可读、写
- extends：表示应用某些现成的 shareable configs
- plugins：
  - 创建自定义规则以暴露给 rules 使用
  - 创建自定义环境功 globals 使用
  - 创建多个自定义 config（整个 eslintrc 配置文件就对应一个 config） 供 extends 使用
  - 创建自定义 processors 的以告知 eslint 如何处理 JavaScript 以外的文件，比如 **.vue** 文件里的 eslint 规则就是通过对应的插件实现
- processor：指定由某个 plugin 提供的 processor
- override：有时可能需要更精细的配置，比如，如果同一个目录下的文件需要有不同的配置。因此，你可以在配置中使用 overrides 键，它只适用于匹配特定的 glob 模式的文件
- rules

rules 的 Type 定义

```
type RuleKey = string
type RuleItemWarnLevel = 0 | 1 | 2 | 'off' | 'warn' | 'error'
type RuleItemValue = string
type RuleValue = RuleItemWarnLevel | [RuleItemWarnLevel, RuleItemValue]
type Rules = {
  [index: RuleKey]: RuleValue
}
```

你会发现基本上所有这种通过一系列配置来决定应用行为的「东西」，都会提供扩展某个（或某些）既定的配置的功能以屏蔽繁琐的细节，比如 Babel 配置文件里的 _preset_ 字段、TypeScript 配置文件里的 _reference_ 字段，同时为每个配置项定义一个合并规则以确保最终输出的是一个稳妥可用的配置。
