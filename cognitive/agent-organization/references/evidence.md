# 证据：更柝 Agent 组织改造（2026-11-15）

> 这份文件记录 skill 里每条规则背后的真实数据。
> 不是示例，是 2026-11-15 当天在一套运行了 30+ 天的 21-agent 系统上做的实测。

---

## 一、改造前的诊断数据

**检查时间**：2026-11-15 19:00
**系统**：Trustbase Lab 更柝（Vigiliae），已经连续运行 30+ 天，累计 25,246 次运行

| 判据 | 结果 |
|---|---|
| 定义数 vs 注册数 | `agents.yaml` 12 个 / `vigiliae.db` 21 个 → **差 9 个** |
| 缺 `reports_to` | 9 个（全部是新注册的） |
| 缺 `boundaries` | 20 个（只有 `vigiliae` 一个自己写了） |
| 缺 `kpi` | 21 个（全部只有 runs/fails 计数） |

**具体缺失的 9 个成员：**

```
运营类 3 个：stipendium(经费) / price_watch(盯价) / applico(入库)
领域类 6 个：rcb/carbon/energy/telecom/health/compute-master
```

**⭐⭐ 关键发现：6 个领域 Master 的 `runs = 0`。**

它们被注册成 `kind: agent` 但从来没有 `schedule`，所以调度器永远不会跑它们。
在运行台的 21 个卡片里，它们永远是「未运行」灰色状态 —— 六个僵尸节点。

**判断**：它们不是 agent，是「按需调用的问答服务」。
**处理**：`kind: agent` → `kind: service`，`schedule: null`，从调度里摘出。

---

## 二、改造过程（8 步，每步都有验证）

| 步骤 | 动作 | 结果 |
|:-:|---|---|
| 1 | 补 3 个运营 agent 的完整定义 | 12 → 15 |
| 2 | 6 个领域 Master 改标 `service` | 15 → 21（总数对上 DB） |
| 3 | 给 8 个原有 agent 补 `boundaries` | 缺 boundaries 20 → 0 |
| 4 | 给 12 个原有 agent 补 `kpi` | 缺 kpi 21 → 0 |
| 5 | 校验 yaml 可解析 + 数量一致 | ✅ 21 = 21 |
| 6 | 重启服务加载新配置 | `active`，21 任务全部加载 |
| 7 | 建 `handbook/README.md` | 9,627 字节，8 条规则 |
| 8 | 做组织视图页 `/ops/org/` | 6 层卡片 + 汇报树 |

**最终校验：**

```
agent 总数       : 21
缺 reports_to    : 无
缺 boundaries    : 无
缺 kpi           : 无
缺 role          : 无
缺 description   : 无
```

---

## 三、改造后的组织结构（真实数据）

```
组织: Vigiliae · Agent Organization / 更柝 Agent 组织
成员: 21

按类型:
  agent     4   vigiliae, libra, arachne, sator
  python    6   annales, nuntius, taeda, terminus, stipendium, applico
  http      5   hesperus, sol-et-luna, nox-media, porta, price_watch
  service   6   rcb/carbon/energy/telecom/health/compute-master

定时调度 15 个 / 按需服务 6 个

汇报树:
  human       ← 8 个（vigiliae, porta, 6 个领域 Master）
  vigiliae    ← 8 个（hesperus, sol-et-luna, annales, libra,
                       nuntius, stipendium, price_watch, applico）
  sol-et-luna ← 1 个（nox-media）
  nuntius     ← 1 个（taeda）
  annales     ← 3 个（arachne, sator, terminus）
```

**运行数据：**

```
累计运行  25,261 次
累计失败     195 次（0.77%）

状态分布：
  运行中   14
  服务节点  6
  故障      1   ← price_watch，见下
```

---

## 四、抓到的一个真实故障（改造过程中发现的）

**`price_watch`（盯价）：19 次运行，19 次失败，失败率 100%。**

**错误信息：**

```
read-only python tasks are not allowed; use a narrow HTTP endpoint
```

**根因**：执行器（`vigiliae_executor.py:224`）有一条硬限制 —— 只读的 python 任务
不允许参与调度，必须走窄 HTTP 端点。

