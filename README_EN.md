# Stock Research Skill — 个股调研研报

A step-by-step research workflow for building a stock research report using IBKR Fundamentals + WRDS Compustat, following 小北's 12-dimension framework.

**When to use this skill**

- You want to research a new stock before entering a position.
- You already hold a position and want to complete or update the research report.
- You want to set a data-backed target price and stop-loss level.

**Trigger format**

```
/research [TICKER]
```

Example: `/research COHR`

---

## Workflow Overview

```
Phase 1 (IBKR, ~30 min)
  ├── Step 1  Overview tab       → valuation anchor
  ├── Step 2  Key Ratios         → P/S, P/E vs history & peers
  ├── Step 3  Analyst Ratings    → Wall Street consensus
  ├── Step 4  Analyst Forecast   → EPS trend + beat/miss
  ├── Step 5  Financials         → quarterly revenue & margin trend
  ├── Step 6  Ownership          → strategic investors (e.g. NVIDIA)
  └── Step 7  估计发布            → next earnings date + EPS history

Phase 2 (WRDS, ~20 min)
  └── Compustat Annual           → long-term revenue & P/S history

Phase 3 (Synthesis, ~30 min)
  └── 12-dimension report        → target price, stop-loss, entry plan
```

---

## Phase 1: IBKR Fundamentals Checklist

Open IBKR → search ticker → click **Fundamentals** tab → follow the steps below.

---

### Step 1 — Overview tab

**截图这些内容：**
- Morningstar Fair Value（公允价值）
- Morningstar Rating（几颗星）
- Economic Moat（护城河宽度）
- Uncertainty（不确定性等级）

**这些数字告诉你什么：**

| 字段 | 含义 | 怎么用 |
|------|------|--------|
| Fair Value | Morningstar用DCF算出的"理论合理价" | 当前股价 > Fair Value 说明偏贵；< 说明低估 |
| Rating（星级）| 5星=严重低估，1星=严重高估 | 快速判断入场时机 |
| Economic Moat | Narrow/Wide/None = 护城河宽窄 | Wide意味着竞争壁垒高，持仓更安全 |
| Uncertainty | Low/Medium/High/Very High | 越高说明估值越难预测，目标价区间越宽 |

**COHR案例：** Fair Value $239.77，2星，Moat Narrow，Uncertainty High → 当前$378已显著高于公允价值，溢价来自AI行情预期，不是基本面低估。

---

### Step 2 — Key Ratios tab

**截图这些内容：**
- Price to Sales (TTM) + 5Y Avg + Industry Avg
- P/E Normalized (TTM) + 5Y Avg + Industry Avg
- Price to Book (TTM)

**这些数字告诉你什么：**

| 指标 | 含义 | 判断逻辑 |
|------|------|---------|
| P/S TTM | 当前市值/过去12个月营收 | 比5Y均值高 = 已有溢价；比行业均值高 = 相对同行贵 |
| P/E TTM | 当前市值/过去12个月净利润 | 制造+成长型公司P/E常常失真，参考P/S为主 |
| 5Y Avg | 5年历史均值 | 当前值 ÷ 5Y均值 = 相对历史贵了多少倍 |
| Industry Avg | 行业平均值 | 判断是公司特有溢价还是整个行业都贵 |

**COHR案例：** P/S TTM 11.3x，5Y均值1.97x，行业均值2.2x → 相对历史贵了5.7倍，这是AI行情溢价，不是正常估值水平。

---

### Step 3 — Analyst Ratings tab

**截图这些内容（选LSEG Ratings）：**
- 共识评级（Buy/Hold/Sell）
- 平均目标价（AVG Target）
- 目标价区间（High / Med / Low）
- Analyst Action Log（最近几条，带机构名、评级、目标价、日期）

**这些数字告诉你什么：**

