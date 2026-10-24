# 币安Agentic Wallet100问

一份**给 AI Agent 阅读**的币安 Agentic Wallet 产品使用说明书——用 100 个问答，把产品能力、交易边界、异常处理和可扩展方向讲清楚。

> 中文展示名「币安Agentic Wallet100问」｜技术标识 `binance-agentic-wallet-100-questions`

---

## 一、它解决什么问题

让 agent 操作链上钱包，最大的风险不是「它不会」，而是「它会瞎做」。市面上教 agent 交易的内容大多是给新手看的科普，讲「是什么」，但不讲「什么时候该停」。agent 拿到这种内容，遇到边界情况时只会继续往前冲。

这份 100 问反过来，是**给 agent 看的操作路由 + 执行约束**，专门解决三件事：

1. **把人的交易纪律变成 agent 能执行的规则。** 作者花了两个月边用边给 agent 补规则：哪些坑要避、哪些时候必须停、怎么把「不追高、不加杠杆、不被套住」这类人的习惯，写成 agent 能逐条检查的边界条件。
2. **每个问答都是「两条腿」结构。**
   - **给 agent 的指令**：遇到某类意图时该走哪条官方路由、查什么、用什么命令。
   - **边界 / 停止条件**：什么时候必须停下来、不能擅自做什么（比如「限价单失败不能偷偷改成市价」「解析失败的域名不能猜地址」）。
3. **把 100 个场景收敛成一张路由表。** 从登录、转账、下单，到预测市场、DeFi、x402 支付，每个场景都标好了「该走官方哪条命令 + 该读哪份 reference」，agent 不再凭感觉瞎猜。

一句话：**它不是科普，是给 agent 的「操作规范 + 踩坑清单 + 认知框架」。**

第 11 章专门讲 **meme 币风控**：怎么识破貔貅盘（只能买不能卖）、怎么在买入前用「卖出方向报价」验证可卖性、怎么设流动性/持有人门槛、怎么用止损+分批止盈+回撤保护离场，以及怎么排除「假聪明钱」信号——这些都是冲土狗最容易被套牢的地方。

**认知引擎（新增）** 是执行任何操作前的前置判断层，解决「怎么判断」的问题：
- 给每条信息打可信度标签（Tier A/B/C/D）
- 区分官方声明、前端实现、链上事实、推断、未决问题
- 单一来源 ≠ 事实；共振才可信
- 先给方向 → 再给候选 → 最后执行，绝不越级
- 地址画像：给聪明钱做 Wallet Persona + A/B/C/D 分级
- 链上自主审计：合约未验证时自己扫描字节码、查 LP 锁定、追踪内部交易
- 认知偏差检查 + 执行后反馈循环

认知引擎的知识来自作者另外 5 个仓库（chokepoint-atlas、meme-narrative-radar、money-money-come、qiuqiu-robin-agent、okx-sol-meme-agent）的方法论沉淀。

---

## 二、100 问结构（10 章 × 10 问 + meme 风控章）

| 问题范围 | 章节 | 讲什么 |
|---|---|---|
| Q001–010 | 产品边界 | 它是什么、和主钱包/交易所 API 的区别、哪些能力不能假设 |
| Q011–020 | 安装登录 | 版本预检、配对、会话、断开 |
| Q021–030 | 授权与纪律 | 权限、额度、把人的习惯写成执行规则 |
| Q031–040 | 资产与转账 | 链、代币、地址簿、域名解析 |
| Q041–050 | 交易与订单 | 报价、市价、限价、成交核实 |
| Q051–060 | 风险与恢复 | 安全审计、授权撤销、gas、重复提交、卡单 |
| Q061–070 | 预测市场 | 事件、份额、报价、赎回 |
| Q071–080 | DeFi 与签名 | 交易预览、仓位、开发者模式、EIP-712 |
| Q081–090 | 支付与友商 | x402、跨产品边界、友商能力对照 |
| Q091–100 | 扩展与验收 | 跟单、定投、巡检、维护、验收清单 |
| Q101–110 | **Meme 币风控** | 貔貅盘识别、rug pull 防范、卖出前报价验证、止损止盈、假聪明钱排除 |
| **认知引擎** | **Agent 认知引擎** | 证据层级、决策分级、交叉验证、地址画像、自主审计、认知偏差、反馈循环 |

完整内容见 [`币安Agentic-Wallet100问.md`](./币安Agentic-Wallet100问.md)。

---

