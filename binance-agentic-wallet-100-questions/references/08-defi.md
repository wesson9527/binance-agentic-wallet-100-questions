# DeFi 与外部签名

来源：S17, S18, S06，链接见 [资料索引](sources.md)。命令片段为路由提示，不是可直接执行的完整指令。

## Q071｜如何找到可用 DeFi 产品？

**性质：** 事实

**给 agent 的指令：** 从 defi protocol-list/info 查协议，再 investment-list/info 查具体产品；使用返回的 defiProtocolId/investmentId 与支持链。

**边界 / 停止条件：** 协议出现在列表不表示每个池都可投资；必须读取具体产品和动作参数。

## Q072｜APY 应该怎么展示和比较？

**性质：** 事实

**给 agent 的指令：** 展示 apyDisplay 原文，排序比较用 apyBps；协议级收益率是其产品中的最高值，标为最高APY，并区分 APR/APY。

**边界 / 停止条件：** 不能把协议最高收益率写成用户所有资金收益；基础APY不包含所有活动加成，也非保证回报。

## Q073｜DeFi 是否只需要有余额？

**性质：** 事实

**给 agent 的指令：** 先用 defi position 读取仓位；按动作检查产品状态、最低额度、支持币、锁定/赎回条件和健康因子。deposit/lp-add 另查 defiQuotaLeft；不能因新增投资额度用尽就推断赎回不可用。

**边界 / 停止条件：** 不要把借贷或LP仓位当作现金余额；健康因子的风险阈值需对应协议。

## Q074｜存入、赎回、LP 与领取奖励如何执行？

**性质：** 事实

**给 agent 的指令：** 对 deposit/redeem/lp-add/lp-remove/claim，先用相同参数执行 defi preview，展示费用、余额变化和全部 warnings，再在授权范围内执行。

**边界 / 停止条件：** preview 未通过则不执行；不静默改变币种、数量、投资ID或价格区间。

## Q075｜为什么 LP 比普通存币复杂？

**性质：** 建议

**给 agent 的指令：** 核对双币比例、区间、滑点基点、NFT头寸与退出条件，并说明无常损失和出区间风险。

**边界 / 停止条件：** 不能把 lp-add 简化为保本存款；移除比例、ticks、百分数各自按文档单位处理。

## Q076｜DeFi 交易后仓位没变化就是失败吗？

**性质：** 事实

**给 agent 的指令：** txHash只表明已提交；仓位数据存在延迟。后续验证先普通查询，仍旧时可按文档限频 refresh 一次，并核对链上交易。

**边界 / 停止条件：** 不立即连续强刷；旧仓位既不能证明交易失败，也不能证明交易成功。

## Q077｜原生路由不支持的协议能扩展吗？

**性质：** 建议

**给 agent 的指令：** 可评估 Developer Mode 的 contract-call；前提是协议接口、交易语义、资产路径和用户授权均明确。优先用已支持的原生路由。

**边界 / 停止条件：** 不将外部签名当成“任何DApp都能安全调用”的承诺；不为绕过平台限制而改走开发者模式。

## Q078｜开发者模式的签名门槛是什么？

**性质：** 事实

**给 agent 的指令：** 读取 devMode.enabled、expiresAt、dailyLimit 与 developerModeQuotaUsed；preview 后展示 parsedTx/parsedMessage、risks、authorityChanges，确认后仅用返回 requestId execute。

**边界 / 停止条件：** 未启用或预览失败不执行；requestId过期必须重新预览，不能复用旧确认掩盖内容变化。

## Q079｜contract-call 的金额和 gas 参数有哪些坑？

**性质：** 事实

**给 agent 的指令：** EVM value 采用 wei 的整数字符串；parsedTx.amount 依 tokenInfos.decimals 转为人类单位。Solana 使用未签名交易格式。

**边界 / 停止条件：** 不能把0.1直接当wei；不传不支持的gas价格参数；gasLimit仅按当前文档和用户明确指定处理。

## Q080｜EIP-712 签名为什么也可能花钱？

**性质：** 事实

**给 agent 的指令：** 读取 domain、chainId、verifyingContract、spender、额度、截止期及 Permit/Permit2 权限；签名执行后可能需 App 确认，再查 sign-message result。

**边界 / 停止条件：** requireConfirmation=false仅指后台不要求App二次确认，不表示用户已授权；不把签名或付款凭证放进公开日志。
