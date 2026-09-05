# Lightweight AI Project Workflow

把一个想法、一次需求或一件日常工作，当作一个可以讨论、规划、执行和验收的小项目。

这个项目面向普通使用者。你不需要先理解 PRD、API、数据库或软件工程流程，只要告诉
AI：

> 我想完成什么，谁会使用，什么结果算做好。

AI 将按下面的流程协作：

```text
讨论清楚 -> 做成计划 -> 一起执行 -> 测试验收 -> 沉淀复用
```

## 立即开始

1. 复制 `templates/project/` 到 `projects/<你的项目名称>/`。
2. 和 AI 一起填写 `01-project-card.md`，先确认目标与边界。
3. AI 生成 `02-plan.md` 并推进任务。
4. AI 自己完成可自动执行的检查，再填写 `03-acceptance.md` 交给你验收。
5. 只有发现反复出现的做法时，才创建 `04-reuse-candidates.json`。

如果当前 AI 支持项目技能，可以直接说：

> 使用 `$lightweight-project` 帮我把这个想法作为一个小项目推进。

## 适合做什么

- 调研、报告、内容和演示材料；
- 活动策划、学习计划和个人事务；
- 表格整理、数据分析和重复工作自动化；
- 业务流程改进和低风险的小工具；
- 已经说了很多轮，需要把散落聊天整理成可交付项目。

涉及资金、隐私、生产数据、公共接口、数据库迁移或不可逆操作时，本流程只负责把需求
整理清楚，随后应进入相应领域的专业流程。

## 核心资料

- [工作流](docs/WORKFLOW.md)
- [质量等级](docs/QUALITY_LEVELS.md)
- [聊天与技能沉淀](docs/REUSE_FROM_CHATS.md)
- [可复用场景目录](docs/SKILL_CANDIDATE_CATALOG.md)
- [完整示例](examples/weekend-trip/01-project-card.md)

首批内置的高频工程协作 Skill 草案：项目导览、报错诊断、代码审查、测试失败修复和
PR 描述。它们已具备可运行结构，但仍需真实历史任务回放才能标记为成熟；也不意味着
普通项目必须使用工程技能。

## AI Agent 求职技能组

针对 AI Agent 岗位，项目提供一条事实约束优先的求职流程：

```text
职位描述分析 -> AI Agent 简历定制 -> 简历事实核验 -> 投递草稿
```

- `job-description-analyzer`：拆解职责、技术要求和岗位匹配；
- `ai-agent-resume-tailor`：基于主简历真实经历进行针对性改写；
- `resume-evidence-check`：检查技术、指标和成果是否有事实来源；
- `job-application-draft`：生成等待人工确认的投递包，不自动提交。

完整使用边界见 [AI Agent 求职流程](docs/AI_AGENT_JOB_WORKFLOW.md)。

本人的项目面试知识库示例见 [AI Agent 开发面试个人知识库](projects/agent-interview-knowledge-base/knowledge-base.md)，配套题目索引见 [项目相关面试题库](projects/agent-interview-knowledge-base/question-bank.md)。

扩展答案卡见 [AI Agent 岗位扩展 50 题个人答案卡](projects/agent-interview-knowledge-base/extended-50-answers.md)。

## 项目原则

- 先确认目标和边界，再大规模执行；
- 文档服务于决策，不以文档数量判断质量；
- AI 自己完成能自动完成的测试，使用者做最终业务验收；
- 一次聊天只能形成候选，不能直接包装成成熟技能；
- 账号、密码、密钥、Cookie、隐私和敏感正文不得进入复用资产。

## 备注说明

- 当前版本是 `0.1.0` 首版，五个高频工程协作 Skill 仍处于历史任务回放阶段。
- `满足 3 项` 只表示值得进入候选池，不表示已经具备正式 Skill 的发布质量。
- 模板中的示例文字需要替换为真实项目内容；不适用的栏目可以删除，不保留空占位。
- 项目产物默认使用简体中文，技术标识符、文件名、命令、代码符号和行业通用缩写保留原文。
- 中文标题、标点、数字、英文与空格的统一规则见[中文格式规范](docs/CHINESE_WRITING_STYLE.md)。

当前版本：`0.1.0`

## License

[MIT](LICENSE)
