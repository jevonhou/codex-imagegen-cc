English | [简体中文](README.zh-CN.md)

# Codex Imagegen for Claude Code

Give Claude Code an image-making companion for design work. Codex Imagegen is a small Claude skill that asks your local Codex CLI to create image assets, then helps Claude use them in your project.

Use it for a website hero, an illustrated cover, a presentation background, a texture, or another visual where a generated image fits the brief. Claude keeps working on the design; Codex generates the image.

> Independent community project. Not affiliated with or endorsed by OpenAI or Anthropic. This skill uses your own local Codex installation and account.

## How it works

1. Ask Claude to make a visual deliverable or explicitly invoke `/codex-imagegen`.
2. Claude decides whether an image is useful, prepares a brief, and invokes `codex exec` on your machine.
3. Codex generates an image and saves a copy in your project. Claude checks it and uses it in the deliverable.

The skill favors editable code or vectors for UI controls, text, charts, and simple shapes. Generated images are illustrative, not proof of real products, people, or events. Your existing assets, instructions, and cost limits take precedence.

## Requirements

- [Claude Code](https://code.claude.com/docs/en/overview), running locally with access to your project and terminal.
- [Codex CLI](https://developers.openai.com/codex/cli), installed and signed in, with image generation available in its active environment.
- Git for the installation command below. The commands use a POSIX shell; Windows users can use a compatible shell with Claude and Codex available in the same environment.
- Permission for Claude to run the necessary command and for Codex to write the requested project asset. Your Claude and Codex settings determine which prompts appear.

Codex usage counts against the applicable account limits or billing. Availability, generation time, and costs depend on your account and configuration. This skill does not bundle an image model or provide a separate subscription.

Check your Codex setup without sharing credentials:

```sh
codex --version
codex login status
codex features list
```

Check `image_generation` in the feature list. A feature flag alone does not guarantee your account or environment can generate an image.

## Install

Clone this repository and copy the skill into your personal Claude Code skills directory:

```sh
git clone https://github.com/jevonhou/codex-imagegen-cc.git
mkdir -p ~/.claude/skills
if [ -e ~/.claude/skills/codex-imagegen ] || [ -L ~/.claude/skills/codex-imagegen ]; then
  echo 'A codex-imagegen skill already exists. Review it before replacing it.'
else
  cp -R codex-imagegen-cc/skills/codex-imagegen ~/.claude/skills/
fi
```

This does not overwrite an existing installation. To install for one project instead, copy `skills/codex-imagegen` into that project's `.claude/skills/` directory. A personal skill with the same name takes precedence over a project skill; check for an existing copy when testing or updating. See [Claude Code's skill documentation](https://code.claude.com/docs/en/skills) for discovery and precedence.

## Try it

From your project in Claude Code, try:

```text
/codex-imagegen Create a calm landscape hero image for a landing page about a lakeside retreat. Leave room for a heading and use the result in the page.
```

You can also describe the design task naturally. Automatic selection depends on Claude's skill discovery and the task context; invoke the skill explicitly if needed. A first run may require a command permission prompt. Ask for a specific destination if you have one, and review the generated image in its final layout.

## Troubleshooting

- **Skill does not appear:** Check the directory and file name, start a new Claude Code session, and see the [skill discovery guide](https://code.claude.com/docs/en/skills).
- **`codex` is not found or not signed in:** Install the CLI and sign in using the [Codex CLI guide](https://developers.openai.com/codex/cli). Never paste credentials into an issue or conversation.
- **Generation fails:** Check image generation availability, permissions, network access, and account usage. Claude should report the failure rather than claim an image was created.
- **No image in the project:** Ask Claude for the saved path and check whether the command was allowed to write there. The original generated file may be stored under your Codex home; project assets should be copied into the project.

On macOS, Claude was tested reading this skill's instructions and using Codex CLI to generate and save an image. Windows and Linux have not been tested; availability also depends on the host, permissions, and account.

## Feedback and contributions

Open an issue or pull request in this repository. Include the operating system, Claude Code and Codex versions, a minimal reproduction, and any relevant error after removing secrets and personal data. Please do not upload private project files or generated images unless you have permission to share them.

## License

[MIT](LICENSE). Generated images are subject to the applicable service terms and any rights in supplied reference material.
