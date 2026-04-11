# 📊 每日股市分析任务模板

**分析师**: 🦞 小龙虾  
**更新时间**: {{YYYY-MM-DD}} {{HH:MM}}  
**数据源**: 同花顺数据中心  

---

## ✅ **每日 6 大核心分析任务**

### 1️⃣ 【涨跌幅排行分析】
- **URL**: https://data.10jqka.com.cn/rank/zdfph/
- **重点**: 涨停板股、资金流向、主力净流入/流出
- **输出**: `daily-reports/YYYY-MM-DD-涨跌幅排行.md`

### 2️⃣ 【创新高股票分析】
- **URL**: https://data.10jqka.com.cn/rank/gxg/
- **重点**: 创 N 日新高 (N≥60 天), 历史级突破，基本面支撑
- **输出**: `thematic-reports/YYYY-MM-DD-创新高.md`

### 3️⃣ 【连续上涨股票分析】
- **URL**: https://data.10jqka.com.cn/rank/lxsz/
- **重点**: 连涨天数≥7 天，累计涨幅>15%，换手率健康
- **输出**: `thematic-reports/YYYY-MM-DD-连续上涨.md`

### 4️⃣ 【持续放量股票分析】
- **URL**: https://data.10jqka.com.cn/rank/cyfl/
- **重点**: 成交量持续放大，主力资金流入明显
- **输出**: `thematic-reports/YYYY-MM-DD-持续放量.md`

### 5️⃣ 【向上突破股票分析】
- **URL**: https://data.10jqka.com.cn/rank/cxg/
- **重点**: 技术形态突破关键压力位，趋势转强信号
- **输出**: `thematic-reports/YYYY-MM-DD-向上突破.md`

### 6️⃣ 【量价齐升股票分析】
- **URL**: https://data.10jqka.com.cn/rank/ljqs/
- **重点**: 价格与成交量同步上升，上涨动力充足
- **输出**: `thematic-reports/YYYY-MM-DD-量价齐升.md`

---

## 🎯 **筛选标准（统一规范）**

```python
✅ 价值股/潜力股特征:
• PE < 行业平均或处于合理区间
• ROE > 10% (近三年平均值)
• 营收增长率 > 15% (最近一期)
• 市值规模：50 亿 -1000 亿之间为佳

✅ 技术分析要求:
• 均线呈多头排列
• MACD 金叉或红柱放大
• 量能温和放大而非爆量

❌ 坚决回避:
• ST/*ST系列
• 市盈率>200 倍无业绩支撑
• 换手率>50% 的游资对倒票
• 近期有重大利空公告
```

---

## 📁 **文件存储路径**

```
stock-analysis-docs/
└── YYYY/
    └── YYYY-MM/
        ├── daily-reports/         # 每日报告 (涨跌幅排行)
        │   └── YYYY-MM-DD-涨跌幅排行.md
        │
        ├── thematic-reports/      # 专题分析 (其他 5 项)
        │   ├── YYYY-MM-DD-创新高.md
        │   ├── YYYY-MM-DD-连续上涨.md
        │   ├── YYYY-MM-DD-持续放量.md
        │   ├── YYYY-MM-DD-向上突破.md
        │   └── YYYY-MM-DD-量价齐升.md
        │
        ├── watchlists/            # 跟踪列表
        │   └── YYYY-MM-DD-今日关注池.md
        │
        ├── attachments/           # 附件资源
        │   ├── YYYY-MM-DD-top.html
        │   └── k 线图.png
        │
        └── INDEX.md               # 月度索引 (自动更新)
```

---

## 🔄 **工作流程（每日收盘后执行）**

