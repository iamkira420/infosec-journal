### 🎧 Fixing Spotify Web Playback on Brave (Fedora KDE)

**Date:** 2025-05-14
**Category:** Troubleshooting
**Tags:** `Brave`, `Spotify`, `Fedora`, `Flatpak`, `Widevine`, `DRM`

---

#### 🐞 Problem

After logging into the Spotify Web Player on Brave (running Fedora KDE), I encountered the following error:

> **"Playback of protected content is not enabled. Visit Spotify Support to learn how to enable playback in your browser."**

Even after enabling all related settings in Brave:

* Protected content (`brave://settings/content/protectedContent`)
* Widevine support (`brave://settings/extensions`)
* Shields disabled
* User-agent spoofing and fingerprinting turned off

…the issue persisted.

---

#### 🔍 Root Cause

Brave on **Linux distributions (like Fedora)** does **not always ship with Widevine DRM** enabled by default — due to licensing restrictions. This means **DRM-protected services like Spotify** will not work out of the box in the browser.

---

#### ✅ Solution: Use the Native Spotify Client via Flatpak

Instead of wrestling with browser DRM on Linux, I opted for a cleaner fix — **installing the native Spotify client using Flatpak**:

##### 1. Enable RPM Fusion (if not already):

```bash
sudo dnf install \
  https://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm \
  https://download1.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm
```

##### 2. Ensure Flatpak is installed:

```bash
sudo dnf install flatpak
```

##### 3. Add the Flathub repository:

```bash
flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
```

##### 4. Install Spotify:

```bash
flatpak install flathub com.spotify.Client
```

##### 5. Launch Spotify:

```bash
flatpak run com.spotify.Client
```

---

#### 📝 Reflection

Sometimes the best fix is avoiding a brittle path. Troubleshooting Brave’s DRM on Linux can be time-consuming and inconsistent — switching to the Flatpak version of Spotify provides a stable, no-hassle solution.

