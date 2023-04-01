# 复旦自动刷锻脚本

使用光华智慧体育小程序的 API 实现自动刷锻。使用帮助请看最后一节。

## 使用

**本节是本地运行脚本的说明，不会使用命令行的用户请直接参看「帮助」一节，使用 GitHub Actions 自动运行。**

- 安装依赖：`pip install -r requirements.txt`
- 设置环境变量 `USER_ID, FUDAN_SPORT_TOKEN`，需要在小程序内抓包获得。
- 查看刷锻路线列表：`python main.py --view`
- 自动刷锻：`python main.py --route <route_id>`，其中 `route_id` 是刷锻路线列表中的 ID。
- 可以设置里程和时间，如 `--distance 1200 --time 360`，更多选项请使用 `python main.py --help` 查看。

## 自动运行

Fork 本仓库，并设置 Secret `USER_ID, FUDAN_SPORT_TOKEN` 即可自动在规定时间刷锻。

## 说明

目前只支持南区田径场，其他体育场的经纬度坐标有待完善。

## 贡献

欢迎参与贡献本项目。本项目目前需要完善的内容包括：
- 支持更多运动场地的坐标
- 直接在脚本内使用 UIS 密码获取 Token，免去抓包的需要

## 帮助

为了方便没有计算机基础知识的同学运行此脚本，特附上使用教程。

###  抓包教程

以 iOS 系统为例，抓包教程可参考 [使用 Stream 抓包](https://www.azurew.com/%e8%bf%90%e7%bb%b4%e5%b7%a5%e5%85%b7/8528.html)，抓包软件可在 [App Store](https://apps.apple.com/cn/app/stream/id1312141691) 下载。

按照教程内的指引配置到设置证书的步骤，然后在软件内点击 Sniff Now 按钮，打开刷锻小程序刷新一下（确保小程序已经登录），再回到 Stream，点击 Stop Sniffing，然后点击 Sniff History，选择最近的一条记录，点开后找到开头为 `GET https://sport.fudan.edu.cn/sapi` 的任意一条记录，点进去选择 Request，在 Request Line 中有 `userid=xxx&token=xxx` 的记录，记下这两段信息。

以 PC 端为例，可参考 [教程](https://juejin.cn/post/6920993581758939150/) 进行相应设置。

在配置完后，微信登录，右上角齿轮进入代理，端口为 127.0.0.1，端口号为 8888（默认）
登录后进入小程序并登录，在 fiddler 里找到下图中的 ID 和 token
![image](https://user-images.githubusercontent.com/51439899/226794395-42eca333-fb65-4e29-a2cb-b8ce3fd13221.png)

**注意，目前 Token 的有效期为 3 天。**

### 自动部署配置教程

首先，你需要注册一个 GitHub 账户，并登录该账户。

在 GitHub 页面顶部，点按按钮 Fork，将项目复制到自己账户名下，然后在复制的项目内，依次点击 Settings - Secrets and variables - Actions - New repository secret，并分别新建名为 `USER_ID` 和 `FUDAN_SPORT_TOKEN` 的两个 Secret（Secret 的值分别为刚才记下的两个值）。配置完成后脚本将在每天早中晚的刷锻时间自动运行。

更新 Token 时，依次点击 Settings - Secrets and variables - Actions，找到 Repository secrets 一栏，点击下方 `FUDAN_SPORT_TOKEN` 右侧的铅笔按钮，更新 Token 的值。

### Issue

如果在使用过程中遇到了问题，请点击页面顶部的 Issue - New Issue，并在出现的文本框中描述你的问题。
