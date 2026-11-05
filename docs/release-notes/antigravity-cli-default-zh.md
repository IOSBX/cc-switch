# Antigravity CLI 默认入口更新

本分支基于 CC Switch 4.0.25，复用已有的 Antigravity CLI 接入，将 `agy` 提升为默认入口。更新已上传到 `feat/antigravity-cli-default` 分支。

## 更新内容

- **默认显示 Antigravity CLI**：应用顺序调整为 Codex 后紧接 Antigravity CLI，Gemini CLI 默认隐藏；应用选择器和页面标题统一使用完整名称。
- **迁移旧 Gemini 布局**：旧设置中 Gemini 为显示状态，且尚无 `agy` 显示开关时，启动后改为显示 Antigravity CLI、隐藏 Gemini；如果保存过应用排序，Antigravity CLI 会接替其中的 Gemini 位置。
- **保留明确的显示选择**：设置中已有 `agy` 显示开关时，沿用用户保存的布局。仍可在「应用」页重新显示 Gemini CLI。
- **恢复上次停留的页面**：上次选中 Gemini，但加载后的设置隐藏 Gemini、显示 Antigravity CLI 时，自动进入 Antigravity CLI。页面会等待设置加载完成再判断。

## 使用方法

1. 确认终端能够运行 `agy --version`，并按 Antigravity CLI 自身的流程完成官方登录，或准备所需的 API Key。
2. 在 CC Switch 中打开 **Antigravity CLI**，添加或编辑供应商。官方登录卡可留空 API Key；第三方卡填写 Key、自定义地址和所需模型。
3. 点击供应商卡片的 **打开终端**，启动使用该卡片配置的 `agy`。如需指定模型，可通过表单中的模型列表选择。

Gemini CLI 的供应商记录与 Antigravity CLI 分开保存，旧 Gemini 供应商不会自动转换成 Antigravity 供应商。官方登录沿用 `agy` 自己的登录状态；第三方 Key 配置作用于卡片打开的终端，直接在其他终端输入 `agy` 仍使用其原有登录。

## 可用功能

本次入口调整沿用已有的供应商配置、模型选择、MCP、Skills、提示词、会话查看与恢复、用量统计。Antigravity CLI 的可用功能以其现有接入为准，本分支的入口调整不增加本地路由、故障转移或 Stack 模式。

配置路径、官方登录与 API Key 的具体行为见 [Antigravity CLI 接入说明](../agy-integration-zh.md)。

## 验证结果

- 98 项相关前端测试通过，覆盖应用顺序、模型表单和终端启动。
- 99 项 Antigravity 接入测试通过，另有 2 项涉及真实 API 或系统钥匙串的测试按默认设置忽略；新增的 2 项布局迁移测试也已通过，其中 1 项包含在上述 99 项中。
- TypeScript 类型检查和 macOS 应用构建通过；构建版本为 4.0.25。
- 本机已安装并启动构建产物，实际设置保存为 `gemini: false`、`agy: true`。
- 对照检查确认原版显示 Gemini、修改版显示 Antigravity CLI，回滚副本恢复原版输出，原有文件的 SHA-256 与基线一致。

测试结果针对本分支的配置和接入逻辑；模型请求是否成功取决于所使用的账号、服务端和模型权限。
