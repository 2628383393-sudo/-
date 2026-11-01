# ChatGPT + DeepSeek 协作系统（试运行）

本仓库目前是诗集 HTML 项目。此提交只添加 AI 执行器和 GitHub Actions 配置，不会主动修改网页，也不会自动发布网站。

## 启用步骤

1. 审核并手动合并此 PR。
2. 在 Settings → Secrets and variables → Actions 添加两个 Repository secrets：`OPENAI_API_KEY`、`DEEPSEEK_API_KEY`。**密钥不要发到聊天、Issue 或代码文件**。两种 API 都可能产生独立费用。
3. 在 Settings → Actions → General 配置允许 Actions 创建 Pull requests，并按需要开放工作流写权限。
4. 在仓库 Issues 中创建标签 `ai-task`。
5. 使用仓库所有者账号创建 Issue，写清楚网页修改需求；**手动添加 `ai-task` 标签**才触发 AI。
6. OpenAI 负责规划和代码审核，DeepSeek 负责提出完整 HTML 替换内容。审核通过后由 GitHub Actions 创建独立 PR。**必须人工审核后合并**。

## 限制与注意事项

- 这是基于 DeepSeek API 的轻量协作实现，**不是 DeepSeek 官方 Super-agent 的直接接入**。
- 一次最多修改一个仓库根目录内、原本就存在的 HTML 文件。
- 无自动部署、无自动合并。首次启动前须自行配置密钥和工作流权限。
- AI 模型可能引入错误；HTML 检查只是基本语法扫描，**不是浏览器端到端测试**。
- HTML 源码和 Issue 内容会发送给模型服务提供商。仓库若包含私密信息，需先清理。
- `issue` 触发仅限仓库 OWNER 创建的任务，并需打标签。不要随意放宽权限。
- 当前两个诗集 HTML 文件内容相同，建议确定真正入口后再让 AI 改动。
