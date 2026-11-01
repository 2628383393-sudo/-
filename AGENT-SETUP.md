# ¥30/月 节约模式

本项目只在 owner 手动给 Issue 添加 `ai-task` 标签时运行。**请勿在配置 API 密钥前合并或测试。**

## 内置停止机制
- 每个 UTC 月最多 **15 次** `ai-task.yml` 运行（按 GitHub 工作流运行数量统计）。超过即在调用模型前退出。
- 每次任务最多 **3 次模型调用**：OpenAI 规划 → DeepSeek Flash 修改 → OpenAI 审核。
- 输入最大 25,000 UTF-8 字节，单次输出分别限 350 / 1800 / 230 tokens，禁用 SDK 自动重试。
- 工作流最长 10 分钟，单次只有一个并发执行任务，不会自动合并 PR。
- Actions 日志中输出 `COST_RECORD` 和 `TASK_COST_ESTIMATE_CNY`，计算仅为估算，未考虑缓存、实际汇率和服务商账单。费用来自 API 平台。
- **¥30 是目标，不是此代码能保证的账单硬上限。** 每月任务运行配额不是精确的花费统计，其他地方使用相同 API 密钥不计入其中。

## 真正限制账单
- 在 OpenAI API Platform 的组织/项目 **Limits** 中设置对应项目月度消费上限，并启用 **Enforce a hard limit**（仅开提醒不会停机）；服务商可能延迟停止，存在少许超额。
- DeepSeek 采用单独少量预付余额，关闭自动充值（如账户可设置），在控制台查看余额和账单；请注意余额不足时 API 调用失败，并确认平台是否提供额外可用限额。
- 建议分配 OpenAI ¥20、DeepSeek ¥10，留意 OpenAI 以美元计价，金额换算为你设置时的实际币种。
- 两个平台开通后，在 GitHub Settings → Secrets and variables → Actions 设置 `OPENAI_API_KEY`、`DEEPSEEK_API_KEY`，密钥不可写入 issue 或聊天。
- 在 GitHub Settings → Actions → General 允许 Actions 创建 PR，并配置 `ai-task` 标签。此测试方案只创建修改提案，不会自动部署网页。

## 限制
- DeepSeek 使用目前官方支持的 `deepseek-flash`，而不是旧的 `deepseek-chat`。
- AI 生成代码可能出错，HTML 检查不是浏览器自动化测试。
- 只支持修改根目录一个既有 HTML 文件。
- 这不是官方 DeepSeek Super-agent 原型直接安装。