| 字段 | 含义 | 怎么用 |
|------|------|--------|
| 共识 Buy/Hold/Sell | 所有覆盖分析师的多数评级 | Buy = 大多数看涨；数量（如17 Buy / 6 Hold）更重要 |
| AVG Target | 所有分析师目标价平均值 | 和当前价对比，算"分析师预期上涨空间" |
| High/Low Target | 最乐观/最悲观的分析师目标价 | 定义合理价格区间的上下界 |
| Action Log | 谁、什么时候、调高还是调低 | 近期连续上调 = 基本面在改善；连续下调 = 警惕 |

**COHR案例：** 23位分析师，17 Buy / 6 Hold，平均目标价$375.60 → 几乎等于现价，华尔街整体认为当前价格已充分定价，没有明显上涨空间。Rosenblatt $425、Stifel $420最乐观；B.Riley $309最悲观。

---

### Step 4 — Analyst Forecast tab

**截图这些内容（选Quarterly）：**
- EPS图表（蓝色=实际，灰色=预测）
- 估计发布（Earnings Releases）页面：COHR收入预期表格

**这些数字告诉你什么：**

| 字段 | 含义 | 怎么用 |
|------|------|--------|
| 实际EPS vs 预测EPS | 每季度是否Beat预期 | 持续Beat = 管理层保守指引，业务好于预期 |
| YoY增速 | 同比增长率 | 判断增长是在加速还是放缓 |
| 华尔街共识 vs 公司Guidance | 分析师预测 vs 管理层给出的指引 | 两者差距大 = 市场预期和公司预期不一致，潜在催化剂 |
| 下次财报时间 | 下次FQ发布日期 | 重要风险点：临近财报不适合加仓 |

**COHR案例：** FQ1'26 EPS实际1.16，共识1.08，Beat +7%；FQ2'26实际1.29，共识1.21，Beat +7%；FQ3'26实际1.41，共识1.40，几乎持平。增速：57%→36%→55%，波动但整体在加速。下次FQ4'26财报：2026年8月13日。

---

### Step 5 — Financials tab（选Quarterly）

**截图这些内容：**
- Revenue（营收）最新季度值 + YoY%变化
- Gross Profit（毛利润）+ YoY%
- 过去4个季度的数值（用于算TTM）

**这些数字告诉你什么：**

| 字段 | 含义 | 怎么用 |
|------|------|--------|
| Revenue YoY | 营收同比增速 | 核心增速指标，20%以上算高增长 |
| Gross Profit Margin | 毛利率 = 毛利/营收 | 连续改善 = 产品结构在优化；下降 = 竞争压力或成本上升 |
| 季度趋势 | 每季度是否在增长 | 看方向，不只看绝对值 |

**TTM营收计算：** 把最近4个季度营收加起来，用于计算当前P/S。

**COHR案例：** Q3'25~Q3'26营收：$1.5B → $1.53B → $1.58B → $1.69B → $1.81B，持续增长，增速+20.55% YoY。TTM = $6.61B。

---

### Step 6 — Ownership tab

**截图这些内容：**
- 机构持仓前5名（体系/Institutional）
- 战略实体（Strategic Entities）列表

**这些数字告诉你什么：**

| 字段 | 含义 | 怎么用 |
|------|------|--------|
| 机构持仓比例 | 富达/先锋/黑石等占多少 | 机构持仓高（>80%）= 专业资金认可；过高 = 散户被动跟随 |
| 战略实体 | 有实业逻辑的股东（如供应商、客户、竞争对手）| 客户/供应商持股 = 产业链绑定，是最强的基本面背书 |
| 1年变化% | 机构过去一年增减仓 | 增仓 = 看好；减仓 = 需要关注原因 |

**COHR最关键发现：** 英伟达持有3.98%（779万股，价值$18.6亿）。这不是财务投资，是产业链战略绑定——NVIDIA需要COHR的光收发器支撑其AI集群。这是研报中最重要的基本面背书，必须写进导语。

---

### Step 7 — 估计发布（Earnings Releases）tab

**截图这些内容：**
- EPS/收入预期表格（历史各季度）
- 下次财报时间

