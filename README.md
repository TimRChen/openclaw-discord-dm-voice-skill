# OpenClaw Discord DM Voice Skill

[English](./README.md) | [简体中文](./README.zh-CN.md)

Install Discord DM voice input for an existing OpenClaw home with local `faster-whisper` transcription.

This repository is also a valid OpenClaw skill repository. The skill entrypoint is [`SKILL.md`](./SKILL.md), and the repository root is the skill root.

## What It Does

- Receives Discord private voice messages
- Transcribes audio locally with `faster-whisper`
- Forwards the transcript into OpenClaw
- Deploys a macOS `launchd` service for the voice bridge
- Adds `oc-voice-*` shell aliases for lifecycle management
- Disables OpenClaw's native audio attachment preflight to avoid racing the bridge

## Repository Layout

```text
SKILL.md
agents/openai.yaml
scripts/install.py
assets/runtime/discord-dm-voice/
README.md
README.zh-CN.md
```

## Install

```bash
python3 scripts/install.py --openclaw-home ~/.openclaw
```

Optional flags:

- `--python /abs/path/to/python3`
- `--model base`
- `--language zh`
- `--skip-python-install`
- `--skip-npm-install`
- `--skip-deploy`

## Validate

```bash
oc-voice-status
oc-voice-logs
```

Then send a fresh voice message to the bot in a Discord DM.

## Notes

- Target platform: macOS with `launchd`
- Scope: Discord DM voice messages only
- Assumption: Discord is already configured in `~/.openclaw/openclaw.json`
