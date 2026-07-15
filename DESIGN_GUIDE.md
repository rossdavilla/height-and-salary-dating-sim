# Height & Salary Simulator — Image & Animation Design Guide

A production guide for upgrading the *Dating Messages Simulator* from emoji/SVG placeholders to
polished, cohesive artwork. Every asset below includes a **ready-to-paste ChatGPT prompt**, the
**exact size** it renders at in your app, and **animation notes**.

> **Image folder note:** in this project the images folder is named **`img/`** (not `images/`).
> Save all generated assets there.

---

## 0. How to use this guide

1. **Copy the "Master Style Block"** (Section 2) and paste it at the **top of every image prompt**.
   This is the single most important trick — it forces ChatGPT/DALL·E to keep one consistent art
   style across all assets so they look like a matched set instead of random clip art.
2. Then paste the specific asset prompt underneath it.
3. **Always ask for a transparent background** for anything that sits *on top* of the scene
   (character, hearts, coins, logo). Add this line to those prompts:
   *"Transparent background (PNG with alpha), no drop shadow baked in, subject fully inside frame with a small margin."*
4. **Ask for the size**, e.g. *"Output a square 1024×1024 image"* — then you downscale. Generating
   large and shrinking keeps edges crisp.
5. If ChatGPT drifts off-style, paste one of your already-good images back in and say
   *"match this exact style, same character, new pose."*

> ℹ️ **ChatGPT makes still images, not animation.** All motion (hearts falling, money stacking,
> character bounce) is done in code — see Section 8. Design the images as clean, separate layers so
> they can be animated individually.

---

## 1. The current look (what we're replacing)

| Element | Currently | Upgrade to |
|---|---|---|
| Avatar | Blue-shirt SVG stick figure, yellow circle head | Illustrated character that scales with height |
| Face / reaction | 8 native emoji (😭 → 😍) | Custom expression set (or keep emoji) |
| Salary / wealth | Grid of 💵 emoji, 1 = $10k | Illustrated cash bills + coin/gold tiers |
| "Likes" | Falling ❤ text characters | Glossy 3D heart PNGs (2–3 variants) |
| App logo | CSS gradient blob | Real app icon |
| Phone screen backdrop | Flat dark-blue radial | Soft "stage" scene the character stands on |
| Page background | Pink→orange gradient | Same gradient + subtle floating décor |

---

## 2. Master Style Block  ⭐ paste this on top of EVERY prompt

```
STYLE: Modern, playful mobile-app illustration. Soft 3D "claymorphism" look —
smooth rounded forms, gentle inflated shapes, soft studio lighting with a soft
top-left light source and soft ambient shadows. Clean, friendly, premium — like
a high-end dating-app onboarding illustration or an Apple emoji rendered in 3D.
Slightly glossy surfaces, subtle rim light, no harsh outlines, no gritty texture.
Color palette centered on hot pink (#fd3a73), warm orange (#ff7a00), with mint-green
(#24e0a7) accents on a dark navy (#0c1222) or transparent background.
Cohesive with a fun romance / dating theme. High detail, crisp edges, centered subject.
```