```powershell
步骤 1: 打开 6 个同花顺数据中心页面
       ├─ https://data.10jqka.com.cn/rank/zdfph/  (涨跌幅)
       ├─ https://data.10jqka.com.cn/rank/gxg/     (创新高)
       ├─ https://data.10jqka.com.cn/rank/lxsz/    (连续上涨)
       ├─ https://data.10jqka.com.cn/rank/cyfl/    (持续放量)
       ├─ https://data.10jqka.com.cn/rank/cxg/     (向上突破)
       └─ https://data.10jqka.com.cn/rank/ljqs/    (量价齐升)

步骤 2: 截图 + 数据提取 (browser action)
       ├─ browser open [URL]
       ├─ browser screenshot
       └─ browser snapshot (结构化数据)

步骤 3: 生成分析报告 (写 markdown 文件)
       ├─ TOP10 推荐标的 (带星级评级⭐⭐⭐⭐⭐)
       ├─ 操作建议 (买点/止损/目标价/仓位%)
       ├─ 风险提示 (避坑指南)
       └─ 复盘总结 (市场特征 + 投资策略)

步骤 4: 复制到指定目录
       Copy-Item "memory/\*" "C:\Users\admin\stock-analysis-docs\2026\2026-04\$分类\"

步骤 5: Git 提交推送
       cd C:\Users\admin\stock-analysis-docs
       git add .
       git commit -m "📊 YYYY-MM-DD: 今日大盘分析"
       git push

步骤 6: 更新 INDEX.md
       ├─ 添加新报告记录到表格
       └─ 更新跟踪状态
```

---

## 📝 **报告格式规范**

### 每个分析模块必须包含

```markdown
# [标题] YYYY-MM-DD 分析报告

**数据源**: 同花顺数据中心  
**更新时间**: YYYY-MM-DD HH:MM  
**分析师**: 🦞 小龙虾  

---

## ⭐⭐⭐⭐⭐ TOP 10 核心推荐

| 排名 | 代码 | 名称 | 现价 | 关键指标 1 | 关键指标 2 | 评级 | 亮点 |
|------|------|------|------|----------|----------|------|------|

### 🥇 第 1 名：[名称](代码) — [特色标签]
【买点】XXX
【止损】XXX
【目标价】XXX
【逻辑】XXX
【评级】⭐⭐⭐⭐⭐

...

## 📊 数据统计

• 样本数量：XX 只
• 符合条件：XX 只
• 重点关注：TOP 前 5

## 💡 行业分布统计

[饼图/条形图可视化]

## 🎯 最终行动清单

### ✅ 立即操作
• 标的 1 @ 价格 — 仓位% — 止损价格
• ...

### ⏳ 等待确认
• 标的 X — 条件触发
• ...

### ❌ 坚决回避
• 风险类型说明
• 具体标的黑名单

---

**记录时间**: YYYY-MM-DD HH:MM  
**声明**: 以上仅为技术分析，不构成投资建议。股市有风险，入市需谨慎！
```

---

## 🔔 **每日执行时间表**

| 时间 | 任务 | 预计耗时 |
|------|------|---------|
| 15:00-15:30 | 收盘数据收集，打开 6 个页面 | 30min |
| 15:30-17:00 | 完成涨跌幅排行 + 创新高分析 | 90min |
| 17:00-18:30 | 完成连续上涨 + 持续放量分析 | 90min |
| 18:30-20:00 | 完成向上突破 + 量价齐升分析 | 90min |
| 20:00-20:30 | Git 提交 + 更新索引 + 汇总报告 | 30min |

**总计**: 约 4-5 小时

---

## 📈 **周末加餐任务**

### 周日额外任务
- [ ] 汇总本周所有推荐标的收益率统计
- [ ] 更新《本周市场回顾》周报
- [ ] 下周一策略调整预案
- [ ] 持仓股复盘检查

### 月末任务（每月最后一个交易日）
- [ ] 生成《月度投资策略调整》报告
- [ ] 归档本月全部数据
- [ ] 创建下月目录结构
- [ ] 发布月度收益总结 Release

---

## 🚀 **快速启动命令**

```powershell
# 一键开启 6 个分析窗口
Start-Process "https://data.10jqka.com.cn/rank/zdfph/"
Start-Process "https://data.10jqka.com.cn/rank/gxg/"
Start-Process "https://data.10jqka.com.cn/rank/lxsz/"
Start-Process "https://data.10jqka.com.cn/rank/cyfl/"
Start-Process "https://data.10jqka.com.cn/rank/cxg/"
Start-Process "https://data.10jqka.com.cn/rank/ljqs/"
```

---

**座右铭**: 🦞 *"在这个市场上活下来，比赚快钱重要一万倍！"*  
**原则**: 保护本金第一，利润第二！💪📈

**最后更新**: 2026-04-11 19:35
