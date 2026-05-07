# Embedded Agent Workflow

> 🤖 多 Agent 自主协作的嵌入式开发流水线演示

[![GitHub Pages](https://img.shields.io/badge/GitHub%20Pages-Live%20Demo-blue)](https://sysifus007.github.io/embedded-agent-workflow)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

---

## 项目简介

本项目展示了一套由 **4 个自主 Agent** 协作驱动的嵌入式固件开发工作流。通过浏览器即可观看完整的 Agent 协作过程，无需硬件。

## 架构

```
┌─────────────────────────────────────────┐
│           Orchestrator Agent            │
│         (调度 / 质量门禁 / 报告)         │
└────────────┬──────────────┬─────────────┘
             │              │
    ┌────────▼──────┐ ┌─────▼────────┐
    │ DriverGen     │ │ ShellGen     │
    │ ( datasheet → │ │ ( 自然语言 → │
    │  寄存器驱动 )  │ │  CLI 命令树 )│
    └────────┬──────┘ └──────┬───────┘
             │               │
             └───────┬───────┘
                     │
            ┌────────▼────────┐
            │   TestGen       │
            │ ( 自主推理用例 → │
            │  HIL 测试报告 )  │
            └─────────────────┘
```

## Agent 自主能力

| Agent | 自主行为 |
|-------|----------|
| **DriverGen** | 解析 datasheet，生成寄存器驱动，**自我静态分析并修正** |
| **ShellGen** | **主动查询** DriverGen 的 API 签名，自动对接回调函数 |
| **TestGen** | **不依赖手写用例**，符号执行推导输入空间，失败时**自主溯源至源码行号** |
| **Orchestrator** | 检测上游变更后**自动触发下游回归**，自主判定质量门禁 |

## 快速体验

1. 打开 [在线演示](https://sysifus007.github.io/embedded-agent-workflow)
2. 点击 **"启动 Agent 流水线"**
3. 观看 4 个 Agent 的实时协作日志与最终测试报告

## 技术栈

- **固件**: STM32F103 裸机寄存器驱动 (C11)
- **测试**: Python + PySerial 硬件在环
- **演示**: 纯前端 HTML/CSS/JS (GitHub Pages 托管)

## 仓库结构

```
embedded-agent-workflow/
├── index.html          # 在线演示页面 (GitHub Pages)
├── README.md           # 本文件
└── .github/
    └── workflows/
        └── pages.yml   # GitHub Pages 自动部署
```

## License

MIT
