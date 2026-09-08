# 黑盒测试用例 Skills

面向 Codex 的黑盒测试用例生成与独立复核 Skill 集合。

## Skills

| Skill | 用途 |
| --- | --- |
| [to-testcase](to-testcase/SKILL.md) | 根据 Spec 设计、生成或修订黑盒测试用例。 |
| [testcase-review](testcase-review/SKILL.md) | 独立复核测试用例，报告生成缺陷与缺口。 |

## 安装

将两个 Skill 目录并列复制到目标项目的 `.agents/skills/`：

```bash
mkdir -p /path/to/project/.agents/skills
cp -R to-testcase testcase-review /path/to/project/.agents/skills/
```

目录结构：

```text
project/
└── .agents/
    └── skills/
        ├── to-testcase/
        │   ├── SKILL.md
        │   └── testcases.md
        └── testcase-review/
            └── SKILL.md
```

两个 Skill 应一同安装，因为 `testcase-review` 会读取 `to-testcase/testcases.md` 中的用例约定和示例。Codex 的 Skill 发现规则见 [OpenAI 官方文档](https://learn.chatgpt.com/zh-Hans/docs/build-skills)。

## 使用

生成时提供已整合原始 PRD 和已确认澄清的 Spec，以及可用测试数据。

```text
$to-testcase 根据这个行为 Spec 生成测试用例
```

独立复核在新会话或独立上下文中调用，提供同一份 Spec、当前版本的用例、未解决问题及可用测试数据；不带入生成对话或既往复核结果。

```text
$testcase-review 根据同一 Spec 独立复核这些测试用例
```

推荐流程：

```text
确认 Spec → 生成用例 → 独立复核 → 按复核结果修订
```

生成缺陷交由 `to-testcase` 修订。新确认的需求先更新到 Spec；测试数据或测试能力缺口补足到能够明确用例的准备要求、操作和预期后，再生成受影响的用例。数据和文件由测试人员按用例要求准备，未受影响的部分继续处理。

修订后，按变更及关联影响确定复核范围。复核结论按 [testcase-review 的报告规则](testcase-review/SKILL.md#报告结果) 给出，修订分歧按 [to-testcase 的复核修订规则](to-testcase/SKILL.md#复核修订) 处理。

## License

[Apache License 2.0](LICENSE)
