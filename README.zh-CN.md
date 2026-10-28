[English](README.md) | 简体中文

# Codex Imagegen for Claude Code

给 Claude Code 一个设计生图搭档。Codex Imagegen 是一个轻量 Claude Skill：让 Claude 调用你本机的 Codex CLI 生成图片素材，再将素材用于当前项目。

网页首屏、插画封面、演示文稿背景、纹理等场景，只要生成图片符合设计需求，就可以使用它。Claude 继续负责设计，Codex 负责生成图片。

> 独立社区项目，与 OpenAI 或 Anthropic 无隶属关系，也未获得其背书。本 Skill 使用你自己本机安装的 Codex 和账户。

## 工作方式

1. 让 Claude 完成视觉设计任务，或显式调用 `/codex-imagegen`。
2. Claude 判断图片是否有帮助，整理图片描述，然后在你的机器上调用 `codex exec`。
3. Codex 生成图片并复制到项目中，Claude 检查后将其用于交付物。

界面控件、文字、图表和简单图形优先使用可编辑的代码或矢量。生成图是视觉素材，不能作为真实产品、人物或事件的事实证明。你提供的现有素材、要求和成本限制始终优先。

## 使用条件

- 在本机运行的 [Claude Code](https://code.claude.com/docs/en/overview)，并能访问项目和终端。
- 已安装并登录的 [Codex CLI](https://developers.openai.com/codex/cli)，且当前 Codex 环境能够使用图片生成。
- 下方安装命令需要 Git 和 POSIX shell；Windows 用户可使用兼容的 shell，且 Claude 与 Codex 需要位于同一可访问环境。
- Claude 获得执行必要命令的权限，Codex 获得写入项目素材的权限。是否出现权限提示取决于你的 Claude 和 Codex 配置。

Codex 的使用会计入对应账户的用量限制或费用。可用性、生成时间和成本取决于账户及配置。本 Skill 不包含图片模型，也不提供独立订阅。

无需分享凭据，即可检查 Codex 环境：

```sh
codex --version
codex login status
codex features list
```

在功能列表中查看 `image_generation`。功能开关本身不能保证账户或环境一定能够生成图片。

## 安装

克隆本仓库，将 Skill 复制到个人 Claude Code Skill 目录：

```sh
git clone https://github.com/jevonhou/codex-imagegen-cc.git
mkdir -p ~/.claude/skills
if [ -e ~/.claude/skills/codex-imagegen ] || [ -L ~/.claude/skills/codex-imagegen ]; then
  echo 'A codex-imagegen skill already exists. Review it before replacing it.'
else
  cp -R codex-imagegen-cc/skills/codex-imagegen ~/.claude/skills/
fi
```

该命令不会覆盖已安装的同名 Skill。如果只想在单个项目使用，可以将 `skills/codex-imagegen` 复制到该项目的 `.claude/skills/` 目录。同名个人 Skill 的优先级高于项目 Skill；测试或更新时请先检查是否已有旧版本。发现规则与优先级见 [Claude Code Skill 文档](https://code.claude.com/docs/en/skills)。

## 试一试

在项目目录中打开 Claude Code，例如输入：

```text
/codex-imagegen 为湖畔度假主题的落地页生成一张宁静的风景首屏图，留出标题空间，并将图片用于页面。
```

也可以直接用自然语言描述设计任务。自动选择取决于 Claude 的 Skill 发现机制和任务上下文；必要时显式调用。首次运行可能出现命令权限提示。如果有指定保存位置，请直接告诉 Claude，并在最终布局中检查图片效果。

## 常见问题

- **找不到 Skill：**检查目录与文件名，开始一个新的 Claude Code 会话，并查看 [Skill 发现说明](https://code.claude.com/docs/en/skills)。
- **找不到 `codex` 或尚未登录：**按 [Codex CLI 指南](https://developers.openai.com/codex/cli)安装和登录。不要在 Issue 或对话中粘贴凭据。
- **生成失败：**检查图片生成功能、权限、网络和账户用量。Claude 应说明失败原因，不应声称已经生成。
- **项目中没有图片：**向 Claude 确认保存路径，并检查命令是否获准写入。原始生成文件可能位于 Codex 主目录；用于项目的素材应复制到项目内。

已在 macOS 上验证：Claude 读取本 Skill 的说明后，调用 Codex CLI 真实生成并保存了图片。Windows 和 Linux 尚未验证；实际可用性也受宿主、权限和账户影响。

## 反馈与贡献

欢迎在本仓库提交 Issue 或 Pull Request。请提供操作系统、Claude Code 和 Codex 版本、最小复现步骤，以及已去除密钥和个人数据的相关错误。未经授权请勿上传私人项目文件或生成图片。

## 许可证

[MIT](LICENSE)。生成图片的使用仍受相应服务条款和所用参考素材权利约束。
