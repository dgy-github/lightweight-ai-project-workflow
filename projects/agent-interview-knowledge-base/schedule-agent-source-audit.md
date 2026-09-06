# 排产 Agent 真实项目跟踪记录

## 当前跟踪对象

- 主项目：`D:/chennian/schedule-agent-langgraph`
- 最小演示项目：`D:/chennian/langgraph-schedule-agent`
- 本记录只引用可读取到的代码、配置、测试和文档，不把目录中的敏感配置写入知识库。

## 已核验事实

### 主项目 `schedule-agent-langgraph`

- README 定义的主链路：`START → route`，只读路径为 `query → rag → respond`，写路径为 `governance → preview → execute → verify → respond`。
- `graph/` 目录存在 `state.py`、`graph.py`、`conditions.py` 以及 route、query、rag、governance、preview、execute、verify、respond 等节点。
- `configs/intents.json` 定义 19 种意图，包含查询、写操作和管理操作；每个意图有触发词、必填实体、风险等级、是否需要审批和最低角色。
- 权限层级为：业务员 < 工艺员 < 主任 < 厂长。
- 数据源为 SQLite `data/schedule.db`，README/CLAUDE 说明包含 49,981 条生产订单。
- RAG 使用 Qdrant + `fastembed`，Qdrant 不可用时回退到规则文件关键词匹配。
- 规则源位于 `rag/rules/`；README/CLAUDE 记录 Qdrant 中有 32 条排产规则向量。
- 意图识别使用规则匹配和关键词打分，明确要求不在 route 节点调用 LLM。
- LLM 用于结构化输出和对话，项目文档记录本地 Qwen 27B 与 `schedule-agent` 模型配置。
- 评测目录包含 30 条 golden cases、LLM judge、audit 和 report；CI 流程为 audit → rule-eval → full-eval。
- 测试覆盖路由、管理 API、鉴权、操作幂等、checkpoint、数据库、评测数据、RAG fallback、会话持久化、事务和迁移；另有 Playwright E2E 目录。
- Dockerfile、Jenkinsfile、CI 脚本和部署文档均存在，说明工程交付链路已有仓库证据。
- 验收矩阵明确：SQLite 通过不等于 PostgreSQL 生产链路完成；发布前还需要 PostgreSQL integration、浏览器 E2E 和评测硬门槛全部成功。

### 最小演示项目 `langgraph-schedule-agent`

- README 明确定位为“面试可讲的最小闭环”。
- 包含 `src/schedule_agent/graph.py`、`tools.py`、`rag.py`、`trace.py`、5 条 golden questions 和 evidence 状态/trace 文件。
- 适合用来讲清楚最小状态机、规则 RAG、只读工具和审批请求；更完整的实现证据优先使用主项目。

## 面试表述更新

推荐把排产项目回答调整为：

> 我跟踪的完整排产 Agent 项目是 `schedule-agent-langgraph`。它不是把所有问题交给大模型，而是用 LangGraph 编排确定性工作流：先由规则和关键词做意图识别，再按只读或写操作分流。只读请求查询 SQLite 并检索排产规则；写操作必须经过权限治理、预览、执行和回读验证。RAG 使用 Qdrant，服务不可用时回退到规则文件关键词匹配。项目还配套 19 个配置化意图、30 条 Golden Cases、LLM judge、audit、Docker/Jenkins 和测试矩阵。

## 需要服务器运行后核验

- 实际启动命令和当前环境变量是否完整可用。
- CLI、管理台 API 和浏览器前端的真实访问地址。
- 一次只读请求的完整 state、trace 和 RAG 返回证据。
- 一次高风险写操作的 governance、preview、execute、verify 实际结果。
- 19 个意图的当前覆盖率、route 准确率和评测报告结果。
- Qdrant 是否实际可用，fallback 是否能在当前环境触发。
- Langfuse/LangSmith trace 是否已接通，当前项目运行是否仍依赖外部服务。
- Docker/Jenkins 的实际构建、测试、部署和回滚结果。

## 面试边界

- 代码和文档能证明“具备实现和测试设计”，不能自动证明“当前服务器已成功上线”。
- README 的开发进度写明管理台和评测追踪仍有 In Progress 项，回答时按实际运行结果更新。
- 不引用部署脚本中的密钥、Token、内网地址或账号信息。
- 服务器启动后，所有“已验证”结论以运行日志、测试输出和实际请求结果为准。
