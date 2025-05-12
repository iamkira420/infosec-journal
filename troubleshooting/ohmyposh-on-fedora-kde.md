## 🧠 Setting Up Oh My Posh on Fedora KDE (w/ Nerd Fonts Fix)

**Date**: May 12, 2025
**Tags**: Linux, Fedora, KDE, Oh My Posh, Nerd Fonts, Terminal

### 🧩 Why Oh My Posh?

Oh My Posh brings a visually rich, customizable prompt to your shell. If you're using Fedora KDE and want that modern, glyph-powered terminal look, this is your quickstart guide.

---

### ✅ Installing Oh My Posh

Run the official installer script:

```bash
sudo curl -s https://ohmyposh.dev/install.sh | bash -s
```

Check it’s working:

```bash
oh-my-posh --version
```

---

### 🎨 Getting Nerd Fonts (Meslo)

1. **Download the font:**

```bash
mkdir -p ~/.local/share/fonts
cd ~/.local/share/fonts

# Recommended: full set
curl -fLo "MesloLGS NF Regular.ttf" https://github.com/ryanoasis/nerd-fonts/raw/master/patched-fonts/Meslo/L/Regular/MesloLGS%20NF%20Regular.ttf
curl -fLo "MesloLGS NF Bold.ttf" https://github.com/ryanoasis/nerd-fonts/raw/master/patched-fonts/Meslo/L/Bold/MesloLGS%20NF%20Bold.ttf
curl -fLo "MesloLGS NF Italic.ttf" https://github.com/ryanoasis/nerd-fonts/raw/master/patched-fonts/Meslo/L/Italic/MesloLGS%20NF%20Italic.ttf
curl -fLo "MesloLGS NF Bold Italic.ttf" https://github.com/ryanoasis/nerd-fonts/raw/master/patched-fonts/Meslo/L/Bold-Italic/MesloLGS%20NF%20Bold%20Italic.ttf
```

2. **Rebuild font cache**:

```bash
fc-cache -f -v
```

3. **⚠️ Font Not Showing in Konsole?**

If fonts were saved in subfolders (e.g. `Meslo/Regular/*.ttf`), move them:

```bash
find ~/.local/share/fonts -type f -name "*.ttf" -exec mv {} ~/.local/share/fonts/ \;
find ~/.local/share/fonts -type d -empty -delete
fc-cache -f -v
```

---

### 🖼️ Apply Nerd Font in Konsole

1. `Settings > Edit Current Profile > Appearance > Font`
2. Select **MesloLGS NF Regular**

---

### 🎛️ Configure Oh My Posh Theme

1. Download a theme:

```bash
mkdir -p ~/.poshthemes
curl -o ~/.poshthemes/paradox.omp.json https://raw.githubusercontent.com/JanDeDobbeleer/oh-my-posh/main/themes/paradox.omp.json
```

2. Update your shell config:

```bash
# For Bash
echo 'eval "$(oh-my-posh init bash --config ~/.poshthemes/paradox.omp.json)"' >> ~/.bashrc

# For Zsh
echo 'eval "$(oh-my-posh init zsh --config ~/.poshthemes/paradox.omp.json)"' >> ~/.zshrc
```

3. Reload your shell:

```bash
source ~/.bashrc   # or ~/.zshrc
```

---

### ✅ Done!

You now have a beautiful, functional terminal with glyphs, colors, and Git status indicators.
