# SoulDub AI Video Translation Skill for AI Agents [![Security: B — Skills Directory](https://www.skillsdirectory.com/api/skills/gravityvortex-souldub-video-translate/badge)](https://www.skillsdirectory.com/skills/gravityvortex-souldub-video-translate)

[English](README.md) | [简体中文](README.zh-CN.md) | [Español](README.es.md) | [ไทย](README.th.md)

<p align="center">
  <img src="cover-readme.png" alt="SoulDub AI video translation skill cover" width="760">
</p>

Translate local MP4 videos with SoulDub AI video translation and original-voice dubbing, then download the translated video, target-language subtitles, and bilingual SRT subtitles.

This repository publishes the `souldub-video-translate` Agent Skill.

Use it when you want an agent to localize an MP4 video, dub a video into another language, translate video subtitles, or generate bilingual subtitles for review.

## What It Does

The skill helps an agent:

- Upload a local `.mp4` video to SoulDub.
- Create a video translation task.
- Track long-running translation progress.
- Download the AI-dubbed translated video and SRT subtitles.

Successful runs save:

- `result.mp4`: translated video
- `translated.srt`: target-language subtitles
- `bilingual.srt`: bilingual subtitles

## Install

Install from the public GitHub repository:

```bash
npx skills add jiabaogithub/souldub-skills --skill souldub-video-translate
```

## Use

After installing, ask your agent to use the skill with a local MP4 path and a target language:

```text
Use the souldub-video-translate skill to translate C:\path\to\video.mp4 into Japanese.
```

Other example prompts:

```text
Use the souldub-video-translate skill to AI dub this MP4 into Chinese.
Use the souldub-video-translate skill to localize this video and generate bilingual subtitles.
```

The skill also accepts supported language names such as `Japanese`, `Chinese`, `日语`, `中文`, and `粤语`.

The agent will collect any missing details, start the translation, report progress, and return the local output paths when the job completes.

## Configure

The skill requires a SoulDub API key.

After installing, ask your agent to check authentication:

```bash
uv run scripts/video_translation.py auth status
```

If no API key is configured, the skill creates this user-level config file:

```text
~/.souldub/souldub.config.yaml
```

Set `souldub_api_key` in that file, or set the `SOULDUB_API_KEY` environment variable.

## Requirements

- Python 3.11+
- `uv`
- Network access to the SoulDub Agent API
- A SoulDub API key
- Read access to the source MP4 file
- Write access to the output directory

## Runtime Data and Safety

Installed skill files are treated as read-only.

Runtime state is stored in the user's platform state directory. Translated outputs default to a `souldub_outputs/` folder next to the source video.

The skill does not persist API keys, presigned upload URLs, media gateway URLs, or temporary signature parameters.

## Development

Repository layout:

```text
skills/
└── souldub-video-translate/
```

From this repository root, verify local discovery:

```bash
npx skills add . --list
```

Install the local working copy:

```bash
npx skills add . --skill souldub-video-translate
```

Run the helper directly for local debugging:

```bash
cd skills/souldub-video-translate
uv run scripts/video_translation.py auth status
```

