# OpenClaw Discord 私聊语音 Skill

[English](./README.md) | [简体中文](./README.zh-CN.md)

![本地转写](https://img.shields.io/badge/local-STT-2da44e?style=flat-square)
![无付费 API](https://img.shields.io/badge/no%20paid-API-0969da?style=flat-square)
![skill-vetter 已审查](https://img.shields.io/badge/skill--vetter-reviewed-8250df?style=flat-square)
![quick_validate 通过](https://img.shields.io/badge/quick__validate-passed-1a7f37?style=flat-square)
![安装冒烟验证](https://img.shields.io/badge/install-smoke--tested-f0883e?style=flat-square)

把 Discord 私聊语音消息，快速接成 OpenClaw 的可用输入链路，全程本地 `faster-whisper` 转写，不引入付费语音 API。

这个仓库本身也是一个合法的 OpenClaw skill 仓库。Skill 入口文件是 [`SKILL.md`](./SKILL.md)，仓库根目录本身就是 skill 根目录。

## 为什么用这套

如果你不想走“让 bot 进语音频道实时听”的重方案，这个 skill 走的是更稳的路径：

- 直接给 bot 发 Discord 私聊语音
- 本地完成转写
- 把文本交给 OpenClaw
- 在同一个聊天里拿到回复

整体更轻、更省钱，也更适合长期跑着。

## 它会做什么

- 接收 Discord 私聊语音消息
- 用本地 `faster-whisper` 转写音频
- 将转写文本转交给 OpenClaw
- 部署一个用于语音桥接的 macOS `launchd` 服务
- 增加 `oc-voice-*` 系列 shell alias 方便管理
- 关闭 OpenClaw 原生的音频附件预处理，避免与桥接流程抢占处理

## 可信信号

- `skill-vetter reviewed`：按 skill-vetter 的思路检查过明显红旗、权限范围和可疑安装行为
- `quick_validate passed`：skill 结构已通过 OpenClaw skill 校验
- `install smoke-tested`：安装脚本已经在临时 OpenClaw 目录里跑过，确认会正确生成文件、改配置并产出 launchd 相关文件

这些标识表示“已审查、已冒烟验证”，不表示“官方 OpenClaw 发行版”或“在所有机器上零差异可用”。

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
- 定位：社区 skill，不是官方 OpenClaw 发布物
