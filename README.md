# smart-agriculture-esp32s3
# 智慧农业微型解决方案（ESP32-S3 智慧灌溉系统）
**演示视频**：https://www.bilibili.com/video/BV1rBWg68E87
低成本智慧灌溉原型，校级大学生创新创业训练计划（编号 J3125127）结题成果。

## 系统架构
设备端 ESP32-S3（YL-69 土壤湿度、ST7789 屏、5V 继电器驱动水泵）
→ 本地 MQTT Broker → PC 端（智能决策、自然语言解析、天气数据）
控制下沉、AI 上移：实时控制留在单片机，策略计算放在 PC 端。

## 功能
- 土壤湿度采集与本地屏幕显示
- 阈值自动灌溉，支持 pump_on / pump_off / set_threshold / status 指令
- 天气联动：按未来短时降雨概率动态调整灌溉阈值
- AI 服务不可用时降级为本地规则解析
- SIM800L 短信告警与按需查询

## 关键调试
- 继电器“上电即吸合”：模块 H/L 双触发与 GPIO 上电默认电平叠加，最终固定 GPIO45 与对应触发逻辑
- SIM800L 供电跌落：独立 3.7–4.2V 供电并与主控共地，消除随机重启

## 目录
firmware/  固件（Arduino / ESP-IDF）
pc/        PC 端控制台与命令行工具
docs/      接线图、实物照片

## 运行
1. 复制 config.example.h 为 config.h，填入 WiFi 与 MQTT 配置
2. 烧录固件
3. 启动本地 MQTT Broker，运行 pc/ 控制台

仓库不含真实 WiFi 密码与 API Key。
