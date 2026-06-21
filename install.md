# Installation

[中文](#中文安装说明)

## Install For Codex

Clone the repository into the Codex skills directory:

```bash
mkdir -p "${CODEX_HOME:-$HOME/.codex}/skills"
git clone https://github.com/kouzt123/image-localization-Codex \
  "${CODEX_HOME:-$HOME/.codex}/skills/image-localization"
```

If you already keep projects in `~/Developer`, clone there and symlink the whole directory:

```bash
git clone https://github.com/kouzt123/image-localization-Codex ~/Developer/image-localization-Codex
mkdir -p "${CODEX_HOME:-$HOME/.codex}/skills"
ln -sfn ~/Developer/image-localization-Codex \
  "${CODEX_HOME:-$HOME/.codex}/skills/image-localization"
```

Restart Codex or refresh skills if your environment requires it.

## Verify

Ask Codex:

```text
Use image-localization to inspect this image and propose localized ad sizes.
```

If the skill is available, Codex should read `SKILL.md` before acting.

## Update

If installed by clone:

```bash
cd "${CODEX_HOME:-$HOME/.codex}/skills/image-localization"
git pull --ff-only
```

If installed by symlink:

```bash
cd ~/Developer/image-localization-Codex
git pull --ff-only
```

## Notes

- No external image API key is required.
- Image generation uses Codex built-in image capabilities and your Codex subscription quota.
- Optional terminology memory lives in `brand_term_memory.json` or a project-local `.image-localization/brand_term_memory.json`.
- Run `./scripts/setup-codex-attribution.sh` if you want future local commits to include `Co-authored-by: codex <codex@openai.com>`.

# 中文安装说明

## 安装到 Codex

直接克隆到 Codex skills 目录：

```bash
mkdir -p "${CODEX_HOME:-$HOME/.codex}/skills"
git clone https://github.com/kouzt123/image-localization-Codex \
  "${CODEX_HOME:-$HOME/.codex}/skills/image-localization"
```

如果你习惯把项目放在 `~/Developer`，可以克隆后软链接整个目录：

```bash
git clone https://github.com/kouzt123/image-localization-Codex ~/Developer/image-localization-Codex
mkdir -p "${CODEX_HOME:-$HOME/.codex}/skills"
ln -sfn ~/Developer/image-localization-Codex \
  "${CODEX_HOME:-$HOME/.codex}/skills/image-localization"
```

如果你的 Codex 环境需要刷新 Skill，安装后重启或刷新一次。

## 验证

在 Codex 中输入：

```text
使用 image-localization，识别这张图片并建议本地化广告尺寸。
```

如果 Skill 生效，Codex 会先读取 `SKILL.md` 再行动。

## 更新

如果是直接克隆安装：

```bash
cd "${CODEX_HOME:-$HOME/.codex}/skills/image-localization"
git pull --ff-only
```

如果是软链接安装：

```bash
cd ~/Developer/image-localization-Codex
git pull --ff-only
```

## 说明

- 不需要额外图片 API Key。
- 图像生成使用 Codex 内置图像能力和你的 Codex 订阅额度。
- 可选术语记忆文件为 `brand_term_memory.json`，也可以使用项目内的 `.image-localization/brand_term_memory.json`。
- 如果你希望本地后续提交包含 `Co-authored-by: codex <codex@openai.com>`，运行 `./scripts/setup-codex-attribution.sh`。
