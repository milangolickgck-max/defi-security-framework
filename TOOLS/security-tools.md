# DeFi 安全工具清单

## 静态分析

| 工具 | 特点 | 使用频率 |
|------|------|---------|
| Slither | Trail of Bits 出品，100+ 漏洞模式 | 必用 |
| Mythril | 符号执行，深度分析执行路径 | 常用 |
| Semgrep | 自定义规则 | 常用 |

## 模糊测试

| 工具 | 特点 |
|------|------|
| Echidna | 属性测试，发现违反不变量的行为 |
| Harvey | 灰盒 fuzzing |
| Medusa | 并行模糊测试 |

## 链上监控

| 工具 | 特点 |
|------|------|
| Forta Network | 去中心化监控网络，实时告警 |
| OpenZeppelin Defender | Admin 面板 + 自动化监控 |
| Tenderly | 交易模拟 + 实时监控 |

## 常用命令

```bash
# Slither 快速扫描
slither . --solc-remaps @openzeppelin=node_modules/@openzeppelin

# 指定漏洞类型
slither . --exclude-dependencies --filter reentrancy,unchecked-low-level

# Echidna 属性测试
echidna . --contract TestContract --config config.yaml
```

## 安全检查清单

1. [ ] Slither 无 High/Critical 告警
2. [ ] Echidna 属性测试全部通过
3. [ ] Mythril 无 Critical 发现
4. [ ] 代码覆盖率 > 90%
5. [ ] 所有 external 函数有权限检查
6. [ ] 数学运算使用 SafeMath 或 0.8+ 自动检查
7. [ ] 预言机有防操纵设计（TWAP 或 Chainlink）
8. [ ] 有 Emergency Stop 机制

---
标签: security-tools slither mythril echidna
