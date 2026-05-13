# DeFi 安全框架

> DeFi 智能合约安全研究：漏洞检查表、审计模板、监控清单、攻击模式分析。

## 目录结构

```
├── CHECKLISTS/          # 漏洞检查表
│   ├── common-vulnerabilities.md
│   ├── access-control.md
│   └── oracle-manipulation.md
├── TEMPLATES/            # 审计报告模板
│   ├── audit-report-template.md
│   └── bug-bounty-template.md
├── MONITORS/             # 链上监控
│   ├── on-chain-alerts.md
│   └── token-monitor-checklist.md
├── TOOLS/                # 安全工具
│   └── security-tools.md
├── ATTACKS/              # 已知攻击案例
│   └── historical-incidents.md
└── README.md
```

## 核心原则

1. **无信任假设** — 所有外部输入都是敌意的
2. **最小权限** — 合约只授予必要的权限
3. **防御深度** — 单层不够，需要多层防御
4. **可升级性** — 合约应设计成可修补的

## 快速开始



## 贡献

发现遗漏或错误？欢迎提交 PR 或 Issue。
