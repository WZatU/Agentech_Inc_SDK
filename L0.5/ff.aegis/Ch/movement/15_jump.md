# `Agentech.jump()`

<!-- START: Definition -->
## 定义

**L0.5 · Movement · Aegis** — 执行官方标准跳跃预设。

来源：[EAIC HUB Aegis SDK](https://www.agent-tech.ai/agentech-products/eaic-hub/view-sdk)，同步日期 2026-07-16。
<!-- END: Definition -->

<!-- START: Syntax -->
## 调用方式

```python
Agentech.jump()
```
<!-- END: Syntax -->

<!-- START: Constraints -->
## 约束

1. 输入必须严格符合参数表中的类型和范围；越界值应被拒绝，不得静默改写。
2. `SafetyGate` 仍处于开发中，不得描述为已完成真机验证。
3. `height_level` 明确不受支持。
<!-- END: Constraints -->

<!-- START: Defaults -->
## 默认设定

| 来源 | 默认值 | 状态 |
| --- | --- | --- |
| `variant` | `standard` | 可用 |
| `stabilize_s` | `5.0` | 可用 |
<!-- END: Defaults -->

<!-- START: Parameters -->
## 参数

| 参数 | 类型 / 范围 | 默认值 | 状态 | 含义 |
| --- | --- | --- | --- | --- |
| `variant` | `standard` | `standard` | 可用 | 动作预设版本。 |
| `stabilize_s` | `float 0..10` | `5.0` | 可用 | 动作完成后的稳定等待时间。 |
| `height_level` | `1 | 2 | 3` | — | 不支持 | 跳跃高度档位。 |
| `SafetyGate` | `system behavior` | — | 开发中 | 系统安全门行为。 |
<!-- END: Parameters -->

<!-- START: Behavior -->
## 行为

执行官方标准跳跃预设。
<!-- END: Behavior -->

<!-- START: Return -->
## 返回

当前官网没有为该 Skill 发布更具体的返回结构。实现应报告成功或拒绝状态，并且不得改变已发布的输入契约。
<!-- END: Return -->

<!-- START: Example -->
## 示例

```python
Agentech.jump(variant="standard", stabilize_s=5.0)
Agentech.jump()
```
<!-- END: Example -->
