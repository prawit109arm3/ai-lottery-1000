# AI_MANIFEST.md — PRAWIT QUANT (`ai-lottery-1000`)

## 1. Purpose & Core Invariants
Single-page mobile-first Quant Lottery Portfolio Terminal (`index.html`) designed for complete beginners to generate balanced 2-digit Thai Government Lottery slips (`2 ตัวบน + 2 ตัวล่าง`) within a **1,000 THB** budget.

### Mathematical Invariants (Do Not Break)
1. **Digit Selection Rules (`triggerSmartRandom`, `resolveSubDigitOverlap`)**:
   - `mainDigits` (2 digits): Must select 1 Low digit (`0–4`) and 1 High digit (`5–9`) with **opposite Odd/Even parity** (`(m1 % 2) !== (m2 % 2)`).
   - `subDigits` (2 digits): Must **never overlap** with `mainDigits`, and prioritize digits whose sum with `mainDigits` falls in the **Golden Sum range (`7–11`)**.
   - Manual keypad selection uses a **FIFO 2-element queue** (`[state.mainDigits[1], d]`) so any two consecutive taps select those exact two digits.
2. **Mode 1 (`mode: 'simple'` — Default Beginner Single-Price Mode)**:
   - **Coverage**: 38 unique 2-digit numbers (`36` from 19-door union of `mainDigits` + `2` reversed pairs from `subDigits`).
   - **Win Probability (at least 1 prize across Top & Bottom)**: $1 - (0.62 \times 0.62) = \mathbf{61.56\%}$.
   - **Sizing**: `13 THB` Top + `13 THB` Bottom per number = **988 THB** total (`38 × 26`).
   - **Payout (at 90x)**: Single-side hit = `1,170 THB` (**+182 THB net profit** on every number); Both-sides hit = `2,340 THB` (**+1,352 THB net profit**).
3. **Mode 2 (`mode: '3group'` — 3-Tier Conviction Mode)**:
   - **Coverage**: 36 unique 2-digit numbers decomposed into **3 mutually exclusive groups**:
     - **Group 1 (2 numbers — `collisionList`)**: `23 THB` Top + `23 THB` Bottom (`92 THB`).
     - **Group 2 (8 numbers — `group2List`)**: `21 THB` Top + `21 THB` Bottom (`336 THB`).
     - **Group 3 (26 numbers — `group3List`)**: `11 THB` Top + `11 THB` Bottom (`572 THB`).
   - **Total Cost**: $92 + 336 + 572 = \mathbf{1,000\text{ THB}}$.
   - **Win Probability**: $1 - (0.64 \times 0.64) = \mathbf{59.04\%}$.

---

## 2. UI / UX Design System Rules (`ui-ux-pro-max`)
- **Theme**: Dark Mode by default (`<html lang="th" class="dark">`), styled after a **Pro Crypto Exchange Terminal** (`#0B0E11` carbon background, `#181A20` card surface, `#1E2329` elevated surface, `#2B3139` 1px borders, `#FCD535` Exchange Gold primary CTA, `#0ECB81` Bullish Green profit/copy CTA, `#F6465D` High-Conviction Red).
- **Typography**: Google Fonts `Sarabun` (Thai UI) + `JetBrains Mono` (`tabular-nums` on all numbers, prices, and 2-digit chips).
- **Icons & Logos**:
  - Functional UI icons: **Lucide Icons** (`https://unpkg.com/lucide@latest`, refreshed via `lucide.createIcons()`).
  - Brand/Exchange/Platform logos: **Simple Icons CDN** (`https://cdn.simpleicons.org/<slug>/<hex>`).
  - **Zero emojis** anywhere in the UI.

---

## 3. Repository & Deployment Map
- **Local Workspace Path**: `C:\Users\ARM-LENOVO\.gemini\antigravity\scratch\ai-lottery-1000`
- **Entry File**: `index.html` (Zero-build static HTML/JS/Tailwind/Lucide bundle)
- **GitHub Repository**: `https://github.com/prawit109arm3/ai-lottery-1000`
- **Production URL (Vercel)**: `https://lottery-prawit.vercel.app`