## 三、快速安装

用官方同款的 `skills` CLI 一条命令装好（这也是币安 Agentic Hub 官方推荐的安装方式）：

```bash
npx skills add wesson9527/binance-agentic-wallet-100-questions
```

### 常用变体

```bash
# 全局安装（所有项目可用），装给 Claude Code
npx skills add wesson9527/binance-agentic-wallet-100-questions -g -a claude-code

# 装给多个 agent（claude-code / codex / cursor / opencode 等）
npx skills add wesson9527/binance-agentic-wallet-100-questions -a claude-code -a codex

# 非交互安装（CI / 脚本里用）
npx skills add wesson9527/binance-agentic-wallet-100-questions -g -a claude-code -y

# 先看看仓库里有什么，再决定装不装
npx skills add wesson9527/binance-agentic-wallet-100-questions --list
```

> 前提：需要 Node.js ≥ 22.20。装完后 agent 会自动在 `.claude/skills/`、`.codex/skills/` 等技能目录里识别到它。

### 不装、直接临时用一次

```bash
npx skills use wesson9527/binance-agentic-wallet-100-questions@binance-agentic-wallet-100-questions
```

### 手动安装（不想要 CLI）

把仓库里的 `binance-agentic-wallet-100-questions/` 整个目录复制到你的 agent 技能目录（如 `~/.claude/skills/` 或 `~/.codex/skills/`），或者解压 `币安Agentic-Wallet100问.skill` 到技能目录即可。

---

## 四、怎么用

这个 skill 本身是**只读的知识 + 路由层**，不带签名能力。它和官方钱包 skill 是配合关系，不是替代关系：

| 层级 | 谁来做 | 说明 |
|---|---|---|
| 路由 + 约束 | **本 skill** | 判断意图、选命令、检查边界、决定停不停 |
| 实际签名执行 | 官方 `binance-agentic-wallet` + `baw` CLI | 真正转账/下单/签名，需要独立安装并授权 |

- **纯问答**：问它「限价单失败怎么办」「x402 怎么付款」，它按 100 问给出路由和停止条件，不需要连接钱包。
- **真要操作钱包**：需要先装官方 skill 和 `baw` CLI，并在币安 App 里完成授权；本 skill 负责在那之前把「能做什么、不能做什么」先讲清楚。
- **策略模板**：`references/policy-template.json` 是一份可填写的授权模板（单笔上限、日累计、滑点上限、加仓条件等），默认 `research_only`（只研究不操作），等你填好数值后 agent 才有执行依据。

---

## 五、目录结构

```
.
├── 币安Agentic-Wallet100问.md               # 100 问完整 Markdown（人读/复制给 agent）
├── 币安Agentic-Wallet100问.skill            # 打包好的 skill（zip 格式）
├── 币安Agentic-Wallet100问.zip              # 同上，通用 zip
├── binance-agentic-wallet-100-questions/    # skill 源码目录
│   ├── SKILL.md                             # skill 主入口（含 frontmatter）
│   ├── agents/openai.yaml                   # 展示名与默认提示
│   └── references/                          # 11 章问答 + 策略模板 + 来源索引
│       ├── 01-basics.md … 10-extensions.md
│       ├── 11-meme-risks.md                 # meme 币风控（貔貅/rug pull）
│       ├── 12-cognition-engine.md           # Agent 认知引擎：证据层级、决策分级、交叉验证、地址画像、自主审计、认知偏差、反馈循环
│       ├── policy-template.json             # 策略模板（默认 research_only）
│       └── sources.md                       # 31 个官方/友商/方法论来源索引
└── README.md
```

---

## 六、重要说明

- **本 skill 没有签名能力**，不代替官方 `binance-agentic-wallet` skill 和 `baw` CLI。实际钱包操作需要安装官方 skill 并完成授权。
- **依赖未安装时仍可解释产品**，但不能伪造执行结果。
- 事实 / 执行规范 / 扩展建议分别标注；`policy-template.json` 里的阈值默认 `null`（未配置），**不是**作者两个月实盘的真实数值——那是留给你自己填的。
- 没有真实钱包登录或链上交易测试，文档验证有限度。
- 不保证收益，不构成投资建议。

---

## 产品入口

Binance Agentic Hub：<https://web3.binance.com/zh-CN/agentic-hub>

官方钱包 skill（执行层，需另行安装）：<https://github.com/binance/binance-skills-hub/tree/main/skills/binance-web3>
