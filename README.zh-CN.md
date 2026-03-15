# OpenClaw Discord 私聊语音 Skill

[English](./README.md) | [简体中文](./README.zh-CN.md)

为现有的 OpenClaw 运行目录安装 Discord 私聊语音输入能力，使用本地 `faster-whisper` 做免费转写。

这个仓库本身也是一个合法的 OpenClaw skill 仓库。Skill 入口文件是 [`SKILL.md`](./SKILL.md)，仓库根目录本身就是 skill 根目录。

## 它会做什么

- 接收 Discord 私聊语音消息
- 用本地 `faster-whisper` 转写音频
- 将转写文本转交给 OpenClaw
- 部署一个用于语音桥接的 macOS `launchd` 服务
- 增加 `oc-voice-*` 系列 shell alias 方便管理
- 关闭 OpenClaw 原生的音频附件预处理，避免与桥接流程抢占处理

## 仓库结构

```text
SKILL.md
agents/openai.yaml
scripts/install.py
assets/runtime/discord-dm-voice/
README.md
README.zh-CN.md
```

## 安装

```bash
python3 scripts/install.py --openclaw-home ~/.openclaw
```

可选参数：

- `--python /绝对路径/python3`
- `--model base`
- `--language zh`
- `--skip-python-install`
- `--skip-npm-install`
- `--skip-deploy`

## 验证

```bash
oc-voice-status
oc-voice-logs
```

然后在 Discord 私聊里给 bot 发一条新的语音消息。

## 说明

- 目标平台：macOS + `launchd`
- 适用范围：仅 Discord 私聊语音消息
- 前提假设：`~/.openclaw/openclaw.json` 里已经配置好 Discord
