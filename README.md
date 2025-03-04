# 微信群聊总结助手 Nodejs 版

[EN Ver: WeChat Group Chat Summary Assistant Nodejs Version](./README_EN.md)

## 项目介绍

本项目是基于微信机器人的微信群聊总结助手，可以帮助群主或管理员自动收集群聊中的聊天记录，并使用 AI 进行总结，最终将其发送到指定的群聊中。

> 这可能是最简单配置可以把完整功能跑起来的项目，因为尝试了几个项目，都不是很能搞得定，所以用 JS 简单封装了下

效果预览

<img src="https://github.com/aoao-eth/wechat-summarize-bot/assets/897401/f3220210-3b7e-411f-8e2e-801f82a0b5da" width="300" />

## 运行

1. 安装依赖

```bash
npm install
```

2. 设置 env 环境变量

```bash
cp .env.example .env
```

.env 中有两个变量，这两个变量代表两个平台，接下来会分别介绍如何获取这两个变量的值。

3. 获取 PADLOCAL_API_KEY

注册 http://pad-local.com 获取一个七天试用的账号，创建应用，然后在 .env 中填入 api key

```bash
PADLOCAL_API_KEY=puppet_padlocal_xxxxxx
```

4. 获取 DIFY_API_KEY

注册 https://dify.ai 账号
创建一个应用，在应用的“访问 api”菜单中，点击“api 秘钥”，点击生成新的秘钥 ，然后在 .env 中填入此秘钥

```bash
DIFY_API_KEY=xxxxxx
```

之后，在提示词编排中，选择模型“Claude-2”，平台免费送了一些免费的调用次数，然后在 Prompt 内容中填入：

```
你是一个中文的群聊总结的助手，你可以为一个微信的群聊记录，提取每个时间段大家在讨论的话题内容。

以下是一个群的群聊记录，请帮忙将其总结成一个今日的群聊报告，包含5个以内的话题总结（如果还有更多话题，可以在后面简单补充）。每个话题包含以下内容：
- 话题名：(50字以内，以 emoji 开头，带序号）（热度，以🔥数量表示）
- 参与者： （5个以下）
- 时间段： 从几点到几点
- 过程总结：(50到200字左右）
- 一句话评价

最终标题《亲爱的，这是对今天大家群聊的总结报告》
```

![](./static/1.jpg)

5. 运行微信监控程序

```bash
npm run watch
```

此时会弹出一个二维码，使用微信扫码登录，登录成功后，程序将持续抓取所有群聊的聊天记录，聊天记录会保存在本地文件中，位置在 data/日期文件夹/群名.txt 中，不会上传到任何第三方。

6. 运行总结程序
   在每天结束的时候，手动对某个群的内容进行总结

```bash
npm run summarize ./data/2023-08-23/xxx.txt
```

即可生成这个群的当日总结。

## 友情链接

- [智囊 AI] https://zhinang.ai/chat
- [Dify.ai] https://dify.ai
- [PadLocal] http://pad-local.com