*(If you'd rather have a flat vector look instead of 3D, swap the first two sentences for:
"STYLE: Flat vector illustration, bold clean shapes, minimal gradients, thick consistent line
weight, modern flat-design mascot style." Keep everything else the same.)*

---

## 3. Color palette (from your CSS — give these to ChatGPT)

| Name | Hex | Used for |
|---|---|---|
| Tinder Pink | `#fd3a73` | Primary brand, background top, buttons |
| Tinder Orange | `#ff7a00` | Background bottom, warmth |
| Accent Pink | `#ff3265` | Button gradient, highlights |
| Heart Pink | `#ff5c8a` | Falling hearts |
| Success Mint | `#24e0a7` | Result number, positive states |
| Ink / Bezel | `#0f1115` | Phone body |
| Screen Navy | `#0c1222` | Phone screen background |
| Soft Yellow | `#fde68a` | (old skin tone — replace as you like) |

---

## 4. ASSET GROUP A — The Character (the star of the show)

The avatar is centered in the phone and **scales from 75% → 150%** as the height slider moves
(short → tall). So it must be **one full-body, front-facing, standing figure** that looks good at
any size.

> **Design decision — the face:** Your code swaps 8 emoji reactions onto the head. Two options:
> - **Option A (least code change):** Give the character a **blank, smooth face** (no eyes/mouth).
>   The reaction emoji/expression sits on top of the head area as the "face." Keep your existing swap logic.
> - **Option B (most polished):** Character has **no fixed face**, and you make the 8-expression set
>   in Group B to swap in as PNGs instead of emoji.
>
> **Recommended: Option A** for v1 (fast), then Option B if you want the premium version.

### A1 — Main character, neutral pose  ⭐ must-have

- **Where:** center of the phone, replaces `#manSvg`
- **Renders at:** ~120 px wide × ~300 px tall (scales up to ~180×450). **Generate 1024×1536 (2:3 tall).**
- **Format:** Transparent PNG. Standing straight, facing forward, arms relaxed at sides, feet together.

```
[PASTE MASTER STYLE BLOCK FIRST]

Subject: A friendly, cute full-body cartoon character standing straight, facing
directly forward, arms relaxed at the sides, feet together, in a confident neutral
pose. Gender-neutral young adult. Wearing a simple modern outfit: a pink-and-orange
gradient t-shirt and dark trousers. The head is a smooth rounded shape with a
SMOOTH BLANK FACE (no eyes, no mouth) — leave the face area clean, because a
separate expression will be placed on top later.
Full body visible head to feet, centered, small margin around the figure.
Symmetrical, balanced, so the figure can be scaled larger or smaller without looking
distorted. Transparent background (PNG with alpha), no baked-in shadow.
Output a tall 1024×1536 image.
```

**Animation notes:** subtle idle "breathing" scale (already scales for height); add a gentle bob when
results appear. Keep the character on its own layer with transform-origin at the feet (your CSS
already does `transform-origin:bottom center`).

### A2 — Contact shadow / platform  *(nice-to-have)*

Gives the character something to stand on so it doesn't float.

- **Renders at:** ~140 px wide, thin ellipse under the feet
- **Format:** Transparent PNG

```
[PASTE MASTER STYLE BLOCK FIRST]

Subject: A single soft, blurred oval contact shadow / floor shadow, as if cast by a
character standing on a floor. Soft dark navy, semi-transparent, feathered edges,
no hard rim. Just the shadow ellipse, nothing else. Transparent background.
Output a wide 1024×512 image.
```

---

## 5. ASSET GROUP B — Reactions / Expressions

Your app shows a mood that gets happier as the score rises:
😭 (worst) → 😢 → 😒 → 🫤 → 🙂 → 😉 → 🥰 → 😍 (best).

### B1 — Custom expression set (8 faces)  *(optional, replaces emoji)*

- **Where:** overlaid on the character's head (`#emoji`), renders ~48 px
- **Format:** Transparent PNG, **one image per expression, all identical style & size**
- **Tip:** Generate them as **one sheet first** for consistency, then export 8 separate files, OR
  ask for each individually while pasting the previous one for style-matching.

```
[PASTE MASTER STYLE BLOCK FIRST]

Subject: A set of 8 cute round face expressions in a single row, all the same
character, same size, same 3D claymorphism style, evenly spaced on a transparent
background. Left to right the expressions are:
1) sobbing / crying hard, 2) sad tearful, 3) unamused / annoyed,
4) meh / unsure, 5) mild neutral smile, 6) winking flirty,
7) smiling with hearts / in love, 8) huge delighted heart-eyes.
Just the faces (round heads), no bodies. Consistent lighting and style across all 8.
Transparent background. Output a wide 2048×512 image.
```

*(If you keep native emoji instead, skip this — but the custom set is what makes it feel bespoke.)*

---

## 6. ASSET GROUP C — Wealth / Money

Salary is shown as a pile that grows; **each unit = $10,000**. Instead of one 💵 emoji, use a small
set so higher salaries visibly "level up" (cash → stacks → gold).

### C1 — Single cash bill  ⭐ must-have

- **Where:** the money pile (`.bill`), renders ~42 px, many tiled in a grid
- **Format:** Transparent PNG

```
[PASTE MASTER STYLE BLOCK FIRST]

Subject: A single crisp banknote of cash, 3D claymorphism style, soft glossy
surface, mint-green and white with a subtle dollar sign, slightly angled in
3/4 view, gentle soft shadow on itself only. Cute and clean, not a real currency
design. Centered, transparent background. Output a square 1024×1024 image.
```

### C2 — Cash stack (bundle)  *(nice-to-have — for mid salaries)*

```
[PASTE MASTER STYLE BLOCK FIRST]

Subject: A neat bundle/stack of banknotes tied with a paper band, 3D claymorphism
style, mint-green and white, soft glossy, slight 3/4 angle. Cute, clean, centered.
Transparent background. Output a square 1024×1024 image.
```

### C3 — Gold coins & bar  *(nice-to-have — for the richest tier)*

```
[PASTE MASTER STYLE BLOCK FIRST]

Subject: A small pile of shiny gold coins with one gold bar, 3D claymorphism style,
warm glossy gold with soft highlights and a subtle sparkle. Cute, premium, centered.
Transparent background. Output a square 1024×1024 image.
```

**Animation notes:** each new bill "pops" in with a quick scale-up + settle bounce as the salary
slider rises. Top tier coins get a slow shimmer/sparkle loop.

---

## 7. ASSET GROUP D — Hearts & Environment

### D1 — Falling heart (2–3 variants)  ⭐ must-have

Replaces the falling ❤ characters. Make 2–3 slightly different hearts and randomize them in the rain
so it doesn't look repetitive.

- **Renders at:** ~44 px, many falling
- **Format:** Transparent PNG

```
[PASTE MASTER STYLE BLOCK FIRST]

Subject: A single cute glossy 3D heart, plump and rounded (claymorphism), hot pink
to soft pink gradient (#ff5c8a to #fd3a73), soft top-left highlight and gentle rim
light, no outline. Centered, symmetrical, transparent background.
Output a square 1024×1024 image.
```

Variations to also generate (same prompt, change one line):
- *"...a heart with a small white sparkle/shine mark on it..."*
- *"...a slightly smaller heart tilted 15 degrees..."*

### D2 — Phone-screen stage backdrop  *(nice-to-have)*

The scene *inside* the phone where the character stands. Keep it dark so the pink hearts and mint
number pop.

- **Renders at:** fills the phone screen ≈ 362 × 518 px. **Generate 768×1024 (3:4 tall).**
- **Format:** Opaque PNG (this is a background, not an overlay)

```
[PASTE MASTER STYLE BLOCK FIRST]

Subject: A softly lit vertical stage/room backdrop for a character to stand in.
Dark navy (#0c1222) base with a subtle warm spotlight glow on the floor in the
center, faint bokeh dots, a gentle pink-to-orange ambient glow near the bottom.
Minimal, uncluttered, lots of empty space in the middle for a character. No text,
no people. Vertical composition. Output a 768×1024 image.
```

### D3 — Page background décor overlay  *(nice-to-have)*

Adds life to the pink→orange page background *behind* the whole app. Must stay **very subtle** so
white text stays readable.

- **Renders at:** full page, sits behind `.container`
- **Format:** Transparent PNG (overlay) OR seamless tile

```
[PASTE MASTER STYLE BLOCK FIRST]

Subject: A subtle decorative overlay pattern of faint, translucent outline hearts
and soft circular bokeh, scattered loosely, very low contrast, mostly transparent.
Designed to sit on top of a pink-to-orange gradient without reducing text
readability. No solid shapes in the center. Seamless, airy, minimal.
Transparent background. Output a 1536×1024 image.
```

---

## 8. ASSET GROUP E — Branding & UI

### E1 — App logo / icon  ⭐ must-have

- **Where:** header (`.logo`), renders 40 × 40, rounded 10 px
- **Format:** PNG, works as a rounded-square app icon

```
[PASTE MASTER STYLE BLOCK FIRST]

Subject: A modern mobile app icon on a rounded-square tile with a pink-to-orange
gradient background (#fd3a73 to #ff7a00). Centered symbol: a glossy 3D white heart
with a subtle flame/spark accent. Clean, bold, recognizable at small sizes, soft
inner glow. App-store icon quality. Output a square 1024×1024 image.
```

### E2 — Button heart icon  *(optional)*

Small icon to sit inside the "Show Results" button.

```
[PASTE MASTER STYLE BLOCK FIRST]

Subject: A simple solid white heart icon, clean and minimal, slight gloss,
centered, transparent background. Output a square 512×512 image.
```

### E3 — Result celebration burst  *(optional)*

A one-shot graphic that flashes when results appear, behind the number.

```
[PASTE MASTER STYLE BLOCK FIRST]

Subject: A celebratory radial burst of confetti, small hearts, and sparkles
exploding outward from the center, pink/orange/mint/gold, on a transparent
background. Symmetrical, energetic, centered empty core. Output a square 1024×1024 image.
```

---

## 9. Animation plan (done in code, not images)

These are the motions to add once the images are in. Design the images as **clean separate layers**
so each can move independently.

| Moment | Animation | Notes |
|---|---|---|
| Idle | Character gentle 2–3 s "breathing" bob | Loop, ease-in-out |
| Height slider | Smooth scale (you already do this) | Keep `transform-origin: bottom center` |
| Salary slider | Each new bill **pops in** (scale 0→1 + tiny bounce) | Stagger by ~40 ms per bill |
| Top salary tier | Gold coins **shimmer** (slow highlight sweep) | Subtle, looping |
| "Show Results" | Character **happy hop**, expression swaps, **hearts rain** (you have this), **burst** flashes behind the number, number **counts up** | Sequence over ~1 s |
| Hearts rain | Randomize which heart PNG (D1 variants), size, speed, drift | You already spawn/clean them up |
| Background | Décor overlay **slow drift/parallax** | Very slow, 30–60 s loop |

---

## 10. Production checklist (suggested order)

**Phase 1 — biggest visual payoff (do these first):**
- [ ] A1 — Main character (neutral)
- [ ] D1 — Falling heart (+ 1–2 variants)
- [ ] C1 — Single cash bill
- [ ] E1 — App logo

**Phase 2 — polish:**
- [ ] B1 — 8-expression set
- [ ] C2 / C3 — Cash stack + gold tiers
- [ ] D2 — Phone-screen stage backdrop
- [ ] A2 — Contact shadow

**Phase 3 — extra shine:**
- [ ] D3 — Background décor overlay
- [ ] E2 — Button heart icon
- [ ] E3 — Celebration burst

---

## 11. File delivery & naming

Save the finished images in the `img/` folder next to `index.html`, named clearly so they're easy
to wire up:

```
img/
  character-neutral.png
  face-01-sob.png … face-08-heart-eyes.png   (if using custom expressions)
  cash-bill.png
  cash-stack.png
  gold-coins.png
  heart-a.png  heart-b.png  heart-c.png
  logo.png
  stage-backdrop.png
  bg-decor.png
  burst.png
```

**Specs recap:**
- Overlays (character, hearts, coins, logo, faces, shadow, décor, burst): **transparent PNG**.
- Backgrounds (stage backdrop): opaque PNG.
- Generate **2–3× larger** than the render size in this guide, then let the browser scale down.
- Keep every asset in the **same style** (Master Style Block) — that consistency is what sells it.

---

*When your images are ready, drop them in `img/` and I can wire them into `index.html` and add
all the animations in Section 9 for you.*
