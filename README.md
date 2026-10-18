# Trustbase Skills

> **Agent Skills that connect AI to verifiable industry facts.**
> **11 skills · 5 cognitive (book-to-skill) + 6 industry (rCB)**
> 让 agent 不只知道"怎么做"，还知道"数据从哪来、对不对、谁负责"。

[![skills.sh](https://skills.sh/b/Trustbaselab/trustbase-skills)](https://skills.sh/Trustbaselab/trustbase-skills)
[![License: Apache-2.0](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](LICENSE)
[![Skills](https://img.shields.io/badge/skills-11-green.svg)](#skill-catalog)
[![Data](https://img.shields.io/badge/verifiable_facts-520+-orange.svg)](https://trustbaselab.com/database)
[![MCP](https://img.shields.io/badge/MCP_tools-59-purple.svg)](https://trustbaselab.com/mcp)

```bash
npx skills add Trustbaselab/trustbase-skills
```

---

## Why this repo is different

**大多数 skill 仓库在教 agent「怎么做」。**
**我们在这里多做一件事：每个 skill 背后，都有**可核验的数据源**。**

| 常见 skill 仓库 | ⭐ 这个仓库 |
|---|---|
| 教你写文档 / 做设计 | 教你**查一个垂直行业的可靠事实** |
| 数据从哪里来？—— 不知道 | **520+ 条事实，每条带 ID、置信度、来源、时点** |
| 出错谁负责？—— 没人 | **纠错通知机制：记录被纠正会主动告知调用方** |
| 能不能验证？—— 不能 | **每条记录可回查：`/record/<id>/`** |

**我们的核心资产不是 skill 文本，是**skill + 可核验数据源**的组合。**
**→ skill 谁都能写；可核验的事实层抄不走。**

---

## Two layers

```
trustbase-skills/
├── cognitive/     ⭐ 认知层 —— 让 agent 工作得更好（方法论）
└── industry/      行业层 —— 让 agent 查到可靠事实（数据）
```

### ⭐ `cognitive/` —— STAR PROJECT

**把经典书籍转成 agent 可执行的行为准则，并在真实项目里验证。**

**⭐ 六层认知操作系统：**

```
① 输入层  factfulness            《事实》         如何正确看数据
② 处理层  thinking-fast-and-slow 《思考，快与慢》  如何不被直觉骗
③ 质量层  noise-in-judgment      《噪声》         如何让判断一致
④ 全局层  thinking-in-systems    《系统之美》      如何看到系统和反馈
⑤ 带宽层  bandwidth-and-deep-work《稀缺》         如何在有限资源下工作
⑥ 执行层  （同上）                                如何产出深度
```

| Skill | 基于 | 核心 |
|---|---|---|
| **`factfulness`** | 《事实》 | **数据口径四件套核查 + 十大情绪化本能诊断** |
| **`thinking-fast-and-slow`** | 《思考，快与慢》 | **识别 AI 的快思考模式，强制慢思考复核** |
| **`noise-in-judgment`** | 《噪声》 | **区分偏差与噪声，用决策卫生减少随机波动** |
| **`thinking-in-systems`** | 《系统之美》 | **存量流量图 + 反馈回路 + 12 个杠杆点** |
| **`bandwidth-and-deep-work`** | 《稀缺》《深度工作》 | ⭐ **本项目：每轮 token 141K → 5.6K（-96%）** |

**⭐ 每个 cognitive skill 都带三样：**
- `SKILL.md` — agent 读的行为准则
- `references/` — 书的核心理念（我们自己写，不抄原文）+ **`evidence.md`（本项目验证数据）**
- `METHOD.md` — **这本书是怎么被转化成 skill 的**（可复用到下一本）

**→ 我们做的不是"读书笔记"，是「**验证过的行为准则 + 真实数据**」。**

**详见 [`cognitive/README.md`](cognitive/README.md)。**

### `industry/` —— 行业层

| Skill | 做什么 |
|---|---|
| `rcb-export-compliance` | rCB 出口合规检查（CBAM / REACH / 循环含量 / 认证链） |
| `rcb-grade-identification` | 从实测参数识别炭黑牌号（ASTM D1765 / R 码） |
| `rcb-price-reference` | rCB 价格参考区间与比价关系 |
| `rcb-substitution-assessment` | rCB 能否替代某原生牌号、替代上限、必须实测什么 |
| `carbon-black-weekly` | 《炭黑周观察》周报制作（价格/走势/判断） |
| `ai-industry-daily` | 《AI 观察》每日专栏 |

**⭐ 全部中英双语**（`SKILL.md` + `references/SKILL.zh.md`）。

---

## Data source

**All industry skills depend on the Trustbase Lab MCP server:**

```
https://trustbaselab.com/mcp
```

- **协议**：MCP `2026-07-28`
- **工具**：**59 个**
- **扩展**：`io.modelcontextprotocol/skills` · `io.modelcontextprotocol/ui`
- **记录**：**520+ 条跨域基准 · 2,738 条总记录**
- **标准**：**TBDS-1**（数据标准）
- ⭐ **每条事实带**：稳定 ID · 置信度 A/B/C · `source_url` · `as_of` · 回查 URL

**⭐ 注册表收录**：`com.trustbaselab/rcb-data`（MCP Registry）

---

## Install

### DSH（DeepSeek Harness）

```bash
# 复制到 DSH 的 skills 目录
git clone https://github.com/<owner>/trustbase-skills.git
cp -r trustbase-skills/industry/* ~/.dsh/skills/
cp -r trustbase-skills/cognitive/* ~/.dsh/skills/
```

### Claude Code / Claude Desktop

```bash
# 作为 plugin marketplace 添加（若仓库已配置 marketplace）
/plugin marketplace add <owner>/trustbase-skills
```

### 其他 agent

**Skills 是一个目录 + `SKILL.md`。任何支持 Agent Skills 规范的 agent 都能直接用：**
- **格式**：[agentskills.io](https://agentskills.io)
- **必需**：`SKILL.md`（YAML frontmatter: `name` · `description`）
- **可选**：`references/` · `scripts/` · `assets/`

---

## Skill catalog

### cognitive/（5）

| Skill | 触发 | 不适用 |
|---|---|---|
| **`factfulness`** | 「世界是不是越来越糟」「这个数据可信吗」「帮我引个数据」「别贩卖焦虑」 | 纯数据查询（不含判断） |
| **`thinking-fast-and-slow`** | 「这个 AI 结论靠谱吗」「感觉回答太自信了」「帮我审核这份 AI 产出」 | 任务过载与专注排程（用 bandwidth） |
| **`noise-in-judgment`** | 「为什么每次答案都不一样」「结论不一致该信谁」「怎么让评估更一致」 | 纯事实查询 · 唯一答案计算 |
| **`thinking-in-systems`** | 「为什么越改越糟」「改了没效果」「怎么找杠杆点」 | 个人专注力问题（用 bandwidth） |
| **`bandwidth-and-deep-work`** | 「任务太多做不完」「总是被打断」「无法专注」「怎么排优先级」 | 纯学术讨论 |

### industry/（6）

| Skill | 触发 |
|---|---|
| **`rcb-export-compliance`** | "rCB 能出口到欧盟吗" · "要过什么认证" · "PAH 超标会怎样" |
| **`rcb-grade-identification`** | "这是什么牌号" · "属于什么等级" · "对标哪个牌号" |
| **`rcb-price-reference`** | "rCB 大概什么价格" · "这个报价合理吗" · "比原生便宜多少" |
| **`rcb-substitution-assessment`** | "rCB 能否替代 N550/N330" · "替代比例多少" · "掺配上限" |
| **`carbon-black-weekly`** | "写炭黑周观察" · "出炭黑走势图" · "分析煤焦油和炭黑的关系" |
| **`ai-industry-daily`** | "今天讲点 AI" · "国产模型对比" · "AI 泡沫怎么看" |

---

## Integrity & anti-counterfeit

**⭐ 每个 skill 的 `SKILL.md` 带 sha256；官方页对照：**

```
https://trustbaselab.com/skills/
```

**下载包校验：**

```bash
sha256sum -c SHA256SUMS
```

**⚠️ 防仿冒**：官方分发只有两个渠道——**本仓库** + **`https://trustbaselab.com/skills/`**。
**其他来源请先核对 sha256。**

---

## Contributing

**⭐ 我们提供模板和规范：**

- [`template/SKILL-TEMPLATE.md`](template/SKILL-TEMPLATE.md) — 新 skill 模板
- [`spec/TBDS-SKILLS-1.md`](spec/TBDS-SKILLS-1.md) — 我们的 skill 规范

**⭐ 提交前请确保：**
1. `name` ≤64 字符、小写、连字符、**= 目录名**
2. `description` ≤1024 字符，**含明确的触发条件和不适用边界**
3. **有 `references/`**（知识来源）
4. **⛔ 不抄原文**——注明来源，写我们自己的理解
5. **⭐ 如果 skill 声称"有效"，附上验证数据**

---

## License

**Apache-2.0** —— 见 [LICENSE](LICENSE)。

**书籍理念的引用**：本仓库的 cognitive skills 基于公开出版书籍的**理念**，
文件内已注明来源；**我们不复制、不翻译原文段落**。
我们贡献的是「**把理念转译成 agent 可执行规则**」这一层。

**工程数据**（如 `evidence.md` 里的 token 数与改造前后对比）为 **Trustbase Lab 项目自有内容**。

---

## Disclaimer

**Skills are provided for use at your own risk.**

**行业类 skill（`industry/`）只提供**检查流程与判断规则**，不含法规数值；
具体数值请通过 MCP 数据源获取，并核对原始来源。**

**本仓库不提供投资、法律或申报建议。**

---

## Links

- **Data platform**: https://trustbaselab.com
- **MCP endpoint**: https://trustbaselab.com/mcp
- **Usage board**: https://trustbaselab.com/usage/
- **Corrections**: https://trustbaselab.com/corrections/
- **Skills page**: https://trustbaselab.com/skills/
- **Agent Skills spec**: https://agentskills.io
