# tmux config

Minimal tmux setup: pane splits, Alt+hjkl navigation, mouse support, and copy mode.
Optional upgrade: tmux-which-key plugin with Alt+Space menu.

---

## Install tmux

**macOS**
```sh
brew install tmux
```

**Ubuntu / Debian**
```sh
sudo apt install tmux
```

**Fedora / RHEL**
```sh
sudo dnf install tmux
```

---

## Setup

### 1. Back up any existing config

```sh
[ -f ~/.tmux.conf ] && cp ~/.tmux.conf ~/.tmux.conf.bak
```

### 2. Copy the config

```sh
cp .tmux.conf ~/.tmux.conf
```

### 3. Reload tmux

If tmux is already running:

```sh
tmux source ~/.tmux.conf
```

Otherwise just open a new tmux session — the config loads automatically.

---

## Bindings

### Splits

| Key | Action |
|-----|--------|
| `Ctrl+b \|` | Split vertically (side by side) |
| `Ctrl+b -` | Split horizontally (top/bottom) |
| `Alt+\|` | Split vertically (no prefix) |
| `Alt+-` | Split horizontally (no prefix) |

`Ctrl+b` is the default tmux prefix.

### Pane navigation

No prefix needed — just hold Alt and press a direction.

| Key | Action |
|-----|--------|
| `Alt+h` | Move to pane on the left |
| `Alt+j` | Move to pane below |
| `Alt+k` | Move to pane above |
| `Alt+l` | Move to pane on the right |

### Scrolling and copy

Mouse scroll works out of the box. Scrolling up automatically enters copy mode so you can read through past output.

To copy with the mouse: click and drag to select text, then use your terminal's copy shortcut (`Cmd+C` on macOS).

To copy with the keyboard:

| Key | Action |
|-----|--------|
| `Ctrl+b [` | Enter copy mode |
| `hjkl` | Move cursor |
| `Ctrl+u` / `Ctrl+d` | Scroll half page up/down |
| `v` | Start selection |
| `y` | Copy selection to clipboard and exit |
| `q` | Exit copy mode without copying |

> **Linux:** The config uses `pbcopy` (macOS clipboard). Open `.tmux.conf` and replace
> `pbcopy` with `xclip -selection clipboard` or `xsel --clipboard --input` in the
> two `copy-pipe-and-cancel` lines.

---

## Optional upgrade: tmux-which-key

This adds a searchable popup menu of all keybindings, opened with `Alt+Space`. Useful while you're still learning the shortcuts.

### 1. Install TPM (tmux plugin manager)

```sh
git clone https://github.com/tmux-plugins/tpm ~/.tmux/plugins/tpm
```

### 2. Uncomment the plugin section in `~/.tmux.conf`

Find the `── Plugins (optional upgrade)` section near the bottom of the file.
Uncomment these four lines (remove the leading `#`):

```
# set -g @plugin 'tmux-plugins/tpm'
# set -g @plugin 'alexwforsythe/tmux-which-key'
# bind -n M-Space run-shell "~/.tmux/plugins/tmux-which-key/scripts/show.sh"
#
# run '~/.tmux/plugins/tpm/tpm'
```

After uncommenting, the section should look like:

```
set -g @plugin 'tmux-plugins/tpm'
set -g @plugin 'alexwforsythe/tmux-which-key'
bind -n M-Space run-shell "~/.tmux/plugins/tmux-which-key/scripts/show.sh"

run '~/.tmux/plugins/tpm/tpm'
```

### 3. Reload the config and install plugins

```sh
tmux source ~/.tmux.conf
```

Then inside tmux, press `Ctrl+b I` (capital I) to install the plugins.
Wait for the install to finish — a confirmation message will appear at the bottom.

### 4. Use it

Press `Alt+Space` to open the which-key menu. You can search by typing.
