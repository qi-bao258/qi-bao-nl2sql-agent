# 贡献指南

感谢关注本项目。这是一个完整可运行的项目，欢迎通过 Issue 或 Pull Request 参与改进。

## 本地开发

环境准备与启动步骤见 [README 快速开始](README.md#quick-start)。**所有改动请基于 `main` 提交。** 开始修改前建议先跑通完整链路，确保基线可用：

```bash
uv sync
# 启动 Docker 基础服务并构建元数据知识库，见 README 第 6~7 步
uv run python -m app.scripts.build_meta_knowledge -c conf/meta_config.yaml
```

## 提交前检查

```bash
# 后端：静态检查与格式
uv run ruff check --fix .
uv run ruff format .

# 前端：类型检查与构建
cd frontend && pnpm install && pnpm build
```

仓库已配置 `pre-commit`，安装后可自动执行上述检查：

```bash
uv run pre-commit install
```

## 提交信息

采用约定式前缀，与现有历史保持一致：

| 前缀 | 用途 |
| --- | --- |
| `feat:` | 新功能 |
| `fix:` | 问题修复 |
| `docs:` | 文档变更 |
| `refactor:` | 不改变行为的重构 |
| `chore:` | 构建、依赖、工具链 |

## 不要提交的内容

以下内容已被 `.gitignore` 覆盖，请勿强制添加：

- `.env`、`frontend/.env` 等本地环境文件
- `docker/embedding/` 下的模型文件（约 1.3 GB）
- `logs/`、`_vite.log` 等运行日志
- `node_modules/`、`.venv/`、`dist/` 等依赖与构建产物
- `package-lock.json`（前端统一使用 pnpm）

## Pull Request

- 说明改动目的与影响范围，涉及流程或配置变更时附上验证方式。
- 一次 PR 聚焦一件事，避免混入无关格式化改动。
- 涉及 SQL 执行、检索策略或配置结构的改动，请在描述中说明对现有行为的影响。
