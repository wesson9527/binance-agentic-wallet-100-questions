# 预测市场

来源：S16, S06, S01，链接见 [资料索引](sources.md)。命令片段为路由提示，不是可直接执行的完整指令。

## Q061｜币安的钱包预测市场是否就是 Polymarket？

**性质：** 事实

**给 agent 的指令：** 核验日 Agentic Hub 明确写 predict.fun；按当前产品来源与市场详情确认。

**边界 / 停止条件：** 不要把 Polymarket 的 marketId、结算币、接口或地域规则直接搬过来。

## Q062｜如何发现某个事件的正确市场？

**性质：** 事实

**给 agent 的指令：** 用 prediction category/list/search 缩小范围，再 market detail 核对问题全文、截止时间、结果定义与结算条件。

**边界 / 停止条件：** 相似标题不等于同一事件；无法确认结算规则就不下单。

## Q063｜marketTopicId、marketId 与 tokenId 能互换吗？

**性质：** 事实

**给 agent 的指令：** 从对应查询响应取得各ID，记录其关系；tokenId 指向具体 outcome，报价和订单簿按各自参数要求构建。

**边界 / 停止条件：** 不得把 YES/NO 文本或代币合约地址冒充 outcome tokenId。

## Q064｜预测交易前怎样检查额度和开关？

**性质：** 事实

**给 agent 的指令：** 读取 predictionEnabled、predictionQuotaLeft 与独立额度，结合钱包可用资产确认。

**边界 / 停止条件：** 普通交易有额度不代表预测交易启用；总余额不等于可下注额度。

## Q065｜预测市场 BUY 与 SELL 的 amount 单位相同吗？

**性质：** 事实

**给 agent 的指令：** 当前文档 BUY amount 为 USDT 支出，SELL amount 为份额；先确定方向再构建 quote。

**边界 / 停止条件：** 不能把卖出10份写成收回10 USDT；不要把其他产品结算单位套入。

## Q066｜预测单应该如何提交？

**性质：** 事实

**给 agent 的指令：** prediction trade quote 获取 quoteId、报价和有效期；确认市场、方向、花费、预期份额、滑点与费用后 place-order。

**边界 / 停止条件：** quote过期就重取；新报价超出原授权时停止，不能无条件接受价格变化。

## Q067｜预测 LIMIT 单与普通钱包限价单一样吗？

**性质：** 事实

**给 agent 的指令：** 预测路由使用 orderType=LIMIT 与 priceLimit；place-order 必须保持报价对应的类型、价格和 slippageBps。

**边界 / 停止条件：** 不要遗漏 LIMIT 导致默认 MARKET；两个模块的参数和订单ID不能混用。

## Q068｜报价里的 feeAmount 和 minReceive 怎么解读？

**性质：** 事实

**给 agent 的指令：** BUY 时 amountOut、feeAmount、minReceive 以份额计；SELL 时相应为 USDT。显示单位，结合订单簿看深度。

**边界 / 停止条件：** 不能把所有数值都显示成美元；市场价格不是经过保证的真实胜率。

## Q069｜部分成交、未成交和取消如何核实？

**性质：** 事实

**给 agent 的指令：** 查 prediction order history：FILLED、PARTIALLY_FILLED、SUBMITTED、CANCELLED、FAILED、EXPIRED 分别处理，并查询持仓对账。

**边界 / 停止条件：** 只撤销尚可取消的部分；不得把 PARTIALLY_FILLED 汇报为全额买入。

## Q070｜赢了怎样赎回，怎样记收益？

**性质：** 事实

**给 agent 的指令：** 核对市场已结算和可赎回份额后走 prediction trade redeem；用 settled-history、pnl、portfolio 区分已实现和未实现结果。

**边界 / 停止条件：** 未结算浮盈不是已到账收益；手续费、卖出及赎回不能重复计入。
