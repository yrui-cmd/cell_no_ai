# cell_no_ai

一张图，两条独立路线：检查官方可识别的水印信号，或通过小描 API 提交去 AI 水印处理并取回结果。

`cell_no_ai` 提供两项功能：

- **检测水印**：打开 OpenAI 官方验证页，由用户自行上传或粘贴图片。
- **去 AI 水印**：通过小描 API 查询实时余额、提交图片、等待处理并下载交付结果。

## 工作方式

每个新的去水印任务先调用 `GET /api/balance`，显示实时可用余额和本次 1 额度费用。只有余额查询成功、额度足够且用户已经授权，才会上传图片；查询失败或余额不足时不会用提交接口试探。

提交后继续查询同一个任务，直到下载并验证返回图片；任务号或“已提交”不算交付。原图不会被覆盖。

本流程主要面向 SynthID 隐藏水印处理；C2PA 内容凭证留给后续描摹流程处理。它描述的是工作分工，不承诺所有水印都能被清除。检测与去水印相互独立，去水印效果以服务返回和后续验证为准。

## 安装

把本仓库复制到 Codex 的 skills 目录，目录名为 `cell_no_ai`：

```sh
git clone https://github.com/yrui-cmd/cell_no_ai.git ~/.codex/skills/cell_no_ai
```

Windows 默认目录是 `%USERPROFILE%\.codex\skills\cell_no_ai`，macOS 是 `~/.codex/skills/cell_no_ai`。若目录已存在，请先查看已有内容，不要盲目覆盖。安装后重启 Codex 并开启新任务。

[ cell_su7 ](https://github.com/yrui-cmd/cell_su7) 安装包也包含本 skill，已有独立安装会保留。

## 使用

告诉 Codex：`用 cell_no_ai 检测水印`，或附上 PNG/JPG 并说 `用 cell_no_ai 去水印`。

去水印需要小描 API Key。你可以直接把 Key 粘贴到 Codex 聊天框，由助手完成配置，无需自己设置环境变量或运行命令。助手不回显密钥，持久保存时仅使用 Windows DPAPI 或 macOS Keychain，不提交到仓库。详细凭据规则、API 契约及操作顺序见 [SKILL.md](SKILL.md) 和 [接口说明](references/api.md)。本仓库提供 agent 工作流说明，不捆绑运行环境或服务端，也不内置密钥。

## 许可

MIT，见 [LICENSE](LICENSE)。
