# Agentech.Global

**L0 · 全局语义** — 所有 skill 卡共享的执行语义、共享映射与错误码；单一事实来源，各卡不重复定义。

## 执行语义

| 项 | 约束 |
|---|---|
| call mode | blocking |
| 抢占 | 执行中收到新指令返回 `rejected(E_BUSY)`；仅 `stop` / `emergency_stop` 可抢占 |
| profile 判定 | 每次调用最多一个 selector；混用返回 `rejected(E_PROFILE_MIXED)` |
| 默认调用 | 全部 selector 省略时执行 canonical profile 及其默认值 |
| 消歧 | selector 与其他 profile 的辅助参数同名时，以 selector 判定 profile（如 `DistanceM + SpeedMps` 选择 `distance-speed`） |
| 坐标系 | robot body frame |
| percent 基准 | 本函数 `SafeMax`（或最大角度） |

## 共享映射

| 输入 | 映射 |
|---|---|
| `*Percent` | `value = pct / 100 × SafeMax（或最大角度）` |
| `*Level` `1..5` | `20% / 35% / 50% / 70% / 90% × SafeMax（或最大角度）` |
| `Pace` | `slow=25%`, `normal=50%`, `fast=75% × SafeMax` |
| distance 请求 | 仅时长估算；无到达验证 |

## 返回与错误码

**返回类型：**`SkillResult(status, trace_id, error_code, message)`（L0 遥测除外）

| 枚举 | 取值 |
|---|---|
| `status` | `ok | rejected | timeout | preempted | estopped | failed` |
| `error_code` | `E_PROFILE_MIXED | E_RANGE | E_BUSY | E_TIMEOUT | E_SAFETY_GATE | E_UNSUPPORTED | E_STATE | E_INTERNAL` |

**约束：**本全局卡是单一事实来源；各函数卡只声明支持的 profile 与本函数常量、上限。
