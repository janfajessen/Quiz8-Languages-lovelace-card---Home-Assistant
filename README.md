
<div align="center">

# Quiz8 Languages — Lovelace Card
## Home Assistant

<img src="https://github.com/janfajessen/Quiz8-Languages---Home-Assistant/blob/c52439777b326e7db3e634f40903392aa059f3ba/custom_components/quiz8_languages/brand/icon%402x.png" width="25%"/>

![Version](https://img.shields.io/badge/version-1.5.28-blue?style=for-the-badge)
![HA](https://img.shields.io/badge/Home%20Assistant-2024.1+-orange?style=for-the-badge&logo=home-assistant)
![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)
![Python](https://img.shields.io/badge/Python-3.12+-3776AB?style=for-the-badge&logo=python)
![HACS](https://img.shields.io/badge/HACS-Custom-41BDF5?style=for-the-badge&logo=homeassistantcommunitystore&logoColor=white)
[![Buy Me A Coffee](https://img.shields.io/badge/Buy%20Me%20A%20Coffee-Donate-yellow?style=for-the-badge&logo=buymeacoffee)](https://www.buymeacoffee.com/janfajessen)
[![Patreon](https://img.shields.io/badge/Patreon-Support-red?style=for-the-badge&logo=patreon)](https://www.patreon.com/janfajessen)
<!--[![Ko-Fi](https://img.shields.io/badge/Ko--Fi-Support-teal?style=for-the-badge&logo=ko-fi)](https://ko-fi.com/janfajessen)
[![GitHub Sponsors](https://img.shields.io/badge/GitHub%20Sponsors-Support-pink?style=for-the-badge&logo=githubsponsors)](https://github.com/sponsors/janfajessen)


[![PayPal](https://img.shields.io/badge/PayPal-Donate-blue?style=for-the-badge&logo=paypal)](https://paypal.me/janfajessen)-->

A Lovelace card for the [Quiz8 Languages](https://github.com/janfajessen/Quiz8-Languages---Home-Assistant) integration. Match words to their translations across 8 languages in a pairing game, directly from your Home Assistant dashboard.

</div>


---

## Features

- **Pairing Cards matching** — tap a word on the left or right, tap its translation on the other side
- **8 language tabs** — visual overview with round progress dots per language
- **Free navigation** — jump to any incomplete language at any time
- **Progress saved** — mid-round progress is preserved when switching languages
- **3 rounds × 8 pairs** — 24 word pairs per language loaded in one shot, no loading between rounds
- **Dark neon aesthetic** — consistent with the Quiz8 trivia card style
- **49 UI languages** — card interface adapts to your Home Assistant language setting
- **Transliteration support** — shown below words for non-Latin scripts (Japanese, Cyrillic, Arabic…)
- **Streak & score** — live display of daily streak and session score in the header
- **No WebSocket events** — reads data directly from sensor attributes, works in all contexts (browser, app, tablet)
- **100 words in A1 and working on** — There are currently at least 100 words at the A1 level in all 28 languages. There is future work to be done with artificial inteligence :)

---

## Requirements

- [Quiz8 Languages integration](https://github.com/janfajessen/Quiz8-Languages---Home-Assistant) installed and configured
- Home Assistant 2024.1 or later

---

## Installation

### Manual

1. Download `quiz8-languages-card.js` from the [latest release](https://github.com/janfajessen/Quiz8-Languages-lovelace-card---Home-Assistant/releases).

2. Copy it to `/config/www/quiz8-languages-card.js`.

3. Add it as a resource in your dashboard:

   **Settings → Dashboards → ⋮ → Manage resources → Add resource**

   ```
   URL: /local/quiz8-languages-card.js
   Type: JavaScript module
   ```

4. Add the card to a dashboard view.

### HACS (coming soon)

Add `https://github.com/janfajessen/Quiz8-Languages-lovelace-card---Home-Assistant` as a custom repository in HACS (category: Lovelace).

---

## Card Configuration

```yaml
type: custom:quiz8-languages-card
```

No additional configuration required — the card reads everything from the integration sensors automatically.

---

## Adding Your Logo and Flags

Open `quiz8-languages-card.js` and paste your base64 strings at the top of the file:

```javascript
// Logo for the card header (any square image works well)
const LOGO_B64 = 'iVBORw0KGgo...'; // your base64 string here

// Regional language flags (optional — emoji fallback used if empty)
const FLAG_CA_B64 = ''; // Catalunya
const FLAG_EU_B64 = ''; // País Vasco
const FLAG_GL_B64 = ''; // Galicia
```

To convert an image to base64:
- Use any online base64 encoder
- Or in terminal: `base64 -i your-image.png | tr -d '\n'`

Paste the result (without the `data:image/png;base64,` prefix) between the quotes.

---

## How to Play

1. The card loads 24 word pairs (3 rounds × 8) for the first language automatically.
2. Tap a word on the **left column** (language you are learning).
3. Tap its translation on the **right column** (your Home Assistant UI language).
4. A correct match turns green and disappears. A wrong match flashes red — try again.
5. Complete all 8 pairs to advance to the next round automatically.
6. After 3 rounds the language is marked complete (green tab) and the next one starts.
7. Use the **language tabs** at the top to jump to any incomplete language at any time — your progress is saved.
8. Finish all 8 languages to see your final score.

---

## Scoring

| Situation | Points |
|-----------|--------|
| Correct answer, word mastery 0 | 10 pts |
| Correct answer, word mastery 5 | 5 pts |
| Correct answer, word mastery 9 | 1 pt |
| Wrong answer | 0 pts, mastery reduced |

Lower-mastery words are worth more — struggling words give higher rewards when you finally get them right.

---

## UI Languages

The card interface automatically adapts to your Home Assistant language. Supported languages:

`af` `ar` `bg` `bn` `ca` `cs` `cy` `da` `de` `de-CH` `el` `en` `es` `et` `eu` `fa` `fi` `fr` `ga` `gl` `gu` `he` `hi` `hr` `hu` `hy` `id` `is` `it` `ja` `ka` `kn` `ko` `kw` `lb` `lt` `lv` `ml` `mn` `ms` `nb` `nl` `pl` `pt` `ro` `ru` `sk` `sl` `sr` `sv` `ta` `te` `th` `tr` `uk` `ur` `vi` `zh-Hans` `zh-Hant`

Falls back to English for any unsupported language.

---

## Sensor Dependencies

The card reads from these sensors provided by the integration:

| Sensor | Used for |
|--------|----------|
| `sensor.quiz8_languages_language_rounds` | Word pairs for the current language (all 3 rounds) |
| `sensor.quiz8_languages_active_language` | Active language code and list of selected languages |
| `sensor.quiz8_languages_daily_streak` | Streak displayed in the header |

---

## Troubleshooting

**Card shows "No data"**
- Make sure the Quiz8 Languages integration is installed and configured.
- Check that `sensor.quiz8_languages_active_language` has a value other than `unknown` in Developer Tools → States.
- Try reloading the page — the sensor may not have updated yet on first boot.

**Spinner keeps spinning after switching languages**
- Tap any other language tab and then return — this forces a sensor refresh.
- If it persists, call `quiz8_languages.set_active_language` manually from Developer Tools → Services.

**Words from old configuration still showing**
- The card detects language changes automatically and resets local state. If it does not, clear the browser cache (Ctrl+Shift+R) to force a fresh load.

**Score always shows 0**
- The score displayed in the card header is the local session total, calculated client-side. The integration score sensor (`sensor.quiz8_languages_session_score`) is updated by `register_answer` service calls and may differ slightly due to the integration's mastery-weighted scoring.

---

## Links

- **Integration:** [Quiz8 Languages Integration](https://github.com/janfajessen/Quiz8-Languages---Home-Assistant)
- **Issues:** [GitHub Issues](https://github.com/janfajessen/Quiz8-Languages-lovelace-card---Home-Assistant/issues)

---


*If this integration or card is useful to you, consider giving it a ⭐ on GitHub.*
Or consider supporting development!

[![Buy Me A Coffee](https://img.shields.io/badge/Buy%20Me%20A%20Coffee-Donate-yellow?style=for-the-badge&logo=buymeacoffee)
](https://www.buymeacoffee.com/janfajessen) 
[![Patreon](https://img.shields.io/badge/Patreon-Support-red?style=for-the-badge&logo=patreon)](https://www.patreon.com/janfajessen)
</div>


## License


MIT License — see [LICENSE](LICENSE) for details.


© [@janfajessen](https://github.com/janfajessen)
