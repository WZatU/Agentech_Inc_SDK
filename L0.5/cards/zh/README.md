# 中文 SDK 卡片

这里是 Agentech L0.5 SDK 卡片的中文阅读入口。

当你需要查看 Aegis 机器狗原子技能的中文 API 合约时，从这里进入：移动、姿态、安全、感知/姿态调整都在同一套卡片结构下说明。

## 这个中文包包含什么

| 层级 | 数量 | 范围 |
| --- | ---: | --- |
| `L0.0` | 1 | 中文遥测快照卡，位于 `../../../L0.0/cards/get_battery_status.zh.md` |
| `L0.5` | 12 | 当前目录下的中文原子技能卡 |

## L0.0 中文卡片

| API | 类别 | 卡片 |
| --- | --- | --- |
| `Agentech.get_battery_status(parameters)` | 遥测 | `../../../L0.0/cards/get_battery_status.zh.md` |

## L0.5 中文卡片

| # | API | 类别 | 卡片 |
| ---: | --- | --- | --- |
| 01 | `Agentech.forward(parameters)` | 移动 | `01_forward.md` |
| 02 | `Agentech.backward(parameters)` | 移动 | `02_backward.md` |
| 03 | `Agentech.lateral(parameters)` | 移动 | `03_lateral.md` |
| 04 | `Agentech.turn(parameters)` | 移动 | `04_turn.md` |
| 05 | `Agentech.twist(parameters)` | 移动 | `05_twist.md` |
| 06 | `Agentech.backflip(parameters)` | 移动 | `06_backflip.md` |
| 07 | `Agentech.jump(parameters)` | 移动 | `07_jump.md` |
| 08 | `Agentech.stand(parameters)` | 姿态 | `08_stand.md` |
| 09 | `Agentech.sit(parameters)` | 姿态 | `09_sit.md` |
| 10 | `Agentech.stop(parameters)` | 安全 | `10_stop.md` |
| 11 | `Agentech.emergency_stop(parameters)` | 安全 | `11_emergency_stop.md` |
| 12 | `Agentech.look(parameters)` | 感知/姿态 | `12_look.md` |

## 怎么读一张卡

建议按这个顺序读：

1. `定义`：确认层级、类别和函数目的。
2. `调用方式`：复制合法调用形状。
3. `约束`：检查选择参数、互斥规则和拒绝行为。
4. `默认设定`：确认省略参数时 SDK 会怎么执行。
5. `参数`：检查范围、单位、档位映射和工程解释。
6. `行为`：理解运行时动作语义。
7. `返回`：用稳定字段做程序分支。
8. `示例`：从真实数值调用开始写代码。

## 中文写作约定

中文卡片使用工程师能直接理解的语言，不做逐字直译。正文解释 API 合约、参数边界和运行语义；内部控制器细节、未公开恢复流程和设备实现名不放进公开卡片。

Python SDK 参数保留 `snake_case`。`调用方式` 只写参数名和类型；具体数值放在 `示例`。
