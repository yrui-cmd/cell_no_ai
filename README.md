# cell_no_ai

独立的 Codex skill，提供两项功能：

- **检测水印**：打开 OpenAI 官方验证页，由用户自行上传或粘贴图片。
- **去 AI 水印**：通过小描 API 查询实时余额、提交图片、等待处理并下载交付结果。

每次使用先介绍功能；每次新任务必须先调用 `GET /api/balance`，可用额度至少为 1，显示余额和本次费用后按用户授权提交。查询失败或余额不足时不提交。去水印每次消耗 1 额度，服务提供方收取；skill 本身免费开源。

提交后必须等待并领取结果，不以“已提交”作为完成。收到图后直接交付图片或链接，不主动增加质量评价或检测说明。检测与去水印相互独立。

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
