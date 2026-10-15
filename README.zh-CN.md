# SoulDub AI Video Translation Skill for AI Agents [![Security: B — Skills Directory](https://www.skillsdirectory.com/api/skills/gravityvortex-souldub-video-translate/badge)](https://www.skillsdirectory.com/skills/gravityvortex-souldub-video-translate)

[English](README.md) | [简体中文](README.zh-CN.md) | [Español](README.es.md) | [ไทย](README.th.md)

<p align="center">
  <img src="cover-readme.png" alt="SoulDub AI video translation skill cover" width="760">
</p>

使用 SoulDub AI 视频翻译和原声配音，将本地 MP4 视频翻译成其他语言，然后下载译制视频、目标语言字幕和双语 SRT 字幕。

本仓库发布 `souldub-video-translate` Agent Skill。

当你希望让 AI Agent 本地化 MP4 视频、为视频配音、翻译视频字幕或生成双语字幕供审核时，可以使用此 Skill。

## 功能

此 Skill 可以帮助 Agent：

- 将本地 `.mp4` 视频上传到 SoulDub。
- 创建视频翻译任务。
- 跟踪长时间运行的翻译进度。
- 下载 AI 配音译制视频和 SRT 字幕。

成功运行后会生成：

- `result.mp4`：译制后的视频
- `translated.srt`：目标语言字幕
- `bilingual.srt`：双语字幕

## 安装

从公开 GitHub 仓库安装：

```bash
npx skills add jiabaogithub/souldub-skills --skill souldub-video-translate
```

## 使用

安装后，向 Agent 提供本地 MP4 路径和目标语言：

```text
使用 souldub-video-translate skill，将 C:\path\to\video.mp4 翻译成日语。
```

其他示例：

```text
使用 souldub-video-translate skill，将这个 MP4 配音成中文。
使用 souldub-video-translate skill，本地化这个视频并生成双语字幕。
```

Skill 支持多种语言名称，例如 `Japanese`、`Chinese`、`日语`、`中文` 和 `粤语`。

Agent 会收集缺少的信息、启动翻译、报告进度，并在任务完成后返回本地输出文件路径。

## 配置

此 Skill 需要 SoulDub API 密钥。

安装后，向 Agent 请求检查认证状态：

```bash
uv run scripts/video_translation.py auth status
```

如果尚未配置 API 密钥，Skill 会创建以下用户级配置文件：

```text
~/.souldub/souldub.config.yaml
```

在该文件中设置 `souldub_api_key`，或设置 `SOULDUB_API_KEY` 环境变量。

## 环境要求

- Python 3.11+
- `uv`
- 可访问 SoulDub Agent API 的网络
- SoulDub API 密钥
- 读取源 MP4 文件的权限
- 输出目录的写入权限

## 运行数据与安全

已安装的 Skill 文件按只读方式处理。

运行时状态保存在用户平台状态目录中。译制结果默认保存到源视频旁边的 `souldub_outputs/` 文件夹。

Skill 不会持久化 API 密钥、预签名上传 URL、媒体网关 URL 或临时签名参数。

## 开发

仓库结构：

```text
skills/
└── souldub-video-translate/
```

在仓库根目录验证本地发现：

```bash
npx skills add . --list
```

安装本地工作副本：

```bash
npx skills add . --skill souldub-video-translate
```

直接运行辅助脚本进行本地调试：

```bash
cd skills/souldub-video-translate
uv run scripts/video_translation.py auth status
```
