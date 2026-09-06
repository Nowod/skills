# 黑盒测试用例 Skills

面向 Codex 的黑盒测试用例生成与独立复核 Skill 集合。

## Skills

| Skill               | 用途                                     |
| ------------------- | ---------------------------------------- |
| `to-testcase`     | 根据 Spec 设计、生成或修订黑盒测试用例。 |
| `testcase-review` | 在独立上下文中复核测试用例。             |

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

两个 Skill 应一同安装，因为 `testcase-review` 会读取 `to-testcase` 及其示例。Codex 的 Skill 发现规则见 [OpenAI 官方文档](https://learn.chatgpt.com/zh-Hans/docs/build-skills)。

## 使用

```text
$to-testcase 根据这个行为 Spec 生成测试用例
```

每次复核都新建会话，提供同一份 Spec、当前版本的用例及其澄清问题，以及可选测试数据；不带入生成对话或既往复核结果。

```text
$testcase-review 根据同一 Spec 独立复核这些测试用例
```

推荐流程：

```text
确认 Spec → 生成用例 → 独立复核 → 按复核结果修订
```

生成缺陷应集中修订；Spec 或测试能力缺口应交由用户确认。重复问题和复核分歧依据 Spec 和用例证据处理；现有依据不足以裁决，或修订持续无法取得进展时，交由用户决定。

## License

[Apache License 2.0](LICENSE)
