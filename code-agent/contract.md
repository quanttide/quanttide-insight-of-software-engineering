# 契约原型：角色 × 义务 × 保证 × 执行者

从两本 handbook（[code 手册](https://github.com/quanttide/quanttide-handbook-of-software-engineering)、[work 手册](https://github.com/quanttide/quanttide-handbook-of-knowledge-work)）与仓库里的 `.quanttide/*/contract.yaml` 捕捉到的共同形状。

## 一、现场的四类契约

| 契约 | 载体 | 谁被约束 | 保证怎么判 |
|---|---|---|---|
| **平台契约**（`categories/platform`） | code 手册 | 跨项目的组件角色（Provider/Studio/CLI） | 质量门禁给命令：dart format / flutter analyze、gofmt / go vet、rustfmt / clippy，本地从严与 CI 一致 |
| **产物规范**（`piece/artifact`） | work 手册 | 每件产物 | 六条共性规则 + 每件产物自己的验收 |
| **任务规范**（`process/task`） | work 手册 | 产物之间的流动 | 三段齐全、已登记画廊、未违反共性规则 |
| **工作流步骤判据**（`code-implement.yaml` 等） | work 档案 | 一次具体工作 | 每步 `criteria` 带执行者：rule 跑命令、agent 判、human 拍 |

外加机器可读的两个实例：`.quanttide/asset/contract.yaml`（资产组成：双轴分类 + audience: human/ai/engine）与 `.quanttide/docs/contract.yaml`（文档规范：标题层级、代码块语言必填、命名大小写）。

## 二、原型拆成四件套

**① 角色**——契约先声明它约束谁。产物规范约束“产物”、平台契约约束“组件角色”（Provider=Go、Studio=Flutter、CLI=Rust，**不以项目为转移**）、工作区规范约束“一次工作的边界”。

**② 义务**——必须做什么，可数、可列。三段式流动、单一去处、不留副本；桶命名 `{产品线}-{用途}`、IaC 目录 `manifests/terraform/`。

**③ 保证**——怎样算做到，且**必须可判**。门禁给的是命令而不是形容词；验收是“未犯常见错误：把 `gallery.md` 改成 `case.md`……”这种可对照的清单。

**④ 执行者**——每条义务与保证标出归属。工作流里这一步是显式的三类：`rule`（机器可运行）/ `agent`（AI 判）/ `human`（人拍）。**这就是“责任分配”在文本里的落地形式**。

## 三、契约与规格的三条差别

**下界而非上界。** 平台契约明文：“**契约未覆盖的选型由项目自定**”“状态管理库（如 Riverpod）属项目内选型，不纳入平台契约”。规格倾向于描述可接受行为（什么可以），契约只锁定必须的（什么一定），未覆盖处留给对方。

**保证由独立方判。** 执行者不能自判：步骤由 AI 跑，判据里常由 rule 或 human 来判——判据的执行者与义务的执行者分离，契约才有约束力。

**有权威载体。** 每份契约住在唯一处：平台契约在 code 手册、产物契约在画廊案例、JSON 形状的权威在 toolkit `tests/fixtures/`、资产与文档契约在 `.quanttide/`。契约不许有第二个副本——否则判的时候不知道按哪份判。

## 四、契约怎么长

**从实践提炼，反例修正规则。** 平台契约“从现有应用的工程实践中提炼”；产物规范明写“新增产物的规格即对共性规则的检验，**出现反例时修正规则而非硬套**”。所以契约是可修订的，且修订有触发条件——反例，不是偏好。

## 五、与观察者的接口

契约就是观察者要的那个中间表示：**义务与保证分开列，人审的是契约而不是产物**。验证记录里那条「反馈循环缺失」在这里闭合——有判据（可跑的门禁、对账脚本、验收清单）就是循环闭合，只能靠事后返工发现就是缺失。所以契约的第三条（保证必须可判）不是文风要求，是观察者能不能成立的前提。