**⭐⭐ 这个 agent 从上线那天起就没成功过一次，但因为只有 runs/fails 计数、
没有 KPI，所以没人发现它一直在失败。**

**这正是「只有活动量指标」的代价。**

**处理**：`kind: python` → `kind: http`，`enabled: false` 挂着，等建窄端点。

---

## 五、另一个数据：组织没有变聪明的证据

**同类错误复发次数 —— C-067「只看局部字段就下结论」：**

| 次 | 日期 | 具体错误 |
|:-:|---|---|
| 1 | — | 晨检误报 name 缺失 |
| 2 | — | agent_kailian 数据误判 |
| 3 | — | A 级无 URL 误报 |
| 4 | — | 模块级 confidence 误报 |
| 5 | 11-14 | 错怪 agent_kailian 备注（用 `tail -1` 只看最后一条） |
| 6 | 11-15 | 误判 138 条 A 级数据没有 quote（只查 `sourced.quote`，实际在 `evidence.quote`） |

**⭐ 结论：前 5 次都只写了「注意 X」，所以第 6 次还是犯。**

**第 6 次之后规则升级为：**

> 写任何「检查数据完整性」的脚本时，**先 `json.dumps(record, indent=1)` 打印 2–3 条完整记录，把字段路径全列出来，再写判定逻辑。**
> **判断依据**：脚本里出现 `x.get('field')` 时，必须确认过这个 field 在真实记录里的路径。

**这是「复发 ≥2 次必须升级规则」这条规则的来源。**

---

## 六、一个反例：为什么不能先做可视化

**改造前，运行台（`/ops/genghe/`）已经能显示 21 个 agent 的卡片、运行次数、状态灯。**

**但它是错的：**

- 6 个僵尸节点显示成「未运行」
- 21 个卡片平铺，看不出谁向谁汇报
- 没有任何一张卡片说明「这个 agent 干得好不好」

**⭐⭐ 可视化做在了结构正确之前，等于把错误画得更清楚。**

**正确顺序：先对齐定义 → 再补四件套 → 最后可视化。**

---

## 七、改造耗时（真实）

| 阶段 | 耗时 |
|---|---|
| 诊断（发现 9 个盲区） | ~20 分钟 |
| 补 9 个定义 + 8 个 boundaries + 12 个 kpi | ~15 分钟 |
| 校验 + 重启服务 | ~5 分钟 |
| 建 handbook | ~20 分钟 |
| 做组织视图页 + nginx + 部署守卫登记 | ~40 分钟 |
| **合计** | **约 1 小时 40 分** |

**⭐ 一套跑了 30 天的 21-agent 系统，组织化的成本是半天以内的人工。**
**不做的成本：一直不知道有 1 个 agent 100% 失败、6 个节点是僵尸。**

---

## 八、可复现的检查脚本

```python
import yaml, sqlite3

d = yaml.safe_load(open('agents.yaml', encoding='utf-8'))
agents = d['agents']
c = sqlite3.connect('vigiliae.db')

# ① 定义 vs 注册
n_db = c.execute('SELECT COUNT(*) FROM tasks').fetchone()[0]
assert len(agents) == n_db, '定义 %d ≠ 注册 %d' % (len(agents), n_db)

# ② 无孤儿
orphans = [a['name'] for a in agents if not a.get('reports_to')]
assert not orphans, '缺 reports_to: %s' % orphans

# ③ 无裸奔
naked = [a['name'] for a in agents if not a.get('boundaries')]
assert not naked, '缺 boundaries: %s' % naked

# ④ 全部可衡量
blind = [a['name'] for a in agents if not (a.get('kpi') or {}).get('primary')]
assert not blind, '缺 kpi: %s' % blind

# ⑤ 服务节点已摘出调度
bad = [a['name'] for a in agents if a.get('kind') == 'service' and a.get('schedule')]
assert not bad, 'service 仍在调度: %s' % bad

print('✅ 组织完整性检查全过（%d 个成员）' % len(agents))
```

**更柝 2026-11-15 运行结果：`✅ 组织完整性检查全过（21 个成员）`**

---

*Trustbase Lab · 2026-11-15*
