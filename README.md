# 🗽 USCIS Case Status Tracker

A privacy-first, single-page web application that parses and visualizes USCIS ELIS API JSON data — transforming raw case records into a rich, human-readable timeline with intelligent event interpretation, progress tracking, and comprehensive case analysis.

> **100% client-side** — No servers, no databases, no data transmission. All processing happens entirely in your browser.

---

## ✨ Features

### 🔍 Case Data Parsing
- Upload a `.json` file or paste raw USCIS API JSON directly
- Automatic validation and error handling for malformed or non-USCIS data
- Supports the full USCIS ELIS API response structure

### 📋 Case Details Dashboard
- **Application Information** — Receipt number, form type, form name, applicant name, filing date, last updated, filing channel
- **Case Flags & Status** — Real-time badges for case status (open/closed), adjudicator acknowledgment, premium processing, group status, travel authorization, action required, and evidence requests

### 📅 Event Timeline
- Chronological timeline of all USCIS system events, sorted newest → oldest
- **60+ event codes** decoded with human-readable names and detailed descriptions based on the [NIEM v5.0](https://niem.github.io/model/5.0/scr/BenefitDocumentStatusCategoryCodeSimpleType/) `scr:BenefitDocumentStatusCategoryCodeSimpleType` schema
- Color-coded categories: Receipt, Background Checks, Interview, Processing, Holds, Approved, Denied, Green Card, RFE, Closed
- **Submission date** displayed in UTC (Zulu time) — fixed filing date regardless of timezone
- **All other events** displayed based on `createdAtTimestamp` with original `eventDateTime` shown in the selected timezone for reference
- **Silent Case Update** detection — identifies when USCIS updates the case record without a formal event code (officer touch)

### 📊 Case Summary & Analysis
- Intelligent narrative generation based on case stage (filing → receipt → background checks → interview → post-interview → decision)
- **Adjudication Progress Bar** — Visual step tracker showing exactly where your case stands
- Key statistics: days since filing, total system events, official notices
- Context-aware messaging for approved, denied, RFE, post-interview, and interview-scheduled cases
- Action-required alerts

### 📬 Official Notices
- Parsed display of all USCIS notices with generation dates
- Interview appointment date/time extraction

### 🌐 Timezone Support
- **Default: Central Time (CT) — CST/CDT** — No location permission prompts
- Full US timezone support via dropdown selector:
  - Continental: Eastern, Central, Mountain, Pacific
  - Non-Continental: Alaska, Hawaii-Aleutian, Hawaii
  - Territories: Puerto Rico (Atlantic), Guam (Chamorro), American Samoa
- All timestamps (except fixed UTC submission date) convert dynamically when timezone is changed

### 🎨 Theme System
- **Dark mode** (default) and **Light mode** with smooth transitions
- **Auto mode** — Switches between dark/light based on sunrise/sunset (uses device geolocation if permitted, otherwise defaults to 7 AM – 7 PM)
- Theme preference persisted in `localStorage`

### 📱 Fully Responsive
- Optimized layouts for desktop, tablet, and mobile
- Date **and** time visible on all device sizes in the event timeline

---

## 🚀 How to Use

### Step 1: Get Your USCIS Case JSON Data

1. **Sign in** to your USCIS account at [https://myaccount.uscis.gov/sign-in](https://myaccount.uscis.gov/sign-in)

2. After signing in, **open a new browser tab** and navigate to:
   ```
   https://my.uscis.gov/account/case-service/api/cases/IOE09XXXXXXXX
   ```

3. Replace `IOE09XXXXXXXX` with your unique application **receipt number**

4. The browser will display the raw JSON response

### Step 2: Load Data into the Tracker

**Option A — Paste JSON:**
1. Select all the JSON text from the API page (`Ctrl+A`)
2. Copy it (`Ctrl+C`)
3. Paste it into the text area on the tracker (`Ctrl+V`)
4. Click **▶ Analyze Case**

**Option B — Upload File:**
1. Save the JSON from the API page as a `.json` or `.txt` file
2. Click the **"Click to upload JSON file"** area on the tracker
3. Select your saved file — it will be automatically parsed

### Step 3: Explore Your Case

Once loaded, the tracker will display:
- **Stat Bar** — Quick overview metrics
- **Case Details** — Two-card grid with application info and status flags
- **Official Notices** — If any notices exist in the data
- **Event Timeline** — Full chronological history with decoded event codes
- **Case Summary & Analysis** — Intelligent narrative with progress bar

### Step 4: Adjust Settings (Optional)

- **Change Timezone** — Use the "Display Timezone" dropdown in the header
- **Toggle Theme** — Click the 🌙/☀️ toggle button, or enable ⚡ AUTO mode

---

## 📂 Project Structure

```
.
├── index.html      # Single-file application (HTML + CSS + JavaScript)
└── README.md       # This file
```

The entire application is contained in a single `index.html` file — no build tools, no dependencies, no frameworks. Just open it in any modern browser.

---

## 🏗️ Architecture

### Technology Stack
| Layer | Technology |
|-------|-----------|
| Structure | HTML5 Semantic |
| Styling | Vanilla CSS with CSS Custom Properties (Design Tokens) |
| Logic | Vanilla JavaScript (ES6+) |
| Fonts | Google Fonts — DM Serif Display, DM Sans, DM Mono |
| Timezone | `Intl.DateTimeFormat` API (DST-aware) |
| Theme | CSS `data-theme` attribute + `localStorage` persistence |

### Design System
- **Dark/Light themes** via CSS custom properties (`--bg`, `--surface`, `--gold`, `--green`, etc.)
- **Typography**: DM Serif Display (headings), DM Sans (body), DM Mono (code/data)
- **Color-coded badges** for event categories (blue, gold, green, red, purple, orange, gray)

### Event Code Dictionary
The application includes a comprehensive dictionary of **60+ USCIS event codes** mapped from the NIEM v5.0 schema, organized into categories:

| Category | Example Codes | Description |
|----------|--------------|-------------|
| Receipt | `IAF`, `IAA`, `AALB` | Application receipt and intake |
| Background Checks | `FTA0`, `FTA1`, `FNB`, `QAA` | FBI, fingerprint, and name checks |
| Interview | `FJ`, `HG`, `FM`, `IM` | Interview scheduling and conduct |
| Processing | `FT0`, `TA`, `FR` | Officer review and adjudication |
| Holds | `FS`, `KA`, `KC` | Supervisory, quality, and adjudication holds |
| Approved | `DA`, `IEA`, `IEC` | Approval and welcome notices |
| Green Card | `LAA`, `LDA`, `LEA` | Card production and mailing |
| RFE | `FBA`, `IK`, `HA` | Requests for evidence |
| Denied | `EA`, `IFA`, `FE` | Denial and intent to deny |
| Closed | `EX`, `EN`, `EZ` | Administrative and system closures |

---

## 🔒 Privacy & Security

- ✅ **Zero data transmission** — No API calls, no analytics, no tracking
- ✅ **No server-side processing** — Everything runs in the browser
- ✅ **No data storage** — Nothing is saved to disk, cookies, or cloud
- ✅ **No external dependencies** — Only Google Fonts are loaded externally
- ✅ **Open source** — Full source code visible and auditable

> Your immigration case data never leaves your device.

---

## ⚠️ Disclaimer

This application is an **independent, third-party informational tool** developed solely for personal reference purposes. It is **not affiliated with, endorsed by, sponsored by, or maintained by** U.S. Citizenship and Immigration Services (USCIS), the Department of Homeland Security (DHS), any other government agency, any licensed immigration attorney, law firm, or their representatives.

All information displayed within this tool is generated entirely from the JSON data that **you** provide. This tool performs no independent data retrieval, verification, or legal interpretation. Event code definitions are derived from publicly available NIEM schema documentation.

**This does not constitute legal advice.** Immigration matters are complex, consequential, and highly individual. Always consult a licensed immigration attorney or accredited representative for advice specific to your situation.

---

## 🛠️ Deployment

### GitHub Pages (Recommended)

1. Create a new GitHub repository
2. Add `index.html` and `README.md` to the repository
3. Go to **Settings → Pages**
4. Set source to **Deploy from a branch** → `main` → `/ (root)`
5. Your tracker will be live at `https://<username>.github.io/<repo-name>/`

### Local Usage

Simply open `index.html` in any modern web browser — no server required.

```bash
# macOS
open index.html

# Windows
start index.html

# Linux
xdg-open index.html
```

---

## 🌟 Browser Compatibility

| Browser | Support |
|---------|---------|
| Chrome 80+ | ✅ Full |
| Firefox 78+ | ✅ Full |
| Safari 14+ | ✅ Full |
| Edge 80+ | ✅ Full |
| Mobile Chrome | ✅ Full |
| Mobile Safari | ✅ Full |

---

## 📝 Changelog

### v1.0 — April 2026
- Initial release
- 60+ NIEM v5.0 event codes with full descriptions
- Dark/Light/Auto theme system with sunrise/sunset detection
- Full US timezone support with Central Time (CT) default
- Responsive design for all devices
- Event timeline with `createdAtTimestamp`-based display
- Filing date shown in UTC (fixed Zulu time)
- API access guide for new users
- Privacy-first architecture — zero data transmission

---

## 👤 Author

**[Sohag Kumar Saha](https://sohagkumarsaha.github.io)**

---

## 📄 License

© 2026 Sohag Kumar Saha. All Rights Reserved.

---

<p align="center">
  Proudly developed with <strong>Claude AI</strong> (claude.ai)<br>
  In close supervision with <a href="https://sohagkumarsaha.github.io"><strong>Sohag Kumar Saha</strong></a>
</p>
