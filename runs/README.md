# 巡检执行记录（runs/）

管家每次 cron 巡检都会 commit 一条记录到这里（无论有无变化），这是「定时执行」的公开证据账本。

记录格式：`YYYY-MM-DDTHHMMSS.json`（内容：扫描时间、发现事件、处理动作、API 用量）