**额外检查（如果有）：**
- 内幕交易（Insider Trading）：近3个月高管是否大量卖出
- 对冲基金情绪：增仓还是减仓

**COHR案例：** 高管近3个月卖出$300万；对冲基金情绪"非常消极"（减仓）。这是风险信号，说明知情者在获利了结，但不代表公司基本面有问题。

---

## Phase 2: WRDS Compustat（补长期历史数据）

IBKR只有约2年季度数据，WRDS提供10年以上年度数据，用于计算**历史P/S区间**。

**路径：** WRDS → Compustat → North America → Fundamentals Annual

**选择变量（Step 3）：**

| 变量 | 含义 |
|------|------|
| `fyear` | 财年年份 |
| `revt` | 总营收 |
| `gp` | 毛利润 |
| `oibdp` | 息税折旧前营业利润 |
| `csho` | 流通股数（注意：WRDS数据可能落后于最新增发） |
| `prcc_f` | 财年末股价 |

**关键用途：** 算出历史P/S区间（正常2-3x vs 当前11x），理解当前溢价的历史位置。

> 注意：WRDS的csho可能落后。**流通股最新值从IBKR → Company Profile → Common Shares Outstanding获取。**

---

## Phase 3: 研报综合写作（12维度框架）

整合以上数据，填写研报模板：

**核心输入数据清单：**

```
来自IBKR：
- 当前流通股数（Company Profile）
- 分析师共识目标价 + 区间（Analyst Ratings）
- 最新季度营收 + YoY增速（Financials）
- TTM P/S（Key Ratios）
- 战略股东（Ownership）
- 下次财报日期（估计发布）
- 内幕交易情况（聪明内幕）

来自WRDS：
- 历史年度P/S区间
- 毛利率历史趋势

自行判断：
- 目标P/S（参考历史区间 + 同行）
- FY下一年营收增速假设（参考管理层Guidance）
```

**目标价计算公式：**

```
FY下一年预期营收 = TTM营收 × (1 + 增速假设)
目标市值 = 目标P/S × 预期营收
目标股价 = 目标市值 / 最新流通股数
```

**止损逻辑：**

止损价 = 对应"不需要任何增长假设、仅基于已实现营收"的P/S下限估值。
通常取历史正常P/S均值（非AI行情时期）× 最近一年营收 / 最新流通股数。

---

## 研报数据采集表模板

每次开始新标的前，先填这张表：

```
标的：___________   日期：___________

【IBKR快速扫描】
Morningstar Fair Value：$______  Rating：__星
当前P/S TTM：______x  5Y均值：______x  行业均值：______x
分析师共识：______  平均目标价：$______  区间 $______ ~ $______
最新季度营收：$______  YoY：______%
TTM营收（4季度合计）：$______
战略股东：______________________________
内幕交易近3月：□ 买入  □ 卖出  金额：$______
下次财报：______________________________
最新流通股数：______________________股

【WRDS历史P/S区间】
最低P/S年份/值：______  最高P/S年份/值：______
合并前正常P/S均值：______x

【估值计算】
增速假设：______%（来源：□ 公司Guidance  □ 分析师共识  □ 历史趋势）
目标P/S：______x（理由：______）
FY预期营收：$______
目标市值：$______
目标股价：$______
止损价：$______（对应P/S ______x）
```

---

## 注意事项

1. **研报完成再入场**，不允许反过来。没有目标价和止损线就不开仓。
2. **开盘前30分钟（9:30–10:00 ET）不手动操作**。GTC单可以提前挂，但不在这段时间新开仓。
3. **流通股数用IBKR最新值**，不用WRDS的csho（WRDS可能落后一年）。
4. **分析师平均目标价 ≈ 当前价**时，说明市场已充分定价，入场需要更强的催化剂才有超额回报。
5. 目标价是**区间而非单点**。模型有四个主观判断点，结论应给出保守/基准/乐观三个场景。
