# 复旦自动刷锻脚本

使用光华智慧体育小程序的 API 实现自动刷锻。

## 使用

- 安装依赖：`pip install -r requirements.txt`
- 设置环境变量 `USER_ID, FUDAN_SPORT_TOKEN`，需要在小程序内抓包获得。
- 查看刷锻路线列表：`python main.py --view`
- 自动刷锻：`python main.py --route <route_id>`，其中 `route_id` 是刷锻路线列表中的 ID。
- 可以设置里程和时间，更多选项请使用 `python main.py --help` 中查看。

## 自动运行

Fork 本仓库，并设置 Secret `USER_ID, FUDAN_SPORT_TOKEN` 即可自动在规定时间刷锻。

## 说明

目前只支持南区田径场，其他体育场的经纬度坐标有待完善。