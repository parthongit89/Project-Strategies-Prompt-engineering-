# Frontend Design System & Strategy (Designs.md)

## 1. Design System Foundations

### 1.1 Color Palette & Theme Specs
The UI uses a modern, sleek dark-mode first design aesthetic powered by Tailwind CSS utility classes:

| Token Name | Tailwind Class | Color Hex | Usage |
| :--- | :--- | :--- | :--- |
| **Background Dark** | `bg-slate-900` | `#0f172a` | Main application background |
| **Surface Dark** | `bg-slate-800` | `#1e293b` | Cards, modals, sidebars |
| **Border Dark** | `border-slate-700` | `#334155` | Card borders, dividers, inputs |
| **Primary Accent** | `bg-indigo-600` / `text-indigo-400` | `#4f46e5` | Primary action buttons, active states |
| **Primary Hover** | `hover:bg-indigo-500` | `#6366f1` | Interactive hover states |
| **Text Primary** | `text-slate-100` | `#f8fafc` | Headings, primary text |
| **Text Muted** | `text-slate-400` | `#94a3b8` | Subtitles, helper text, timestamps |
| **Success State** | `text-emerald-400` | `#34d399` | Success notifications, high scores |
| **Error State** | `text-rose-400` | `#fb7185` | Validation errors, alert banners |

---

## 2. Component Guidelines (HTML & Tailwind CSS)

### 2.1 Primary Action Button
```html
<button class="w-full px-4 py-2.5 bg-indigo-600 hover:bg-indigo-500 text-white font-medium rounded-lg shadow-md transition-all duration-200 focus:outline-none focus:ring-2 focus:ring-indigo-400 focus:ring-offset-2 focus:ring-offset-slate-900 active:scale-[0.98]">
    Sign In
</button>
```

### 2.2 Form Input Field with Validation State
```html
<div class="space-y-1.5">
    <label for="email" class="block text-sm font-medium text-slate-300">Email Address</label>
    <input type="email" id="email" name="email" placeholder="user@example.com"
        class="w-full px-3.5 py-2 bg-slate-800 border border-slate-700 rounded-lg text-slate-100 placeholder-slate-500 focus:outline-none focus:border-indigo-500 focus:ring-1 focus:ring-indigo-500 transition-colors"
    />
    <p class="text-xs text-rose-400 hidden" id="email-error">Please enter a valid email address.</p>
</div>
```

---

## 3. UI Ingestion Workflows

### Workflow Option A: Direct Google Stitch AI Prompting
1. **Prompt Template**:
   > *"Generate a responsive, dark-themed dashboard UI component using Tailwind CSS and Semantic HTML5. Color scheme: slate-900 background, slate-800 cards, indigo-600 accent buttons. Include clean JS event listener hooks for API fetch calls."*
2. **Integration Steps**:
   - Copy generated HTML structure into `/frontend/public/index.html` or template partials.
   - Extract embedded script logic into `/frontend/public/assets/js/app.js`.

### Workflow Option B: Figma Designs + MCP Server Integration
1. **MCP Server Connection**: Use Model Context Protocol (MCP) server for Figma to fetch frame layout data directly.
2. **Conversion Pipeline**:
   - Inspect Figma node layout JSON (flex dimensions, color styles, typography).
   - Map Figma auto-layout attributes directly to Tailwind CSS flexbox/grid classes (`flex flex-col gap-4 items-center`).
   - Extract image/SVG assets to `/frontend/public/assets/images/`.

### Workflow Option C: Manual Custom Layout
1. **Wireframing**: Map page layouts using mobile-first grid structures (`grid grid-cols-1 md:grid-cols-12 gap-6`).
2. **Utility Class Composition**: Enforce component consistency using Tailwind CSS custom utilities or clean, reusable component classes.
