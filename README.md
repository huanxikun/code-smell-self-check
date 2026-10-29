# 代码坏味道自查

一个用于代码坏味道自查的 Codex Skill。

**当前状态：已加入十四条规则。** 覆盖《代码之丑》讲解的主要坏味道及作者补充内容；其他规则后续补充。

1. 命名准确体现业务含义：检查不精准的命名、用实现细节代替意图，以及业务角色不明确的问题。
2. 英语命名准确、规范且一致：检查语法结构、业务词义、拼写、拼音和不清晰的简写，并对照团队命名规范和词汇表。
3. 重复代码：检查复制粘贴、结构重复和 if/else 中高度相似的语句，遵循 DRY 原则，避免重复维护同一知识，也避免仅凭表面相似强行抽象。
4. 长函数：超过 20 行就重点检查，识别多个业务流程或不同细节层次混杂的问题，优先可维护性，以小步整理避免持续堆积逻辑。
5. 大类：检查职责不单一、字段未合理分组的问题，按业务含义与变化方式拆分小类，明确字段、行为和协作边界。
6. 长参数列表：按共同业务含义封装参数对象，分离稳定依赖与每次输入，移除控制行为的标记参数，避免只隐藏参数而未降低复杂度。
7. 滥用控制语句：消除嵌套与不必要的 else，用卫语句和提前返回降低缩进；重复 switch 引入模型以多态取代，辅以圈复杂度检查。
8. 缺乏封装：消除火车残骸式的连续调用，隐藏委托关系；对有业务约束的基本类型、字符串和集合引入模型，避免基本类型偏执。
9. 可变的数据：移除 setter，用表达业务行为的方法或构造函数限制修改入口；值对象设计为不变类，全局可变数据收敛到受控入口。
10. 变量声明与赋值分离：一次性完成变量初始化，用 final 约束赋值；集合用声明式写法一次初始化，优先不可变集合。
11. 依赖混乱：不在接口层与业务层之间直接传递请求对象，引入防腐层模型；业务代码不出现具体实现，依赖抽象并向稳定的方向依赖。
12. 不一致的代码：命名、方案和代码层次保持一致；类似含义用类似表达，同一问题统一一套方案，不同层次的代码分开。
13. 落后的代码风格：评估用 Optional 表达可能缺失的值，用简洁的列表转换表达筛选、映射和汇总；复杂控制流保留清晰的循环，结合项目版本演进写法，不在 lambda 中写长代码。
14. 谨慎变动与易被忽视的坏味道：新需求到来时不假思索地加接口、改实体，霰弹式修改与发散式变化，中间人，static 与 Singleton，命名遗留习惯（I/Impl、随意缩写），用注释代替清晰代码，潦草的项目文档——这些坏味道缺少直观形态或被当作正常习惯，靠症状和变化原因识别。

## 目录结构

```text
code-smell-self-check/
├── README.md
├── .gitignore
└── skills/
    └── code-smell-self-check/
        ├── SKILL.md
        └── agents/
            └── openai.yaml
```

- `skills/code-smell-self-check/SKILL.md`：Skill 名称、说明和检查规则入口。
- `skills/code-smell-self-check/agents/openai.yaml`：在 Codex 中显示的中文名称、简介和调用提示。

## 安装

仓库发布到 GitHub 后，可在 Codex 中输入以下提示。如果仓库归属、名称或默认分支不同，请相应修改链接。

```text
使用 $skill-installer 安装以下 GitHub 路径中的 Skill：
https://github.com/huanxikun/code-smell-self-check/tree/main/skills/code-smell-self-check
```

也可以克隆仓库，将 `skills/code-smell-self-check` 文件夹复制到用户技能目录 `~/.agents/skills/`。若已有同名 Skill，请先检查已有内容，避免覆盖。

安装后如果没有显示，可重启 Codex。

## 使用

```text
使用 $code-smell-self-check 检查本次代码改动。
```

目前检查已定义的十四条规则，覆盖命名、重复代码、长函数、大类、长参数列表、控制语句、封装、可变数据、变量初始化、依赖方向、一致性、代码风格，以及接口与实体变动、static、Singleton、注释等易被忽视的问题。自查会给出问题位置、原因和改进建议；仅请求检查时不直接修改代码。

## 补充规则

编辑 `skills/code-smell-self-check/SKILL.md` 中的“检查规则”区域，继续添加希望执行的规则即可。

## 上传 GitHub

在 GitHub 新建名为 `code-smell-self-check` 的空仓库，然后在此项目目录执行：

```bash
git init -b main
git add README.md .gitignore skills
git commit -m "Initialize code smell self-check skill scaffold"
git remote add origin https://github.com/huanxikun/code-smell-self-check.git
git push -u origin main
```

上述命令适用于尚未初始化 Git 的本地目录，以及未添加 README 等初始文件的远程空仓库。已经初始化并提交的本地仓库只需设置远程地址并推送，无需重复初始化或提交。

## 许可证

尚未选择开源许可证。正式开放他人复用前，请选定许可证并在仓库根目录添加 `LICENSE` 文件。
