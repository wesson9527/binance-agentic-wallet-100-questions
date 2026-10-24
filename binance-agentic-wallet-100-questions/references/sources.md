# 资料索引与核验方法

核验日期：2026-10-24，Asia/Shanghai。以下共26个官方入口/文档，不以媒体转述作为命令依据。

- **S01** [Binance Agentic Hub：能力入口、独立钱包、地址簿、预测来源、永续状态](https://web3.binance.com/en/agentic-hub)
- **S02** [Binance Developer Docs：产品概览、MPC、API级权限、链支持](https://developers.binance.com/en/docs/products/agentic-wallet/welcome)
- **S03** [官方钱包 SKILL：命令路由、安全政策、条件单处理](https://github.com/binance/binance-skills-hub/blob/main/skills/binance-web3/binance-agentic-wallet/SKILL.md)
- **S04** [版本和连接预检](https://github.com/binance/binance-skills-hub/blob/main/skills/binance-web3/binance-agentic-wallet/references/preflight.md)
- **S05** [登录与会话排查](https://github.com/binance/binance-skills-hub/blob/main/skills/binance-web3/binance-agentic-wallet/references/authentication.md)
- **S06** [设置与独立额度](https://github.com/binance/binance-skills-hub/blob/main/skills/binance-web3/binance-agentic-wallet/references/wallet-setting.md)
- **S07** [状态、余额、链、历史、锁](https://github.com/binance/binance-skills-hub/blob/main/skills/binance-web3/binance-agentic-wallet/references/wallet-view.md)
- **S08** [转账、地址簿、广播状态](https://github.com/binance/binance-skills-hub/blob/main/skills/binance-web3/binance-agentic-wallet/references/send.md)
- **S09** [域名解析与确认](https://github.com/binance/binance-skills-hub/blob/main/skills/binance-web3/binance-agentic-wallet/references/domain-resolve.md)
- **S10** [市价、报价、终态](https://github.com/binance/binance-skills-hub/blob/main/skills/binance-web3/binance-agentic-wallet/references/market-order.md)
- **S11** [限价、触发、状态](https://github.com/binance/binance-skills-hub/blob/main/skills/binance-web3/binance-agentic-wallet/references/limit-order.md)
- **S12** [代币审计前置检查](https://github.com/binance/binance-skills-hub/blob/main/skills/binance-web3/binance-agentic-wallet/references/security.md)
- **S13** [授权检查与撤销](https://github.com/binance/binance-skills-hub/blob/main/skills/binance-web3/binance-agentic-wallet/references/approvals.md)
- **S14** [gas单位与档位](https://github.com/binance/binance-skills-hub/blob/main/skills/binance-web3/binance-agentic-wallet/references/gas.md)
- **S15** [替换交易与nonce约束](https://github.com/binance/binance-skills-hub/blob/main/skills/binance-web3/binance-agentic-wallet/references/speedup-cancel.md)
- **S16** [预测交易、单位和结算](https://github.com/binance/binance-skills-hub/blob/main/skills/binance-web3/binance-agentic-wallet/references/prediction.md)
- **S17** [DeFi查询、预览、交易及缓存](https://github.com/binance/binance-skills-hub/blob/main/skills/binance-web3/binance-agentic-wallet/references/defi.md)
- **S18** [开发者模式与签名](https://github.com/binance/binance-skills-hub/blob/main/skills/binance-web3/binance-agentic-wallet/references/external-sign.md)
- **S19** [x402版本、网络、支付选项与重放](https://github.com/binance/binance-skills-hub/blob/main/skills/binance-web3/binance-agentic-wallet/references/x402-payment.md)
- **S20** [Binance Web3 skills 集合：研究、审计、信号的独立模块](https://github.com/binance/binance-skills-hub/tree/main/skills/binance-web3)
- **S21** [当前活动规则：仅供核验，不纳入永久默认行为](https://github.com/binance/binance-skills-hub/blob/main/skills/binance-web3/binance-agentic-wallet/references/campaign.md)
- **C01** [Coinbase Agentic Wallet：CLI与MCP能力边界](https://docs.cdp.coinbase.com/agentic-wallet/welcome)
- **C02** [OKX Agentic Wallet：TEE、多子钱包与支付](https://web3.okx.com/onchainos/dev-docs/home/agentic-wallet-overview)
- **C03** [MetaMask：Agentic wallet security，权限和签名隔离](https://metamask.io/news/agentic-wallet-security)
- **C04** [Coinbase CLI Skills：查询、支付及服务商业化](https://docs.cdp.coinbase.com/agentic-wallet/cli/skills/overview)
- **C05** [Coinbase 产品页：支出限制、密钥隔离和KYT](https://www.coinbase.com/developer-platform/products/agentic-wallets)

## 证据口径

- 读取官方 GitHub 钱包 SKILL 及17份 references；研究快照保留在交付目录的 research 中，未打包进技能，避免分发一套过期的官方手册。运行时读取当前官方文档。
- GitHub 路径最近一次提交核验：`b402990be1748d02b7b79ab958f278b1709e5de7`。下载快照的metadata为skill 1.13.0、requiredCliVersion 1.11.0；核验日期不代表所有页面发布时间。
- 用户给出的中文带ref入口在网页读取器中失败，已读取同站英文Agentic Hub及其链接指向的官方开发文档。推荐参数只在推文链接保留，不用于推断产品能力。
- 来源页更新时间、营销概览与GitHub详细reference可能不同。概览未列出某高级功能，不据此否认详细reference；概览的Coming Soon也不据此捏造CLI。实际操作必须对照当前help和后台响应。
- 本次完成文档研究、静态命令比对和技能结构校验；没有登录钱包、下单、签名、付款或进行链上实测。
- “规则”和“建议”是整理者提出的执行规范与扩展设计；不是币安官方承诺，也不冒充用户的实盘经验。
- 当前100问覆盖通用产品，不将S21活动支付币、奖励、积分或PnL口径写成永久规则；参加活动时按其日期和具体规则单独加载。

## 来源适用范围

S01—S03用于产品定位；S04—S05用于安装登录；S06用于权限；S07—S09用于资产转账；S10—S12用于交易与审计；S13—S15用于授权和异常；S16—S19用于高级模块。C01—C05只用于友商对照，不能作为币安功能支持证据。
