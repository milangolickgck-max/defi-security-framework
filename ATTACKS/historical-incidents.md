# 历史 DeFi 攻击案例库

记录重大攻击事件，提取可复用的防御经验。

## 2024

### Ronin Network 攻击 (~$625M)
- 类型: 私钥被盗
- 原因: 5/9 多签节点被钓鱼攻击拿下
- 教训: 社会工程防御 = 技术安全同等重要
- 防御: 多签阈值应 > 50%，节点隔离，定期轮换

### Euler Finance 攻击 (~$197M)
- 类型: 闪电贷 + 预言机操纵
- 原因: donateToReserves 逻辑错误导致抵押不足账户被清算
- 教训: 清算逻辑需要与存款/借款逻辑同步审计
- 防御: 状态一致性数学证明

## 2022

### Nomad 桥攻击 (~$190M)
- 类型: 初始化漏洞
- 原因: 合约升级时 zero 值被接受为有效消息，攻击者大量伪造提款
- 教训: 初始化函数需要 initializer 修饰符保护
- 防御: 代理合约必须使用可升级安全模式

### Wormhole 桥攻击 (~$320M)
- 类型: 签名验证漏洞
- 原因: 签名验证逻辑缺陷，攻击者伪造 SysVars CPI
- 教训: 跨链消息验证是最高风险区域
- 防御: 多重验证、独立安全委员会、紧急熔断

## 关键教训总结

| 教训类型 | 典型案例 |
|---------|---------|
| 跨链验证必须多重验证 | Poly Network, Wormhole |
| 预言机防操纵 | Cream Finance, Fortress |
| 代理合约初始化安全 | Nomad |
| 多签安全 > 50% | Ronin |
| CEI 原则 | Euler Finance |
| 闪电贷 + 组合攻击 | Cream Finance, Euler |

---
标签: attacks history reentrancy oracle flash-loan
