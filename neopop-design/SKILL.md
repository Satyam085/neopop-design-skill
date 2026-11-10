---
name: neopop-design
description: Build UIs in CRED's NeoPOP design language: 3D plunk buttons, black-first palette, bold type. Use for any NeoPOP, CRED-style or CRED-like screen, component or page.
license: Apache-2.0. Complete terms in LICENSE.txt; attribution in NOTICE
---

# NeoPOP design language

NeoPOP is CRED's open-source design system (Apache-2.0, with libraries for web, Android, iOS and Flutter). Every value in this skill comes from the official source: the primitives and component styles in `CRED-CLUB/neopop-web`, plus the edge-colour maths in `CRED-CLUB/neopop-android`. Prefer these numbers over a general impression of "what CRED looks like". The style is usually rebuilt from vague memory, and that is how it ends up generic.

Copy the design language, not the brand. Never use CRED's logo, wordmark, product names or mascots in what you build.

**Credits.** NeoPOP was designed and built by CRED (Dreamplug Technologies Private Limited) and released under the Apache License 2.0 in [neopop-web](https://github.com/CRED-CLUB/neopop-web) and [neopop-android](https://github.com/CRED-CLUB/neopop-android). This skill adapts their colour values, type scale, component measurements, CSS geometry, SVG icon paths and edge-colour rule, rewritten as plain CSS with changes (focus states, reduced motion, light-theme contrast, colour presets). Adaptation © 2026 Satyam Singh, also Apache-2.0. Unofficial: not affiliated with or endorsed by CRED. When you copy the foundation CSS into a project, keep its header comment, because that is the credit line that travels with the code.

## 1. Choose the implementation path

| Situation | Path |
|---|---|
| React 17/18 app that already uses (or can add) `styled-components@5` | You may use the official package `@cred/neopop-web` (section 9) |
| React 19, Next, TanStack Start, Vue, Svelte, Astro, plain HTML, server templates, Tailwind/DaisyUI, anything else | Build it yourself with the foundation CSS in section 3 |
| Not sure | Build it yourself |

Why: the package is v1.0.0 from July 2022. It needs React ^17/^18 and styled-components ^5.3.5 as peers, it is optimised for mobile, and its buttons ship with `outline: none`. The foundation CSS draws the same geometry with no dependencies and adds focus states.

## 2. The look in eight rules

1. **Hard edges.** Every surface has `border-radius: 0`. The only exceptions are radio dots and circular score meters, which are round by nature, and a 4px radius on floating (not full-width) toasts.
2. **Depth comes from geometry, not blur.** A raised surface has a solid "plunk": a right edge and a bottom edge, each a 45° parallelogram, `--np-depth` thick (3px by default). Don't use blurred box-shadows, glows or gradients to show depth.
3. **Light comes from the top-left.** That is why the right and bottom edges show. The right edge is the lighter of the two and the bottom edge the darker.
4. **Pressing is physical.** On press, the face slides down-right by exactly the depth and the edges disappear under it, in 120ms ease-in-out. Flat buttons work the other way: they sink into their parent and show a top wall and a left wall.
5. **Black first.** The canvas is `#0d0d0d`, raised panels are `#121212`, and hairlines are 10% white. Text is white at four opacity levels (90/70/50/30%), not a set of separate greys.
6. **Mostly monochrome, plus one loud accent.** Most of a screen is black, white and grey. One saturated accent (neo-paccha lime, park green, poli purple, …) marks the single most important surface or action on the view.
7. **Two typefaces.** A geometric sans (Gilroy) for all UI, and a sharp, high-contrast display serif (Cirka) for editorial headlines. Tiny uppercase "caps" with very wide letter-spacing go on eyebrows, labels and tags.
8. **Quiet chrome, loud content.** Inputs have no boxes, just a tiny caps label above a big bold value. Copy is lowercase, short and confident ("pay now", "your bill is due in 3 days").

## 3. Foundation CSS — copy this into the project as `neopop.css`

```css
/* neopop.css: NeoPOP foundation (unofficial).
   Adapted from NeoPOP by CRED, https://github.com/CRED-CLUB/neopop-web
   Copyright 2022 Dreamplug Technologies Private Limited, Apache-2.0.
   Modified by Satyam Singh, 2026 (plain-CSS rewrite, a11y, presets). Apache-2.0.
   Fonts: self-host licensed Gilroy + Cirka, or use the free stand-ins:
   @import url("https://fonts.googleapis.com/css2?family=Outfit:wght@400;500;600;700;800&family=Playfair+Display:wght@700&display=swap"); */

:root {
  --np-black: #0d0d0d; --np-white: #ffffff;
  --np-red: #ee4d37; --np-yellow: #f08d32; --np-blue: #144cc7; --np-green: #06c270;
  /* neutrals (lib names: popWhite 500..100, popBlack 100..500) */
  --np-n-0: #ffffff; --np-n-50: #fbfbfb; --np-n-100: #efefef; --np-n-200: #e0e0e0; --np-n-300: #d2d2d2;
  --np-n-500: #8a8a8a; --np-n-800: #3d3d3d; --np-n-900: #161616; --np-n-950: #121212; --np-n-1000: #0d0d0d;
  /* accents 100..800 (500 is the "pop" shade) */
  --np-poli-purple-100:#e8dfff; --np-poli-purple-200:#d2c2ff; --np-poli-purple-300:#b49aff; --np-poli-purple-400:#9772ff; --np-poli-purple-500:#6a35ff; --np-poli-purple-600:#4a25b3; --np-poli-purple-700:#351a80; --np-poli-purple-800:#20104d;
  --np-orange-sunshine-100:#ffefe6; --np-orange-sunshine-200:#ffdbc7; --np-orange-sunshine-300:#ffc3a2; --np-orange-sunshine-400:#ffab7c; --np-orange-sunshine-500:#ff8744; --np-orange-sunshine-600:#b35f30; --np-orange-sunshine-700:#804322; --np-orange-sunshine-800:#4d2914;
  --np-park-green-100:#ddfff1; --np-park-green-200:#c4ffe6; --np-park-green-300:#9dffd6; --np-park-green-400:#76ffc6; --np-park-green-500:#3bffad; --np-park-green-600:#29b379; --np-park-green-700:#1e8057; --np-park-green-800:#124d34;
  --np-pink-pong-100:#ffe1e9; --np-pink-pong-200:#ffc6d4; --np-pink-pong-300:#ffa0b7; --np-pink-pong-400:#ff7b9a; --np-pink-pong-500:#ff426f; --np-pink-pong-600:#b32e4e; --np-pink-pong-700:#802138; --np-pink-pong-800:#4d1421;
  --np-mannna-100:#fff8e5; --np-mannna-200:#ffefc7; --np-mannna-300:#ffe5a2; --np-mannna-400:#ffdb7d; --np-mannna-500:#ffcb45; --np-mannna-600:#b38e30; --np-mannna-700:#806623; --np-mannna-800:#4d3d15;
  --np-neo-paccha-100:#fbffe6; --np-neo-paccha-200:#f7ffc6; --np-neo-paccha-300:#f2ff9f; --np-neo-paccha-400:#edfe79; --np-neo-paccha-500:#e5fe40; --np-neo-paccha-600:#a0b22d; --np-neo-paccha-700:#727f20; --np-neo-paccha-800:#454c13;
  --np-yoyo-100:#f4e5ff; --np-yoyo-200:#e5c5ff; --np-yoyo-300:#d59fff; --np-yoyo-400:#c379ff; --np-yoyo-500:#aa3fff; --np-yoyo-600:#772cb3; --np-yoyo-700:#552080; --np-yoyo-800:#33134d;
  /* status scales 100..500 */
  --np-error-100:#fce2dd; --np-error-200:#f6a69b; --np-error-300:#f47564; --np-error-400:#f05e4b; --np-error-500:#ee4d37;
  --np-warning-100:#fbddc2; --np-warning-200:#f8c699; --np-warning-300:#f5ac6a; --np-warning-400:#f29947; --np-warning-500:#f08d32;
  --np-info-100:#c2d0f2; --np-info-200:#89a5e3; --np-info-300:#3f6fd9; --np-info-400:#2c5ecd; --np-info-500:#144cc7;
  --np-success-100:#e6f9f1; --np-success-200:#83e0b8; --np-success-300:#4fe3a3; --np-success-400:#1fc87f; --np-success-500:#06c270;

  --np-depth: 3px;
  --np-press: 120ms ease-in-out;
  --np-font-sans: "Gilroy", "Outfit", "Urbanist", system-ui, sans-serif;
  --np-font-serif: "Cirka", "Playfair Display", "DM Serif Display", Georgia, serif;
}

/* ---------- themes (dark is the default) ---------- */
:root, [data-np-theme="dark"] {
  --np-bg: #0d0d0d; --np-surface: #121212; --np-hairline: rgba(255,255,255,.1);
  --np-text-1: rgba(255,255,255,.9); /* headings */
  --np-text-2: rgba(255,255,255,.7); /* sub-headings */
  --np-text-3: rgba(255,255,255,.5); /* body, labels */
  --np-text-4: rgba(255,255,255,.3); /* placeholder / disabled ONLY */
  --np-line: #3d3d3d; --np-focus: #ffffff;
  --np-ctl-ink: #ffffff; --np-ctl-bg: #0d0d0d; --np-plunk-t: #3d3d3d; --np-plunk-l: #8a8a8a;
  --np-tgl-off-track: #0a0a0a; --np-tgl-border: #ffffff; --np-tgl-off-knob: #ffffff; --np-tgl-off-knob-border: #0a0a0a; --np-tgl-off-mark: #e0e0e0;
  --np-tgl-on-track: #b4edd4; --np-tgl-on-knob-border: #b4edd4;
}
[data-np-theme="light"] {
  --np-bg: #ffffff; --np-surface: #fbfbfb; --np-hairline: rgba(13,13,13,.1);
  --np-text-1: rgba(13,13,13,.9); --np-text-2: rgba(13,13,13,.7);
  --np-text-3: rgba(13,13,13,.7); /* lib uses .5; .5 black on white is 3.6:1, too low for small text */
  --np-text-4: rgba(13,13,13,.3);
  --np-line: #e0e0e0; --np-focus: #0d0d0d;
  --np-ctl-ink: #0d0d0d; --np-ctl-bg: #ffffff; --np-plunk-t: #e0e0e0; --np-plunk-l: #8a8a8a;
  --np-tgl-off-track: #ffffff; --np-tgl-border: #0a0a0a; --np-tgl-off-knob: #e0e0e0; --np-tgl-off-knob-border: #ffffff; --np-tgl-off-mark: #ffffff;
  --np-tgl-on-track: #caffe2; --np-tgl-on-knob-border: #f7f7f7;
}
.np-page { background: var(--np-bg); color: var(--np-text-1); font-family: var(--np-font-sans);
  -webkit-font-smoothing: antialiased; -moz-osx-font-smoothing: grayscale; }

/* ---------- type roles (lib key in comment) ---------- */
.np-display  { font: 700 36px/45px var(--np-font-serif); letter-spacing: .2px; color: var(--np-text-1); } /* tsh36b */
.np-title    { font: 700 24px/30px var(--np-font-serif); letter-spacing: .2px; color: var(--np-text-1); } /* tsh24b: page header */
.np-amount   { font: 800 34px/43px var(--np-font-sans);  letter-spacing: .2px; color: var(--np-text-1); } /* th34eb */
.np-heading  { font: 800 22px/28px var(--np-font-sans);  letter-spacing: .2px; color: var(--np-text-1); } /* th22eb */
.np-subhead  { font: 600 16px/20px var(--np-font-sans);  letter-spacing: .4px; color: var(--np-text-2); } /* th16sb */
.np-card-title { font: 700 14px/18px var(--np-font-sans); letter-spacing: .2px; color: var(--np-text-1); } /* th14b */
.np-body     { font: 500 14px/21px var(--np-font-sans);  letter-spacing: .4px; color: var(--np-text-3); } /* tb14m */
.np-body-sm  { font: 500 13px/20px var(--np-font-sans);  letter-spacing: .4px; color: var(--np-text-3); } /* tb13m */
.np-eyebrow  { font: 700 12px/15px var(--np-font-sans);  letter-spacing: 2px; text-transform: uppercase; color: var(--np-text-3); } /* tc12b */
.np-label    { font: 700 8px/10px var(--np-font-sans);   letter-spacing: 1px; text-transform: uppercase; color: var(--np-text-3); } /* tc8b */

/* ---------- the pop surface: face + right edge + bottom edge ---------- */
.np-pop {
  --np-face: #ffffff; --np-on-face: #0d0d0d; --np-stroke: transparent;
  --np-edge-r: #e0e0e0; --np-edge-b: #8a8a8a;   /* elevated: right lighter, bottom darker */
  --np-edge-t: #3d3d3d; --np-edge-l: #8a8a8a;   /* flat: walls revealed on press */
  --np-sink: 0px;
  position: relative; display: inline-flex; box-sizing: border-box;
  padding: 0 var(--np-depth) var(--np-depth) 0;   /* room for the edges */
  overflow: hidden;                               /* hides edges as they slide away */
  margin: 0; border: 0; background: transparent; color: inherit; font: inherit; text-align: inherit;
  text-decoration: none; -webkit-tap-highlight-color: transparent; user-select: none;
}
.np-pop > .np-face {
  position: relative; z-index: 1; flex: 1; display: block; box-sizing: border-box;
  background: var(--np-face); color: var(--np-on-face);
  box-shadow: inset 0 0 0 1px var(--np-stroke);
  transform: translate(var(--np-sink), var(--np-sink));
  transition: transform var(--np-press);
}
.np-pop::before, .np-pop::after {
  content: ""; position: absolute; transform-origin: 0 0; transition: transform var(--np-press);
}
.np-pop::before { /* right edge */
  top: 0; right: 0; width: var(--np-depth); height: calc(100% - var(--np-depth));
  background: var(--np-edge-r); transform: translate(var(--np-sink), var(--np-sink)) skewY(45deg);
}
.np-pop::after { /* bottom edge */
  left: 0; bottom: 0; width: calc(100% - var(--np-depth)); height: var(--np-depth);
  background: var(--np-edge-b); transform: translate(var(--np-sink), var(--np-sink)) skewX(45deg);
}
/* press: the face sinks into its own plunk */
:is(button, a, [role="button"], label).np-pop { cursor: pointer; }
:is(button, a, [role="button"], label).np-pop:active:not(:disabled):not([aria-disabled="true"]),
.np-pop.is-pressed { --np-sink: var(--np-depth); }

/* flat kind: no plunk at rest; on press it sinks into the parent, showing a top wall and a left wall */
.np-pop.np-flat { padding: 0; }
.np-pop.np-flat::before { top: 0; left: 0; right: auto; width: calc(100% - var(--np-depth)); height: var(--np-depth);
  background: var(--np-edge-t); transform: skewX(45deg); }
.np-pop.np-flat::after  { top: 0; left: 0; bottom: auto; width: var(--np-depth); height: calc(100% - var(--np-depth));
  background: var(--np-edge-l); transform: skewY(45deg); }

/* colour presets: set face, text and edges together */
.np-c-white { --np-face: #ffffff; --np-on-face: #0d0d0d; --np-edge-r: #e0e0e0; --np-edge-b: #8a8a8a; --np-edge-t: #3d3d3d; --np-edge-l: #8a8a8a; }
.np-c-black { --np-face: #0d0d0d; --np-on-face: #ffffff; --np-edge-r: #8a8a8a; --np-edge-b: #3d3d3d; --np-edge-t: #3d3d3d; --np-edge-l: #8a8a8a; }
/* accent faces: edges from the neopop-android HSL rule (section 4); lime is stepped one notch darker so its plunk reads */
.np-c-lime   { --np-face: #e5fe40; --np-on-face: #0d0d0d; --np-edge-r: #bbd701; --np-edge-b: #8fa401; }
.np-c-green  { --np-face: #3bffad; --np-on-face: #0d0d0d; --np-edge-r: #08ff98; --np-edge-b: #00d47b; }
.np-c-purple { --np-face: #6a35ff; --np-on-face: #ffffff; --np-edge-r: #4402ff; --np-edge-b: #3600ce; }
.np-c-orange { --np-face: #ff8744; --np-on-face: #0d0d0d; --np-edge-r: #ff6611; --np-edge-b: #dd4f00; }
.np-c-pink   { --np-face: #ff426f; --np-on-face: #0d0d0d; --np-edge-r: #ff0f48; --np-edge-b: #db0034; }
.np-c-yellow { --np-face: #ffcb45; --np-on-face: #0d0d0d; --np-edge-r: #ffbd12; --np-edge-b: #dea000; }
.np-c-yoyo   { --np-face: #aa3fff; --np-on-face: #ffffff; --np-edge-r: #930cff; --np-edge-b: #7800d8; }
.np-stroke-black { --np-stroke: #0d0d0d; }  /* white button on dark page (lib "secondary, dark") */
.np-stroke-white { --np-stroke: #ffffff; }  /* black button on light page (lib "secondary, light") */

.np-pop:is(:disabled, [aria-disabled="true"]) {
  --np-face: #8a8a8a; --np-on-face: rgba(255,255,255,.5); --np-edge-r: #b6b6b6; --np-edge-b: #3d3d3d;
  --np-stroke: transparent; cursor: not-allowed;
}
:is(.np-pop, .np-link):focus-visible { outline: 2px solid var(--np-focus); outline-offset: 2px; }

/* ---------- buttons ---------- */
.np-btn > .np-face { display: flex; align-items: center; justify-content: center; gap: 10px;
  height: 40px; padding: 0 20px; white-space: nowrap; font: 700 13px/16px var(--np-font-sans); letter-spacing: .2px; }
.np-btn.np-btn--lg > .np-face { height: 50px; padding: 0 30px; font-size: 14px; line-height: 18px; }
.np-btn.np-btn--sm > .np-face { height: 30px; padding: 0 25px; font-size: 11px; line-height: 14px; letter-spacing: .4px; }
.np-btn--block { display: flex; width: 100%; }
.np-btn svg { flex: none; }
.np-link { padding: 0; border: 0; border-bottom: 1px solid currentColor; background: none; cursor: pointer;
  font: 700 13px/16px var(--np-font-sans); letter-spacing: .2px; color: var(--np-text-1); }

/* optional shimmer: one light band sweeps across the face (use on ONE hero CTA at most).
   The default band is white, for black/accent faces; on a white face set --np-shimmer: rgba(13,13,13,.12) */
.np-pop.np-shimmer > .np-face {   /* painted as a background layer, so it passes BEHIND the label */
  background-image: linear-gradient(110deg, transparent 0 40%, var(--np-shimmer, rgba(255,255,255,.55)) 40% 43.5%, transparent 43.5%);
  background-size: 250% 100%; background-repeat: no-repeat; animation: np-shimmer 3s ease-in-out infinite; }
@keyframes np-shimmer { 0% { background-position: 100% 0; } 50%, 100% { background-position: 0 0; } }

/* ---------- cards & containers ---------- */
.np-card { display: flex; width: 100%; }
.np-card > .np-face { padding: 20px; }
.np-container { background: var(--np-surface); box-shadow: inset 0 0 0 1px var(--np-hairline); padding: 20px; }
.np-divider { height: 1px; margin: 0; border: 0; background: var(--np-hairline); }

/* ---------- inputs ---------- */
.np-field > label { display: block; margin-bottom: 10px; font: 700 8px/10px var(--np-font-sans);
  letter-spacing: 1px; text-transform: uppercase; color: var(--np-text-3); transition: color .15s ease; }
.np-field:focus-within > label { color: var(--np-text-1); }
.np-field.is-error > label { color: var(--np-red); }   /* the label TEXT becomes the error message */
.np-input { display: block; width: 100%; box-sizing: border-box; margin: 0; padding: 0; border: 0; outline: 0;
  background: transparent; font: 700 22px/28px var(--np-font-sans); letter-spacing: .2px;
  color: var(--np-text-1); caret-color: var(--np-blue); }
.np-input::placeholder { color: var(--np-text-4); }
.np-search { display: flex; align-items: center; gap: 10px; padding: 11px 15px;
  background: var(--np-surface); border: 1px solid var(--np-line); }
.np-search:focus-within { border-color: var(--np-focus); }
.np-search input { flex: 1; min-width: 0; border: 0; outline: 0; padding: 0; background: transparent;
  font: 600 13px/16px var(--np-font-sans); letter-spacing: .4px; color: var(--np-text-1); }
.np-search input::placeholder { color: var(--np-text-4); }
.np-select { display: inline-flex; align-items: center; gap: 10px; padding: 10px 15px; border: 1px solid var(--np-hairline);
  background: transparent; color: var(--np-text-3); font: 600 13px/16px var(--np-font-sans); letter-spacing: .4px; cursor: pointer; }

/* ---------- checkbox / radio / toggle (native inputs, visually hidden) ---------- */
.np-check, .np-radio, .np-toggle { position: relative; display: inline-flex; align-items: center; gap: 15px; cursor: pointer;
  -webkit-tap-highlight-color: transparent; user-select: none; }
:is(.np-check, .np-radio, .np-toggle) > input { position: absolute; opacity: 0; width: 1px; height: 1px; margin: 0; }
:is(.np-check, .np-radio, .np-toggle) > input:focus-visible + span { outline: 2px solid var(--np-focus); outline-offset: 2px; }

.np-check__box { position: relative; flex: none; width: 20px; height: 20px; overflow: hidden; }
.np-check__box::before, .np-check__box::after { content: ""; position: absolute; left: 0; top: 0; opacity: 0; transform-origin: 0 0; }
.np-check__box::before { width: 20px; height: var(--np-depth); background: var(--np-plunk-t); transform: skewX(45deg); }
.np-check__box::after  { width: var(--np-depth); height: 20px; background: var(--np-plunk-l); transform: skewY(45deg); }
.np-check__mark { position: absolute; inset: 0; z-index: 1; display: grid; place-items: center; box-sizing: border-box;
  border: 1px solid var(--np-ctl-ink); background: var(--np-ctl-bg); color: var(--np-ctl-bg);
  transition: transform .15s ease, background-color .15s ease; }
.np-check__mark svg { opacity: 0; transition: opacity .15s ease; }
.np-check > input:checked + .np-check__box .np-check__mark { background: var(--np-ctl-ink); }
.np-check > input:checked + .np-check__box svg { opacity: 1; }
.np-check:active .np-check__mark { transform: translate(var(--np-depth), var(--np-depth)); }
.np-check:active .np-check__box::before, .np-check:active .np-check__box::after { opacity: 1; transition: opacity .1s ease .03s; }

.np-radio__dot { position: relative; flex: none; width: 20px; height: 20px; box-sizing: border-box; border-radius: 50%;
  border: 1px solid var(--np-ctl-ink); background: var(--np-ctl-bg); }
.np-radio__dot::after { content: ""; position: absolute; left: 50%; top: 50%; width: 7px; height: 7px; border-radius: 50%;
  transform: translate(-50%, -50%); background: var(--np-ctl-bg); display: none; }
.np-radio > input:checked + .np-radio__dot { background: var(--np-ctl-ink); }
.np-radio > input:checked + .np-radio__dot::after { display: block; }
.np-radio:active > input:not(:checked) + .np-radio__dot { border: 0; background: var(--np-ctl-ink); box-shadow: inset 2px 2px 0 #8a8a8a; }
/* radio as a selectable option tile */
.np-option { display: flex; width: 100%; box-sizing: border-box; padding: 15px; border: 1px solid rgba(255,255,255,.1);
  background: #121212; color: #ffffff; }
.np-option:has(input:checked) { background: var(--np-poli-purple-500); border-color: #2c5ecd; }

.np-toggle__track { position: relative; flex: none; display: inline-block; width: 40px; height: 22px; box-sizing: border-box;
  border: 1px solid var(--np-tgl-border); background: var(--np-tgl-off-track); overflow: hidden; transition: background-color .15s ease; }
.np-toggle__knob { position: absolute; top: 0; left: 0; width: 20px; height: 20px; box-sizing: border-box;
  background: var(--np-tgl-off-knob); border: 1px solid var(--np-tgl-off-knob-border); transition: transform .15s ease; }
.np-toggle__knob::after { content: ""; position: absolute; left: 50%; top: 50%; width: 8px; height: 8px;
  transform: translate(-50%, -50%); background: var(--np-tgl-off-mark); }
.np-toggle > input:checked + .np-toggle__track { background: var(--np-tgl-on-track); }
.np-toggle > input:checked + .np-toggle__track .np-toggle__knob { transform: translateX(18px); background: #38b36f; border-color: var(--np-tgl-on-knob-border); }
.np-toggle > input:checked + .np-toggle__track .np-toggle__knob::after { background: #ffffff; }

/* ---------- tags ---------- */
.np-tag { display: inline-flex; align-items: center; gap: 5px; padding: 5px 10px 4px;
  font: 700 8px/10px var(--np-font-sans); letter-spacing: 1px; text-transform: uppercase; color: #fbfbfb; }
.np-tag--success { background: var(--np-green); } .np-tag--error { background: var(--np-red); }
.np-tag--warning { background: var(--np-yellow); } .np-tag--info { background: var(--np-blue); }
[data-np-theme="light"] .np-tag--success { background: #e6f9f1; color: var(--np-green); }
[data-np-theme="light"] .np-tag--error   { background: #fdedeb; color: var(--np-red); }
[data-np-theme="light"] .np-tag--warning { background: #fef4eb; color: var(--np-yellow); }
[data-np-theme="light"] .np-tag--info    { background: #ebf1fe; color: var(--np-blue); }
.np-tag--text { padding: 0; background: none; font-size: 10px; line-height: 13px; letter-spacing: 2px; } /* tag without a container */

/* ---------- toast ---------- */
.np-toast { position: fixed; top: 0; left: 0; right: 0; z-index: 1001; display: flex; align-items: flex-start; gap: 15px;
  margin: 8px; padding: 15px; border-radius: 4px; color: #f8f8f8; animation: np-toast 3s ease-in forwards; }
.np-toast--full { margin: 0; border-radius: 0; }
.np-toast--success { background: var(--np-green); } .np-toast--warning { background: var(--np-yellow); } .np-toast--error { background: var(--np-red); }
.np-toast__title { font: 600 13px/16px var(--np-font-sans); letter-spacing: .4px; }
.np-toast__body  { font: 400 11px/17px var(--np-font-sans); letter-spacing: .4px; }
@keyframes np-toast { 0% { transform: translateY(-120%); } 7%, 90% { transform: translateY(0); } 100% { transform: translateY(-120%); } }

/* ---------- bottom sheet: light sheet with a "top-centre" roof ---------- */
.np-scrim { position: fixed; inset: 0; z-index: 100; background: rgba(13,13,13,.9); }
.np-sheet { position: fixed; left: 0; right: 0; bottom: 0; z-index: 101; max-height: 90vh; overflow: visible;
  background: #fbfbfb; color: #0d0d0d; animation: np-sheet-up .3s cubic-bezier(.2,.9,.3,1.05); }
.np-sheet::before, .np-sheet::after { content: ""; position: absolute; top: -3.5px; height: 4px; width: 55%; background: var(--np-sheet-edge, #c4c4c4); }
.np-sheet::after  { left: 0;  margin-left: 1.5px;  transform: skewX(-45deg); }
.np-sheet::before { right: 0; margin-right: 1.5px; transform: skewX(45deg); }
.np-sheet__notch { position: absolute; top: -18px; left: 50%; width: 60px; height: 2px; background: #8a8a8a; transform: translateX(-50%); }
.np-sheet__body { max-height: 90vh; overflow: auto; padding: 30px 20px; }
@keyframes np-sheet-up { from { transform: translateY(100%); } to { transform: translateY(0); } }

@media (prefers-reduced-motion: reduce) {
  .np-pop > .np-face, .np-pop.np-shimmer > .np-face, .np-pop::before, .np-pop::after, .np-toast, .np-sheet { transition: none; animation: none; }
}
```

### Markup patterns

```html
<!-- elevated button: wrapper + .np-face; the pseudo-elements draw the edges -->
<button class="np-pop np-btn np-btn--lg np-c-white np-stroke-black">
  <span class="np-face">pay now <!-- arrow svg below --></span>
</button>
<!-- flat button -->
<button class="np-pop np-flat np-btn np-c-white"><span class="np-face">skip</span></button>
<!-- link button -->
<button class="np-link">view statement</button>
<!-- elevated card (not pressable: use a div) -->
<div class="np-pop np-card np-c-lime"><div class="np-face">…</div></div>
<!-- input -->
<div class="np-field"><label for="amt">enter amount</label><input id="amt" class="np-input" inputmode="numeric" placeholder="₹0"></div>
<!-- checkbox -->
<label class="np-check"><input type="checkbox"><span class="np-check__box"><span class="np-check__mark">
  <svg width="10" height="8" viewBox="0 0 11 8" fill="none"><path d="M1.45456 3.99973L4.18183 6.72701L10.5455 1.27246" stroke="currentColor" stroke-width="1.36364"/></svg>
</span></span><span class="np-body">autopay this card</span></label>
<!-- radio + radio tile -->
<label class="np-option np-radio"><input type="radio" name="plan"><span class="np-radio__dot"></span><span>pay full amount</span></label>
<!-- toggle -->
<label class="np-toggle"><input type="checkbox" role="switch"><span class="np-toggle__track"><span class="np-toggle__knob"></span></span><span class="np-body">rewards</span></label>
<!-- tag -->
<span class="np-tag np-tag--success">paid</span>
<!-- bottom sheet -->
<div class="np-scrim"></div><div class="np-sheet" data-np-theme="light" role="dialog" aria-modal="true"><span class="np-sheet__notch"></span><div class="np-sheet__body">…</div></div>
```

Icons are thin (1.5px), square-capped line icons. NeoPOP's two signature glyphs:

```html
<!-- "pointer" arrow used after CTA labels (21×9). fill = text colour -->
<svg width="21" height="9" viewBox="0 0 21 9" fill="none" aria-hidden="true"><path fill="currentColor" d="M1 3.75H.25v1.5H1v-1.5Zm0 1.5h19v-1.5H1v1.5ZM16.379.5c0 2.6 2.046 4.75 4.621 4.75v-1.5c-1.7 0-3.121-1.432-3.121-3.25h-1.5ZM21 3.75c-2.575 0-4.621 2.15-4.621 4.75h1.5c0-1.818 1.42-3.25 3.121-3.25v-1.5Z"/></svg>
<!-- back arrow for page headers (32×12) -->
<svg width="32" height="12" viewBox="0 0 32 12" fill="none" aria-hidden="true"><path d="M31 6H1" stroke="currentColor" stroke-width="1.5" stroke-linecap="square"/><path d="M7 12A6 6 0 0 0 1 6M1 6a6 6 0 0 0 6-6" stroke="currentColor" stroke-width="1.5"/></svg>
<!-- chevron (8×11), rotate for other directions -->
<svg width="8" height="11" viewBox="0 0 8 11" fill="none" aria-hidden="true"><path d="M2 9.5l4-4-4-4" stroke="currentColor" stroke-width="1.5" stroke-linecap="square"/></svg>
```

## 4. Elevation in detail

**Geometry.** If you draw it another way (SVG, canvas, native, a component library), reproduce exactly this, with `d` = depth:
- The face sits at the top-left of the box, inset by `d` from the right and the bottom.
- Right edge: a `d` × (H−d) strip on the right side, `skewY(45deg)` from the top-left origin. It runs from the face's top-right corner down to the box's bottom-right corner.
- Bottom edge: a (W−d) × `d` strip along the bottom, `skewX(45deg)` from the top-left origin.
- The box clips its overflow. On press, the face and both edges translate by (d, d), so the edges slide out of view and the face lands where the plunk was.

**Edge colours for the stock faces** (from the web library):

| Face | Text | Right edge | Bottom edge | Flat walls (top / left) |
|---|---|---|---|---|
| white `#fff` | `#0d0d0d` | `#e0e0e0` | `#8a8a8a` | `#3d3d3d` / `#8a8a8a` |
| black `#0d0d0d` | `#fff` | `#8a8a8a` | `#3d3d3d` | `#3d3d3d` / `#8a8a8a` |
| disabled `#8a8a8a` | white 50% | `#b6b6b6` | `#3d3d3d` | none (no press) |

**Any other colour.** Use the rule from neopop-android (`PopFrameLayoutStyle`). Convert the face colour to HSL. If L ≥ 30%, right = L − 10 and bottom = L − 20. Otherwise right = L + 20 and bottom = L + 10. H and S stay the same. The accent presets in section 3 come from this rule. It keeps the edges as vivid as the face, so they look like the same material in shade, not a muddy shadow. Very light, saturated faces such as lime can end up with an edge that barely differs from the face; if the plunk doesn't read at a glance, step one notch further (−20/−30), as the lime preset does.

```js
// edge colours for a custom face (neopop-android rule)
function neopopEdges(hex) {
  const n = parseInt(hex.slice(1), 16), r = (n >> 16 & 255) / 255, g = (n >> 8 & 255) / 255, b = (n & 255) / 255;
  const max = Math.max(r, g, b), min = Math.min(r, g, b), l = (max + min) / 2, dd = max - min;
  const s = dd === 0 ? 0 : dd / (1 - Math.abs(2 * l - 1));
  const h = dd === 0 ? 0 : max === r ? 60 * (((g - b) / dd) % 6) : max === g ? 60 * ((b - r) / dd + 2) : 60 * ((r - g) / dd + 4);
  const hsl = L => `hsl(${(h + 360) % 360} ${(s * 100).toFixed(1)}% ${Math.max(0, Math.min(100, L * 100)).toFixed(1)}%)`;
  return l >= 0.3 ? { right: hsl(l - 0.1), bottom: hsl(l - 0.2) } : { right: hsl(l + 0.2), bottom: hsl(l + 0.1) };
}
```

**Depth.** 3px is the library default for every component. The mobile libraries let you change the depth: go deeper (6–8px) only for large hero cards or one showcase CTA, and keep one depth per component type on a screen. Set it per element with `style="--np-depth: 6px"`.

**Direction.** Keep bottom-right everywhere, so the light source stays consistent. The one exception is the bottom sheet's top-centre "roof", built into `.np-sheet`.

**Adjacent elevated items** (keypads, option grids): leave a gap of at least the depth so each plunk stays visible.

## 5. Components

**Buttons.** Three sizes, all with 0 radius:

| Size | Height | Padding | Label | Icon |
|---|---|---|---|---|
| big (`--lg`) | 50px | 0 30px | Gilroy 700 14px, tracking .2px | 20px |
| medium (default) | 40px | 0 20px | Gilroy 700 13px, tracking .2px | 16px |
| small (`--sm`) | 30px | 0 25px | Gilroy 700 11px, tracking .4px | 14px |

- Kinds: **elevated** (the plunk) for primary actions, **flat** for secondary actions, and **link** (text with a 1px underline in the text colour) for tertiary ones. A leading icon sits 10px before the label, and the pointer arrow 10px after it (`showArrow`).
- The library's variant naming is easy to misread. `colorMode` is the theme of the page. "primary" matches the page tone, so it reads as a block defined by its edges: a black face on a dark page, white on a light one. "secondary" is the inverted, high-contrast block: a white face with a 1px black stroke on dark, a black face with a 1px white stroke on light. For the single most important action, use the inverted block or one accent preset.
- Use one elevated accent button per view. Full-width (`np-btn--block`) big buttons work for the main mobile CTA, often pinned to the bottom of the screen.

**Cards.** An *elevated card* is `.np-pop.np-card` with an accent or white face, 20px padding inside, and isn't pressable unless it's a link (then make it an `<a>`). A *container card* is the quiet default for grouping: `#121212`, a 1px hairline at 10% white, a 14px bold title and a 13px medium description.

**Inputs.** There is no box. A caps label (8px, bold, 1px tracking, 50% opacity) sits 10px above a 22px bold value with a blue caret and a 30% placeholder. On error, replace the label text with the error message and turn it red; don't add red borders. A search bar is a bordered row: padding 11px 15px, a `#3d3d3d` border that turns white on focus, a 16px icon with 10px gap, and 13px semibold text. A dropdown trigger has padding 10px 15px, a 10% hairline and a chevron.

**Selection controls** are 20px. The checkbox is a square with a 1px border. When checked it fills with the ink colour and shows the tick in the background colour. On press it sinks 3px and shows top and left walls. The radio is a circle that fills with ink when checked, with a 7px dot. As an option tile: padding 15px, `#121212` with a 10% border, turning poli-purple 500 with a `#2c5ecd` border when selected. The toggle is a 40×22 rectangle with a square 20×20 knob holding an 8×8 inner square; when on, the knob turns `#38b36f` and moves 18px. All of them animate over 150ms ease.

**Tags** have no radius: padding 5px 10px 4px, 8px bold caps with 1px tracking. On dark pages they use a solid status fill with `#fbfbfb` text; on light pages, a pale tint with saturated text. The text-only variant is 10px caps with 2px tracking.

**Toasts** drop from the top and auto-close after 3s. They use a solid status colour, `#f8f8f8` text, 15px padding, a 13px semibold title and 11px regular body text. They're full-width with no radius, or inset 8px with a 4px radius.

**Bottom sheets.** The scrim is `#0d0d0d` at 90%. The sheet is a `#fbfbfb` surface with dark text, a 4px top-centre roof in `#c4c4c4` made of two 55%-wide bars skewed ±45°, and a 60×2 `#8a8a8a` notch 18px above. It slides up with a slight spring.

**Page header.** The back arrow sits in a 36px-tall row with 12px vertical padding. Below it, 10px down, is the title in Cirka 700 24px at 90% (max-width 75%); 5px below that is a description in Gilroy 500 14px at 50%.

**Score meter** (credit-score style): a 160px circle with a 1px `#3d3d3d` border and a 270° arc starting at 135°. The arc is `#06c270` for excellent, neo-paccha 400 for average and warning 400 for poor. A 95px inner disc holds the score.

**Dividers** are 1px at 10% of the text colour, full-width, between list rows and sections.

## 6. Typography

- **Fonts.** Gilroy (geometric sans; weights 400/500/600/700/800) handles all UI. Cirka (Pangram Pangram's PP Cirka, Bold) handles editorial headlines only. Both are commercial typefaces, so use them only if the project holds licences, and self-host the files. Don't hot-link `web-assets.cred.club`: those files are licensed to CRED. Otherwise, use the free stand-ins already in the font stacks: **Outfit** (or Urbanist) for Gilroy, **Playfair Display 700** (or DM Serif Display) for Cirka.
- **Four type families of roles** (lib key = `t` + family + size + weight; families `h` heading, `b` body, `c` caps, `sh` serif heading; weights `eb` 800, `b` 700, `sb` 600, `m` 500, `r` 400):
  - Heading (sans): 44, 34, 28, 22, 20, 18, 16, 15, 14, 13 px at 800/700/600.
  - Body (sans): 16–11 px at 500/400.
  - Caps (sans, uppercase): 12/10/8 px at 800/700/600.
  - Serif heading: 36, 34, 32, 24, 22, 20, 18 px at 700.
- **Line height.** Round to whole pixels: font size × 1.25 for heading, caps and serif text, and × 1.5 for body text.
- **Letter-spacing.**
  - Heading: 0.2px, except 800 weight at 44px+ (0), 700 weight below 13px (0.4px), and 600 weight below 18px (0.4px).
  - Body: 0.4px.
  - Caps: 2px when larger than 8px, 1px at 8px.
  - Serif: 0.2px.
- **Hierarchy comes from opacity, not grey hexes.** Use 90% for headings, 70% for sub-headings, 50% for body and labels, and 30% only for placeholders and disabled text. On `#0d0d0d`, 50% white is 5.3:1, which passes; 30% is 2.7:1, which fails. On white, use 70% black for body text, since 50% black is only 3.6:1.
- **Hero pattern** from the NeoPOP intro page: a 12–14px caps eyebrow at 50% with wide tracking (up to 7px for a single word), then a big serif headline, then a 18–22px semibold sans paragraph at 50–90%. Centre it on landing pages; elsewhere, align left.

## 7. Layout, spacing, motion, voice

- **Spacing.** Use a 5px grid (the library's spacers are `n × 5px`). Common steps are 5, 10, 15, 20, 30 and 40. Inside components, use 10–15px; between sections, 30–40px; at the edges of a mobile screen, 20–30px. The intro page uses 100px/160px padding on desktop and 50px on mobile.
- **Composition.** Use one column on mobile, left-aligned text, big bold numerals for money and scores, and hairline dividers between rows. Leave lots of black space, and keep content at the same level flat instead of nesting boxes.
- **Motion.**
  - Press: 120ms ease-in-out.
  - Controls: 150ms ease.
  - Toasts: a 3s slide-down and back.
  - Sheets: slide up with a slight spring.
  - Shimmer (optional): a 1.5s sweep and then a pause, on one CTA at most.
  - Don't use fades, scale-ups or bouncy entrances on ordinary elements, and honour `prefers-reduced-motion`.
- **Voice.**
  - Write all copy in lowercase, including buttons and headings, and let the caps style uppercase labels through CSS.
  - Keep sentences short, declarative and a little playful ("behind every masterpiece there exists a framework").
  - Write money in Indian format with no space: `new Intl.NumberFormat('en-IN', {style:'currency', currency:'INR', maximumFractionDigits: 2}).format(n).replace(/\s/g,'')` → `₹1,23,456`.

## 8. Tailwind and DaisyUI

Keep `neopop.css` as the source of the component classes, because skewed pseudo-element edges are awkward to write as utilities. Expose the tokens to utilities as well:

```css
/* Tailwind v4 */
@import "tailwindcss";
@import "./neopop.css";
@theme {
  --color-np-black: #0d0d0d; --color-np-surface: #121212; --color-np-lime: #e5fe40; --color-np-green: #3bffad;
  --color-np-purple: #6a35ff; --color-np-orange: #ff8744; --color-np-pink: #ff426f; --color-np-yellow: #ffcb45;
  --font-np-sans: "Gilroy", "Outfit", "Urbanist", system-ui, sans-serif;
  --font-np-serif: "Cirka", "Playfair Display", "DM Serif Display", Georgia, serif;
  --radius-*: initial;   /* drops the rounded-sm/md/lg… scale; only rounded-none/full remain */
}
```

For DaisyUI 5, add a theme with zero radii and no depth or noise, then use the `np-*` classes for buttons, cards and toggles instead of DaisyUI's (DaisyUI's `btn` cannot draw plunk edges):

```css
@plugin "daisyui/theme" {
  name: "neopop"; default: true; color-scheme: dark;
  --color-base-100: #0d0d0d; --color-base-200: #121212; --color-base-300: #161616; --color-base-content: #ffffff;
  --color-primary: #ffffff; --color-primary-content: #0d0d0d; --color-accent: #e5fe40; --color-accent-content: #0d0d0d;
  --color-success: #06c270; --color-warning: #f08d32; --color-error: #ee4d37; --color-info: #144cc7;
  --radius-selector: 0rem; --radius-field: 0rem; --radius-box: 0rem; --border: 1px; --depth: 0; --noise: 0;
}
```

## 9. React with the official package (`@cred/neopop-web`)

Install with `npm i @cred/neopop-web styled-components@5`, which needs React 17/18. The package does **not** load fonts or set `font-family`, so set it on `body` yourself. Serif headings also need `font-family` passed through `style`.

```jsx
import { Button, ElevatedCard, Typography, InputField, Toggle, Checkbox, Radio, Tag, Header,
  SearchBar, Dropdown, BottomSheet, ScoreMeter, HorizontalDivider, HorizontalSpacer, Pointer,
  showToast, ToastContainer } from '@cred/neopop-web/lib/components';
import { mainColors, colorPalette, colorGuide, fontNameSpaces } from '@cred/neopop-web/lib/primitives';

<Button variant="secondary" kind="elevated" size="big" colorMode="dark" showArrow fullWidth onClick={pay}>pay now</Button>

// custom accent: pass the full colorConfig; for kind="elevated" keep top/left transparent
<Button kind="elevated" size="big" colorConfig={{ backgroundColor: colorPalette.neoPaccha[500], color: mainColors.black,
  edgeColors: { top: 'transparent', left: 'transparent', right: '#bbd701', bottom: '#8fa401' } }}>claim reward</Button>

<ElevatedCard backgroundColor={colorPalette.poliPurple[500]} edgeColors={{ right: '#4402ff', bottom: '#3600ce' }}>
  <div style={{ padding: 20 }}>…</div>   {/* the card adds no padding */}
</ElevatedCard>

<Typography {...fontNameSpaces.th22eb} color={colorGuide.darkComponents.font.heading}>₹12,480</Typography>
<Typography {...fontNameSpaces.tsh24b} style={{ fontFamily: 'Cirka, "Playfair Display", serif' }} color={mainColors.white}>your cards</Typography>

<InputField id="amt" label="enter amount" colorMode="dark" placeholder="₹0" value={v} onChange={e => setV(e.target.value)}
  hasError={!!err} errorMessage={err} inputMode="numeric" />
<Toggle isChecked={on} handleChange={() => setOn(!on)} colorMode="dark" />
<Checkbox isChecked={c} handleChange={() => setC(!c)} colorMode="dark">autopay</Checkbox>
<Radio id="full" name="plan" value="full" label="pay full amount" isChecked={plan === 'full'} handleChange={() => setPlan('full')} colorMode="dark" />
<Tag type="success" colorMode="dark">paid</Tag>
<Header heading="credit cards" description="manage all your cards in one place" onBackClick={back} />
<ToastContainer />  {/* mount once */}
showToast('payment successful', { type: 'success', description: '₹12,480 paid', autoCloseTime: 3000, fullWidth: true })
```

Other props:
- `Button`: `elevationDirection` (`'bottom-right'` etc.), `icon` (an img URL), `disabled`, `spacingConfig`, `textStyle`.
- `BottomSheet`: `open`, `handleClose`, `onCloseEnd`, `sheetPlunkColor`, `maxHeight`.
- `SearchBar`: `placeholder`, `handleSearchInput`, `iconUrl`, `colorMode`.

The buttons ship with `outline: none`, so add a `:focus-visible` outline in your own CSS.

## 10. Before you finish, check

- [ ] Zero border-radius everywhere except radio dots, meters and inset toasts.
- [ ] Raised surfaces have both edges, at 45°, with the right edge lighter than the bottom, and the plunk is visible against its background.
- [ ] Press moves the face exactly the depth down-right in 120ms. Nothing uses a blurred shadow, glow or gradient for depth.
- [ ] The page is black or white with one accent colour. The text hierarchy uses the opacity levels, and 30% is used only for placeholders and disabled text.
- [ ] Gilroy (or Outfit) is used for UI and Cirka (or Playfair) only for headlines. Caps labels are tracked 1–2px. All copy is lowercase.
- [ ] Inputs have no boxes, and errors replace the label instead of adding red borders.
- [ ] Focus-visible outlines exist, contrast passes WCAG AA for body text, and `prefers-reduced-motion` is honoured.
- [ ] No CRED logo, wordmark or product names, and no hot-linked CRED font files.
