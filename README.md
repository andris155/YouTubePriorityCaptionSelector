# YouTube Priority Caption Selector

<p align="center">
  <strong>Intelligent, automated YouTube subtitle priority selector with auto-translate fallback</strong><br/><br/>
  <img src="https://img.shields.io/badge/Platform-YouTube-red" alt="Platform" />
  <img src="https://img.shields.io/badge/Userscript-Tampermonkey%20%7C%20Violentmonkey-green" alt="Userscript" />
  <img src="https://img.shields.io/badge/License-MIT-lightgrey" alt="License" />
  <img src="https://img.shields.io/badge/Made%20With-Vibecoding-purple" alt="Vibecoded" />
</p>

> **Note:** This is a vibecoded script (built and refined with AI assistance).

<p align="center">
  <a href="#overview">Overview</a> •
  <a href="#features">Features</a> •
  <a href="#requirements">Requirements</a> •
  <a href="#installation--updates">Installation</a> •
  <a href="#configuration--settings">Configuration</a> •
  <a href="#how-it-works--security">How It Works</a> •
  <a href="#author--license">License</a>
</p>

---

## Overview

**YouTube Priority Caption Selector** is an intelligent, lightweight Tampermonkey / Violentmonkey userscript for YouTube that automatically selects and activates subtitle tracks based on an ordered priority list, with auto-translate fallback and smart contextual controls.

---

## Features

- **Multi-Level Priority Rules:** Specify an ordered list of preferred subtitle languages. The script tests each rule in sequence and applies the first available match.
- **Manual vs. Automated Subtitle Distinction:** Match strictly human-crafted subtitles, automatic speech recognition (ASR), or allow either.
- **Auto-Translate Fallback:** When none of your preferred languages are available directly, automatically selects the best source track and requests YouTube's auto-translation into your chosen target language.
- **Smart Mute:** Automatically enables subtitles whenever volume is reduced to zero or the player is muted, and restores your previous subtitle preference as soon as volume is restored.
- **Native Audio Auto-Disable:** Automatically turns subtitles off if the video's original audio matches one of your native spoken languages.
- **Channel Filters:** Specify channel whitelists (always leave subtitles on) or blacklists (keep subtitles off).
- **Music & Shorts Controls:** Optionally turn subtitles off on official music videos, topic tracks, or YouTube Shorts.
- **Manual Override Respect:** If you manually toggle the CC button, press `C`, or change subtitle options via YouTube's menu, the script stands down for that video.
- **Built-in Settings GUI:** Open the in-page settings dashboard directly from your userscript extension menu to configure priority languages, switches, and channel rules without touching any code.
- **Automatic Light & Dark Mode:** The settings interface automatically adapts to YouTube's active appearance theme.
- **Persistent Across Updates:** Custom settings are saved to disk in extension storage (`GM_getValue`) so GitHub updates never overwrite your configuration.
- **Flicker-Free Navigation:** Seamlessly tracks YouTube's single-page app navigation without jarring UI flashes.

---

## Requirements

- A modern web browser (Chrome, Firefox, Edge, Safari, Brave, Opera)
- A userscript manager:
  - **[Tampermonkey](https://www.tampermonkey.net/)** (Recommended)
  - **[Violentmonkey](https://violentmonkey.github.io/)**

---

## Installation & Updates

1. Ensure your userscript manager is installed and enabled.
2. Click the direct raw install link:
   - **[Install YouTube Priority Caption Selector](https://raw.githubusercontent.com/andris155/YouTubePriorityCaptionSelector/main/YouTube%20Priority%20Caption%20Selector.user.js)**
3. Your userscript manager will open an installation tab — click **Install**.
4. The userscript includes `@updateURL` and `@downloadURL`, so future updates from GitHub are checked and installed automatically by your userscript manager.

---

## Configuration & Settings

Custom settings are saved in your userscript manager's persistent database (`GM_getValue`), meaning **future script updates from GitHub will never overwrite your custom settings!**

### Method 1: Extension Menu GUI (Recommended)

1. Open any video on [YouTube](https://www.youtube.com/).
2. Click the **Tampermonkey** or **Violentmonkey** extension icon in your browser toolbar.
3. Click **`⚙️ Edit Caption Settings`**:
   - Opens the visual configuration dashboard.
   - Reorder priority rules with `↑` and `↓`, edit language codes, or add new languages.
   - Toggle **Smart Mute**, **Native Language Auto-Disable**, **Shorts**, and **Music Video** options.
   - Automatically matches YouTube's active Light or Dark theme.
   - Click **Save & Apply** and the page refreshes with your updated settings.
4. To revert to defaults at any time, click **Reset Defaults**.

### Method 2: In-Code Default Settings

If you prefer editing code directly, you can customize `DEFAULT_CONFIG` near the top of the userscript file:

```javascript
const DEFAULT_CONFIG = {
    // 1. Language Priority List
    // Evaluated from top to bottom; activates the first match found.
    PRIORITY: [
        { lang: 'hu', autoGenerated: false, name: 'Hungarian (Manual)' },
        { lang: 'en', autoGenerated: false, name: 'English (Manual)' },
        { lang: 'hu', autoGenerated: true,  name: 'Hungarian (Auto-generated)' },
        { lang: 'en', autoGenerated: true,  name: 'English (Auto-generated)' }
    ],

    // 2. Auto-Translate Target
    // Language code to translate into if no priority track exists. Set to '' or null to disable.
    AUTO_TRANSLATE_TARGET: 'en',

    // 3. Smart Mute Trigger
    // Automatically enables subtitles while muted / at 0 volume, and turns them off when unmuted.
    SMART_MUTE: false,

    // 4. Native Spoken Language Auto-Disable
    // Automatically disables subtitles when the video's audio matches your native language.
    NATIVE_LANG_AUTO_DISABLE: {
        enabled: false,
        languages: ['hu']
    },

    // 5. Shorts & Music Auto-Disable
    DISABLE_ON_SHORTS: false,
    DISABLE_ON_MUSIC: false,

    // 6. Channel Whitelist & Blacklist
    CHANNEL_WHITELIST: {
        enabled: false,
        channels: ['@ExampleCreator']
    },
    CHANNEL_BLACKLIST: {
        enabled: false,
        channels: ['@AnotherChannel']
    },

    // 7. Manual Override Detection
    // Pauses automation for the current video if you toggle subtitles manually.
    RESPECT_MANUAL_OVERRIDE: true
};
```

---

## How It Works & Security

- **Strictly Local Execution:** Uses standard userscript grants (`GM_getValue`, `GM_setValue`, `GM_registerMenuCommand`, `unsafeWindow`) exclusively to persist your preferences across script updates and integrate the settings menu.
- **Trusted Types / CSP Compliant:** Completely free of `innerHTML` assignments to comply with YouTube's strict Content Security Policy.
- **Zero External Network Calls:** Operates entirely inside the local YouTube tab without contacting external servers or analytics.
- **No Data Collection:** Does not monitor, store, or transmit your watch history, search queries, or account credentials.

---

## Author & License

- **Author:** [andris155](https://github.com/andris155)
- **License:** [MIT License](https://opensource.org/licenses/MIT)
