![Python](https://img.shields.io/badge/Python-3.10+-blue.svg)
![License](https://img.shields.io/badge/License-MIT-green.svg)
![Platform](https://img.shields.io/badge/Platform-Windows%20%7C%20macOS%20%7C%20Linux-lightgrey.svg)
![Version](https://img.shields.io/badge/Version-0.0.2-orange.svg)
[![Download](https://img.shields.io/badge/Download_Installer-darkgreen.svg)](https://github.com/TsvetanG2/InstagramPostScrapper/raw/refs/heads/main/dist_installer/InstagramPostScrapperSetup_0.0.2v.exe)

# Latest Update 0.0.2v:
- New method _is_challenge_page() — more reliable recognition of captcha/challenge pages through URL checks + DOM selectors (instead of simply searching the page source)
- Human-like scrolling — instead of directly scrolling to the bottom:
- Scrolls in random steps (50-90% of viewport)
- Sometimes scrolls up (simulates reading)
- Random pauses between 2-5 seconds
- Better detection of profile end — 5 retries with scroll up/down before stopping (instead of 1 attempt)
- Challenge detection when scrolling — check every 10 scrolls for rate limit
- Improved carousel retry — additional retry for duplicate URL + skip if the slide is blocked
- Longer initial waits — 4-7s when opening a profile (was 3-5s)

---

# InstagramWrapperPostScraper

A Selenium-based wrapper for downloading photos and videos from public Instagram profiles. Drives a real Microsoft Edge browser to mimic human behavior — bypassing rate limits more reliably than API or plain HTTP scraping approaches.

>  **Disclaimer:** Use responsibly and in accordance with [Instagram's Terms of Service](https://help.instagram.com/581066165581870) and applicable laws. This tool is intended for personal and research use only.

## Method: Selenium + Edge (recommended)

**File:** `scraper_selenium.py`

### Prerequisites
- Python 3.10+
- Microsoft Edge installed
- On Linux, you may need the `python3-tk` package for the GUI (tkinter is not always included by default).

---

### Advantages
- Bypasses common Instagram rate limits more reliably than API-based approaches
- Harder to detect than simple HTTP scraping (uses a real browser)
- Can keep working even after temporary 429/rate-limit blocks
- You can see what the browser is doing (or run headless)
- Uses Microsoft Edge (no ChromeDriver required if Edge WebDriver is available on your system)

---

## Output structure

```
downloads/
└── username/
    ├── images/
    │   ├── post_1/
    │   │   ├── username_1.jpg
    │   │   └── description.txt
    │   ├── post_2/
    │   │   ├── username_2_01.jpg   ← carousel slide 1
    │   │   ├── username_2_02.jpg   ← carousel slide 2
    │   │   └── description.txt
    └── videos/
        └── post_3/
            ├── username_3.mp4
            └── description.txt
```

---

## Usage notes
- Instagram changes often. If something breaks, update Selenium/Edge and retry.
- If you want headless mode, enable it in the script (search for `headless` options).

---

## Known limitations
- **Public profiles only** — private profiles require the scraper account to be a follower
- **Edge only** — currently does not support Chrome or Firefox
- **Instagram UI changes** — if selectors break after an IG update, update Selenium/Edge and retry
- **Rate limits still apply** — for very large profiles (1000+ posts), expect pauses and retries
- **No proxy support** — all requests come from your real IP

---

## Troubleshooting

**`SessionNotCreatedException` or Edge not found**
→ Make sure Microsoft Edge is installed. The msedgedriver version must match your Edge version. Update Edge or run `winget upgrade Microsoft.Edge`.

**Stuck on login / challenge page**
→ Instagram may have flagged the session. Wait 30–60 minutes and try again. Avoid running multiple sessions simultaneously.

**No images found on profile**
→ The profile may be private, or Instagram changed its DOM structure. Check for a new version of this tool.

**Linux: `_tkinter` import error**
→ Run `sudo apt install python3-tk` and retry.

---
### v0.0.1
- Initial release

## Contributing

Contributions are welcome! Feel free to open an issue or submit a pull request.

If Instagram breaks something (it happens), please include:
- The error message or log output
- Your Edge and Selenium versions (`msedge --version`, `pip show selenium`)

---

License
MIT — see LICENSE.md
