# Typography & Icons Strategy (Typography_icons.md)

## 1. Executive Summary
This document establishes the typography hierarchy, Google Fonts configuration, and icon system specifications for tech applications. Visual clarity and font performance are optimized using **Google Fonts** and **Google Material Symbols**, integrated seamlessly into Tailwind CSS.

---

## 2. Google Fonts Selection & Typography Scale

### 2.1 Selected Typefaces

| Classification | Font Name | Weights | Primary Usage |
| :--- | :--- | :--- | :--- |
| **Primary UI Sans** | **Inter** / **Plus Jakarta Sans** | `400 (Regular)`, `500 (Medium)`, `600 (SemiBold)`, `700 (Bold)` | Body text, form fields, UI controls, navigation |
| **Code / Technical** | **Fira Code** / **JetBrains Mono** | `400 (Regular)`, `600 (SemiBold)` | Code blocks, API payloads, terminals, data tables |
| **Display / Hero** | **Outfit** | `700 (Bold)`, `800 (ExtraBold)` | Hero titles, landing page headers, marketing copy |

### 2.2 Fluid Typography Scale (Tailwind Mapping)

| Level | Size (rem / px) | Line Height | Weight | Tailwind Classes |
| :--- | :--- | :--- | :--- | :--- |
| **Display 1** | `3.75rem (60px)` | `1.1` | `800` | `text-5xl md:text-6xl font-display font-extrabold tracking-tight` |
| **Heading 1** | `2.25rem (36px)` | `1.2` | `700` | `text-3xl md:text-4xl font-sans font-bold tracking-tight` |
| **Heading 2** | `1.50rem (24px)` | `1.3` | `600` | `text-xl md:text-2xl font-sans font-semibold` |
| **Heading 3** | `1.25rem (20px)` | `1.4` | `600` | `text-lg font-sans font-semibold` |
| **Body Lead** | `1.125rem (18px)`| `1.6` | `400` | `text-lg font-sans font-normal text-slate-300` |
| **Body Regular**| `1.00rem (16px)` | `1.5` | `400` | `text-base font-sans font-normal text-slate-300` |
| **Caption / Small**| `0.875rem (14px)`| `1.4` | `500` | `text-sm font-sans font-medium text-slate-400` |

---

## 3. Google Fonts CDN Integration

Include high-performance preconnect tags in the HTML `<head>`:

```html
<!-- Google Fonts Preconnect for Zero Render-Blocking Delay -->
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>

<!-- Google Fonts: Plus Jakarta Sans, Fira Code, Outfit & Material Symbols -->
<link href="https://fonts.googleapis.com/css2?family=Fira+Code:wght@400;600&family=Outfit:wght@700;800&family=Plus+Jakarta+Sans:wght@400;500;600;700&display=swap" rel="stylesheet">
<link href="https://fonts.googleapis.com/css2?family=Material+Symbols+Outlined:opsz,wght,FILL,GRAD@20..48,100..700,0..1,-50..200" rel="stylesheet" />
```

---

## 4. Tailwind CSS Font Family Configuration

Extend your `tailwind.config.js` to expose custom font families:

```javascript
/** @type {import('tailwindcss').Config} */
module.exports = {
  theme: {
    extend: {
      fontFamily: {
        sans: ['"Plus Jakarta Sans"', 'Inter', 'system-ui', 'sans-serif'],
        mono: ['"Fira Code"', '"JetBrains Mono"', 'monospace'],
        display: ['Outfit', 'sans-serif'],
      },
    },
  },
}
```

---

## 5. Google Material Symbols & Icons Guide

### 5.1 Material Symbols Outlined Standard Markup
```html
<!-- Search Icon Button -->
<button class="inline-flex items-center gap-2 px-4 py-2 bg-indigo-600 hover:bg-indigo-500 text-white rounded-lg transition-colors">
    <span class="material-symbols-outlined text-xl">search</span>
    <span>Search Projects</span>
</button>

<!-- Success Toast Icon -->
<div class="flex items-center gap-3 p-4 bg-slate-800 border border-slate-700 rounded-xl">
    <span class="material-symbols-outlined text-emerald-400 text-2xl">check_circle</span>
    <span class="text-slate-100 font-medium">Operation completed successfully.</span>
</div>
```

### 5.2 Icon Sizing & Alignment Utility Standard
- **Small (18px)**: `text-lg` or `text-[18px]`
- **Medium (24px - Default)**: `text-2xl` or `text-[24px]`
- **Large (32px)**: `text-3xl` or `text-[32px]`
- Always apply `align-middle` or flexbox alignment (`inline-flex items-center`) to prevent vertical baseline displacement.
