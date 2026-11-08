# 管理学领域 Benchmark 文献工作汇总

> **一句话**：把 87 个「管理学领域基准」按 **发表时间、基准类型、基准领域** 三条轴整理成一张可维护的地图，并把每个基准的 **论文入口、开源仓库、许可与可复现性** 合并到同一张表里。

| 项目 | 内容 |
|---|---|
| 覆盖对象 | 87 个面向管理学各子领域的 LLM / 智能体评测基准（2022—2026） |
| 整理维度 | 发表时间（5 年）· 基准类型（7 类）· 基准领域（7 域）· 语言 · 公开入口 · 许可 |
| 资料依据 | 各基准的论文原文、arXiv / DOI 页面与公开项目仓库的公开说明（资源信息按经核对后的记录，截至 2026-11-08） |
| 配套文件 | `data/benchmarks.csv`（87 条结构化数据，便于筛选与二次统计） |
| 使用提示 | 引用请以附录 A 的论文条目为准；本文档只做整理与导航，不替代原文 |

**目录**

- [0. 一页速览](#0-一页速览)
- [1. 整理说明与分类口径](#1-整理说明与分类口径)
- [2. 总体格局](#2-总体格局)
- [3. 按发表时间分类](#3-按发表时间分类)
- [4. 按基准类型分类](#4-按基准类型分类)
- [5. 按基准领域分类](#5-按基准领域分类)
- [6. 开源与可复现性](#6-开源与可复现性)
- [7. 命名、别名与引用易错点](#7-命名别名与引用易错点)
- [8. 研究空白与选题建议](#8-研究空白与选题建议)
- [9. 数据表与引用说明](#9-数据表与引用说明)
- [附录 A 全量文献清单](#附录-a-全量文献清单)
- [附录 B 推荐使用清单](#附录-b-推荐使用清单)
- [License](#license)

## 0. 一页速览

| 维度 | 分布 | 一句话解读 |
|---|---|---|
| 总量 | 87 个（2022—2026） | 覆盖 7 个管理学子领域、7 类评测范式 |
| 时间 | 2026 年 **50 个**（57%） | 2026 一年产出超过此前四年总和，领域仍在加速扩张 |
| 领域 | 运营 28 · 财务 26 · 信息 11 · 综合 10 · 战略 5 · 营销 4 · 人力 3 | 「运营 + 财务」占 62%，管人、管市场的基准最少 |
| 类型 | 推理 25 · 智能体 17 · 决策 15 · 模拟 11 · 知识 8 · 效度 7 · 套件 4 | 评测对象正从「答对」转向「做完」与「长时间做好」 |
| 入口 | 有入口 70（80%）· 部分公开 6 · 无入口 11 | 拿到入口 ≠ 能复跑：许可与数据形态决定实际可用性（第 6 节） |
| 许可 | 宽松 50（57%）· 非商业 10 · **不明 27（31%）** | 近三成许可不明，商用或二次发布前必须核对 |
| 语言 | 英文 73（84%）· 中文 8 · 中英 2 · 日文 2 · 多语 2 | 非英语基准稀缺，且中文几乎全部集中在财务 |
| 发表状态 | 预印本 69（79%）· 正式发表 16 · 工作论文 2 | 多数尚无正式同行评议版本，引用需注明版本与日期 |

**五条结论**

1. **范式在 2025—2026 完成迁移。** 2026 年的 50 个新增中，智能体 13 个 + 模拟环境 9 个 = 22 个（占当年 44%），而 2023 年这两类合计为 0。评价对象从「答案正确」变成「任务完成」「长期表现」。
2. **供给由「有公开数据的子领域」驱动。** 财务（26）大量复用 SEC 文件与公司财报，运营（28）大量复用 MIPLIB / NL4OPT 一类的传统优化实例；人力（3）、营销（4）因涉及个人数据与消费者调研，供给明显不足。
3. **中文是最大的空白。** 中文/中英条目共 10 个，其中 8 个属于财务；「中文 + 运营/战略/人力」的组合为 **0**。
4. **实际可用集合小于名义集合。** 有入口 70 个，但「有入口 + 许可宽松」的 A 级集合只有 **46** 个；做横向对比实验应优先在此集合内选型。
5. **方法论层面的空白比任务层面的空白更值钱。** 只有 7 个做「效度/行为」检验、4 个做聚合套件，长程指标（多少天算长、如何计分）尚无统一口径——这是低成本、高影响的切入点。

## 1. 整理说明与分类口径

### 1.1 收录范围与整理口径

**收录标准**

| 纳入 | 排除 |
|---|---|
| 以「评测」为核心产出的基准、数据集或可执行环境 | 纯模型 / 训练方法论文（无独立评测集） |
| 有明确任务定义与评分方式（准确率、收益、完成率等） | 通用 NLP / 常识推理基准（无商业或管理场景） |
| 场景落在管理学各子领域（财务、运营、战略、营销、人力、信息系统） | 仅有单篇论文内的小规模自测集、无对外复用价值 |

**整理口径**

1. **资源信息按核对后的记录取值**：年份、语言、公开入口、许可、规模、载体、论文与数据链接均直接采用经逐条核对后的记录，不做二次推断；文献题名与首位作者按论文原文。
2. **类型按「主要评测对象」唯一归类**，边界情形在第 4 节说明；**领域按「主要应用场景」归类**，跨域套件归入「综合/跨领域」。
3. **公开度分三档**：*有入口* = 有可访问的项目页、仓库或数据页面；*部分公开* = 仅公开样例、需申请授权、或仅匿名仓库；*无入口* = 未检索到任何公开页面。
4. **本文档不重跑任何评测**，也不对仓库的当前可用性作实时担保；许可与可复现性判断均基于公开说明，正式使用前请以仓库现状复核。

### 1.2 分类体系一：基准领域（7 域）

| 代码 | 领域 | 条目 | 覆盖范围 | 说明 |
|---|---|---|---|---|
| 综合 | 综合/跨领域 | 10 | 商业通识、企业全景、跨子域套件 | 含商业创意类与跨域聚合套件 |
| 财务 | 财务与会计 | 26 | 财报分析、金融知识、审计、金融智能体 | 数据来源最丰富（SEC 文件、考试题库） |
| 运营 | 管理科学与运营 | 28 | 运筹优化建模、供应链、库存、博弈谈判 | 含经济学序列推理（交叉位置） |
| 战略 | 战略管理与创业 | 5 | 风险投资、企业合作、CEO 长程决策 | 条目少，但都是「高不确定性决策」 |
| 营销 | 市场营销与消费者 | 4 | 消费者模拟、零售经营、合成用户效度 | 以「像不像消费者」为核心问题 |
| 人力 | 组织行为与人力资源 | 3 | 招聘公平、简历评估、交叉性偏见 | 全部为公平性/效度类，无任务能力类 |
| 信息 | 商业分析与信息系统 | 11 | CRM/ERP、BPM、电子表格、数据分析、Text-to-SQL | 与「企业软件」高度重叠 |

### 1.3 分类体系二：基准类型（7 类，按「评测什么」划分）

| 类型 | 评测对象 | 判定口径 | 条目 |
|---|---|---|---|
| **知识型** | 领域知识的记忆与理解 | 答案可直接由领域知识/考试题库给出，单选题为主，不依赖外部文档检索与多步工具 | 8 |
| **推理型** | 多步计算、文档/表格推理、建模求解 | 需要检索证据、跨表计算、写出可执行模型或代码才能得到答案，但仍是「一问一答」 | 25 |
| **决策与博弈型** | 判断、选择、策略 | 答案无唯一标准解，以最优解、人类偏好或博弈均衡为参照，评的是「决定得好不好」 | 15 |
| **智能体型** | 多步任务执行 | 要求在一段交互中操作工具/界面/工作流并交付最终产物，过程与产物都被评 | 17 |
| **模拟环境型** | 长期经营与环境互动 | 提供一个可持续运行的经济/运营环境，指标是累计绩效、轨迹或长期一致性 | 11 |
| **效度与行为型** | 「像不像人」「是否公平」 | 不评能力高低，而以人类数据为参照检验偏差、失效条件与行为一致性 | 7 |
| **综合套件型** | 多任务聚合评测体系 | 本身是一个聚合多个数据集/任务并配统一 harness 的评测体系，而非单一任务 | 4 |

> 边界说明：例如 ERPBench（企业决策）虽用仿真环境，但评的是决策结论能否跨市场生态迁移，故归入「智能体型」；FinanceBench 虽需检索证据，但仍是一问一答，故归入「推理型」。

### 1.4 附加维度

- **发表时间**：按各条目的记录年份统计；正式版与预印本年份不一致的，在第 7 节说明。
- **语言**：英文 / 中文 / 中英双语 / 日文 / 多语种。
- **公开入口**：项目页、GitHub、HuggingFace、SourceForge、匿名仓库、无入口。
- **许可**：*宽松*（MIT、Apache-2.0、CC-BY-4.0、CC BY-SA 4.0）/ *非商业*（CC-BY-NC 系列、Non-Commercial 条款）/ *不明*（未声明、仓库无 LICENSE、NOASSERTION）。

## 2. 总体格局

### 2.1 发表时间分布

```text
年份   分布                               数量  占比

2022   █                                    1  1%
2023   ████                                 7  8%
2024   ██████████                          15  17%
2025   █████████                           14  16%
2026   ████████████████████████████████    50  57%
```

| 年份 | 数量 | 占比 |
|---|---|---|
| 2022 | 1 | 1% |
| 2023 | 7 | 8% |
| 2024 | 15 | 17% |
| 2025 | 14 | 16% |
| 2026 | 50 | 57% |

**读法**：2022—2025 四年合计 37 个，2026 一年 50 个。这既反映该方向在 2025 年下半年后的加速，也受检索截止时间（2026 年 11 月）的影响；做趋势判断时应把它读作**加速信号**，而不是绝对产量。

### 2.2 领域分布

```text
领域           分布                               数量  占比

综合/跨领域       ███████████                         10  11%
财务与会计        ██████████████████████████████      26  30%
管理科学与运营      ████████████████████████████████    28  32%
战略管理与创业      ██████                               5  6%
市场营销与消费者     █████                                4  5%
组织行为与人力资源    ███                                  3  3%
商业分析与信息系统    █████████████                       11  13%
```

**读法**：供给高度集中在两个「有现成公开数据」的子领域——财务（SEC 文件、财报、考试题库）与运营（MIPLIB、NL4OPT、供应链教学模拟）。与之相对，人力（3）与营销（4）的稀缺不是研究兴趣不足，而是**数据敏感与伦理成本**导致的供给约束。

### 2.3 类型分布

```text
类型         分布                               数量  占比

知识型        ██████████                           8  9%
推理型        ████████████████████████████████    25  29%
决策与博弈型     ███████████████████                 15  17%
智能体型       ██████████████████████              17  20%
模拟环境型      ██████████████                      11  13%
效度与行为型     █████████                            7  8%
综合套件型      █████                                4  5%
```

**读法**：推理型（25）是存量主体，主要来自 2023—2026 的优化建模与金融文档推理；智能体（17）与模拟（11）合计 28 个，几乎全部出现在 2025—2026；知识型（8）已基本停止新增（2026 年仅 2 个），说明「考试型基准」的红利期结束。

### 2.4 交叉视图

**年份 × 领域**

| 年份 | 综合/跨领域 | 财务与会计 | 管理科学与运营 | 战略管理与创业 | 市场营销与消费者 | 组织行为与人力资源 | 商业分析与信息系统 | 合计 |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| 2022 | · | 1 | · | · | · | · | · | **1** |
| 2023 | 1 | 4 | 2 | · | · | · | · | **7** |
| 2024 | 1 | 6 | 5 | · | · | 1 | 2 | **15** |
| 2025 | · | 3 | 5 | 1 | · | 1 | 4 | **14** |
| 2026 | 8 | 12 | 16 | 4 | 4 | 1 | 5 | **50** |
| 合计 | **10** | **26** | **28** | **5** | **4** | **3** | **11** | **87** |

**年份 × 类型**

| 年份 | 知识型 | 推理型 | 决策与博弈型 | 智能体型 | 模拟环境型 | 效度与行为型 | 综合套件型 | 合计 |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| 2022 | · | 1 | · | · | · | · | · | **1** |
| 2023 | 2 | 4 | · | · | · | · | 1 | **7** |
| 2024 | 4 | 4 | 3 | 2 | · | 1 | 1 | **15** |
| 2025 | · | 5 | 3 | 2 | 2 | 2 | · | **14** |
| 2026 | 2 | 11 | 9 | 13 | 9 | 4 | 2 | **50** |
| 合计 | **8** | **25** | **15** | **17** | **11** | **7** | **4** | **87** |

三条迁移路径可以直接读出来：

1. **2023 → 2024：知识 → 推理。** 2023 年知识型占 2/7，2024 年推理与套件开始增多，金融领域完成「考试题 → 真实文档推理」的升级。
2. **2024 → 2025：推理 → 智能体。** 第一批企业环境出现后，智能体与模拟开始成规模，决策/博弈随之增加。
3. **2025 → 2026：智能体 + 模拟双爆发。** 2026 年智能体 13 个、模拟 9 个，合计占当年 25%。

### 2.5 其他维度

| 维度 | 取值与数量 |
|---|---|
| 语言 | 英 73 · 中 8 · 中英 2 · 日 2 · 多语 2（非纯英文合计 14 个） |
| 公开入口 | GitHub 51 · HF 15 · 无任何地址（仅论文） 13 · 项目页 6 · 匿名仓库 1 · SourceForge 1 |
| 公开度 | 有 70 · 部分 6 · 无 11 |
| 许可 | 宽松 50 · 非商业 10 · 不明 27 |
| 发表状态 | 正式发表 16 · 工作论文 2 · 预印本 69 |

## 3. 按发表时间分类

按年份切成 5 段，每段给出「阶段特征 → 代表工作 → 该阶段留下的方法论资产」。

### 3.1 2022—2023：奠基期（8 个，9%）

**特征**：把专业文本「题目化」。所有工作都是问答式，评测对象是最终答案，指标统一为 accuracy / EM；数据可以完全公开，因此这一批至今仍是最好复现的部分。

**代表工作**：ConvFinQA、BizBench、CFBenchmark、FinEval、FinanceBench、PIXIU、NL4OPT、OptiMUS / NLP4LP

**留下的资产**：
- ConvFinQA 把「多轮对话 + 数值推理链」确立为金融推理的标准设定，后续大量基准沿用其题型。
- NL4OPT → OptiMUS → ORLM 三代工作把「自然语言 → 优化模型」从竞赛任务变成独立研究方向（`B37` / `B38` / `B42`），至今仍是运筹建模基准的公共底座。
- PIXIU 提出「模型 + 指令数据 + 评测」的三位一体，FinBen 后来把它扩成 36 数据集套件。
- FinEval 与 CFBenchmark 把中文金融知识评测标准化，此后中文金融基准基本都在它们的题型上做增量。

### 3.2 2024：专业化与套件化（15 个，17%）

**特征**：三条分岔同时出现——(a) 从「题目」走向「真实企业文档」；(b) 从「单任务」走向「多任务套件」；(c) 第一批企业环境型智能体基准入场；同时开始有人问「模型公不公平」。

**代表工作**：TheAgentCompany、CFLUE、CFinBench、FinBen、Golden Touchstone、Japanese Financial Benchmark、UCFE、Bargaining（议价基准）、EconLogicQA、GTBench、ORLM / IndustryOR、ORQA、JobFair、Kourani BPM、WorkArena

**阶段判断**：2024 是从「答题」到「干活」的过渡年。智能体只有 2 个，但这两条（WorkArena 的企业网页、TheAgentCompany 的数字员工）定义了之后两年最主流的两种环境形态。

### 3.3 2025：从「答对」到「做完」（14 个，16%）

**特征**：评测对象从「答案」变成「过程」与「长期表现」。长程一致性、行为偏差、真实业务流程（BPM、CRM、审计）同时进入视野。

**构成**：推理型 5 · 决策与博弈型 3 · 智能体型 2 · 模拟环境型 2 · 效度与行为型 2

**代表工作**：AuditBench、SECQUE、XFinBench、AI Playing Business Games、AIM-Bench、CHBench、OptMATH、Vending-Bench、VCBench、FAIRE、Busch & Leopold BPM、CORGI、CRMArena-Pro、DABstep

**留下的资产**：Vending-Bench 用「单次运行吃掉 2000 万 token」把长程一致性变成可测量的成本项；CRMArena-Pro 让企业沙盒既真实又可控；AIM-Bench 把行为经济学指标（牛鞭效应、锚定）引入库存决策评测。

### 3.4 2026：智能体与模拟的爆发（50 个，57%）

**特征**：一年 50 个，超过此前四年总和；但其中只有 6 个有正式发表版本，其余仍为预印本或工作论文。内容可归为四个簇：

**簇 A · 企业软件与流程智能体（13 个）**
Era by Eon、BlueFin、FinMaster、Finch、Herculean、CertiGATE、OR-Space、SupChain-Bench、CRM-Agent-Bench、ERPBench（Computer-Use）、ERPBench（企业决策）、RevOpsBench、SpreadsheetBench 2

**簇 B · 长程经营与环境模拟（9 个）**
Business Arena、Market-Bench、E-Commerce Bench、FM-Bench、SCM-Arena、CEO Arena、CEO-Bench、YC-Bench、RetailBench

**簇 C · 更难的推理（11 个）**
BizFinBench、BizFinBench.v2、Fin-RATE、FinRule-Bench、FinVQA（FIND）、FrontierOR、JOR-Bench、MIPLIB-NL、MM-OptBench、OPT-Engine、FirmCORe

**簇 D · 决策、效度、知识与套件（17 个）**
BizCompass、BusinessCaseBench、MBA-Bench、AuditFraudBench、AgenticPay、Cattle Trade、Negotiation Mechanism Benchmark、STAR Benchmark、The Language of Bargaining；Artificial Societies Benchmark、ConsumerSimBench、When Synthetic Users Fail、FairHireBench；CFMME、FINESSE-Bench；EGI-BENCH、EnterpriseBench

**阶段判断**：这一年的共同取向是**把基准做成环境**——有状态、可交互、能跑几十天、给出轨迹而非答案。代价是复现门槛上升：12 个无法完整获取，许可不明 17 个。

**全局时间轴一览**

| 年份 | 条目 | 该年主导类型 | 标志性变化 |
|---|---:|---|---|
| 2022 | 1 | 推理 | ConvFinQA：多轮数值推理成为标准题型 |
| 2023 | 7 | 推理 / 知识 | BizBench、NL4OPT、PIXIU：定量推理与建模奠基 |
| 2024 | 15 | 知识 / 推理 | FinanceBench、WorkArena、FinBen：真实文档、企业环境、套件化 |
| 2025 | 14 | 推理 / 决策 | 长程一致性、行为偏差、企业沙盒进入评测 |
| 2026 | 50 | 智能体 / 模拟 | 基准 = 环境；一年新增占历史总量近六成 |

## 4. 按基准类型分类

### 4.1 类型总览

| 类型 | 条目 | 评测对象 | 典型指标 | 年份重心 |
|---|---:|---|---|---|
| 知识型 | 8 | 领域知识记忆 | accuracy | 2023—2024 |
| 推理型 | 25 | 多步计算 / 文档 / 建模 | exact match、可执行性、求解器对比 | 2023—2026 |
| 决策与博弈型 | 15 | 判断与策略 | 收益、成交率、均衡偏离 | 2024—2026 |
| 智能体型 | 17 | 多步任务执行 | 任务完成率、轨迹质量 | 2024—2026 |
| 模拟环境型 | 11 | 长期经营表现 | 累计收益、长期一致性 | 2025—2026 |
| 效度与行为型 | 7 | 像不像人 / 是否公平 | 与人类分布的一致性、偏差幅度 | 2024—2026 |
| 综合套件型 | 4 | 多任务综合能力 | 各子任务加权平均 | 2023—2026 |

### 4.2 知识型（8 个）

**判定口径**：评「知不知道」：从考试题库、教材习题、专业准则里抽单选/简答，模型不许查文档。

**分布**：年份 2023、2024、2026；领域构成 财务与会计 8。

- 优点是可比性强、成本低、可无限扩充；适合做模型选型的第一道筛子。
- 缺点是与真实工作任务脱节，且题目多来自公开考试，存在训练数据污染风险。
- 2026 年新增仅 2 个，说明这一层已接近饱和。

**使用建议**：用它快速筛掉不合格模型，但**不要**用它论证「能胜任管理工作」。

| 编号 | 基准 | 年 | 领域 | 语言 | 链接 | 公开度 |
|---|---|---:|---|---|---|---|
| B12 | CFBenchmark | 2023 | 财务与会计 | 中文 | [arXiv](https://arxiv.org/abs/2311.05812) · [GitHub](https://github.com/TongjiFinLab/CFBenchmark) | 有入口 |
| B13 | FinEval | 2023 | 财务与会计 | 中文 | [arXiv](https://arxiv.org/abs/2308.09975) · [GitHub](https://github.com/SUFE-AIFLM-Lab/FinEval) | 有入口 |
| B16 | CFLUE | 2024 | 财务与会计 | 中文 | [DOI](https://doi.org/10.18653/v1/2024.findings-acl.337) · [GitHub](https://github.com/aliyun/cflue) | 有入口 |
| B17 | CFinBench | 2024 | 财务与会计 | 中文 | [arXiv](https://arxiv.org/abs/2407.02301) · [项目页](https://cfinbench.github.io/) | 有入口 |
| B19 | Golden Touchstone | 2024 | 财务与会计 | 中英双语 | [arXiv](https://arxiv.org/abs/2411.06272) · [GitHub](https://github.com/IDEA-FinAI/Golden-Touchstone) | 有入口 |
| B20 | Japanese Financial Benchmark | 2024 | 财务与会计 | 日文 | [arXiv](https://arxiv.org/abs/2403.15062) · [GitHub](https://github.com/pfnet-research/japanese-lm-fin-harness) | 有入口 |
| B29 | CFMME | 2026 | 财务与会计 | 中文 | [arXiv](https://arxiv.org/abs/2605.29462) · [GitHub](https://github.com/aliyun/qwen-dianjin) | 有入口 |
| B30 | FINESSE-Bench | 2026 | 财务与会计 | 英文 | [arXiv](https://arxiv.org/abs/2605.15482) · [GitHub](https://github.com/LimexAILab/FINESSE-Bench) | 有入口 |

### 4.3 推理型（25 个）

**判定口径**：评「算不算得对」：需要检索证据、跨表计算、写出可执行模型或代码，但仍是单轮问答。

**分布**：年份 2022、2023、2024、2025、2026；领域构成 综合/跨领域 1、财务与会计 9、管理科学与运营 11、战略管理与创业 1、商业分析与信息系统 3。

- 是存量最大的一类（25 个），也是方法最成熟的一类：答案可自动判分。
- 分化出两条路：一是「更复杂的文档」（多文档、多模态、跨期），二是「更难的数学」（优化建模、算法设计）。
- 隐忧是「答案唯一」的假设：真实的财务判断与建模选择往往没有唯一解，容易高估模型能力。

**使用建议**：做横向实验首选此类；注意区分「恰好算对」与「过程正确」，必要时加中间步骤评测。

| 编号 | 基准 | 年 | 领域 | 语言 | 链接 | 公开度 |
|---|---|---:|---|---|---|---|
| B01 | BizBench | 2023 | 综合/跨领域 | 英文 | [arXiv](https://arxiv.org/abs/2311.06602) · [HF](https://huggingface.co/datasets/kensho/bizbench) | 有入口 |
| B11 | ConvFinQA | 2022 | 财务与会计 | 英文 | [DOI](https://doi.org/10.18653/v1/2022.emnlp-main.421) · [GitHub](https://github.com/czyssrs/ConvFinQA) | 有入口 |
| B14 | FinanceBench | 2023 | 财务与会计 | 英文 | [arXiv](https://arxiv.org/abs/2311.11944) · [HF](https://huggingface.co/datasets/PatronusAI/financebench) | 部分公开 |
| B23 | SECQUE | 2025 | 财务与会计 | 英文 | [arXiv](https://arxiv.org/abs/2504.04596) · [HF](https://huggingface.co/datasets/nogabenyoash/SecQue) | 有入口 |
| B24 | XFinBench | 2025 | 财务与会计 | 英文 | [DOI](https://doi.org/10.18653/v1/2025.findings-acl.457) · [GitHub](https://github.com/Zhihan72/XFinBench) | 有入口 |
| B26 | BizFinBench | 2026 | 财务与会计 | 中文 | [arXiv](https://arxiv.org/abs/2505.19457) · [GitHub](https://github.com/HiThink-Research/BizFinBench) | 有入口 |
| B27 | BizFinBench.v2 | 2026 | 财务与会计 | 中文 | [DOI](https://doi.org/10.48550/arXiv.2601.06401) · [GitHub](https://github.com/HiThink-Research/BizFinBench) | 有入口 |
| B31 | Fin-RATE | 2026 | 财务与会计 | 英文 | [arXiv](https://arxiv.org/abs/2602.07294) · [HF](https://huggingface.co/datasets/GGLabYale/Fin-RATE) | 有入口 |
| B33 | FinRule-Bench | 2026 | 财务与会计 | 英文 | [arXiv](https://arxiv.org/abs/2603.11339) · [匿名仓库](https://anonymous.4open.science/r/FinRule-Bench-6723/README.md) | 部分公开 |
| B34 | FinVQA（FIND） | 2026 | 财务与会计 | 多语种 | [arXiv](https://arxiv.org/abs/2605.13330) · [GitHub](https://github.com/sarmistha-D/FIND_FinVQA) | 有入口 |
| B37 | NL4OPT | 2023 | 管理科学与运营 | 英文 | [arXiv](https://arxiv.org/abs/2303.08233) · [GitHub](https://github.com/nl4opt/nl4opt-competition) | 有入口 |
| B38 | OptiMUS / NLP4LP | 2023 | 管理科学与运营 | 英文 | [arXiv](https://arxiv.org/abs/2310.06116) · [HF](https://huggingface.co/datasets/udell-lab/NLP4LP) | 有入口 |
| B40 | EconLogicQA | 2024 | 管理科学与运营 | 英文 | [arXiv](https://arxiv.org/abs/2405.07938) · [HF](https://huggingface.co/datasets/yinzhu-quan/econ_logic_qa) | 有入口 |
| B42 | ORLM / IndustryOR | 2024 | 管理科学与运营 | 英文 | [arXiv](https://arxiv.org/abs/2405.17743) · [GitHub](https://github.com/Cardinal-Operations/ORLM) | 有入口 |
| B43 | ORQA | 2024 | 管理科学与运营 | 英文 | [arXiv](https://arxiv.org/abs/2412.17874) · [GitHub](https://github.com/nl4opt/ORQA) | 有入口 |
| B47 | OptMATH | 2025 | 管理科学与运营 | 英文 | [arXiv](https://arxiv.org/abs/2502.11102) · [GitHub](https://github.com/optsuite/OptMATH) | 有入口 |
| B54 | FrontierOR | 2026 | 管理科学与运营 | 英文 | [arXiv](https://arxiv.org/abs/2605.25246) · [GitHub](https://github.com/Minw913/FrontierOR) | 有入口 |
| B55 | JOR-Bench | 2026 | 管理科学与运营 | 日文 | [arXiv](https://arxiv.org/abs/2607.16777) | 部分公开 |
| B56 | MIPLIB-NL | 2026 | 管理科学与运营 | 英文 | [arXiv](https://arxiv.org/abs/2602.10450) · [GitHub](https://github.com/optsuite/MIPLIB-NL) | 有入口 |
| B57 | MM-OptBench | 2026 | 管理科学与运营 | 英文 | [arXiv](https://arxiv.org/abs/2605.12154) · [GitHub](https://github.com/ZhongLIFR/MM-OptBench) | 有入口 |
| B59 | OPT-Engine | 2026 | 管理科学与运营 | 英文 | [arXiv](https://arxiv.org/abs/2601.19924) · [HF](https://huggingface.co/datasets/chenyitian-shanshu/OPTEngine) | 有入口 |
| B68 | FirmCORe | 2026 | 战略管理与创业 | 中英双语 | [arXiv](https://arxiv.org/abs/2609.17128) | 无入口 |
| B77 | Kourani BPM | 2024 | 商业分析与信息系统 | 英文 | [arXiv](https://arxiv.org/abs/2412.00023) · [GitHub](https://github.com/humam-kourani/EvaluatingLLMsProcessModeling) | 有入口 |
| B79 | Busch & Leopold BPM | 2025 | 商业分析与信息系统 | 英文 | [DOI](https://doi.org/10.24251/hicss.2025.709) · [GitHub](https://github.com/KiriBu10/openLLMinBPM-benchmark/tree/dev_kiran) | 有入口 |
| B80 | CORGI | 2025 | 商业分析与信息系统 | 英文 | [arXiv](https://arxiv.org/abs/2510.07309) · [GitHub](https://github.com/Moonn521/CORGI) | 有入口 |

### 4.4 决策与博弈型（15 个）

**判定口径**：评「做得好不好」：答案无唯一标准，参照最优解、人类偏好或博弈均衡。

**分布**：年份 2024、2025、2026；领域构成 综合/跨领域 3、财务与会计 3、管理科学与运营 8、战略管理与创业 1。

- 分成两支：博弈/谈判（GTBench、AgenticPay、Cattle Trade 等）与专业判断（VCBench、UCFE、审计类）。
- 评测指标从 accuracy 转向收益、成交率、与人类偏好的一致性、均衡偏离度。
- 最大难点是「什么算好」的标准不统一，跨基准结果不可直接比较。

**使用建议**：适合做能力深度的探测；跨基准比较时务必先统一收益口径。

| 编号 | 基准 | 年 | 领域 | 语言 | 链接 | 公开度 |
|---|---|---:|---|---|---|---|
| B03 | BizCompass | 2026 | 综合/跨领域 | 英文 | [arXiv](https://arxiv.org/abs/2604.17305) · [项目页](https://bizcompass.dev.ypemc.com) | 有入口 |
| B05 | BusinessCaseBench | 2026 | 综合/跨领域 | 英文 | [arXiv](https://arxiv.org/abs/2607.16057) | 无入口 |
| B09 | MBA-Bench | 2026 | 综合/跨领域 | 英文 | [arXiv](https://arxiv.org/abs/2608.11616) · [HF](https://huggingface.co/hchoi256/mba) | 有入口 |
| B21 | UCFE | 2024 | 财务与会计 | 英文 | [arXiv](https://arxiv.org/abs/2410.14059) · [GitHub](https://github.com/TobyYang7/UCFE-Benchmark/tree/main) | 有入口 |
| B22 | AuditBench | 2025 | 财务与会计 | 英文 | [arXiv](https://arxiv.org/abs/2506.17282) | 无入口 |
| B25 | AuditFraudBench | 2026 | 财务与会计 | 英文 | [arXiv](https://arxiv.org/abs/2606.08345) | 无入口 |
| B39 | Bargaining（议价基准） | 2024 | 管理科学与运营 | 英文 | [DOI](https://doi.org/10.18653/v1/2024.findings-acl.213) · [GitHub](https://github.com/TianXiaSJTU/AmazonPriceHistory) | 有入口 |
| B41 | GTBench | 2024 | 管理科学与运营 | 英文 | [arXiv](https://arxiv.org/abs/2402.12348) · [GitHub](https://github.com/jinhaoduan/GTBench) | 有入口 |
| B46 | CHBench | 2025 | 管理科学与运营 | 英文 | [arXiv](https://arxiv.org/abs/2508.11944) | 无入口 |
| B49 | AgenticPay | 2026 | 管理科学与运营 | 英文 | [arXiv](https://arxiv.org/abs/2602.06008) · [GitHub](https://github.com/SafeRL-Lab/AgenticPay) | 有入口 |
| B50 | Cattle Trade | 2026 | 管理科学与运营 | 英文 | [arXiv](https://arxiv.org/abs/2605.14537) | 无入口 |
| B58 | Negotiation Mechanism Benchmark | 2026 | 管理科学与运营 | 英文 | [arXiv](https://arxiv.org/abs/2608.14613) | 无入口 |
| B62 | STAR Benchmark | 2026 | 管理科学与运营 | 英文 | [arXiv](https://arxiv.org/abs/2603.09337) · [GitHub](https://github.com/star-nexus/star) | 有入口 |
| B64 | The Language of Bargaining | 2026 | 管理科学与运营 | 多语种 | [arXiv](https://arxiv.org/abs/2601.04387) | 无入口 |
| B65 | VCBench | 2025 | 战略管理与创业 | 英文 | [arXiv](https://arxiv.org/abs/2509.14448) · [项目页](https://vcbench.com) | 有入口 |

### 4.5 智能体型（17 个）

**判定口径**：评「做不做得完」：在一段交互里操作工具、界面、企业系统，最后交付产物。

**分布**：年份 2024、2025、2026；领域构成 综合/跨领域 2、财务与会计 4、管理科学与运营 3、商业分析与信息系统 8。

- 企业软件是大头：CRM / ERP / 工单 / 电子表格，其中 8 个属于「信息」域。
- 环境形态两种：真实系统沙盒（WorkArena、CRMArena）与合成环境（Era by Eon、ERPBench）。
- 评价从「答案」变成「产物 + 过程」，需要环境快照、状态重置与轨迹记录，工程成本最高。

**使用建议**：进入前先确认能否稳定拉起环境；建议用 Docker/快照固定环境版本，否则结果不可比。

| 编号 | 基准 | 年 | 领域 | 语言 | 链接 | 公开度 |
|---|---|---:|---|---|---|---|
| B02 | TheAgentCompany | 2024 | 综合/跨领域 | 英文 | [arXiv](https://arxiv.org/abs/2412.14161) · [GitHub](https://github.com/TheAgentCompany/TheAgentCompany) | 有入口 |
| B08 | Era by Eon | 2026 | 综合/跨领域 | 英文 | [arXiv](https://arxiv.org/abs/2609.09853) · [GitHub](https://github.com/eon-io/era) | 有入口 |
| B28 | BlueFin | 2026 | 财务与会计 | 英文 | [arXiv](https://arxiv.org/abs/2605.30907) · [HF](https://huggingface.co/datasets/Longitude-Labs/bluefin-release) | 有入口 |
| B32 | FinMaster | 2026 | 财务与会计 | 英文 | [DOI](https://doi.org/10.18653/v1/2026.findings-acl.385) · [GitHub](https://github.com/JiangInsight/Finmaster) | 有入口 |
| B35 | Finch | 2026 | 财务与会计 | 英文 | [DOI](https://doi.org/10.18653/v1/2026.findings-acl.523) | 无入口 |
| B36 | Herculean | 2026 | 财务与会计 | 英文 | [arXiv](https://arxiv.org/abs/2605.14355) · [HF](https://huggingface.co/datasets/TheFinAI/Herculean) | 部分公开 |
| B51 | CertiGATE | 2026 | 管理科学与运营 | 英文 | [DOI](https://doi.org/10.2139/ssrn.7529119) · [GitHub](https://github.com/NTUZZH/CertiGATE) | 有入口 |
| B60 | OR-Space | 2026 | 管理科学与运营 | 英文 | [arXiv](https://arxiv.org/abs/2605.28158) · [GitHub](https://github.com/0xzhouchenyu/OR-Space) | 有入口 |
| B63 | SupChain-Bench | 2026 | 管理科学与运营 | 英文 | [arXiv](https://arxiv.org/abs/2602.07342) · [GitHub](https://github.com/Damon-GSY/SC-bench) | 有入口 |
| B78 | WorkArena | 2024 | 商业分析与信息系统 | 英文 | [arXiv](https://arxiv.org/abs/2403.07718) · [GitHub](https://github.com/ServiceNow/WorkArena) | 有入口 |
| B81 | CRMArena-Pro | 2025 | 商业分析与信息系统 | 英文 | [arXiv](https://arxiv.org/abs/2505.18878) · [GitHub](https://github.com/SalesforceAIResearch/CRMArena) | 有入口 |
| B82 | DABstep | 2025 | 商业分析与信息系统 | 英文 | [arXiv](https://arxiv.org/abs/2506.23719) · [HF](https://huggingface.co/datasets/adyen/dabstep) | 有入口 |
| B83 | CRM-Agent-Bench | 2026 | 商业分析与信息系统 | 英文 | [arXiv](https://arxiv.org/abs/2610.32004) · [GitHub](https://github.com/salesforce-misc/crm-agent-bench) | 有入口 |
| B84 | ERPBench（Computer-Use） | 2026 | 商业分析与信息系统 | 英文 | [arXiv](https://arxiv.org/abs/2609.17885) | 无入口 |
| B85 | ERPBench（企业决策） | 2026 | 商业分析与信息系统 | 英文 | [arXiv](https://arxiv.org/abs/2609.04667) · [GitHub](https://github.com/GAIR-NLP/erp-bench) | 有入口 |
| B86 | RevOpsBench | 2026 | 商业分析与信息系统 | 英文 | [DOI](https://doi.org/10.1109/southeastcon63549.2026.11475978) | 部分公开 |
| B87 | SpreadsheetBench 2 | 2026 | 商业分析与信息系统 | 英文 | [arXiv](https://arxiv.org/abs/2606.29955) · [HF](https://huggingface.co/datasets/KAKA22/SpreadsheetBench-v2) | 有入口 |

### 4.6 模拟环境型（11 个）

**判定口径**：评「长时间能不能一直做好」：在可持续运行的经济/运营环境里长期行动，看累计绩效。

**分布**：年份 2025、2026；领域构成 综合/跨领域 2、管理科学与运营 5、战略管理与创业 3、市场营销与消费者 1。

- 时长口径极不统一：180 天、365 天、500 天、1 年、20 年、2000 万 token 都有。
- 多数采用「与人类玩家/其他 LLM 竞争」的相对指标，而非绝对分数。
- 复现难点在随机性与对手：确定性种子程序生成是目前最可复现的做法。

**使用建议**：选型时优先看「是否有确定性种子」，否则同一模型的分数波动可能大于模型差距。

| 编号 | 基准 | 年 | 领域 | 语言 | 链接 | 公开度 |
|---|---|---:|---|---|---|---|
| B04 | Business Arena | 2026 | 综合/跨领域 | 英文 | [arXiv](https://arxiv.org/abs/2608.08621) · [项目页](https://business-arena.site.accio.ai/) | 有入口 |
| B10 | Market-Bench | 2026 | 综合/跨领域 | 英文 | [arXiv](https://arxiv.org/abs/2604.05523) · [GitHub](https://github.com/aiben-ch/Market-Bench) | 有入口 |
| B44 | AI Playing Business Games | 2025 | 管理科学与运营 | 英文 | [arXiv](https://arxiv.org/abs/2509.26331) · [SourceForge](https://sourceforge.net/projects/supply-chain-competition-game/files/) | 有入口 |
| B48 | Vending-Bench | 2025 | 管理科学与运营 | 英文 | [arXiv](https://arxiv.org/abs/2502.15840) · [项目页](https://andonlabs.com/evals/vending-bench-2) | 有入口 |
| B52 | E-Commerce Bench | 2026 | 管理科学与运营 | 英文 | [arXiv](https://arxiv.org/abs/2608.30730) · [GitHub](https://github.com/QwenLM/E-CommerceBench) | 有入口 |
| B53 | FM-Bench | 2026 | 管理科学与运营 | 英文 | [arXiv](https://arxiv.org/abs/2608.18423) · [GitHub](https://github.com/Analogy-AI/fm-bench) | 有入口 |
| B61 | SCM-Arena | 2026 | 管理科学与运营 | 英文 | [DOI](https://doi.org/10.2139/ssrn.6514506) · [项目页](https://scm-arena.com) | 有入口 |
| B66 | CEO Arena | 2026 | 战略管理与创业 | 英文 | [arXiv](https://arxiv.org/abs/2609.34821) · [GitHub](https://github.com/FoundationAgents/CEO-Arena) | 有入口 |
| B67 | CEO-Bench | 2026 | 战略管理与创业 | 英文 | [arXiv](https://arxiv.org/abs/2606.18543) · [GitHub](https://github.com/zlab-princeton/ceobench-src) | 有入口 |
| B69 | YC-Bench | 2026 | 战略管理与创业 | 英文 | [arXiv](https://arxiv.org/abs/2604.01212) · [GitHub](https://github.com/collinear-ai/yc-bench) | 有入口 |
| B72 | RetailBench | 2026 | 市场营销与消费者 | 英文 | [arXiv](https://arxiv.org/abs/2603.16453) · [GitHub](https://github.com/linghuazhang01/RetailBench) | 有入口 |

### 4.7 效度与行为型（7 个）

**判定口径**：评「像不像人、公不公平」：以人类数据为参照检验偏差、失效条件与行为一致性。

**分布**：年份 2024、2025、2026；领域构成 管理科学与运营 1、市场营销与消费者 3、组织行为与人力资源 3。

- 又分两支：合成用户效度（营销）与招聘公平性（人力），几乎各占一半。
- 方法论上最诚实的一类：它明确承认「我们不知道模型是否真的理解」。
- 只有 7 个，且没有一个覆盖财务/信息/战略——这是最明显的方法论空白。

**使用建议**：如果你的研究涉及「用 LLM 替代人类被试」，这类基准是必需的前置检验。

| 编号 | 基准 | 年 | 领域 | 语言 | 链接 | 公开度 |
|---|---|---:|---|---|---|---|
| B45 | AIM-Bench | 2025 | 管理科学与运营 | 英文 | [arXiv](https://arxiv.org/abs/2508.11416) | 无入口 |
| B70 | Artificial Societies Benchmark | 2026 | 市场营销与消费者 | 英文 | [arXiv](https://arxiv.org/abs/2609.30030) · [GitHub](https://github.com/artificial-societies/artificial-societies-benchmark) | 有入口 |
| B71 | ConsumerSimBench | 2026 | 市场营销与消费者 | 中文 | [arXiv](https://arxiv.org/abs/2605.17079) · [HF](https://huggingface.co/datasets/wty500/ConsumerSimBench) | 有入口 |
| B73 | When Synthetic Users Fail | 2026 | 市场营销与消费者 | 英文 | [arXiv](https://arxiv.org/abs/2607.26348) · [GitHub](https://github.com/ZihanChen1995/when-synthetic-users-fail-a-cross-domain-benchmark-of-llm-simulated-human-survey-responses) | 有入口 |
| B74 | JobFair | 2024 | 组织行为与人力资源 | 英文 | [DOI](https://doi.org/10.18653/v1/2024.findings-emnlp.184) · [HF](https://huggingface.co/datasets/holistic-ai/job-fair-resume) | 部分公开 |
| B75 | FAIRE | 2025 | 组织行为与人力资源 | 英文 | [arXiv](https://arxiv.org/abs/2504.01420) · [GitHub](https://github.com/athenawen/FAIRE-Fairness-Assessment-In-Resume-Evaluation) | 有入口 |
| B76 | FairHireBench | 2026 | 组织行为与人力资源 | 英文 | [DOI](https://doi.org/10.1145/3805689.3806487) · [HF](https://huggingface.co/datasets/Sweta6/FairHire) | 有入口 |

### 4.8 综合套件型（4 个）

**判定口径**：评「综合能力」：聚合多个数据集/任务，配统一 harness，本身就是一个评测体系。

**分布**：年份 2023、2024、2026；领域构成 综合/跨领域 2、财务与会计 2。

- 只有 4 个：PIXIU（FLARE）、FinBen、EGI-BENCH、EnterpriseBench。
- 价值在于减少「挑基准」的成本，代价是组件许可需逐项核对。
- 目前缺一个跨领域的「元基准」：不同套件的任务口径无法对齐。

**使用建议**：适合做整体能力汇报；单独引用某子任务分数时，要说明它来自哪个组件。

| 编号 | 基准 | 年 | 领域 | 语言 | 链接 | 公开度 |
|---|---|---:|---|---|---|---|
| B06 | EGI-BENCH | 2026 | 综合/跨领域 | 英文 | [arXiv](https://arxiv.org/abs/2610.27234) · [GitHub](https://github.com/SalesforceAIResearch/egi-bench) | 有入口 |
| B07 | EnterpriseBench | 2026 | 综合/跨领域 | 英文 | [arXiv](https://arxiv.org/abs/2609.37658) · [GitHub](https://github.com/sduyangmin/FirmBench) | 有入口 |
| B15 | PIXIU | 2023 | 财务与会计 | 英文 | [arXiv](https://arxiv.org/abs/2306.05443) · [GitHub](https://github.com/The-FinAI/PIXIU) | 有入口 |
| B18 | FinBen | 2024 | 财务与会计 | 英文 | [arXiv](https://arxiv.org/abs/2402.12659) · [GitHub](https://github.com/The-FinAI/PIXIU) | 有入口 |

## 5. 按基准领域分类

### 5.1 领域总览

| 领域 | 条目 | 年份跨度 | 类型构成 | 有入口 |
|---|---:|---|---|---|
| 综合/跨领域 | 10 | 2023—2026 | 推理型 1 · 决策与博弈型 3 · 智能体型 2 · 模拟环境型 2 · 综合套件型 2 | 9/10 |
| 财务与会计 | 26 | 2022—2026 | 知识型 8 · 推理型 9 · 决策与博弈型 3 · 智能体型 4 · 综合套件型 2 | 20/26 |
| 管理科学与运营 | 28 | 2023—2026 | 推理型 11 · 决策与博弈型 8 · 智能体型 3 · 模拟环境型 5 · 效度与行为型 1 | 22/28 |
| 战略管理与创业 | 5 | 2025—2026 | 推理型 1 · 决策与博弈型 1 · 模拟环境型 3 | 4/5 |
| 市场营销与消费者 | 4 | 2026 | 模拟环境型 1 · 效度与行为型 3 | 4/4 |
| 组织行为与人力资源 | 3 | 2024—2026 | 效度与行为型 3 | 2/3 |
| 商业分析与信息系统 | 11 | 2024—2026 | 推理型 3 · 智能体型 8 | 9/11 |

> 「有入口」= 有可访问的项目页、仓库或数据页面；分母为该域条目数。

### 5.2 各领域主表

以下 7 张表是本文档的主体：每个基准给出**规模、语言、公开度、论文与入口链接、许可、一句话定位**，按年份升序排列。

### 5.3 综合/跨领域（10 个）

**观察**
- 该域横跨两代：旧代是「题目」（BizBench 的定量推理、TheAgentCompany 的数字员工），新代是「企业全景」（Era by Eon 的生成式企业、EGI-BENCH 聚合套件、Business Arena / Market-Bench 竞技场）。
- 类型最杂（7 类里占了 5 类），说明「综合」不是一种评测方法，而是「不属于任何单一子域」的剩余集合。
- 条目之间的场地差异极大：既有 20k 题的静态题库，也有需要持续运营数十天的在线环境。

| 编号 | 基准 | 年 | 类型 | 规模 | 语 | 公开 | 链接（论文 · 入口） | 许可 | 定位 |
|---|---|---:|---|---|---|---|---|---|---|
| B01 | BizBench | 2023 | 推理型 | 20k, 8任务（商业与金融领域的定量推理基准） | 英文 | 有入口 | [arXiv](https://arxiv.org/abs/2311.06602) · [HF](https://huggingface.co/datasets/kensho/bizbench) | Apache-2.0 | 商业与金融定量推理基准，20k 题分 8 类任务（财报计算、比率、图表读数等），是「商业数值推理」的奠基性工作。 |
| B02 | TheAgentCompany | 2024 | 智能体型 | 未披露 | 英文 | 有入口 | [arXiv](https://arxiv.org/abs/2412.14161) · [GitHub](https://github.com/TheAgentCompany/TheAgentCompany) | MIT | 模拟一家软件公司的工作环境，检验智能体完成真实岗位任务（沟通、编码、协作）的能力。 |
| B03 | BizCompass | 2026 | 决策与博弈型 | 4域×3角色 | 英文 | 有入口 | [arXiv](https://arxiv.org/abs/2604.17305) · [项目页](https://bizcompass.dev.ypemc.com) | MIT | 以「商业知识 + 商业应用」两层任务衡量 LLM 的经理人式推理，覆盖 4 个商业域与 3 类角色视角。 |
| B04 | Business Arena | 2026 | 模拟环境型 | 15模型/长程 | 英文 | 有入口 | [arXiv](https://arxiv.org/abs/2608.08621) · [项目页](https://business-arena.site.accio.ai/) | 未声明 | 真实跨境店铺经营环境下的长程竞争基准，多个 LLM 在相近初始条件下运营店铺并比较长期收益。 |
| B05 | BusinessCaseBench | 2026 | 决策与博弈型 | 数百题/18学科 | 英文 | 无入口 | [arXiv](https://arxiv.org/abs/2607.16057) | CC-BY-4.0 | 以商学院案例为素材，跨 18 个学科评测知识工作与商业分析推理能力。 |
| B06 | EGI-BENCH | 2026 | 综合套件型 | 8个企业基准 | 英文 | 有入口 | [arXiv](https://arxiv.org/abs/2610.27234) · [GitHub](https://github.com/SalesforceAIResearch/egi-bench) | CC-BY-NC-4.0 | 企业通用智能套件，聚合 8 个企业基准，覆盖 CRM 操作、异构文档检索、个人数据理解与多轮规划等能力弧。 |
| B07 | EnterpriseBench | 2026 | 综合套件型 | 多领域，4基础QA+3交互决策 | 英文 | 有入口 | [arXiv](https://arxiv.org/abs/2609.37658) · [GitHub](https://github.com/sduyangmin/FirmBench) | Apache-2.0 | 企业级战略推理与决策的多任务套件，由 4 类基础问答与 3 类交互式决策任务构成。 |
| B08 | Era by Eon | 2026 | 智能体型 | 23公司/33题 | 英文 | 有入口 | [arXiv](https://arxiv.org/abs/2609.09853) · [GitHub](https://github.com/eon-io/era) | 未声明 | 生成式企业环境基准，构造 23 家公司与 33 道题并给出精确 ground truth，避免使用客户生产数据做评测。 |
| B09 | MBA-Bench | 2026 | 决策与博弈型 | 30K | 英文 | 有入口 | [arXiv](https://arxiv.org/abs/2608.11616) · [HF](https://huggingface.co/hchoi256/mba) | MIT | 多模态商业创意基准与创意 Agent，30K 规模，评测模型提出可落地商业创意的能力。 |
| B10 | Market-Bench | 2026 | 模拟环境型 | 20模型 | 英文 | 有入口 | [arXiv](https://arxiv.org/abs/2604.05523) · [GitHub](https://github.com/aiben-ch/Market-Bench) | 未声明 | 经济与贸易竞争基准，智能体在供应链竞标与定价环境中争夺资源，衡量其获取与管理经济资源的能力。 |

### 5.4 财务与会计（26 个）

**观察**
- 结构最完整：知识 8 → 推理 9 → 智能体 4 → 套件 2，四层齐全，是唯一「全谱系」覆盖的子领域。
- 上游数据高度集中：SEC 文件（FinanceBench、SECQUE、Fin-RATE）、上市公司财报（FinRule-Bench）、考试题库（CFinBench、FinEval、CFLUE、CFBenchmark、FINESSE-Bench、Japanese Financial Benchmark）。
- 中文金融是全球中文基准中最成熟的样板：8 个中文/中英财务条目，已覆盖知识、多模态（CFMME）、真实业务问句（BizFinBench）。
- 空白在「审计」：仅 2 个（AuditFraudBench、AuditBench），且都无公开入口；「财务决策」只有 3 个（UCFE 及两个审计类），远少于「财务计算」。

| 编号 | 基准 | 年 | 类型 | 规模 | 语 | 公开 | 链接（论文 · 入口） | 许可 | 定位 |
|---|---|---:|---|---|---|---|---|---|---|
| B11 | ConvFinQA | 2022 | 推理型 | 大规模 | 英文 | 有入口 | [DOI](https://doi.org/10.18653/v1/2022.emnlp-main.421) · [GitHub](https://github.com/czyssrs/ConvFinQA) | MIT | 对话式金融问答基准，要求在多轮对话中串联数值推理链，是金融多步数值推理的奠基性工作。 |
| B12 | CFBenchmark | 2023 | 知识型 | 8任务 | 中文 | 有入口 | [arXiv](https://arxiv.org/abs/2311.05812) · [GitHub](https://github.com/TongjiFinLab/CFBenchmark) | Apache-2.0 | 中文金融助手基准，按金融文本处理、金融计算、金融分析与报告生成等任务划分评测。 |
| B13 | FinEval | 2023 | 知识型 | 8351题 | 中文 | 有入口 | [arXiv](https://arxiv.org/abs/2308.09975) · [GitHub](https://github.com/SUFE-AIFLM-Lab/FinEval) | Apache-2.0 | 中文金融知识基准，8,351 道单选题覆盖金融、经济、会计、统计等学科。 |
| B14 | FinanceBench | 2023 | 推理型 | 10231题 | 英文 | 部分公开 | [arXiv](https://arxiv.org/abs/2311.11944) · [HF](https://huggingface.co/datasets/PatronusAI/financebench) | CC-BY-NC-4.0 | 基于真实上市公司财报的开放书问答基准，需先检索证据片段再完成数值计算。 |
| B15 | PIXIU | 2023 | 综合套件型 | 136K指令 | 英文 | 有入口 | [arXiv](https://arxiv.org/abs/2306.05443) · [GitHub](https://github.com/The-FinAI/PIXIU) | MIT | 金融领域「模型 + 指令数据 + 评测基准（FLARE）」一体化资源，为该方向的奠基性工作。 |
| B16 | CFLUE | 2024 | 知识型 | 38K+/16K+ | 中文 | 有入口 | [DOI](https://doi.org/10.18653/v1/2024.findings-acl.337) · [GitHub](https://github.com/aliyun/cflue) | CC-BY-NC-SA-4.0 | 中文金融语言理解评测集，覆盖金融考试、业务知识、文本匹配与金融文本生成。 |
| B17 | CFinBench | 2024 | 知识型 | 99100题 | 中文 | 有入口 | [arXiv](https://arxiv.org/abs/2407.02301) · [项目页](https://cfinbench.github.io/) | Apache-2.0（代码）/未声明（数据） | 中文金融考试型知识基准，9.91 万题覆盖金融从业与高校课程考试题型。 |
| B18 | FinBen | 2024 | 综合套件型 | 36数据集/24任务 | 英文 | 有入口 | [arXiv](https://arxiv.org/abs/2402.12659) · [GitHub](https://github.com/The-FinAI/PIXIU) | MIT | 金融 LLM 综合评测套件，聚合 36 个数据集、24 项任务，覆盖信息抽取、问答、生成、预测与决策。 |
| B19 | Golden Touchstone | 2024 | 知识型 | 8任务 | 中英双语 | 有入口 | [arXiv](https://arxiv.org/abs/2411.06272) · [GitHub](https://github.com/IDEA-FinAI/Golden-Touchstone) | Apache-2.0 | 中英双语金融基准，围绕金融考试与工作任务设 8 类评测，兼顾中英两种语境。 |
| B20 | Japanese Financial Benchmark | 2024 | 知识型 | 未披露 | 日文 | 有入口 | [arXiv](https://arxiv.org/abs/2403.15062) · [GitHub](https://github.com/pfnet-research/japanese-lm-fin-harness) | MIT | 日文金融知识基准，把英文金融考试题本地化，评测日语金融语境下的知识与理解。 |
| B21 | UCFE | 2024 | 决策与博弈型 | 804用户 | 英文 | 有入口 | [arXiv](https://arxiv.org/abs/2410.14059) · [GitHub](https://github.com/TobyYang7/UCFE-Benchmark/tree/main) | Apache-2.0 | 以用户为中心评测金融专业能力，基于 804 份用户调研构建题目与评分维度，强调与人类偏好对齐。 |
| B22 | AuditBench | 2025 | 决策与博弈型 | 5阶段 | 英文 | 无入口 | [arXiv](https://arxiv.org/abs/2506.17282) | 未声明 | 将财务报表审计拆为 5 个阶段，评测 LLM 完成自动化审计流程的能力。 |
| B23 | SECQUE | 2025 | 推理型 | 565题 | 英文 | 有入口 | [arXiv](https://arxiv.org/abs/2504.04596) · [HF](https://huggingface.co/datasets/nogabenyoash/SecQue) | MIT | 基于 SEC 文件的真实财务分析基准，565 道专家撰写问题覆盖多行业与多类分析任务。 |
| B24 | XFinBench | 2025 | 推理型 | 4235题 | 英文 | 有入口 | [DOI](https://doi.org/10.18653/v1/2025.findings-acl.457) · [GitHub](https://github.com/Zhihan72/XFinBench) | MIT | 真实金融场景的复杂问题求解基准，4,235 题强调多步数值推理与专业分析。 |
| B25 | AuditFraudBench | 2026 | 决策与博弈型 | 3任务 | 英文 | 无入口 | [arXiv](https://arxiv.org/abs/2606.08345) | 未声明 | 审计判断基准，检验模型识别财务报表舞弊性错报的能力。 |
| B26 | BizFinBench | 2026 | 推理型 | 6781题 | 中文 | 有入口 | [arXiv](https://arxiv.org/abs/2505.19457) · [GitHub](https://github.com/HiThink-Research/BizFinBench) | CC-BY-4.0 | 以真实金融业务问题构建的中文基准，6,781 题覆盖知识问答、数值计算、信息抽取与逻辑推理等多类任务。 |
| B27 | BizFinBench.v2 | 2026 | 推理型 | 6781题 | 中文 | 有入口 | [DOI](https://doi.org/10.48550/arXiv.2601.06401) · [GitHub](https://github.com/HiThink-Research/BizFinBench) | CC-BY-4.0 | BizFinBench 升级版，引入真实用户问句与离线／在线双语评测，缓解模拟数据与真实分布的偏差。 |
| B28 | BlueFin | 2026 | 智能体型 | 131任务/3225标准 | 英文 | 有入口 | [arXiv](https://arxiv.org/abs/2605.30907) · [HF](https://huggingface.co/datasets/Longitude-Labs/bluefin-release) | CC-BY-NC-4.0 | 专业财务场景的电子表格智能体基准，131 个任务含 3,225 条评分标准，覆盖表格合成、操作与理解。 |
| B29 | CFMME | 2026 | 知识型 | 6052题 | 中文 | 有入口 | [arXiv](https://arxiv.org/abs/2605.29462) · [GitHub](https://github.com/aliyun/qwen-dianjin) | MIT | 中文金融多模态评测集，6,052 题含图表与研报版面等视觉信息，检验大视觉语言模型的金融理解。 |
| B30 | FINESSE-Bench | 2026 | 知识型 | 3993题/8套 | 英文 | 有入口 | [arXiv](https://arxiv.org/abs/2605.15482) · [GitHub](https://github.com/LimexAILab/FINESSE-Bench) | Apache-2.0 | 分层金融知识与技术分析基准，8 套子集共 3,993 题，含 CFA 类题库与俄语子集。 |
| B31 | Fin-RATE | 2026 | 推理型 | 17模型 | 英文 | 有入口 | [arXiv](https://arxiv.org/abs/2602.07294) · [HF](https://huggingface.co/datasets/GGLabYale/Fin-RATE) | MIT | 基于 SEC 文件的真实财务分析与追踪评测，强调多文档查阅与跨期指标计算。 |
| B32 | FinMaster | 2026 | 智能体型 | 未披露 | 英文 | 有入口 | [DOI](https://doi.org/10.18653/v1/2026.findings-acl.385) · [GitHub](https://github.com/JiangInsight/Finmaster) | 未声明 | 全流程财务管理的整体性基准，覆盖从数据处理到报表与决策建议的完整链条。 |
| B33 | FinRule-Bench | 2026 | 推理型 | 1117+4385+400 | 英文 | 部分公开 | [arXiv](https://arxiv.org/abs/2603.11339) · [匿名仓库](https://anonymous.4open.science/r/FinRule-Bench-6723/README.md) | MIT | 联合「结构化财务报表 + 会计准则条文」的推理基准，评测规则约束下的计算与判断。 |
| B34 | FinVQA（FIND） | 2026 | 推理型 | 18900题 | 多语种 | 有入口 | [arXiv](https://arxiv.org/abs/2605.13330) · [GitHub](https://github.com/sarmistha-D/FIND_FinVQA) | 未声明 | 面向印度语系的多模态金融推理问答（含图表），18,900 题检验多语言财务数值推理。 |
| B35 | Finch | 2026 | 智能体型 | 未披露 | 英文 | 无入口 | [DOI](https://doi.org/10.18653/v1/2026.findings-acl.523) | 未声明 | 面向「以电子表格为中心」的财务与会计企业工作流基准，任务跨越多个表格与业务环节。 |
| B36 | Herculean | 2026 | 智能体型 | 4工作流×30配置 | 英文 | 部分公开 | [arXiv](https://arxiv.org/abs/2605.14355) · [HF](https://huggingface.co/datasets/TheFinAI/Herculean) | CC-BY-4.0 | 金融智能体型基准，以 4 条金融工作流 × 30 种配置检验多步工具调用与结果交付。 |

### 5.5 管理科学与运营（28 个）

**观察**
- 运筹优化建模是最大簇（11 个推理）：从 NL4OPT（2023 竞赛）→ ORLM/IndustryOR（工业落地）→ MIPLIB-NL（工业级规模）→ MM-OptBench（多模态）、OR-Space（全生命周期）、FrontierOR（算法设计）、OptMATH（数据合成），是本研究方向最完整的一条演进链。
- 博弈与谈判自成一簇（8 个决策）：形式化博弈（GTBench、CHBench、STAR）与真实议价（Bargaining、AgenticPay、Cattle Trade）两条线并行。
- 模拟/长程 5 个：供应链（SCM-Arena）、电商运营（E-Commerce Bench）、售货机（Vending-Bench）、教学模拟（AI Playing Business Games）、多智能体竞争（FM-Bench）。
- 方法论缺口：行为效度只有 1 个（AIM-Bench 的库存决策偏差），而运筹/供应链恰恰是行为运作管理最有积累的领域。

| 编号 | 基准 | 年 | 类型 | 规模 | 语 | 公开 | 链接（论文 · 入口） | 许可 | 定位 |
|---|---|---:|---|---|---|---|---|---|---|
| B37 | NL4OPT | 2023 | 推理型 | 1101题 | 英文 | 有入口 | [arXiv](https://arxiv.org/abs/2303.08233) · [GitHub](https://github.com/nl4opt/nl4opt-competition) | MIT | 运筹优化建模竞赛基准，将自然语言业务描述转为线性／整数规划模型，是该方向的奠基性基准。 |
| B38 | OptiMUS / NLP4LP | 2023 | 推理型 | 361 | 英文 | 有入口 | [arXiv](https://arxiv.org/abs/2310.06116) · [HF](https://huggingface.co/datasets/udell-lab/NLP4LP) | CC-BY-NC-4.0 | 面向优化建模的智能体式求解框架，配套 NLP4LP 数据集（361 题）检验从自然语言到 MIP 模型的建模能力。 |
| B39 | Bargaining（议价基准） | 2024 | 决策与博弈型 | 未披露 | 英文 | 有入口 | [DOI](https://doi.org/10.18653/v1/2024.findings-acl.213) · [GitHub](https://github.com/TianXiaSJTU/AmazonPriceHistory) | Apache-2.0 | 基于真实商品价格历史的买卖议价基准，配套「买方增强」方法提升 LLM 的谈判成交率。 |
| B40 | EconLogicQA | 2024 | 推理型 | 650+ | 英文 | 有入口 | [arXiv](https://arxiv.org/abs/2405.07938) · [HF](https://huggingface.co/datasets/yinzhu-quan/econ_logic_qa) | CC-BY-NC-SA-4.0 | 经济学序列推理问答基准，要求沿经济逻辑链条推断事件后续，650+ 题。 |
| B41 | GTBench | 2024 | 决策与博弈型 | 10游戏 | 英文 | 有入口 | [arXiv](https://arxiv.org/abs/2402.12348) · [GitHub](https://github.com/jinhaoduan/GTBench) | MIT | 用 10 个形式化博弈评测 LLM 的策略推理，量化其与博弈论最优解的差距。 |
| B42 | ORLM / IndustryOR | 2024 | 推理型 | 100 | 英文 | 有入口 | [arXiv](https://arxiv.org/abs/2405.17743) · [GitHub](https://github.com/Cardinal-Operations/ORLM) | Apache-2.0 | 工业界真实场景的优化建模基准（100 题），同时提出 ORLM 训练框架，强调「从企业需求到模型」的落地能力。 |
| B43 | ORQA | 2024 | 推理型 | 1500 | 英文 | 有入口 | [arXiv](https://arxiv.org/abs/2412.17874) · [GitHub](https://github.com/nl4opt/ORQA) | 无（仓库未声明） | 运筹学领域推理基准，1,500 题覆盖 OR 概念理解与建模推理。 |
| B44 | AI Playing Business Games | 2025 | 模拟环境型 | 12个月 | 英文 | 有入口 | [arXiv](https://arxiv.org/abs/2509.26331) · [SourceForge](https://sourceforge.net/projects/supply-chain-competition-game/files/) | Creative Commons Attribution Non-Commercial License V2.0 | 以开源电子表格供应链竞争模拟游戏为环境，评测 LLM 在动态竞争中的管理决策，可完全复现。 |
| B45 | AIM-Bench | 2025 | 效度与行为型 | 未披露 | 英文 | 无入口 | [arXiv](https://arxiv.org/abs/2508.11416) | 未声明 | 把 LLM 当作「库存经理」，检验其在需求不确定下的订货决策偏差（如牛鞭效应、锚定偏差）。 |
| B46 | CHBench | 2025 | 决策与博弈型 | 15标准式 | 英文 | 无入口 | [arXiv](https://arxiv.org/abs/2508.11944) | 未声明 | 认知层级基准，用 15 个标准式博弈推断 LLM 的策略层级与迭代推理深度。 |
| B47 | OptMATH | 2025 | 推理型 | 合成数据+难题基准 | 英文 | 有入口 | [arXiv](https://arxiv.org/abs/2502.11102) · [GitHub](https://github.com/optsuite/OptMATH) | Apache-2.0 | 双向数据合成框架，产出可扩展的优化建模训练数据与难题测试集，用于提升建模鲁棒性。 |
| B48 | Vending-Bench | 2025 | 模拟环境型 | 2000万token/次 | 英文 | 有入口 | [arXiv](https://arxiv.org/abs/2502.15840) · [项目页](https://andonlabs.com/evals/vending-bench-2) | 未声明 | 以自动售货机经营为场景的长程一致性基准，单次运行消耗约 2,000 万 token，检验长期目标保持与库存／定价决策。 |
| B49 | AgenticPay | 2026 | 决策与博弈型 | 110+任务 | 英文 | 有入口 | [arXiv](https://arxiv.org/abs/2602.06008) · [GitHub](https://github.com/SafeRL-Lab/AgenticPay) | MIT | 买卖双方的多智能体谈判仿真基准，110+ 任务覆盖不同商品、预算与对手策略下的成交与让价。 |
| B50 | Cattle Trade | 2026 | 决策与博弈型 | 242局 | 英文 | 无入口 | [arXiv](https://arxiv.org/abs/2605.14537) | 未声明 | 多智能体博弈基准，在信息不完全与资源约束下评测 LLM 的诈唬、竞价与议价能力，共 242 局。 |
| B51 | CertiGATE | 2026 | 智能体型 | 2000指令 | 英文 | 有入口 | [DOI](https://doi.org/10.2139/ssrn.7529119) · [GitHub](https://github.com/NTUZZH/CertiGATE) | MIT | 设施管理工单调度的「护栏」基准，用 2,000 条指令检验 LLM 改派工单时能否被确定性守卫正确拦截，并给出质量证书协议。 |
| B52 | E-Commerce Bench | 2026 | 模拟环境型 | 365天 | 英文 | 有入口 | [arXiv](https://arxiv.org/abs/2608.30730) · [GitHub](https://github.com/QwenLM/E-CommerceBench) | Apache-2.0 | 长时程自主商业运营的可执行评测环境，智能体需连续 365 天经营电商店铺并做出定价、选品与营销决策。 |
| B53 | FM-Bench | 2026 | 模拟环境型 | 20年/26工具 | 英文 | 有入口 | [arXiv](https://arxiv.org/abs/2608.18423) · [GitHub](https://github.com/Analogy-AI/fm-bench) | Apache-2.0 | 长时程经营管理的多智能体竞争基准，由确定性种子程序生成 20 年企业运营轨迹并开放 26 类工具接口。 |
| B54 | FrontierOR | 2026 | 推理型 | 180任务 | 英文 | 有入口 | [arXiv](https://arxiv.org/abs/2605.25246) · [GitHub](https://github.com/Minw913/FrontierOR) | CC-BY-4.0 | 面向大规模优化问题的高效算法设计基准，180 个任务检验模型能否给出可运行且性能可比的求解算法。 |
| B55 | JOR-Bench | 2026 | 推理型 | 1319题 | 日文 | 部分公开 | [arXiv](https://arxiv.org/abs/2607.16777) | 未声明 | 日文运筹学基准，由 5 个英文 OR 基准日译并本地化而来（1,319 题），用于检验跨语言迁移。 |
| B56 | MIPLIB-NL | 2026 | 推理型 | 223题 | 英文 | 有入口 | [arXiv](https://arxiv.org/abs/2602.10450) · [GitHub](https://github.com/optsuite/MIPLIB-NL) | CC BY-SA 4.0 | 工业级优化建模基准，从 MIPLIB 2017 反演生成 223 道自然语言建模题，保证与真实工业规模对齐。 |
| B57 | MM-OptBench | 2026 | 推理型 | 780题 | 英文 | 有入口 | [arXiv](https://arxiv.org/abs/2605.12154) · [GitHub](https://github.com/ZhongLIFR/MM-OptBench) | CC BY-SA 4.0 | 多模态优化建模基准，780 题以带图表的业务场景描述检验从图文到优化模型的转换，并以求解器结果为准。 |
| B58 | Negotiation Mechanism Benchmark | 2026 | 决策与博弈型 | 30次/条件 | 英文 | 无入口 | [arXiv](https://arxiv.org/abs/2608.14613) | 未声明 | 基于机制设计的可验证多智能体交互框架（A2A/MCP），检验谈判过程是否满足理性与激励相容。 |
| B59 | OPT-Engine | 2026 | 推理型 | 10类问题 | 英文 | 有入口 | [arXiv](https://arxiv.org/abs/2601.19924) · [HF](https://huggingface.co/datasets/chenyitian-shanshu/OPTEngine) | MIT | 通过复杂度分级刻画 LLM 优化建模能力上限，按 10 类问题难度递增施测。 |
| B60 | OR-Space | 2026 | 智能体型 | 3种任务模式 | 英文 | 有入口 | [arXiv](https://arxiv.org/abs/2605.28158) · [GitHub](https://github.com/0xzhouchenyu/OR-Space) | CC-BY-NC-4.0 | 面向工业优化智能体的全生命周期工作空间基准，覆盖建模、求解、调试与结果解读的完整链路。 |
| B61 | SCM-Arena | 2026 | 模拟环境型 | 75模型/53K+回合 | 英文 | 有入口 | [DOI](https://doi.org/10.2139/ssrn.6514506) · [项目页](https://scm-arena.com) | 未声明 | 供应链管理的仿真式行为基准，以多期仿真对比 LLM 与人类管理者的订货、库存与协同决策。 |
| B62 | STAR Benchmark | 2026 | 决策与博弈型 | 模拟 | 英文 | 有入口 | [arXiv](https://arxiv.org/abs/2603.09337) · [GitHub](https://github.com/star-nexus/star) | 未声明 | 零和对抗环境下的策略推理与快速决策基准，检验模型在时间压力与对手博弈中的表现。 |
| B63 | SupChain-Bench | 2026 | 智能体型 | 435+工具调用 | 英文 | 有入口 | [arXiv](https://arxiv.org/abs/2602.07342) · [GitHub](https://github.com/Damon-GSY/SC-bench) | Apache-2.0 | 真实供应链管理场景的智能体基准，任务需串联 435+ 次工具调用完成采购、排产、物流与异常处置。 |
| B64 | The Language of Bargaining | 2026 | 决策与博弈型 | 3游戏×5语言 | 多语种 | 无入口 | [arXiv](https://arxiv.org/abs/2601.04387) | 未声明 | 跨语言议价实验，3 类博弈 × 5 种语言检验语言差异如何影响 LLM 的谈判结果与公平感知。 |

### 5.6 战略管理与创业（5 个）

**观察**
- 全部围绕「高不确定性下的长期决策」：投资（VCBench）、合作（FirmCORe）、长期经营（CEO-Bench、CEO Arena、YC-Bench）。
- 与运营域的边界模糊：CEO Arena、FM-Bench 都涉及企业长期经营，本文档按「是否以市场竞争对抗为核心」分入两域（CEO Arena 战略、FM-Bench 运营）。
- 五条里没有一条覆盖「战略分析」的经典任务（行业分析、竞争定位、并购判断），这是明显的选题空位。

| 编号 | 基准 | 年 | 类型 | 规模 | 语 | 公开 | 链接（论文 · 入口） | 许可 | 定位 |
|---|---|---:|---|---|---|---|---|---|---|
| B65 | VCBench | 2025 | 决策与博弈型 | 9000档案 | 英文 | 有入口 | [arXiv](https://arxiv.org/abs/2509.14448) · [项目页](https://vcbench.com) | 未声明 | 风险投资决策基准，9,000 份创业公司档案用于检验模型的投资判断（是否投资、估值与理由）。 |
| B66 | CEO Arena | 2026 | 模拟环境型 | 8公司/500天 | 英文 | 有入口 | [arXiv](https://arxiv.org/abs/2609.34821) · [GitHub](https://github.com/FoundationAgents/CEO-Arena) | MIT | 竞争市场中的长程多智能体决策基准，8 家公司对战 500 天，以配对替换设计控制公司间差异。 |
| B67 | CEO-Bench | 2026 | 模拟环境型 | 500天 | 英文 | 有入口 | [arXiv](https://arxiv.org/abs/2606.18543) · [GitHub](https://github.com/zlab-princeton/ceobench-src) | 无（仓库未声明） | 「CEO 长局」基准，智能体在 500 天仿真中持续做经营决策，检验长期规划与目标一致性。 |
| B68 | FirmCORe | 2026 | 推理型 | 2805对 | 中英双语 | 无入口 | [arXiv](https://arxiv.org/abs/2609.17128) | 未声明 | 企业间合作机会的结构化推理基准，2,805 对企业配对要求模型推断合作可行性与匹配理由。 |
| B69 | YC-Bench | 2026 | 模拟环境型 | 1年 | 英文 | 有入口 | [arXiv](https://arxiv.org/abs/2604.01212) · [GitHub](https://github.com/collinear-ai/yc-bench) | MIT（PyPI元数据） | 面向初创企业一年经营周期的规划与执行基准，检验长程计划的一致落地。 |

### 5.7 市场营销与消费者（4 个）

**观察**
- 三个是「效度」、一个是「长程经营」，说明该域的核心问题已经从「LLM 懂不懂营销」转为「LLM 能不能替代消费者/被试」。
- ConsumerSimBench 是唯一的中文条目，做的是「群体级反应重建」——比个体级模拟更难，也更接近营销实务。
- RetailBench 单独承担「长程经营」，180 天的策略稳定性是营销域唯一的长期视角。
- 空白：广告文案/创意、定价与促销、渠道与投放等营销主干任务，一个基准都没有。

| 编号 | 基准 | 年 | 类型 | 规模 | 语 | 公开 | 链接（论文 · 入口） | 许可 | 定位 |
|---|---|---:|---|---|---|---|---|---|---|
| B70 | Artificial Societies Benchmark | 2026 | 效度与行为型 | 11测试/20数据源 | 英文 | 有入口 | [arXiv](https://arxiv.org/abs/2609.30030) · [GitHub](https://github.com/artificial-societies/artificial-societies-benchmark) | MIT | 合成社会／合成用户研究的验证框架，以 11 项测试、20 个数据源检验模拟结果的可信度。 |
| B71 | ConsumerSimBench | 2026 | 效度与行为型 | 1553话题/23122标准 | 中文 | 有入口 | [arXiv](https://arxiv.org/abs/2605.17079) · [HF](https://huggingface.co/datasets/wty500/ConsumerSimBench) | CC-BY-NC-4.0 | 检验 LLM 能否重建「群体级」消费者反应，1,553 个话题 × 23,122 条评价标准，服务于营销决策预演。 |
| B72 | RetailBench | 2026 | 模拟环境型 | 180天 | 英文 | 有入口 | [arXiv](https://arxiv.org/abs/2603.16453) · [GitHub](https://github.com/linghuazhang01/RetailBench) | MIT | 真实零售环境的长时程自主决策基准，180 天经营考察策略稳定性与长程一致性。 |
| B73 | When Synthetic Users Fail | 2026 | 效度与行为型 | GSS+WVS两域 | 英文 | 有入口 | [arXiv](https://arxiv.org/abs/2607.26348) · [GitHub](https://github.com/ZihanChen1995/when-synthetic-users-fail-a-cross-domain-benchmark-of-llm-simulated-human-survey-responses) | CC-BY-4.0 | 跨域效度基准，用 GSS 与 WVS 两套社会调查数据检验 LLM 模拟人类作答在什么条件下失效。 |

### 5.8 组织行为与人力资源（3 个）

**观察**
- 全部是公平性审计（JobFair、FAIRE、FairHireBench），**没有一条**评测任务能力（简历筛选、绩效评估、培训材料生成、面试提问）。
- FairHireBench 引入交叉性（年龄 × 性别 × 种族）是方法上最细的一条；JobFair 用 300 份简历对做对照，成本最低、最易复现。
- 数据最敏感：简历类数据普遍涉及隐私，公开形态多为样例或需申请。
- 这一域是「供给最少 + 伦理需求最强」的矛盾区，也是中文研究最容易做出差异化的方向。

| 编号 | 基准 | 年 | 类型 | 规模 | 语 | 公开 | 链接（论文 · 入口） | 许可 | 定位 |
|---|---|---:|---|---|---|---|---|---|---|
| B74 | JobFair | 2024 | 效度与行为型 | 300 | 英文 | 部分公开 | [DOI](https://doi.org/10.18653/v1/2024.findings-emnlp.184) · [HF](https://huggingface.co/datasets/holistic-ai/job-fair-resume) | MIT | 招聘性别偏见基准，用 300 份简历对检验模型在不同岗位与条件下对性别的隐性偏好。 |
| B75 | FAIRE | 2025 | 效度与行为型 | 未披露 | 英文 | 有入口 | [arXiv](https://arxiv.org/abs/2504.01420) · [GitHub](https://github.com/athenawen/FAIRE-Fairness-Assessment-In-Resume-Evaluation) | MIT | 简历评估中的种族与性别偏见基准，通过成对简历对照检验模型的评分差异。 |
| B76 | FairHireBench | 2026 | 效度与行为型 | 10005档案/15组 | 英文 | 有入口 | [DOI](https://doi.org/10.1145/3805689.3806487) · [HF](https://huggingface.co/datasets/Sweta6/FairHire) | MIT / CC-BY-4.0 | 跨代际交叉性偏见基准，10,005 份档案 × 15 组属性组合，考察年龄 × 性别 × 种族的叠加歧视。 |

### 5.9 商业分析与信息系统（11 个）

**观察**
- CRM/ERP 是企业软件主战场：CRMArena-Pro、CRM-Agent-Bench、ERPBench（企业决策）、ERPBench（Computer-Use）、RevOpsBench 五个构成「CRM → ERP → 营收运营」的完整链条。
- 电子表格已独立成赛道：SpreadsheetBench 2、BlueFin、Finch 三个，且都强调「端到端交付」而非单元格级操作。
- BPM 只有 2 个（Kourani、Busch & Leopold），属于「高价值低供给」，且都无明确数据许可。
- WorkArena（2024）是最早的企业网页智能体基准，许可标注为 NOASSERTION，复用前需与作者确认。

| 编号 | 基准 | 年 | 类型 | 规模 | 语 | 公开 | 链接（论文 · 入口） | 许可 | 定位 |
|---|---|---:|---|---|---|---|---|---|---|
| B77 | Kourani BPM | 2024 | 推理型 | 20流程 | 英文 | 有入口 | [arXiv](https://arxiv.org/abs/2412.00023) · [GitHub](https://github.com/humam-kourani/EvaluatingLLMsProcessModeling) | 未声明 | 业务流程建模基准，要求模型把自然语言流程描述转为 BPMN 模型，20 个流程覆盖多种结构。 |
| B78 | WorkArena | 2024 | 智能体型 | 33任务 | 英文 | 有入口 | [arXiv](https://arxiv.org/abs/2403.07718) · [GitHub](https://github.com/ServiceNow/WorkArena) | 其他（NOASSERTION） | 基于 ServiceNow 实例的网页智能体基准，33 类知识工作任务检验浏览器操作能力，是该方向的高引用基准。 |
| B79 | Busch & Leopold BPM | 2025 | 推理型 | 4类任务 | 英文 | 有入口 | [DOI](https://doi.org/10.24251/hicss.2025.709) · [GitHub](https://github.com/KiriBu10/openLLMinBPM-benchmark/tree/dev_kiran) | 无（仓库未声明） | 面向业务流程管理（BPM）任务的 LLM 基准，分 4 类任务（流程要素抽取、模型生成、问答等）。 |
| B80 | CORGI | 2025 | 推理型 | 4类问题 | 英文 | 有入口 | [arXiv](https://arxiv.org/abs/2510.07309) · [GitHub](https://github.com/Moonn521/CORGI) | MIT | 面向商业领域的 Text-to-SQL 基准，要求模型不仅取数还要完成经营分析型查询（4 类问题）。 |
| B81 | CRMArena-Pro | 2025 | 智能体型 | 19任务 | 英文 | 有入口 | [arXiv](https://arxiv.org/abs/2505.18878) · [GitHub](https://github.com/SalesforceAIResearch/CRMArena) | CC BY-NC 4.0 | 在 CRM 沙盒中评测 LLM 智能体的多轮交互与业务动作，覆盖 19 类任务并强调保密意识与多轮对话。 |
| B82 | DABstep | 2025 | 智能体型 | 450+挑战 | 英文 | 有入口 | [arXiv](https://arxiv.org/abs/2506.23719) · [HF](https://huggingface.co/datasets/adyen/dabstep) | CC-BY-4.0 | 面向真实支付／交易数据的多步数据分析智能体基准，挑战需串联查询、计算与业务判断。 |
| B83 | CRM-Agent-Bench | 2026 | 智能体型 | 555任务 | 英文 | 有入口 | [arXiv](https://arxiv.org/abs/2610.32004) · [GitHub](https://github.com/salesforce-misc/crm-agent-bench) | Apache-2.0 | 有状态企业环境中的工具调用基准，555 个任务要求智能体正确执行多步业务流程并遵守领域规则。 |
| B84 | ERPBench（Computer-Use） | 2026 | 智能体型 | 未披露 | 英文 | 无入口 | [arXiv](https://arxiv.org/abs/2609.17885) | 未声明 | 面向企业软件（ERP）的「状态接地」评测范式，智能体通过截图与模拟操作完成企业任务。 |
| B85 | ERPBench（企业决策） | 2026 | 智能体型 | 100题/6轮 | 英文 | 有入口 | [arXiv](https://arxiv.org/abs/2609.04667) · [GitHub](https://github.com/GAIR-NLP/erp-bench) | MIT | 检验企业决策结论能否跨「竞争性市场生态」迁移，以 100 题 × 6 轮交互模拟多市场竞争。 |
| B86 | RevOpsBench | 2026 | 智能体型 | 6100任务/78350轨迹 | 英文 | 部分公开 | [DOI](https://doi.org/10.1109/southeastcon63549.2026.11475978) | 未声明 | 面向企业营收运营（RevOps）的大规模 CRM 智能体基准，6,100 个任务、78,350 条轨迹，基于 1,487 名终端用户的真实操作日志。 |
| B87 | SpreadsheetBench 2 | 2026 | 智能体型 | 321任务 | 英文 | 有入口 | [arXiv](https://arxiv.org/abs/2606.29955) · [HF](https://huggingface.co/datasets/KAKA22/SpreadsheetBench-v2) | MIT | 端到端商业表格工作流基准，321 个任务要求智能体在真实工作簿上完成数据整理、计算与交付。 |

## 6. 开源与可复现性

### 6.1 入口形式

| 入口形式 | 条目 | 占比 |
|---|---:|---:|
| GitHub | 51 | 59% |
| HF | 15 | 17% |
| 无任何地址（仅论文） | 13 | 15% |
| 项目页 | 6 | 7% |
| 匿名仓库 | 1 | 1% |
| SourceForge | 1 | 1% |

有入口不等于能复跑：70 个条目给出了可访问地址，但其中一部分只有演示页或仅有仓库骨架；6 个仅公开样例或需申请授权，11 个未检索到任何公开页面。有入口的 70 个 + 无任何地址的 13 个 = 87，两个口径的差额来自「标注部分公开但未给出地址」的 2 个条目。

### 6.2 可复现性分级

按「数据能否拿到 + 许可能否直接用」把 87 个基准分成三级：

| 级别 | 判定标准 | 条目 | 说明 |
|---|---|---|---|
| **A · 可直接用于论文实验** | 有入口 + 有仓库/数据页 + 许可宽松 | **46** | MIT / Apache-2.0 / CC-BY-4.0 / CC BY-SA 4.0，可直接下载、可二次发布衍生数据 |
| **B · 可用但受限** | 部分公开，或非商业许可，或许可不明 | **28** | 需申请授权、只能内部实验、或使用前必须先确认许可 |
| **C · 实际不可复现** | 无入口，或无任何公开地址 | **13** | 只能引用其结论，无法复跑 |

**A 级清单（46 个，做横向实验优先从这里选）**

- **综合/跨领域**：BizBench、TheAgentCompany、BizCompass、EnterpriseBench、MBA-Bench
- **财务与会计**：ConvFinQA、CFBenchmark、FinEval、PIXIU、FinBen、Golden Touchstone、Japanese Financial Benchmark、UCFE、SECQUE、XFinBench、BizFinBench、BizFinBench.v2、CFMME、FINESSE-Bench、Fin-RATE
- **管理科学与运营**：NL4OPT、Bargaining（议价基准）、GTBench、ORLM / IndustryOR、OptMATH、AgenticPay、CertiGATE、E-Commerce Bench、FM-Bench、FrontierOR、MIPLIB-NL、MM-OptBench、OPT-Engine、SupChain-Bench
- **战略管理与创业**：CEO Arena、YC-Bench
- **市场营销与消费者**：Artificial Societies Benchmark、RetailBench、When Synthetic Users Fail
- **组织行为与人力资源**：FAIRE、FairHireBench
- **商业分析与信息系统**：CORGI、DABstep、CRM-Agent-Bench、ERPBench（企业决策）、SpreadsheetBench 2

**C 级清单（13 个，只能引用、不能复跑）**

BusinessCaseBench（`B05`）、AuditBench（`B22`）、AuditFraudBench（`B25`）、Finch（`B35`）、AIM-Bench（`B45`）、CHBench（`B46`）、Cattle Trade（`B50`）、JOR-Bench（`B55`）、Negotiation Mechanism Benchmark（`B58`）、The Language of Bargaining（`B64`）、FirmCORe（`B68`）、ERPBench（Computer-Use）（`B84`）、RevOpsBench（`B86`）

### 6.3 使用前必须确认的三类条目

**（1）数据可得性受限（17 个：部分公开 6 + 无入口 11）**

| 编号 | 基准 | 公开度 | 入口 |
|---|---|---|---|
| B05 | BusinessCaseBench | 无入口 | 无 |
| B14 | FinanceBench | 部分公开 | [HF](https://huggingface.co/datasets/PatronusAI/financebench) |
| B22 | AuditBench | 无入口 | 无 |
| B25 | AuditFraudBench | 无入口 | 无 |
| B33 | FinRule-Bench | 部分公开 | [匿名仓库](https://anonymous.4open.science/r/FinRule-Bench-6723/README.md) |
| B35 | Finch | 无入口 | 无 |
| B36 | Herculean | 部分公开 | [HF](https://huggingface.co/datasets/TheFinAI/Herculean) |
| B45 | AIM-Bench | 无入口 | 无 |
| B46 | CHBench | 无入口 | 无 |
| B50 | Cattle Trade | 无入口 | 无 |
| B55 | JOR-Bench | 部分公开 | 无 |
| B58 | Negotiation Mechanism Benchmark | 无入口 | 无 |
| B64 | The Language of Bargaining | 无入口 | 无 |
| B68 | FirmCORe | 无入口 | 无 |
| B74 | JobFair | 部分公开 | [HF](https://huggingface.co/datasets/holistic-ai/job-fair-resume) |
| B84 | ERPBench（Computer-Use） | 无入口 | 无 |
| B86 | RevOpsBench | 部分公开 | 无 |

**（2）许可不明（27 个）**

| 编号 | 基准 | 许可记录 |
|---|---|---|
| B04 | Business Arena | 未声明 |
| B08 | Era by Eon | 未声明 |
| B10 | Market-Bench | 未声明 |
| B17 | CFinBench | Apache-2.0（代码）/未声明（数据） |
| B22 | AuditBench | 未声明 |
| B25 | AuditFraudBench | 未声明 |
| B32 | FinMaster | 未声明 |
| B34 | FinVQA（FIND） | 未声明 |
| B35 | Finch | 未声明 |
| B43 | ORQA | 无（仓库未声明） |
| B45 | AIM-Bench | 未声明 |
| B46 | CHBench | 未声明 |
| B48 | Vending-Bench | 未声明 |
| B50 | Cattle Trade | 未声明 |
| B55 | JOR-Bench | 未声明 |
| B58 | Negotiation Mechanism Benchmark | 未声明 |
| B61 | SCM-Arena | 未声明 |
| B62 | STAR Benchmark | 未声明 |
| B64 | The Language of Bargaining | 未声明 |
| B65 | VCBench | 未声明 |
| B67 | CEO-Bench | 无（仓库未声明） |
| B68 | FirmCORe | 未声明 |
| B77 | Kourani BPM | 未声明 |
| B78 | WorkArena | 其他（NOASSERTION） |
| B79 | Busch & Leopold BPM | 无（仓库未声明） |
| B84 | ERPBench（Computer-Use） | 未声明 |
| B86 | RevOpsBench | 未声明 |

许可不明主要来自三种情况：仓库**没有 LICENSE 文件**、许可只写在论文里而仓库未落地、GitHub 显示 **NOASSERTION**（机器无法识别）。三者对使用的实际影响不同：第一种需联系作者；第二种可以论文声明主张；第三种属于「事实上常用、法律上未明示」，商用前必须书面确认。

**（3）非商业许可（10 个）**

EGI-BENCH、FinanceBench、CFLUE、BlueFin、OptiMUS / NLP4LP、EconLogicQA、AI Playing Business Games、OR-Space、ConsumerSimBench、CRMArena-Pro

这批只能做学术研究；若要发布衍生数据集（例如把题目翻译成中文后公开），需要逐条检查 Non-Commercial 条款。

### 6.4 使用建议

1. **先按 A 级筛**：做横向对比实验时，从 46 个 A 级里挑覆盖目标能力的 3—5 个，避免做到一半发现数据要审批。
2. **引用时写清版本与日期**：69 个是预印本，其中 42 个集中在 2026 年——同名基准的 v1/v2 与同名不同基准都必须注明版本或团队（见第 7 节）。
3. **需申请的数据提前排队**：需授权或 gated 的数据集要预留 1—2 周审批时间，纳入计划前先确认。
4. **「可复跑」比「有仓库」更重要**：仓库存在但无环境描述、无固定随机种子、无版本锁定的基准，复跑成本可能高于重写。

## 7. 命名、别名与引用易错点

同一个基准在论文题、仓库名、数据集名之间经常不一致；不同团队的基准又会撞名。本节汇总会影响检索与引用的情形。

### 7.1 名称 / 别名对照

| 本文档名称 | 论文题或仓库名 | 说明 |
|---|---|---|
| EnterpriseBench | FirmBench | 仓库名与基准名不一致 |
| CORGI | Agent Bain vs. Agent McKinsey | 论文题与数据集名不一致 |
| FinVQA | FIND | 数据集名与论文题不一致 |
| MBA-Bench | MBA | 数据集名与基准名不完全一致 |
| OptiMUS | NLP4LP | 框架名与数据集名互为别名 |
| ORLM | IndustryOR | 框架名与基准名互为别名 |
| AuditBench | Automating Financial Statement Audits | 以论文题代指基准 |
| BusinessCaseBench | Frontier AI business disciplines | 以论文题代指基准 |
| Bargaining | Measuring Bargaining Abilities of LLMs | 简称与全称并用 |
| Japanese Financial Benchmark | Construction of a Japanese Financial Benchmark | 简称与全称并用 |

### 7.2 同名不同基准

| 名称 | 团队 | 内容差异 |
|---|---|---|
| ERPBench（企业决策）`B85` | GAIR-NLP | 100 题 × 6 轮，评企业决策跨市场生态的迁移性 |
| ERPBench（Computer-Use）`B84` | 另一团队 | 以截图与模拟操作为接口，评 ERP 软件操作，无公开入口 |

检索「ERPBench」时会同时命中两者，引用时必须带上括号限定或论文题。

### 7.3 同族多版本

| 名称 | 版本关系 | 引用建议 |
|---|---|---|
| BizFinBench `B26` / BizFinBench.v2 `B27` | v1 与 v2 为两篇独立论文，共用同一仓库 | 引用时注明版本号；报告结果时说明用的是哪一代题库 |

### 7.4 三条引用建议

1. **以论文题为准、以数据集名为辅**：正文首次出现时写「数据集名（论文题）」，避免读者按数据集名检索不到原文。
2. **预印本注明编号与访问日期**：69 个条目为预印本，版本可能随时更新，只给年份不足以定位。
3. **正式版与预印本年份不同时，两个都写**：例如 ORQA 的预印本为 2024 年末、正式版发表于 AAAI 2025，单写一个年份都会造成检索偏差。

## 8. 研究空白与选题建议

### 8.1 八个空白（均有数据支撑）

| # | 空白 | 数据证据 | 可做的题目 |
|---|---|---|---|
| 1 | **非英语基准稀缺** | 英文 73 个（84%）；日文 2 个、多语 2 个，且 JOR-Bench 是对英文 OR 基准的翻译本地化 | 跨语言管理决策的迁移性：同一批题目在中英语境下的分数差异 |
| 2 | **中文只覆盖财务** | 中文/中英 10 个，其中 8 个为财务；「中文 + 运营/战略/人力」= 0 | 中文供应链/战略/HR 基准（可借生成式环境降低标注成本） |
| 3 | **人力与营销缺少「任务能力」基准** | 人力 3 个全为公平性审计；营销 4 个无一个覆盖广告、定价、渠道 | 简历筛选/绩效评估的任务型基准；营销 4P 的可执行任务集 |
| 4 | **真实企业数据受合规挤压** | 部分公开 6 个 + 无入口 11 个，多数因使用企业真实数据或私有简历 | 「不出域」评测协议；合成企业 + 精确真值（Era by Eon、FM-Bench 的思路） |
| 5 | **过程指标缺失** | 只有 BlueFin（3,225 条评分标准）、RevOpsBench（78,350 条轨迹）、UCFE（804 名用户偏好）等少数做过程级评分 | 在现有 A 级基准上补「部分得分 / 错误定位 / 合规检查」的评测协议 |
| 6 | **长程度量学未建立** | 时长口径横跨 180 天、365 天、500 天、1 年、20 年、2,000 万 token；无统一指标 | 长程基准的度量框架：如何定义「一致性」、如何控制随机性、如何固定对手 |
| 7 | **效度检验只覆盖 2 个域** | 效度型 7 个：营销 3、人力 3、运营 1；财务/信息/战略为 0 | 把「合成用户效度」迁移到运营/财务模拟基准，比较 LLM 与人类管理者的决策分布 |
| 8 | **缺元基准 / 统一 harness** | 套件型仅 4 个，任务口径互不对齐 | 跨套件的可比性研究：任务分类学 + 统一评分层 |

### 8.2 三个可落地的选题（按投入产出排序）

1. **过程级评测协议（低成本、高复用）**——不新建数据集，选 3—5 个 A 级基准（如 NL4OPT、FinanceBench、SpreadsheetBench 2、FM-Bench），在其上定义中间步骤检查点与部分得分规则，产出开源 harness + 一篇方法论文。风险最低，因为数据与许可都已就绪。
2. **中文管理决策基准（差异化最强）**——以生成式环境为底座（确定性种子 + 精确真值），先做「中文供应链运营」一个场景，做满人类对照与效度检验，可直接对标 SCM-Arena 与 FM-Bench 的评测设计。
3. **效度迁移研究（方法论贡献）**——把营销/HR 的合成用户效度框架（When Synthetic Users Fail、ConsumerSimBench）迁移到「LLM 管理者」：同一批管理决策给人类管理者与 LLM 做，比较分布而非准确率。

### 8.3 汇报用一页结论

1. 管理学基准在 2025—2026 完成了**从「考试」到「环境」**的范式迁移：2026 年 50 个新增中，智能体与模拟合计 22 个。
2. 供给高度集中在**财务与运营**（54 个，62%），因为这两个子领域有现成的公开数据。
3. 有入口 70 个，但**真正能直接复跑的只有 46 个（A 级）**；11 个无任何入口，27 个许可不明。
4. 中文是最大的空白：10 个中文/中英条目中 8 个是财务，运营/战略/人力为零。
5. 下一步建议：先做**过程级评测协议**（复用现有 A 级基准），同时启动**中文运营场景基准**的数据构建。

## 9. 数据表与引用说明

### 9.1 文件构成

```text
.
├── README.md              # 本文档：分类、统计、逐条清单与分析
└── data/
    └── benchmarks.csv     # 87 条结构化数据（UTF-8 with BOM，可直接用 Excel 打开）
```

### 9.2 `data/benchmarks.csv` 字段

| 字段 | 含义 | 取值示例 |
|---|---|---|
| `no` | 本文档编号 | `B04` |
| `name` | 基准名称 | `BizBench` |
| `title` | 论文全名 | `BizBench: A Quantitative Reasoning Benchmark...` |
| `first_author` | 首位作者姓氏 | `Koncel-Kedziorski` |
| `year` | 年份 | `2023` |
| `venue` | 载体 | `arXiv` / `NeurIPS` / `ACL Findings` / `KDD 2026` |
| `pub_status` | 发表状态 | `预印本` / `正式发表` / `工作论文` |
| `domain` | 领域（7 类） | `财务与会计` |
| `type` | 基准类型（7 类） | `推理型` |
| `language` | 语言 | `英文` / `中文` / `中英双语` |
| `scale` | 规模 | `20k, 8任务` |
| `openness` | 公开度 | `有入口` / `部分公开` / `无入口` |
| `repo_url` | 项目页 / 仓库 / 数据页 | `https://huggingface.co/...` |
| `license` | 许可（原始记录） | `Apache-2.0` |
| `license_level` | 许可分级 | `宽松` / `非商业` / `不明` |
| `paper_url` | 论文链接 | `https://arxiv.org/abs/2311.06602` |
| `repro_level` | 可复现分级 | `A` / `B` / `C` |
| `tags` | 关键词 | `定量推理、奠基性` |
| `desc` | 一句话定位 | `商业与金融定量推理基准……` |

### 9.3 引用建议

- 引用**具体基准**时，用附录 A 的论文条目（含载体与链接），不要直接引用本汇总。
- 引用**本汇总的统计口径**时，写明「截至 2026-11-08 的 87 个条目」，并注明分类为整理者自定，不同划分方式会得到不同分布。
- 本汇总的分类（7 域 / 7 类）是一件**分析工具**，不是领域内的公认标准；与他人结果对比时请说明口径。

### 9.4 更新与补充

- 建议每季度复查一次：arXiv（cs.CL / cs.AI / cs.MA）、以及 ACL / EMNLP / NeurIPS / KDD / AAAI / HICSS / FAccT 的评测类论文。
- 欢迎通过 Issue / Pull Request 补充条目或修正字段；新增条目至少需要：论文链接、载体与年份、一句话定位、公开入口（若有）、许可（若有）。
- 统计数字（第 2 / 3 节）与逐条清单（第 4 / 5 节）均以 `data/benchmarks.csv` 为同一数据源计算，口径一致；若增删条目，请同步更新 CSV 与正文计数。

## 附录 A 全量文献清单

按编号排序，共 87 条：编号、基准名、首位作者、论文全名、载体（年份）、论文链接。

- `B01` **BizBench** — Koncel-Kedziorski 等. *BizBench: A Quantitative Reasoning Benchmark for Business and Finance*. arXiv（2023）. [arXiv](https://arxiv.org/abs/2311.06602)
- `B02` **TheAgentCompany** — Xu 等. *TheAgentCompany: Benchmarking LLM Agents on Consequential Real World Tasks*. arXiv（2024）. [arXiv](https://arxiv.org/abs/2412.14161)
- `B03` **BizCompass** — Hao 等. *BizCompass: Benchmarking the Reasoning Capabilities of LLMs in Business Knowledge and Applications*. arXiv（2026）. [arXiv](https://arxiv.org/abs/2604.17305)
- `B04` **Business Arena** — Pan 等. *Business Arena: Benchmarking LLM Agents in a Realistic Marketplace*. arXiv（2026）. [arXiv](https://arxiv.org/abs/2608.08621)
- `B05` **BusinessCaseBench** — Patel 等. *Frontier AI performance across the business disciplines: a case-grounded benchmark of knowledge work and analytical reasoning*. arXiv（2026）. [arXiv](https://arxiv.org/abs/2607.16057)
- `B06` **EGI-BENCH** — Liu 等. *EGI-BENCH: An Enterprise General Intelligence Benchmark Suite*. arXiv（2026）. [arXiv](https://arxiv.org/abs/2610.27234)
- `B07` **EnterpriseBench** — Yang 等. *EnterpriseBench: Benchmarking LLM Agents on Enterprise-Level Strategic Reasoning and Decision-Making*. arXiv（2026）. [arXiv](https://arxiv.org/abs/2609.37658)
- `B08` **Era by Eon** — Gruenbaum 等. *The Era by Eon Benchmark: A Generated Enterprise Estate with Exact Ground Truth for Benchmarking LLM Agents*. arXiv（2026）. [arXiv](https://arxiv.org/abs/2609.09853)
- `B09` **MBA-Bench** — Choi 等. *MBA: Multimodal Benchmark and Agents for Real-World Business Ideation*. arXiv（2026）. [arXiv](https://arxiv.org/abs/2608.11616)
- `B10` **Market-Bench** — Zheng 等. *Market-Bench: Benchmarking Large Language Models on Economic and Trade Competition*. arXiv（2026）. [arXiv](https://arxiv.org/abs/2604.05523)
- `B11` **ConvFinQA** — Chen 等. *ConvFinQA: Exploring the Chain of Numerical Reasoning in Conversational Finance Question Answering*. EMNLP 2022. [DOI](https://doi.org/10.18653/v1/2022.emnlp-main.421)
- `B12` **CFBenchmark** — Lei 等. *CFBenchmark: Chinese Financial Assistant Benchmark for Large Language Model*. arXiv（2023）. [arXiv](https://arxiv.org/abs/2311.05812)
- `B13` **FinEval** — Guo 等. *FinEval: A Chinese Financial Domain Knowledge Evaluation Benchmark for Large Language Models*. arXiv（2023）. [arXiv](https://arxiv.org/abs/2308.09975)
- `B14` **FinanceBench** — Islam 等. *FinanceBench: A New Benchmark for Financial Question Answering*. arXiv（2023）. [arXiv](https://arxiv.org/abs/2311.11944)
- `B15` **PIXIU** — Xie 等. *PIXIU: A Large Language Model, Instruction Data and Evaluation Benchmark for Finance*. arXiv（2023）. [arXiv](https://arxiv.org/abs/2306.05443)
- `B16` **CFLUE** — Zhu 等. *Benchmarking Large Language Models on CFLUE - A Chinese Financial Language Understanding Evaluation Dataset*. ACL Findings（2024）. [DOI](https://doi.org/10.18653/v1/2024.findings-acl.337)
- `B17` **CFinBench** — Nie 等. *CFinBench: A Comprehensive Chinese Financial Benchmark for Large Language Models*. arXiv（2024）. [arXiv](https://arxiv.org/abs/2407.02301)
- `B18` **FinBen** — Xie 等. *FinBen: A Holistic Financial Benchmark for Large Language Models*. NeurIPS（2024）. [arXiv](https://arxiv.org/abs/2402.12659)
- `B19` **Golden Touchstone** — Wu 等. *Golden Touchstone: A Comprehensive Bilingual Benchmark for Evaluating Financial Large Language Models*. arXiv（2024）. [arXiv](https://arxiv.org/abs/2411.06272)
- `B20` **Japanese Financial Benchmark** — Hirano 等. *Construction of a Japanese Financial Benchmark for Large Language Models*. arXiv（2024）. [arXiv](https://arxiv.org/abs/2403.15062)
- `B21` **UCFE** — Yang 等. *UCFE: A User-Centric Financial Expertise Benchmark for Large Language Models*. arXiv（2024）. [arXiv](https://arxiv.org/abs/2410.14059)
- `B22` **AuditBench** — Wang 等. *Automating Financial Statement Audits with Large Language Models*. arXiv（2025）. [arXiv](https://arxiv.org/abs/2506.17282)
- `B23` **SECQUE** — Yoash 等. *SECQUE: A Benchmark for Evaluating Real-World Financial Analysis Capabilities*. ACL 2025. [arXiv](https://arxiv.org/abs/2504.04596)
- `B24` **XFinBench** — Zhang 等. *XFinBench: Benchmarking LLMs in Complex Financial Problem Solving and Reasoning*. ACL Findings（2025）. [DOI](https://doi.org/10.18653/v1/2025.findings-acl.457)
- `B25` **AuditFraudBench** — Liu 等. *AuditFraudBench: Benchmarking Audit Judgment in Detecting Fraudulent Misstatements*. arXiv（2026）. [arXiv](https://arxiv.org/abs/2606.08345)
- `B26` **BizFinBench** — Lu 等. *BizFinBench: A Business-Driven Real-World Financial Benchmark for Evaluating LLMs*. arXiv（2026）. [arXiv](https://arxiv.org/abs/2505.19457)
- `B27` **BizFinBench.v2** — Guo 等. *BizFinBench.v2: Towards Reliable LLMs in Finance via Real-User Data and Offline/Online Bilingual Evaluation*. arXiv（2026）. [DOI](https://doi.org/10.48550/arXiv.2601.06401)
- `B28` **BlueFin** — Kundurthy 等. *BlueFin: Benchmarking LLM Agents on Financial Spreadsheets*. arXiv（2026）. [arXiv](https://arxiv.org/abs/2605.30907)
- `B29` **CFMME** — Chen 等. *Benchmarking Large Vision-Language Models on CFMME: A Comprehensive Chinese Financial Multimodal Evaluation Dataset*. ACL 2026. [arXiv](https://arxiv.org/abs/2605.29462)
- `B30` **FINESSE-Bench** — Stanishevskii 等. *FINESSE-Bench: A Hierarchical Benchmark Suite for Financial Domain Knowledge and Technical Analysis in Large Language Models*. arXiv（2026）. [arXiv](https://arxiv.org/abs/2605.15482)
- `B31` **Fin-RATE** — Jiang 等. *Fin-RATE: A Real-world Financial Analytics and Tracking Evaluation Benchmark for LLMs on SEC Filings*. KDD 2026. [arXiv](https://arxiv.org/abs/2602.07294)
- `B32` **FinMaster** — Jiang 等. *FinMaster: A Holistic Benchmark for Full-Pipeline Financial Management with Large Language Models*. ACL Findings（2026）. [DOI](https://doi.org/10.18653/v1/2026.findings-acl.385)
- `B33` **FinRule-Bench** — Malarkkan 等. *FinRule-Bench: A Benchmark for Joint Reasoning over Financial Tables and Principles*. arXiv（2026）. [arXiv](https://arxiv.org/abs/2603.11339)
- `B34` **FinVQA（FIND）** — Das 等. *FIND: Toward Multimodal Financial Reasoning and Question Answering for Indic Languages*. arXiv（2026）. [arXiv](https://arxiv.org/abs/2605.13330)
- `B35` **Finch** — Dong 等. *Finch: Benchmarking Finance & Accounting across Spreadsheet-Centric Enterprise Workflows*. ACL Findings（2026）. [DOI](https://doi.org/10.18653/v1/2026.findings-acl.523)
- `B36` **Herculean** — Peng 等. *Herculean: An Agentic Benchmark for Financial Intelligence*. arXiv（2026）. [arXiv](https://arxiv.org/abs/2605.14355)
- `B37` **NL4OPT** — Ramamonjison 等. *NL4Opt Competition: Formulating Optimization Problems Based on Their Natural Language Descriptions*. arXiv（2023）. [arXiv](https://arxiv.org/abs/2303.08233)
- `B38` **OptiMUS / NLP4LP** — AhmadiTeshnizi 等. *OptiMUS: Optimization Modeling Using MIP Solvers and large language models*. arXiv（2023）. [arXiv](https://arxiv.org/abs/2310.06116)
- `B39` **Bargaining（议价基准）** — Xia 等. *Measuring Bargaining Abilities of LLMs: A Benchmark and A Buyer-Enhancement Method*. ACL Findings（2024）. [DOI](https://doi.org/10.18653/v1/2024.findings-acl.213)
- `B40` **EconLogicQA** — Quan 等. *EconLogicQA: A Question-Answering Benchmark for Evaluating Large Language Models in Economic Sequential Reasoning*. arXiv（2024）. [arXiv](https://arxiv.org/abs/2405.07938)
- `B41` **GTBench** — Duan 等. *GTBench: Uncovering the Strategic Reasoning Limitations of LLMs via Game-Theoretic Evaluations*. NeurIPS（2024）. [arXiv](https://arxiv.org/abs/2402.12348)
- `B42` **ORLM / IndustryOR** — Huang 等. *ORLM: A Customizable Framework in Training Large Models for Automated Optimization Modeling*. arXiv（2024）. [arXiv](https://arxiv.org/abs/2405.17743)
- `B43` **ORQA** — Mostajabdaveh 等. *Evaluating LLM Reasoning in the Operations Research Domain with ORQA*. AAAI（2024）. [arXiv](https://arxiv.org/abs/2412.17874)
- `B44` **AI Playing Business Games** — Ovezmyradov 等. *AI Playing Business Games: Benchmarking Large Language Models on Managerial Decision-Making in Dynamic Simulations*. arXiv（2025）. [arXiv](https://arxiv.org/abs/2509.26331)
- `B45` **AIM-Bench** — Zhao 等. *AIM-Bench: Evaluating Decision-making Biases of Agentic LLM as Inventory Manager*. arXiv（2025）. [arXiv](https://arxiv.org/abs/2508.11416)
- `B46` **CHBench** — Liu 等. *CHBench: A Cognitive Hierarchy Benchmark for Evaluating Strategic Reasoning Capability of LLMs*. arXiv（2025）. [arXiv](https://arxiv.org/abs/2508.11944)
- `B47` **OptMATH** — Lu 等. *OptMATH: A Scalable Bidirectional Data Synthesis Framework for Optimization Modeling*. arXiv（2025）. [arXiv](https://arxiv.org/abs/2502.11102)
- `B48` **Vending-Bench** — Backlund 等. *Vending-Bench: A Benchmark for Long-Term Coherence of Autonomous Agents*. arXiv（2025）. [arXiv](https://arxiv.org/abs/2502.15840)
- `B49` **AgenticPay** — Liu 等. *AgenticPay: A Multi-Agent LLM Negotiation System for Buyer-Seller Transactions*. arXiv（2026）. [arXiv](https://arxiv.org/abs/2602.06008)
- `B50` **Cattle Trade** — Müller 等. *Cattle Trade: A Multi-Agent Benchmark for LLM Bluffing, Bidding, and Bargaining*. arXiv（2026）. [arXiv](https://arxiv.org/abs/2605.14537)
- `B51` **CertiGATE** — Zhang 等. *CertiGATE: A Guard Benchmark and Quality-Certificate Protocol for Large Language Model-Based Work-Order Scheduling in Facility Management*. SSRN（2026）. [DOI](https://doi.org/10.2139/ssrn.7529119)
- `B52` **E-Commerce Bench** — Fan 等. *E-Commerce Bench: Evaluating LLM Agents on Long-Horizon Autonomous Business Operation*. arXiv（2026）. [arXiv](https://arxiv.org/abs/2608.30730)
- `B53` **FM-Bench** — Wang 等. *FM-Bench: A Benchmark for Long-Horizon Management with Competing Agents*. arXiv（2026）. [arXiv](https://arxiv.org/abs/2608.18423)
- `B54` **FrontierOR** — Kong 等. *FrontierOR: Benchmarking LLMs' Capacity for Efficient Algorithm Design in Large-Scale Optimization*. arXiv（2026）. [arXiv](https://arxiv.org/abs/2605.25246)
- `B55` **JOR-Bench** — Jinnai 等. *JOR-Bench: Japanese Operations Research Benchmarks for Large Language Models*. arXiv（2026）. [arXiv](https://arxiv.org/abs/2607.16777)
- `B56` **MIPLIB-NL** — Li 等. *Constructing Industrial-Scale Optimization Modeling Benchmark*. arXiv（2026）. [arXiv](https://arxiv.org/abs/2602.10450)
- `B57` **MM-OptBench** — Li 等. *MM-OptBench: A Solver-Grounded Benchmark for Multimodal Optimization Modeling*. arXiv（2026）. [arXiv](https://arxiv.org/abs/2605.12154)
- `B58` **Negotiation Mechanism Benchmark** — Albayaydh 等. *Do LLM Agents Negotiate Rationally? A Mechanism-Design Framework for Verifiable Multi-Agent Interaction over A2A/MCP*. arXiv（2026）. [arXiv](https://arxiv.org/abs/2608.14613)
- `B59` **OPT-Engine** — Chen 等. *OPT-Engine: Benchmarking the Limits of LLMs in Optimization Modeling via Complexity Scaling*. arXiv（2026）. [arXiv](https://arxiv.org/abs/2601.19924)
- `B60` **OR-Space** — Zhou 等. *OR-Space: A Full-Lifecycle Workspace Benchmark for Industrial Optimization Agents*. arXiv（2026）. [arXiv](https://arxiv.org/abs/2605.28158)
- `B61` **SCM-Arena** — Hasija 等. *SCM-Arena: A Behavioral Benchmark for LLM Decision-Making in Supply Chains*. SSRN（2026）. [DOI](https://doi.org/10.2139/ssrn.6514506)
- `B62` **STAR Benchmark** — Li 等. *Beyond Scaling: Assessing Strategic Reasoning and Rapid Decision-Making Capability of LLMs in Zero-sum Environments*. arXiv（2026）. [arXiv](https://arxiv.org/abs/2603.09337)
- `B63` **SupChain-Bench** — Guan 等. *SupChain-Bench: Benchmarking Large Language Models for Real-World Supply Chain Management*. arXiv（2026）. [arXiv](https://arxiv.org/abs/2602.07342)
- `B64` **The Language of Bargaining** — Sinha 等. *The Language of Bargaining: Linguistic Effects in LLM Negotiations*. arXiv（2026）. [arXiv](https://arxiv.org/abs/2601.04387)
- `B65` **VCBench** — Chen 等. *VCBench: Benchmarking LLMs in Venture Capital*. arXiv（2025）. [arXiv](https://arxiv.org/abs/2509.14448)
- `B66` **CEO Arena** — Yan 等. *CEO Arena: Evaluating Long-Horizon Multi-Agent Decision-Making in Competitive Markets*. arXiv（2026）. [arXiv](https://arxiv.org/abs/2609.34821)
- `B67` **CEO-Bench** — Chen 等. *CEO-Bench: Can Agents Play the Long Game?*. arXiv（2026）. [arXiv](https://arxiv.org/abs/2606.18543)
- `B68` **FirmCORe** — Du 等. *FirmCORe: A Benchmark for Structured Reasoning about Inter-Firm Collaboration Opportunities*. arXiv（2026）. [arXiv](https://arxiv.org/abs/2609.17128)
- `B69` **YC-Bench** — He 等. *YC-Bench: Benchmarking AI Agents for Long-Term Planning and Consistent Execution*. arXiv（2026）. [arXiv](https://arxiv.org/abs/2604.01212)
- `B70` **Artificial Societies Benchmark** — Chidichimo 等. *Artificial Societies Benchmark: A Validation Framework for Synthetic Research*. arXiv（2026）. [arXiv](https://arxiv.org/abs/2609.30030)
- `B71` **ConsumerSimBench** — Wang 等. *Can LLMs Think Like Consumers? Benchmarking Crowd-Level Reaction Reconstruction with ConsumerSimBench*. arXiv（2026）. [arXiv](https://arxiv.org/abs/2605.17079)
- `B72` **RetailBench** — Zhang 等. *RetailBench: Evaluating Long-Horizon Autonomous Decision-Making and Strategy Stability of LLM Agents in Realistic Retail Environments*. arXiv（2026）. [arXiv](https://arxiv.org/abs/2603.16453)
- `B73` **When Synthetic Users Fail** — Chen 等. *When Synthetic Users Fail: A Cross-Domain Benchmark of LLM-Simulated Human Survey Responses*. arXiv（2026）. [arXiv](https://arxiv.org/abs/2607.26348)
- `B74` **JobFair** — Wang 等. *JobFair: A Framework for Benchmarking Gender Hiring Bias in Large Language Models*. EMNLP Findings（2024）. [DOI](https://doi.org/10.18653/v1/2024.findings-emnlp.184)
- `B75` **FAIRE** — Wen 等. *FAIRE: Assessing Racial and Gender Bias in AI-Driven Resume Evaluations*. arXiv（2025）. [arXiv](https://arxiv.org/abs/2504.01420)
- `B76` **FairHireBench** — Ratnani 等. *FairHireBench: A Cross-Generational Intersectional Bias Benchmark for Large Language Models in Automated Hiring*. FAccT 2026. [DOI](https://doi.org/10.1145/3805689.3806487)
- `B77` **Kourani BPM** — Kourani 等. *Evaluating Large Language Models on Business Process Modeling: Framework, Benchmark, and Self-Improvement Analysis*. arXiv（2024）. [arXiv](https://arxiv.org/abs/2412.00023)
- `B78` **WorkArena** — Drouin 等. *WorkArena: How Capable Are Web Agents at Solving Common Knowledge Work Tasks?*. arXiv（2024）. [arXiv](https://arxiv.org/abs/2403.07718)
- `B79` **Busch & Leopold BPM** — Busch 等. *Towards a Benchmark for Large Language Models for Business Process Management Tasks*. HICSS（2025）. [DOI](https://doi.org/10.24251/hicss.2025.709)
- `B80` **CORGI** — Li 等. *Agent Bain vs. Agent McKinsey: A New Text-to-SQL Benchmark for the Business Domain*. arXiv（2025）. [arXiv](https://arxiv.org/abs/2510.07309)
- `B81` **CRMArena-Pro** — Huang 等. *CRMArena-Pro: Holistic Assessment of LLM Agents Across Diverse Business Scenarios and Interactions*. arXiv（2025）. [arXiv](https://arxiv.org/abs/2505.18878)
- `B82` **DABstep** — Egg 等. *DABstep: Data Agent Benchmark for Multi-step Reasoning*. arXiv（2025）. [arXiv](https://arxiv.org/abs/2506.23719)
- `B83` **CRM-Agent-Bench** — Banerjee 等. *CRM-Agent-Bench: Benchmarking Tool-Using Agents in Stateful Enterprise Environments*. arXiv（2026）. [arXiv](https://arxiv.org/abs/2610.32004)
- `B84` **ERPBench（Computer-Use）** — Bhagtani 等. *ERPBench: A State-Grounded Evaluation Paradigm for Computer-Use Agents in Enterprise Software*. arXiv（2026）. [arXiv](https://arxiv.org/abs/2609.17885)
- `B85` **ERPBench（企业决策）** — Zhang 等. *ERPBench: Evaluating LLM Agents for Enterprise Decision-Making Across Competitive Market Ecologies*. arXiv（2026）. [arXiv](https://arxiv.org/abs/2609.04667)
- `B86` **RevOpsBench** — Masetty 等. *RevOpsBench: A Large-Scale Benchmark for Evaluating LLM Agents on Enterprise CRM Operations*. IEEE SoutheastCon（2026）. [DOI](https://doi.org/10.1109/southeastcon63549.2026.11475978)
- `B87` **SpreadsheetBench 2** — Zhu 等. *SpreadsheetBench 2: Evaluating Agents on End-to-End Business Spreadsheet Workflows*. arXiv（2026）. [arXiv](https://arxiv.org/abs/2606.29955)

## 附录 B 推荐使用清单

如果只读 / 只用 12 个，建议从下面选（判定依据：代表性 + 可复现性 + 是否被后续工作当作公共底座，**不代表做过引用量统计**）。

| 用途 | 首选 | 备选 | 理由 |
|---|---|---|---|
| 入门必读（建模类） | NL4OPT `B37` | OptiMUS `B38`、ORLM `B42` | 运筹建模任务的公共底座，1,101 题、许可宽松、可完全复现 |
| 入门必读（金融数值推理） | ConvFinQA `B11` | BizBench `B01` | 题型设定被后续大量沿用，是最干净的「多步数值推理」实验床 |
| 金融综合能力 | FinBen `B18` | PIXIU `B15` | 36 数据集 / 24 任务，适合整体汇报 |
| 真实企业文档 | FinanceBench `B14` | SECQUE `B23`、Fin-RATE `B31` | 真实 10-K/10-Q，最接近实际财务分析工作 |
| 中文金融 | BizFinBench `B26` / v2 `B27` | CFinBench `B17` | 真实业务问句 + 中文 |
| 运筹（工业规模） | MIPLIB-NL `B56` | IndustryOR `B42` | 从 MIPLIB 2017 反演，规模真实 |
| 运筹（算法设计） | FrontierOR `B54` | — | 评「能否设计出可运行算法」，方向独特 |
| 博弈与谈判 | GTBench `B41` | AgenticPay `B49` | 10 个形式化博弈，许可宽松，指标清晰 |
| 企业网页智能体 | WorkArena `B78` | CRMArena-Pro `B81` | 最早的成熟企业环境；WorkArena 许可为 NOASSERTION，需先确认 |
| 数字员工 / 岗位任务 | TheAgentCompany `B02` | ERPBench（企业决策）`B85` | 最贴近「替代真人工作」的设定 |
| 长程一致性 | FM-Bench `B53` | Vending-Bench `B48` | FM-Bench 用确定性种子生成，是目前最可复现的长程设计 |
| 合成用户 / 效度 | ConsumerSimBench `B71` | When Synthetic Users Fail `B73` | 前者中文、群体级；后者提供失效条件的跨域框架 |

**三条使用纪律**

1. 引用预印本时写明「arXiv 编号 + 访问日期」，69 个预印本里 42 个集中在 2026 年，版本可能随时更新。
2. 发表结果时同时报告许可与数据获取方式，避免读者按「有仓库」推定「可复跑」。
3. 不用不同口径的长程基准直接比较绝对分数（天数 180/365/500/20 年不可通约）。

## License

本仓库分两类内容授权：

| 内容 | 许可 | 说明 |
|---|---|---|
| 文档（`README.md`）与整理后的数据（`data/benchmarks.csv`） | [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/)（全文见 `LICENSE`） | 可复制、修改、商用，需署名并注明是否改动 |
| 第三方评测基准的数据、代码与环境 | **不适用本仓库许可** | 各基准的条款以其论文与仓库声明为准，见第 5 节「许可」列 |

**引用请注明**：本仓库地址 + 访问日期。

**范围与免责**：本仓库只收录第三方基准的公开元信息（名称、论文链接、仓库入口、许可记录）与整理者的分类分析，不托管、不分发这些基准的数据或代码，也不对其当前可用性作担保。「许可」列是对公开说明的转述，可能随上游变化，实际使用前请以对应仓库的 `LICENSE` 文件为准。

> 若后续加入可执行脚本，代码部分将另附 `LICENSE-CODE`（MIT）与 CC BY 4.0 并行，以分别覆盖软件与文档。
