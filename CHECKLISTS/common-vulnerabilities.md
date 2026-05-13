# 常见漏洞检查表

> 每次审计 DeFi 合约必查项目。

---

## 1. 重入攻击 (Reentrancy) ⚠️ 高危

**原理：** 合约在状态更新之前调用外部合约，外部合约回调回来再次执行同一操作。

**检查项：**
- [ ] 是否存在 、、 到外部地址
- [ ] 状态变量是否在外部调用**之前**已更新（Checks-Effects-Interactions）
- [ ] 是否使用了 
- [ ] 跨合约调用是否用了  而非 
- [ ] ERC-777 tokens 的  hook 是否被正确防护

**经典案例：** TheDAO (2016), Uniswap LP token 攻击

---

## 2. 整数溢出/下溢 (Overflow/Underflow) ⚠️ 高危

**检查项：**
- [ ] 是否使用了 Solidity 0.8+（自动检查 overflow）
- [ ] 如果用 0.8 以下，是否用了 SafeMath 或等效库
- [ ]  块内是否有潜在的溢出风险
- [ ] 汇率计算是否有精度问题（先乘后除 vs 先除后乘）

---

## 3. 访问控制 (Access Control) ⚠️ 高危

**检查项：**
- [ ] 所有 / 函数是否都有权限检查
- [ ] / 修饰符是否正确实现
- [ ] 多签钱包是否配置了正确的阈值
- [ ] 是否有绕过修饰符的 way（通过 、parity hack 等）
- [ ]  /  权限是否仅属管理员

---

## 4. 闪电贷攻击 (Flash Loan) ⚠️ 高危

**原理：** 借大量资产操纵价格或绕过余额检查，在同一 tx 内归还。

**检查项：**
- [ ] 价格预言机是否依赖可被单笔 tx 操纵的 AMM 实时价格
- [ ] 是否使用了时间加权平均价格 (TWAP) 而非即时价格
- [ ] 关键操作是否检查了区块时间戳范围（ 可被 miner 操控 ±15s）
- [ ] 余额检查是否用了  而非 

**防御：** TWAP 预言机 + 滑点限制 + 最大操作金额上限

---

## 5. 预言机操纵 (Oracle Manipulation) ⚠️ 高危

**检查项：**
- [ ] 预言机数据源是否去中心化
- [ ] 是否使用了 Chainlink、Pyth 等第三方预言机
- [ ] 如果用内部预言机：是否有多源聚合
- [ ] 是否有最小/最大价格阈值保护（防止异常数据）
- [ ] 历史价格数据是否被检查（防止数据源缓存攻击）

---

## 6. 前置运行 (Front-Running) ⚠️ 中危

**原理：** 攻击者监听 mempool，用更高 gas 复制用户交易。

**检查项：**
- [ ] 是否涉及公开竞价/荷兰式拍卖
- [ ] 是否依赖区块顺序（先到先得）
- [ ] AMM 的  是否存在滑点被精确探测后 sandwich attack

**防御：** 隐蔽交易（commit-reveal）、批量拍卖、MEV 保护

---

## 7. 逻辑漏洞 (Business Logic) ⚠️ 高危

**检查项：**
- [ ] 代币转账手续费是否被考虑（实际到账 < 声明金额）
- [ ] 除法取整是否导致累积误差
- [ ] 循环批量处理是否有 gas 上限保护（防止 DoS）
- [ ] 多签交易的执行是否验证了足够的签名数
- [ ] 时间锁（Timelock）操作的等待期是否正确

---

## 8. 权限升级风险 (Privilege Escalation)

**检查项：**
- [ ] 合约是否可升级（proxy pattern）
- [ ] Proxy admin 是否被正确管理
- [ ] 升级是否经过时间锁
- [ ] 是否有紧急开关（Emergency Stop）

---

## 9. 结算/清算法错误 ⚠️ 高危

**检查项：**
- [ ] 多用户同时结算时余额是否正确
- [ ] 债务计算是否有浮点误差
- [ ] 强制清算阈值是否合理
- [ ] 清算人的奖励是否被正确计算

---

## 10. 初始化漏洞 (Initializer) ⚠️ 高危

**检查项：**
- [ ]  是否是  修饰（只执行一次）
- [ ] Proxy 合约的  初始化是否完整
- [ ] 旧实现是否可能被重新初始化

---

## 检查工具

| 工具 | 用途 | 链接 |
|------|------|------|
| Slither | 静态分析 | trailofbits/slither |
| Mythril | 符号执行 | trailofbits/mythril |
| Echidna | 属性测试 | trailofbits/echidna |
| Certora Prover | 形式化验证 | certora.com |
| OpenZeppelin Test | 单元测试 | openzeppelin.com |

---

*相关：[[ATTACKS/historical-incidents]]* 
*标签：#reentrancy #oracle-manipulation #flash-loan #access-control* 
