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

**Display font:**  
**Body font:**  
**Fallback strategy:**  

**Type scale (define actual sizes and line-heights):**
- H1:  
- H2:  
- H3:  
- Body:  
- Small:  

**Notes (tracking, caps usage, numeric style, etc.):**
-  

---

## 3) Palette (semantic)

Define semantic intent first, then actual values.

- Background:  
- Surface/Card:  
- Foreground/Text:  
- Muted text:  
- Border/Input:  
- Accent:  
- Accent foreground:  
- Ring (focus):  

Optional:
- Danger:  
- Danger foreground:  

---

## 4) Tokens (implementation notes)

Where tokens live:
- CSS variables in `globals.css` (`:root` and `.dark`)
- Tailwind maps semantic color names to CSS variables

Rules:
- No raw hex values in components unless explicitly justified.
- One accent is usually enough.

---

## 5) Motion language

**Primary easing:**  
**Durations:** fast / normal / slow  
**Signature moments:** (1–2 only)

Reduced motion policy:
- what gets disabled or simplified when `prefers-reduced-motion` is enabled?

---

## 6) Layout density

- Container max width:  
- Default section spacing (top/bottom):  
- Default vertical rhythm (stack gap):  

---

## 7) Component style notes (optional)

- Buttons:  
- Cards:  
- Inputs:  
- Tables:  
- Toasts:  

