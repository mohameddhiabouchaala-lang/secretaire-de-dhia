# [Bug Report / Audit] Faults & Improvements in `Secrétaire de Dhia` (`secretaire-dhia.html`)

## Summary
Static analysis of the 3,759-line `Secrétaire de Dhia` application (`secretaire-dhia.html`) found **no syntax errors**, but identified **4 functional/logical faults** and **1 portability limitation** when running outside Claude. All 4 code faults have been patched in `index.html`.

---

## Identified Faults

### 1. Hidden Alert Badges on Grouped Sub-tabs (`#b-cand` & `#b-sem`)
- **Location:** Lines 1069–1090 (`GROUPS` / `route()`), Line 1315 (`renderCand()`), Line 1408 (`renderWeek()`), Line 1542 (`renderOffres()`)
- **Problem:** On startup, `GROUPS` moves the `Candidatures` (`#b-cand`), `Semaine` (`#b-sem`), and `Examens` (`#b-rev`) tabs out of `.side` into `#subnav`. Whenever the user is on **Accueil**, **Discussion**, or **Mentor**, `#subnav` has `hidden = true`. As a result, overdue application follow-up badges (`#b-cand`) and weekly schedule conflict badges (`#b-sem`) are hidden from the main navigation bar.
- **Fix Applied:** Rolled up the overdue follow-up count (`follow`) into the main **Postuler** badge (`#b-off`) with `.badge.alert` styling so urgent follow-ups are always visible in the sidebar.

### 2. Unhandled En-Dash / Em-Dash / Bullet Characters in Cover Letter PDF (`PDF_SAFE`)
- **Location:** Line 2273 (`PDF_SAFE` in `letterPdfB64()`)
- **Problem:** `jsPDF`'s built-in `helvetica` font only supports WinAnsi/Latin-1 characters. `PDF_SAFE` normalizes `/[‐‑]/g` (`\u2010`, `\u2011`), curly quotes, and `œ/Œ`, but omits en-dash `–` (`\u2013`), em-dash `—` (`\u2014`), and bullet `•` (`\u2022`), which Claude frequently outputs in French cover letters.
- **Fix Applied:** Extended character normalization to `/[‐‑–—•]/g`.

### 3. Unreachable Browser Tools (`BRT` Hardcoded to `false`)
- **Location:** Line 3219 (`ask()`)
- **Problem:** `const avail = TOOLS.filter((t) => (BRT.includes(t.name) ? false : MCPT.includes(t.name) ? !!mcp : !!db));` hardcodes `false` for all 5 `BRT` tools (`navigateur_ouvrir`, `navigateur_lire`, `navigateur_remplir`, `navigateur_cliquer`, `demander_envoi`), rendering lines 2860–2908 and 3069–3128 unreachable dead code even when `browserOk` is `true` in Claude Desktop.
- **Fix Applied:** Replaced `? false` with `? browserOk`.

### 4. Missing `tanitjobs.com` in Browser Tool Domain Whitelist (`ALLOWED`)
- **Location:** Line 2862 (`ALLOWED`) vs. Line 3270 (`#findOffers`)
- **Problem:** `#findOffers` searches job alerts from **LinkedIn, Tanitjobs, UNV, and Jamaity**, but `ALLOWED = ["unv.org", "jamaity.org", "linkedin.com"]` blocks `tanitjobs.com`.
- **Fix Applied:** Added `"tanitjobs.com"` to `ALLOWED`.

### 5. Claude-Only Storage Lock-In (`window.claude.use("db")`)
- **Location:** Lines 3280–3302 & Lines 3736–3756
- **Problem:** Outside the Claude artifact iframe, `window.claude` is undefined, disabling database persistence (`taches`, `candidatures`, `revisions`, `offres`, `engagements`, `notions`, `bilans`).
- **Recommendation:** Add a `localStorage` / IndexedDB fallback adapter when `window.claude` is absent so the app works standalone on PC and mobile.
