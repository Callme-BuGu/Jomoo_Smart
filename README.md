# 九牧马桶控制 / JOMOO Toilet Control

> 九牧 SQ7650 智能马桶自研蓝牙控制软件 —— Android APK + 网页版，双端统一 X 黑白风格、跟随系统深浅色。
> A self-built Bluetooth control app for the JOMOO SQ7650 smart toilet (Android APK + Web, unified black-and-white UI that follows system light/dark mode).

<p align="center">
  <b>非官方项目 · 与九牧集团（JOMOO）无关 · 仅供个人学习使用</b><br>
  <i>Unofficial project, not affiliated with JOMOO. For personal / noncommercial use only.</i>
</p>

## 功能 / Features

- **蓝牙直连**：Web-Bluetooth / Android BLE 直连马桶（服务 `0xFFE0`，特征 `0xFFE1`）
- **核心控制**：大冲 / 小冲 / 翻盖 / 翻圈 / 停止
- **设置项**：泡沫盾、预湿润、座圈加热（0–3 档）
- **状态轮询**：连接后每 3 秒自动刷新（工作状态 / 盖 / 圈 / 着座 / 座温）
- **双端统一 UI**：X（Twitter）黑白风格，跟随系统深浅色；网页版 PC/手机双布局自动适配
- **协议文档**：完整命令表与状态位定义（逆向自官方小程序，经实物蓝牙实测验证）

## 快速开始 / Quick Start

### Android（手机端）
1. 下载 `手机端-Android/九牧马桶控制_v1.10.apk` 并安装（允许未知来源）
2. 打开 App → 扫描设备 → 选择 **JOMOO** 开头的设备连接
3. 控制 / 设置 / 日志，状态每 3 秒自动更新

### Web（电脑 / 手机浏览器）
- 在线访问：`https://jm.bugu-offical.cn`（已部署至 CloudflarePages ）
- 本地打开：双击 `电脑端-Web/九牧马桶控制-网页版.html`（连蓝牙需 HTTPS 或 localhost 环境）
- 自部署：将 `电脑端-Web/worker.js` 内容粘贴至 Cloudflare Workers 编辑器保存即可

## 目录结构 / Repository Layout

```
├── 手机端-Android/
│   └── 九牧马桶控制_v1.10.apk      # Android 安装包
├── 电脑端-Web/
│   ├── 九牧马桶控制-网页版.html    # 单文件网页版（X 黑白风格）
│   └── worker.js                   # Cloudflare Worker 部署脚本
└── 文档/
    ├── 更新日志.md                  # 全部版本变更记录（v1.1 → v1.10 + 网页版）
    ├── README.md                   # 归档使用说明
    └── 九牧SQ7650-BLE协议说明.md    # 蓝牙协议逆向文档
```

## 蓝牙协议摘要 / Protocol Summary

- 服务 UUID：`0000FFE0-...`；特征 UUID：`0000FFE1-...`（WRITE NO RESPONSE + NOTIFY）
- 命令帧：`FC [csum] 01 00 00 00 [cmd] [val] FC`（csum = 字节 2..len-2 求和 & 0xFF）
- 常用命令：`0x11` 状态查询 · `0x35` 冲水（val 1=小冲 / 2=大冲）· `0x33` 翻盖 · `0x34` 翻圈 · `0x3C` 座温档（0–3）· `0x40` 设置帧（泡沫盾 / 预湿润）
- 详见 `文档/九牧SQ7650-BLE协议说明.md`

## 免责声明 / Disclaimer

本项目为个人学习研究产物，与九牧集团（JOMOO）及其官方 App 无任何关联。协议通过逆向官方小程序并经实物实测获得，可能随固件版本变化而失效。请仅在自有设备上使用；因使用本项目产生的任何问题与原作者无关。

## 许可 / License

本项目使用 **PolyForm Noncommercial License 1.0.0**（非商用开源许可）：

- ✅ 允许：个人学习 / 研究 / 实验 / 家庭使用；复制、修改、再分发
- ❌ 禁止：任何形式的**商业用途**（销售、付费服务、企业内使用、广告等）
- 📌 要求：再分发时必须保留本许可全文与本项目的版权声明（**Required Notice**）；**修改后发布须注明原作者与修改者**

```
Required Notice: Copyright 2026 BuGu
```

Copyright © 2026 BuGu. All rights reserved under the terms above.
