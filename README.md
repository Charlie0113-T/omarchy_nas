> [!IMPORTANT]
> **This repository has moved to [Charlie0113-T/omarchy-nas](https://github.com/Charlie0113-T/omarchy-nas)**, which now holds the bar plugin and omarchy-nas together. This copy is archived and gets no updates. Install the plugin from the new home:
>
> ```sh
> omarchy plugin remove io.github.charlie0113-t.omarchy-nas --yes
> omarchy plugin add https://github.com/Charlie0113-T/omarchy-nas.git --enable
> ```
>
> 本仓库已迁移到 [Charlie0113-T/omarchy-nas](https://github.com/Charlie0113-T/omarchy-nas)，顶栏插件和 omarchy-nas 都在那里；这里已归档，不再更新。

> **Note:** I'm still a student, so I may not be able to respond to issues or ship updates right away. I'll keep maintaining this project in my spare time as best I can.

<div align="center">

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="assets/omarchy-logo-dark.svg">
  <img src="assets/omarchy-logo.svg" alt="Omarchy" width="360">
</picture>

# Omarchy NAS

**Your omarchy-nas shares in the Omarchy bar: online, paused or offline at a glance**

Omarchy 4 bar plugin · Pause, resume and diagnostics one click away · Never runs `sudo` in the background

![version](https://img.shields.io/badge/version-0.1.0-2ea44f)
![platform](https://img.shields.io/badge/platform-Omarchy%204-1793D1?logo=archlinux&logoColor=white)
![built with](https://img.shields.io/badge/built%20with-QML%20%2F%20Quickshell-41CD52?logo=qt&logoColor=white)
![license](https://img.shields.io/badge/license-AGPL--3.0-blue)

**English** · [简体中文](#中文)

</div>

---

An [Omarchy](https://github.com/omacom/omarchy) 4 bar plugin for the machine that runs [omarchy-nas](https://github.com/Charlie0113-T/omarchy-nas). It shows which shares are online, paused or offline, and puts pause, resume and diagnostics one click away.

## At a glance

| Part | What it does |
| --- | --- |
| 💾 **Bar icon** | Colour shows the NAS state. Hover for a one-line summary ("NAS · 2/2 online"); right-click to refresh. |
| 📋 **Panel** | One row per share: state, name, size, file system and mode, or why it is offline. |
| ⏯️ **Actions** | Pause or resume a share, renew the gateway certificate, open the status page, run diagnostics. |
| ⌨️ **Keys** | Drive the whole panel from the keyboard. |
| 🌐 **Languages** | 简体中文, 繁體中文 and English, following Omarchy's language setting. |

## Requirements

- Omarchy 4: the desktop runs as omarchy-shell, which has the plugin system.
- omarchy-nas set up on the same machine (`omarchy-nas setup`).
- `curl` and `wl-copy`, which come with Omarchy.

> [!NOTE]
> The plugin shows this machine's NAS only. It doesn't browse shares from other computers.

## 📦 Install

```sh
omarchy plugin add https://github.com/Charlie0113-T/omarchy_nas.git --enable
```

The icon lands on the right of the bar.

### Update and remove

```sh
omarchy plugin update io.github.charlie0113-t.omarchy-nas
omarchy plugin remove io.github.charlie0113-t.omarchy-nas
```

## 🧩 What you see

### The bar icon

| Icon | Meaning |
| --- | --- |
| Normal colour | Everything is fine. |
| Urgent colour | A share is offline, the service is down, omarchy-nas reports an error, or the file gateway's certificate has 14 days or fewer. |
| Faded | No status has arrived yet, or omarchy-nas isn't installed or set up. |

### The panel

- Click a share to copy its `smb://` address; its icon turns into a check.
- The button at the end of the row pauses or resumes that share.
- With under 30 days left on the gateway certificate, a row offers to renew it.
- The footer opens the local status page or runs diagnostics.

### Keys

| Key | Action |
| :---: | --- |
| `↑` `↓` | Pick a share |
| `Enter` | Copy its `smb://` address |
| `p` | Pause or resume it |
| `r` | Refresh |
| `s` | Open the status page |
| `Esc` | Close the panel |

## 🔒 Safety

- The plugin only reads status, and never with sudo. It asks the local status page (`http://127.0.0.1:8787/api/status`) and, when that isn't running, runs `omarchy-nas status`.
- Only share names omarchy-nas itself accepts (a lowercase letter, then letters, digits, `-` or `_`) ever reach a command line.

> [!IMPORTANT]
> Actions that need root (pause, resume, renew) open a terminal that shows the full command, where you type your own password. **Nothing runs in the background.**

## ⚙️ Settings

Settings sit inline on the widget's entry in `~/.config/omarchy/shell.json`, for example:

```json
{ "id": "io.github.charlie0113-t.omarchy-nas", "refreshIntervalSec": 120 }
```

| Key | Default | Range | What it does |
| --- | :---: | :---: | --- |
| `refreshIntervalSec` | 60 | 15–3600 | How often to read the status. Opening the panel always refreshes. |
| `statusPort` | 8787 | 1024–65535 | Port of the local omarchy-nas status page. |

## 🛠️ Development

```text
omarchy_nas/
├── manifest.json        # plugin id, entry point and settings schema
├── Widget.qml           # bar icon and panel
├── Status.qml           # reads the status page, or falls back to omarchy-nas status
├── Model.js             # status logic, texts and commands (no QML, testable in Node)
└── tests/
    └── model.test.mjs
```

```sh
omarchy plugin validate .            # Omarchy's own manifest checks
node --test tests/model.test.mjs     # status logic, texts and commands
```

> [!TIP]
> omarchy-shell reloads an installed plugin when one of its files is saved.

## License

Released under the [GNU Affero General Public License v3.0](LICENSE), like omarchy-nas. Copyright © 2026 Charles Tao.

The Omarchy logo comes from [omacom/omarchy](https://github.com/omacom/omarchy) under the [MIT license](assets/LICENSE). This is a community tool and is not affiliated with Omarchy.

---

## 中文

> **说明：** 我目前还是学生，可能没法及时处理问题或更新，但会在空闲时间尽力维护这个项目。

在运行 omarchy-nas 的那台 Omarchy 电脑上，把 NAS 的状态放进顶栏。

### 需要

Omarchy 4，并且同一台电脑上已经用 `omarchy-nas setup` 设置好 NAS。插件只看本机。用到的 `curl` 和 `wl-copy` 是 Omarchy 自带的。

### 📦 安装

```sh
omarchy plugin add https://github.com/Charlie0113-T/omarchy_nas.git --enable
```

图标在顶栏右侧。更新：`omarchy plugin update io.github.charlie0113-t.omarchy-nas`；卸载：`omarchy plugin remove io.github.charlie0113-t.omarchy-nas`。

### 🧩 看到什么

- **图标颜色**：一切正常是普通颜色。有共享离线、服务没运行、出错，或网关证书只剩 14 天以内，变成警示色。还没读到状态、没安装或没设置时颜色变淡。
- **悬停和右键**：鼠标停在图标上显示一行摘要，右键立即刷新。
- **面板**：
  - 每个共享一行，写着容量、文件系统、只读还是可读写；离线时写原因。点一行复制 `smb://` 地址。
  - 行尾按钮暂停或继续这个共享。
  - 证书剩不到 30 天时有续期按钮。底部打开状态页、运行诊断。

| 按键 | 作用 |
| :---: | --- |
| `↑` `↓` | 选共享 |
| `Enter` | 复制 `smb://` 地址 |
| `p` | 暂停/继续 |
| `r` | 刷新 |
| `s` | 打开状态页 |
| `Esc` | 关闭 |

### 🔒 安全

- 插件读状态从不用 sudo。

> [!IMPORTANT]
> 需要 root 的操作会打开终端显示完整命令，由你自己输入密码。
