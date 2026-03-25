# align v2

复杂多轮 AI 协作守卫。  
Lightweight guardrails for complex multi-turn AI collaboration.

## 它是什么
## What It Is

`align v2` 是一套轻量规则，用来减少复杂协作中的漂移、偷换和断档。  
`align v2` is a lightweight rule set for reducing drift, silent reinterpretation, and context loss in complex collaboration.

它不是任务管理器，不是 agent 框架，也不是通用 prompt 模板。  
It is not a task manager, an agent framework, or a generic prompt template.

它更像一个 guardrail：简单任务保持轻量，复杂任务再展开。  
It acts more like a guardrail: stay light for simple work, expand only when complexity requires it.

## 它解决什么
## What It Solves

- 把假设写成结论  
  Turning assumptions into conclusions
- 把改写版当成用户原意  
  Treating rewritten wording as user intent
- 长对话后目标和约束漂移  
  Goal and constraint drift across long conversations
- 重要状态只留在聊天里  
  Leaving important state only in chat memory
- 新信息改变旧结论却没人回查  
  Failing to revisit old conclusions after new information

## 核心规则
## Core Rules

1. 区分 `已确认 / 暂定假设 / 待确认`  
   Keep `confirmed / temporary assumptions / needs confirmation` separate.

2. 不擅自把 agent 改写版沉淀成既定事实  
   Do not silently turn the assistant's rewrite into accepted durable state.

3. 高影响内容在必要时外化  
   Externalize high-impact state when later work depends on it.

4. 新信息影响旧内容时必须联查  
   Revisit earlier conclusions when new information changes them.

5. 目标和约束足够稳定后再执行  
   Move into execution only when goals and constraints are stable enough.

## 快速开始
## Quick Start

1. 先说清当前任务。  
   State the current task clearly.

2. 让 AI 分出四类内容：  
   Ask the assistant to separate:
   - `confirmed`
   - `temporary assumptions`
   - `needs confirmation`
   - `out of scope for this step`

3. 如果后续还要依赖，就只外化最小状态层：  
   If later work will depend on it, externalize only the minimum state layer:
   - `current-goal`
   - `confirmed-constraints`
   - `pending-items`
   - `decisions`

4. 当前步够清楚时，交付最小有用结果。  
   Once the current step is clear enough, deliver the smallest useful result.

## 适用场景
## Good Fit

- 长对话协作  
  Long multi-turn collaboration
- 框架、方法、系统设计  
  Framework, method, or system design
- 会跨阶段推进的任务  
  Work that spans stages or sessions
- 对定义、边界、约束、决策很敏感的任务  
  Tasks sensitive to wording, boundaries, constraints, and decisions

## 不太适合
## Not For

- 一次性小任务  
  One-shot small tasks
- 简单问答  
  Simple Q&A
- 不需要承接状态的快速修改  
  Quick edits with no state carryover

## 最小状态层
## Minimal State

这不是完整备份，只是继续协作时最小够用的状态。  
This is not a full transcript, only the minimum state needed for continuation.

- `current-goal`
- `confirmed-constraints`
- `pending-items`
- `decisions`

## 仓库结构
## Repo Structure

- `SKILL.md`  
  主规则 / Main rules
- `references/workflow.md`  
  展开流程 / Expanded workflow
- `references/checklist.md`  
  检查清单 / Checklist
- `references/update-rules.md`  
  更新规则 / Rule update policy
- `examples/`  
  示例 / Examples

## 示例
## Example

用户说：先做方案，不要开始实现。  
User says: design the approach first, do not start implementation.

`align v2` 会先区分：  
`align v2` first separates:

- 已确认：当前轮不进入实现  
  Confirmed: do not implement in this round
- 暂定假设：先给一个结构化方案可能有帮助  
  Temporary assumption: a structured outline may help
- 待确认：这个结构是否会成为正式结构  
  Needs confirmation: whether this structure should become official

这样后续不会把暂定结构悄悄升级成既定事实。  
This prevents temporary structure from being silently upgraded into settled fact.
