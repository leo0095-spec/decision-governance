RFC–DG-0001

决策权治理与 MRU 规范

（Decision Governance & Meta-Reasoning Unit Specification · Draft v0.1）

⸻

说明 / Note:

本 RFC 当前以中文撰写，用于优先固定概念结构、治理边界与工程约束。
在内容稳定后，可能会提供英文版本以便更广泛讨论。
语言并非规范的一部分，治理原则与结构本身才是核心。

This RFC is currently written in Chinese to stabilize concepts, governance boundaries,
and engineering constraints first. An English version may be provided once the content
is stable. Language is not part of the specification; the governance structure is.

⸻

1. 摘要（Abstract）

随着自动化系统与 AI 模型能力的快速提升，
系统在高速运行中触发不可逆决策错误的概率呈非线性上升。

本规范提出一种 决策权治理层（Decision Governance Layer），
通过一个称为 MRU（Meta-Reasoning Unit，元推理单元） 的结构来实现。

MRU 的唯一职责不是决定“应该做什么”，
而是治理一个更基础的问题：

是否允许自动化继续做决策。

MRU 为复杂系统引入一种系统级“刹车机制”，
确保关键决策始终具备：
	•	可回退性
	•	可审计性
	•	人类可中断性

⸻

2. 问题定义（Problem Statement）

当前复杂系统普遍面临以下问题：
	•	自动化持续加速，但缺乏明确的停止条件
	•	决策越来越多由模型概率驱动
	•	不可逆操作被提前触发
	•	系统中缺乏一个统一的“继续 / 停止”裁决权威

现有方案主要优化 决策质量，
却回避了一个更基础的问题：

谁拥有“是否继续决策”的治理权？

本 RFC 试图填补这一缺失的治理层。

⸻

3. 非目标（Non-Goals）

本规范明确不试图解决以下问题：
	•	❌ 优化业务 KPI
	•	❌ 替代人类判断
	•	❌ 执行任何具体动作
	•	❌ 在多个方案中做选择
	•	❌ 构建自治 Agent

MRU 治理的是“决策许可权”，
而不是“决策内容”。

⸻

4. 核心治理原则（Core Principles）

以下原则为 宪法级约束，
任何实现不得违反。

4.1 状态优先于因果

MRU 基于可观测状态与趋势进行判断，而非因果叙事。

4.2 趋势优先于瞬时

判断必须基于时间序列，而不是单次事件。

4.3 风险优先于结果

风险升级优先级高于期望收益或最优解。

4.4 可回退优先

任何不可回退的行动都必须触发升级或暂停。

4.5 模型无关性

MRU 不得依赖模型置信度或概率作为核心裁决依据。

4.6 人类主权

在任何层级，人类必须保有最终接管与中断权。

⸻

5. MRU 的职责范围（Functional Scope）

MRU 只负责 一件事：

判断是否允许自动化决策继续进行。

MRU 不输出：
	•	决策建议
	•	行动方案
	•	执行指令

⸻

6. MRU 裁决状态机（Decision States）

MRU 只能输出以下 四种互斥状态：
状态
含义
CONTINUE
允许自动化继续
ESCALATE
必须立即交由人类
DEFER
延迟决策，等待更多信号
SUSPEND
立即暂停自动化
不允许存在第五种状态。

⸻

7. 输入信号（Signals）

MRU 可以接收：
	•	时间序列指标（速率、漂移、方差）
	•	事件密度与聚集
	•	结构性违规信号
	•	规则阈值触发
	•	人类主动干预信号

MRU 不得接收：
	•	行业业务语义
	•	KPI 或优化指标
	•	模型生成的执行计划

⸻

8. 模型交互规则（Model Interaction）
	•	MRU 可以授权模型提供分析
	•	模型只能作为顾问

模型不得：
	•	触发 MRU 状态转换
	•	覆盖 MRU 裁决
	•	直接执行动作

模型是建议者，不是治理者。

⸻

9. 可审计性（Auditability）

每一次状态变化必须记录：
	•	触发信号
	•	对应原则
	•	时间戳
	•	人类确认（如存在）

日志必须可回放、可复查、不可篡改。

⸻

10. 失败哲学（Failure Philosophy）

MRU 被允许：
	•	过度保守
	•	误报
	•	延迟

MRU 不得：
	•	造成不可逆伤害
	•	掩盖不确定性
	•	执行动作

MRU 优化的是“存活”，不是效率。

⸻

11. 部署模型（Deployment）

MRU 应当：
	•	内嵌于系统控制平面
	•	与业务逻辑解耦
	•	可跨领域迁移

⸻

12. 安全考量（Security）
	•	MRU 本身必须防止被绕过
	•	不得存在单点 bypass
	•	升级通道必须在故障时仍可用

⸻

13. 设计动机（Rationale）

在自动化系统中：

发动机解决速度问题，
刹车解决生存问题。

本规范确立了一个核心理念：

“是否允许继续决策”
是系统中的一等治理问题。

⸻

14. 结论（Conclusion）

MRU 引入了一层长期缺失的治理结构：

一个专门决定“什么时候不该继续”的系统。
