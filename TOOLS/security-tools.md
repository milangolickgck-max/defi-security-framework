# DeFi 安全工具清单

## 静态分析

| 工具 | 语言 | 特点 | 使用频率 |
|------|------|------|---------|
| **Slither** | Python | Trail of Bits 出品，检测 100+ 种漏洞模式 | ⭐⭐⭐ 必用 |
| **Mythril** | Python | 符号执行，深度分析合约执行路径 | ⭐⭐ 常用 |
| **Semgrep** | 多语言 | 自定义规则，支持自定义检测 | ⭐⭐ 常用 |

## 形式化验证

| 工具 | 特点 | 适用场景 |
|------|------|---------|
| **Certora Prover** | 自动证明合约属性 | 高安全性要求 |
| **Dafny** | 函数式验证语言 | 关键业务逻辑 |
| **K Framework** | 形式化语义 | 复杂协议验证 |

## 模糊测试

| 工具 | 特点 | 适用场景 |
|------|------|---------|
| **Echidna** | 属性测试，发现违反不变量的行为 | DeFi 核心逻辑 |
| **Harvey** | 灰盒 fuzzing | 大型合约 |
| **Medusa** | 并行模糊测试 | 快速发现崩溃 |

## 链上监控

| 工具 | 特点 |
|------|------|
| **Forta Network** | 去中心化监控网络，实时告警 |
| **OpenZeppelin Defender** | Admin 面板 + 自动化监控 |
| **Tenderly** | 交易模拟 + 实时监控 |
| **Chainlink Automation** | 条件触发执行 |

## 审计框架

| 工具 | 特点 |
|------|------|
| **OpenZeppelin Contracts** | 安全标准库（金库、代理、权限）|
| **Solady** | 高性能 + 安全性优先的库 |
| **Solmate** | 现代 DeFi 原语（ERC4626 等）|

## 常用命令



## 安全检查清单

1. ☐ Slither 无 High/Critical 告警
2. ☐ Echidna 属性测试全部通过
3. ☐ Mythril 无 Critical 发现
4. ☐ 代码覆盖率 > 90%
5. ☐ 外部调用前完成状态更新（CEI 原则）
6. ☐ 所有 external 函数有权限检查
7. ☐ 数学运算使用 SafeMath 或 0.8+ 自动检查
8. ☐ 预言机有防操纵设计（TWAP 或 Chainlink）
9. ☐ 有 Emergency Stop 机制
10. ☐ 时间锁配置正确

---

*标签：#security-tools #slither #mythril #echidna #audit*
