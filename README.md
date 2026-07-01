# 🎨 NeXuS-mutagen-musl

> **matugen** — Material You color palette generator, pre-built for **Alpine Linux** and all **musl libc** systems.

No Rust toolchain needed. Download, chmod, run.

---

## 🔥 What is matugen?

[matugen](https://github.com/InioX/matugen) generates dynamic **Material You** color schemes from any wallpaper image. It follows Google's Material Design 3 color theory — extracting a dominant color from your wallpaper and deriving a full palette of harmonious tones for your entire desktop.

Used by the **NeXuS Desktop** to keep waybar, terminals, app themes, and shell colors in sync with the current wallpaper — automatically.

---

## 📦 Why this release?

The upstream matugen releases are built against **glibc**. They do **not** work on:

- 🐧 **Alpine Linux**
- 🐳 musl-based Docker containers
- 📦 Void Linux (musl variant)
- 🔒 Any hardened system using musl libc

This binary is compiled from source and dynamically linked against **musl libc** — ready to drop into any musl system.

---

## ⚡ Quick Install

```bash
# Download the binary
curl -LO https://github.com/hackenstacks/NeXuS-mutagen-musl/releases/latest/download/matugen

# Make executable
chmod +x matugen

# Move to PATH
doas mv matugen /usr/local/bin/
# or: mv matugen ~/.local/bin/

# Verify
matugen --version
```

---

## 🚀 Usage

### Generate a color scheme from a wallpaper

```bash
matugen image /path/to/wallpaper.jpg
```

### Output formats

```bash
# JSON — full palette
matugen image wallpaper.jpg --json

# Specific format
matugen image wallpaper.jpg --format hex
matugen image wallpaper.jpg --format rgb
matugen image wallpaper.jpg --format hsl
```

### Use with templates

matugen supports **Tera templates** to auto-generate config files for any application.

```bash
# Apply templates defined in config
matugen image wallpaper.jpg --config ~/.config/matugen/config.toml
```

### Color modes

```bash
# Dark scheme (default)
matugen image wallpaper.jpg --type dark

# Light scheme
matugen image wallpaper.jpg --type light

# Amoled (pure black backgrounds)
matugen image wallpaper.jpg --type amoled
```

### Pipe wallpaper from another command

```bash
# Use current wallpaper from swww
matugen image "$(swww query | awk -F': ' '{print $2}')"
```

---

## 🗂️ Template Setup (recommended)

Create `~/.config/matugen/config.toml`:

```toml
[config]
reload_apps = true

[templates.waybar]
input_path = "~/.config/waybar/colors.css.templ"
output_path = "~/.config/waybar/colors.css"

[templates.foot]
input_path = "~/.config/foot/colors.ini.templ"
output_path = "~/.config/foot/colors.ini"
```

### Example template (`colors.css.templ`)

```css
@define-color primary {{colors.primary.default.hex}};
@define-color surface {{colors.surface.default.hex}};
@define-color on_surface {{colors.on_surface.default.hex}};
@define-color secondary {{colors.secondary.default.hex}};
```

---

## 🔄 Auto-run on wallpaper change

### With swww

```bash
# In your wallpaper script
swww img "$wallpaper" && matugen image "$wallpaper"
```

### With hyprpaper / wpaperd

Add `matugen image "$wallpaper"` after setting the wallpaper in your startup script.

---

## 📋 Full Help

```
matugen --help
```

```
matugen image --help
```

---

## 🖥️ System Info

| Field | Value |
|-------|-------|
| Binary | `matugen` |
| Version | `4.1.0` |
| Arch | `x86_64` |
| Libc | `musl` |
| Built on | Alpine Linux |
| Size | ~8.6MB |

---

## 🔗 Links

- 📖 [matugen upstream](https://github.com/InioX/matugen)
- 🌐 [NeXuS Project](https://github.com/hackenstacks)
- 📦 [matugen docs & templates](https://github.com/InioX/matugen/wiki)

---

## ⚖️ License

matugen is licensed under **GPL-2.0**. This repository distributes a pre-compiled binary for convenience. All credit to [@InioX](https://github.com/InioX).

---

*Part of the **NeXuS** ecosystem — Sane • Simple • Secure • Stealthy • Beautiful*
