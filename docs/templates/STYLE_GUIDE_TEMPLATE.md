# STYLE_GUIDE.md (template)

This file is the source of truth for **typography, palette, tokens, and motion**.
Fill it early. Keep it updated when decisions change.

---

## 1) Direction

**Project:**  
**Audience:**  
**Primary use:** (marketing / SaaS app / dashboard / internal tool)

**3–5 adjectives:**
-  
-  
-  
-  

**Signature element (one memorable thing):**
-  

**Theme:** (light / dark / both)

---

## 2) Typography

### 2.1 Font faces

**Display font:**  
**Body font:**  
**Language coverage:** (latin / cyrillic / etc.)  
**Fallback strategy:**  

### 2.2 Font tokens (Next.js + `next/font`)

Set font families via CSS variables:

- `--font-body`:  
- `--font-display`:  

Implementation note:
- Use `next/font` with `variable: "--font-body"` / `variable: "--font-display"`.

### 2.3 Type scale tokens (sizes + leading + tracking)

Define a small scale and stick to it:

- `--text-h1`, `--leading-h1`, `--tracking-h1`:  
- `--text-h2`, `--leading-h2`, `--tracking-h2`:  
- `--text-h3`, `--leading-h3`, `--tracking-h3`:  
- `--text-body`, `--leading-body`, `--tracking-body`:  
- `--text-sm`, `--leading-sm`, `--tracking-sm`:  

Notes (caps usage, numeric style, etc.):
-  

---

## 3) Palette (semantic)

Define semantic intent first, then values. Prefer a shadcn-compatible semantic set.

Core:

- Background:  
- Foreground/Text:  
- Card surface:  
- Card foreground:  
- Primary:  
- Primary foreground:  
- Secondary:  
- Secondary foreground:  
- Muted:  
- Muted foreground:  
- Accent:  
- Accent foreground:  
- Border/Input:  
- Ring (focus):  
- Destructive:  
- Destructive foreground:  

Optional product states (add only if needed):

- Success:  
- Success foreground:  
- Warning:  
- Warning foreground:  
- Info:  
- Info foreground:  

---

## 4) Tokens (implementation notes)

Where tokens live:

- CSS variables in `globals.css` (`:root` and `.dark`)
- Tailwind maps semantic names to CSS variables

Rules:

- No raw hex values in components unless explicitly justified.
- Avoid one-off colors for hover/active; use consistent conventions or derived tokens.
- Keep the token set small and semantic.

---

## 5) Motion language

**Primary easing:**  
**Durations:** fast / normal / slow  
**Signature moments:** (1–2 only)

Reduced motion policy:

- What gets disabled or simplified when `prefers-reduced-motion` is enabled?

---

## 6) Layout density

Baseline:

- Container max width:  
- Side padding (mobile / desktop):  
- Reading width (if applicable): (~65ch)

Spacing scale (px → Tailwind):

- 4 → `1`
- 8 → `2`
- 12 → `3`
- 16 → `4`
- 24 → `6`
- 32 → `8`
- 48 → `12`

Defaults:

- Section spacing (top/bottom):  
- Stack gaps (vertical rhythm):  
- Card padding:  

---

## 7) Component style notes (optional)

- Buttons:  
- Cards:  
- Inputs:  
- Tables:  
- Toasts:  
