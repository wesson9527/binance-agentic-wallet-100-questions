# 币安Agentic Wallet100问

一份**给 AI Agent 阅读**的币安 Agentic Wallet 产品使用说明书，用 100 个问答把产品能力、交易边界、异常处理和可扩展方向讲清楚。

> 中文展示名「币安Agentic Wallet100问」，技术标识 `binance-agentic-wallet-100-questions`。

## 这是什么

这不是给新手看的科普帖，而是给 agent 看的「操作路由 + 执行约束」。每个问答都拆成两条腿：

- **给 agent 的指令**：遇到某类意图时该走哪条官方路由、查什么。
- **边界 / 停止条件**：什么时候必须停下来、不能擅自做什么。

## 为什么会有这份文档

作者花了两个月边用边给自己的 agent 补规则——哪些坑要避、哪些时候该停、怎么把人的交易习惯写成 agent 能执行的边界。把这些思路和官方资料一起蒸馏成了这 100 问。

## 100 问结构（10 章 × 10 问）

| 范围 | 问题 | 内容 |
|---|---|---|
| Q001–010 | 产品边界 | 是什么、哪些能力不能假设 |
| Q011–020 | 安装登录 | 版本、配对、会话、断开 |
| Q021–030 | 授权与纪律 | 权限、额度、人类习惯 |
| Q031–040 | 资产与转账 | 链、代币、地址、域名 |
| Q041–050 | 交易与订单 | 报价、市价、限价、成交核实 |
| Q051–060 | 风险与恢复 | 审计、授权、gas、重复提交 |
| Q061–070 | 预测市场 | 事件、份额、报价、赎回 |
| Q071–080 | DeFi 与签名 | 预览、仓位、开发者模式 |
| Q081–090 | 支付与友商 | x402、跨产品边界 |
| Q091–100 | 扩展与验收 | 跟单、定投、巡检、维护 |

完整内容见 [`币安Agentic-Wallet100问.md`](./币安Agentic-Wallet100问.md)。

## 目录结构

```
.
├── 币安Agentic-Wallet100问.md          # 100 问完整 Markdown（人类审核/复制给 agent）
├── 币安Agentic-Wallet100问.skill       # 打包好的 skill（zip 格式）
├── 币安Agentic-Wallet100问.zip         # 同上，通用 zip
├── binance-agentic-wallet-100-questions/  # skill 源码目录
│   ├── SKILL.md                          # skill 主入口
│   ├── agents/openai.yaml                # 展示名与默认提示
│   └── references/                       # 10 章问答 + 策略模板 + 来源索引
│       ├── 01-basics.md ... 10-extensions.md
│       ├── policy-template.json          # 策略模板（默认 research_only）
│       └── sources.md                    # 官方资料索引
└── README.md
```

## 安装 skill

### 直接复制

把 `binance-agentic-wallet-100-questions` 整个目录放进你的 agent skills 目录（如 Codex 的 `~/.codex/skills/`），或解压 `币安Agentic-Wallet100问.skill` 到 skills 目录即可。

### 手动解压

```bash
unzip 币安Agentic-Wallet100问.skill -d ~/.codex/skills/
```

## 重要说明

- **本 skill 没有签名能力**，也不代替官方 `binance-agentic-wallet` skill 和 `baw` CLI。实际钱包操作需要安装官方 skill 并完成授权。
- **依赖未安装时仍可解释产品**，但不能伪造执行结果。
- 事实 / 执行规范 / 扩展建议分别标注；`policy-template.json` 中的阈值默认 `null`（未配置），**不是**作者两个月实盘的真实数值。
- 没有真实钱包登录或链上交易测试，文档验证有限度。
- 不保证收益，不构成投资建议。

## 产品入口

Binance Agentic Hub：<https://web3.binance.com/zh-CN/agentic-hub>
