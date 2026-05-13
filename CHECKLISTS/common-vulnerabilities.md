# 常见漏洞检查表

每次审计 DeFi 合约必查项目。

## 1. 重入攻击 (Reentrancy) - 高危

原理: 合约在状态更新之前调用外部合约，外部合约回调回来再次执行同一操作。

检查项:
- [ ] 是否存在 call / transfer / send 到外部地址
- [ ] 状态变量是否在外部调用之前已更新（CEI 原则）
- [ ] 是否使用了 ReentrancyGuard
- [ ] ERC-777 tokens 的 tokensReceived hook 是否被正确防护

经典案例: TheDAO (2016)

## 2. 整数溢出/下溢 - 高危

检查项:
- [ ] 是否使用 Solidity 0.8+（自动检查 overflow）
- [ ] 0.8 以下是否用了 SafeMath
- [ ] unchecked 块内是否有潜在溢出风险

## 3. 访问控制 - 高危

检查项:
- [ ] 所有 external/public 函数是否都有权限检查
- [ ] onlyOwner / onlyAdmin 修饰符是否正确实现
- [ ] 多签钱包是否配置了正确的阈值

## 4. 闪电贷攻击 (Flash Loan) - 高危

原理: 借大量资产操纵价格，在同一 tx 内归还。

检查项:
- [ ] 预言机是否依赖可被单笔 tx 操纵的 AMM 即时价格
- [ ] 是否使用了 TWAP 而非即时价格
- [ ] 关键操作是否检查了区块时间戳范围
- [ ] 余额检查是否用了 >= 而非 ==

## 5. 预言机操纵 - 高危

检查项:
- [ ] 预言机数据源是否去中心化
- [ ] 是否使用了 Chainlink、Pyth 等第三方预言机
- [ ] 如果用内部预言机：是否有多源聚合
- [ ] 是否有最小/最大价格阈值保护

## 6. 前置运行 (Front-Running) - 中危

检查项:
- [ ] 是否涉及公开竞价/荷兰式拍卖
- [ ] AMM swap 是否存在 sandwich attack 风险

防御: 隐蔽交易（commit-reveal）、批量拍卖、MEV 保护

## 7. 逻辑漏洞 - 高危

检查项:
- [ ] 代币转账手续费是否被考虑
- [ ] 除法取整是否导致累积误差
- [ ] 循环批量处理是否有 gas 上限保护
- [ ] 时间锁操作的等待期是否正确

## 8. 初始化漏洞 - 高危

检查项:
- [ ] initialize() 是否使用了 initializer 修饰符
- [ ] 旧实现是否可能被重新初始化

## 9. 权限升级风险

检查项:
- [ ] 合约是否可升级（proxy pattern）
- [ ] 升级是否经过时间锁
- [ ] 是否有紧急开关（Emergency Stop）

## 工具速查

| 工具 | 用途 |
|------|------|
| Slither | 静态分析，100+ 漏洞模式 |
| Mythril | 符号执行，深度分析 |
| Echidna | 属性测试，发现违反不变量 |
| Certora Prover | 形式化验证 |
| OpenZeppelin Test | 单元测试 |

---
标签: reentrancy oracle flash-loan access-control
